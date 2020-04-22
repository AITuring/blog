---
title: vscode remote ssh配置
date: 2019-11-15 23:57:43
tags: [vscode]
categories: [vscode]
---



Remote Development是vscode的远程编程与调试的插件，使用这个插件可以在很多情况下代替vim直接远程修改与调试服务器上的代码，就和在本地使用VScode一样。

<img src="https://code.visualstudio.com/assets/docs/remote/ssh/architecture-ssh.png" alt>
<h2 id="1-本地和服务器的ssh配置"><a href="#1-本地和服务器的ssh配置" class="headerlink" title="1.本地和服务器的ssh配置"></a>1.本地和服务器的ssh配置</h2><p>我的服务器是Ubuntu，本地是win10。MAC等更多环境配置请看<a href="https://code.visualstudio.com/docs/remote/ssh" target="_blank" rel="noopener">官方文档</a>。 </p>
<h3 id="1-1-服务器安装ssh-server"><a href="#1-1-服务器安装ssh-server" class="headerlink" title="1.1 服务器安装ssh-server"></a>1.1 服务器安装ssh-server</h3>

```bash
# Linux 系统
sudo apt-get install openssh-server
```

<h3 id="1-2本地安装ssh-client"><a href="#1-2本地安装ssh-client" class="headerlink" title="1.2本地安装ssh-client"></a>1.2本地安装ssh-client</h3><p>一般如果安装过xshell或putty等工具的就不需要单独安装了，可以在cmd中输入ssh查看本机是否安装了ssh。我已经安装了xshell，这里就不再赘述了。</p>
<h3 id="1-3设置无密码登陆服务器"><a href="#1-3设置无密码登陆服务器" class="headerlink" title="1.3设置无密码登陆服务器"></a>1.3设置无密码登陆服务器</h3><p>如果之前已经生成了公钥，直接去<code>%USERPROFILE%\.ssh\id_rsa.pub</code>就是公钥。如果设备是MAC或linux，位置在<code>~/.ssh/id_rsa.pub</code>。</p>
<p>如果还没有明白，更多相关内容请看<a href="https://code.visualstudio.com/docs/remote/troubleshooting#_configuring-key-based-authentication" target="_blank" rel="noopener">官方文档</a>。</p>
<p>如果没有秘钥，在终端运行以下命令：

```bash
# 生成本地密钥， 该命令在本地电脑端完成
ssh-keygen -t rsa -b 4096
```

<p>这样就能生成公钥了，然后去<code>%USERPROFILE%\.ssh\id_rsa.pub</code>找即可。</p>
<h4 id="1-3-1-使用专用秘钥提高安全性"><a href="#1-3-1-使用专用秘钥提高安全性" class="headerlink" title="1.3.1 使用专用秘钥提高安全性"></a>1.3.1 使用专用秘钥提高安全性</h4><p>在所有SSH主机上使用单个SSH密钥虽然很方便，但是如果任何人都可以访问我们的私钥，那么他们也将有权访问我们的所有主机。 </p>
<p>我们可以通过为开发主机创建单独的SSH密钥来防止这种情况。只需按照以下步骤操作：

```bash
ssh-keygen -t rsa -b 4096 -f %USERPROFILE%\.ssh\id_rsa-remote-ssh
```

<h3 id="1-4将本地公钥上传到服务器，并添加到-authorized-keys-文件中。"><a href="#1-4将本地公钥上传到服务器，并添加到-authorized-keys-文件中。" class="headerlink" title="1.4将本地公钥上传到服务器，并添加到 authorized_keys 文件中。"></a>1.4将本地公钥上传到服务器，并添加到 authorized_keys 文件中。</h3>


<figure class="highlight bash"><table><tr><td class="gutter"><pre><span class="line">1</span><br><span class="line">2</span><br><span class="line">3</span><br></pre></td><td class="code"><pre><span class="line">scp %USERPROFILE%\.ssh\id_rsa.pub %REMOTEHOST%:~/tmp.pub</span><br><span class="line"></span><br><span class="line">ssh %REMOTEHOST% <span class="string">"mkdir -p ~/.ssh &amp;&amp; chmod 700 ~/.ssh &amp;&amp; cat ~/tmp.pub &gt;&gt; ~/.ssh/authorized_keys &amp;&amp; chmod 600 ~/.ssh/authorized_keys &amp;&amp; rm -f ~/tmp.pub"</span></span><br></pre></td></tr></table></figure>
<p>注意， 需要将命令行中的变量替换为具体的内容：<br><code>%USERPROFILE%:C:\Users\xxx</code><br><code>%REMOTEHOST% :username@192.168.1.xxx(ip)</code></p>
<p><code>scp xxxxxx时</code>如果出现<code>REMOTE HOST IDENTIFICATION HAS CHANGED</code>查看错误日志中是否有<code>Add correct host key in /Users/Administrator/.ssh/known_hosts to get rid of this message</code>.如果有，打开<code>/Users/Administrator/.ssh/known_hosts</code>文件，删除这次远程服务器ip的条目。更多请看官方文档。</p>
<h2 id="2-VScode配置"><a href="#2-VScode配置" class="headerlink" title="2.VScode配置"></a>2.VScode配置</h2><h3 id="2-1-vscode安装Remote-Development插件。"><a href="#2-1-vscode安装Remote-Development插件。" class="headerlink" title="2.1 vscode安装Remote Development插件。"></a>2.1 vscode安装Remote Development插件。</h3><p>在插件那里安装即可。设置登陆时自动打开命令行窗口，通过<code>ctrl+shift+p</code>打开设置<code>Remote-SSH：Settings</code>，设置<code>Remote.SSH:Show Login Terminal</code>为<code>true</code>.</p>
<p><img src="http://lishengyu.xyz/vscode.png" alt></p>
<h3 id="2-2-连接远程主机"><a href="#2-2-连接远程主机" class="headerlink" title="2.2 连接远程主机"></a>2.2 连接远程主机</h3><p>安装完插件后左下角会出现一个绿色的图标，点击选择会在命令窗口弹出几个选项。 选择 <code>SSH | Remote-SSH：Connect to Host</code>接着会弹出：</p>
<p><img src="http://lishengyu.xyz/vscode1.png" alt></p>
<p>让你选择config文件放在哪里，必须放到被授权的秘钥所在的文件目录，如果你没有修改配置就是第一个。</p>
<h3 id="2-3-config文件配置"><a href="#2-3-config文件配置" class="headerlink" title="2.3 config文件配置"></a>2.3 config文件配置</h3>

```bash
Host server # 给配置起个名字
	HostName 1.1.1.1 # 填写远程服务器的IP或者Host
	User   username # 填写登陆远程服务器的用户的名字
```
<p>复制代码连接配置完毕后，再次<code>Connect to Host</code>选择你刚刚配置的服务器，这里连接的就是你的server了，弹出新窗口，连接成功~ </p>
<p>然后就能像本地一样编辑代码了，可以使用面板上的<code>Terminal</code>来对服务器进行操作，基本完全取代<code>xshell</code>。禁不住大喊巨硬nb！🐱‍🏍</p>
<h2 id="参考"><a href="#参考" class="headerlink" title="参考"></a>参考</h2><ul>
<li><a href="https://juejin.im/post/5cff4de6e51d45777a126171" target="_blank" rel="noopener">VSCode远程开发:Remote Development -SSH配置实录</a></li>
</ul>

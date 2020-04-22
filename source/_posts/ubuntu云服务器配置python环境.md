---
title: ubuntu云服务器配置python环境
date: 2019-10-10 23:49:03
tags: [linux,python,云]
categories: [linux]
---

<p><img src="http://lishengyu.xyz/16ba8cce3545dce9.jpg" alt></p>

<h2 id="1-安装python3-7"><a href="#1-安装python3-7" class="headerlink" title="1.安装python3.7"></a>1.安装python3.7</h2><p>购买服务器之后，需要安装一些软件，和对软件进行更新。首先一波<code>sudo apt-get update</code>,<code>sudo apt-get upgrade</code>对系统进行更新。</p>
<p>然后打开python，发现默认版本是2.7。

```python
root@Turing:~# python
Python 2.7.15+ (default, Oct  7 2019, 17:39:04) 
[GCC 7.4.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
```
<p>现在python2.x已经要被淘汰了，所以需要将默认python环境改为python3。我的服务器版本是Ubuntu 18.04。系统内置了Python 3.6和Python 2.7版本，以下是在Ubuntu 18.04系统中安装Python 3.7版本的方法。</p>
<h3 id="1-1-安装编译Python源程序所需的包"><a href="#1-1-安装编译Python源程序所需的包" class="headerlink" title="1.1 安装编译Python源程序所需的包"></a>1.1 安装编译Python源程序所需的包</h3>

```python
sudo apt install build-essential -y
sudo apt install libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev -y
sudo apt-get install zlib1g-dev
```

<h3 id="1-2-下载python-3-7源代码压缩包"><a href="#1-2-下载python-3-7源代码压缩包" class="headerlink" title="1.2 下载python 3.7源代码压缩包"></a>1.2 下载python 3.7源代码压缩包</h3>

```python
wget https://www.python.org/ftp/python/3.7.4/Python-3.7.4.tgz
```

<p>下载位置就在默认的root文件夹下：

```bash
root@Turing:~# pwd
/root
root@Turing:~# cd ..
root@Turing:/# ls -l
total 970060
drwxr-xr-x  2 root root      4096 Oct 10 23:51 bin
drwxr-xr-x  3 root root      4096 Oct 10 23:52 boot
drwxr-xr-x 19 root root      3840 Oct 10 23:48 dev
drwxr-xr-x 86 root root      4096 Oct 10 23:52 etc
drwxr-xr-x  2 root root      4096 Apr 24  2018 home
lrwxrwxrwx  1 root root        33 Jun 24 18:09 initrd.img -> boot/initrd.img-4.15.0-52-generic
lrwxrwxrwx  1 root root        33 Jun 24 18:03 initrd.img.old -> boot/initrd.img-4.15.0-20-generic
drwxr-xr-x 19 root root      4096 Jun 24 18:10 lib
drwxr-xr-x  2 root root      4096 Jun 24 18:10 lib64
drwx------  2 root root     16384 Jun 24 18:02 lost+found
drwxr-xr-x  4 root root      4096 Jun 24 18:02 media
drwxr-xr-x  2 root root      4096 Apr 27  2018 mnt
drwxr-xr-x  2 root root      4096 Apr 27  2018 opt
dr-xr-xr-x 89 root root         0 Oct 10 23:47 proc
drwx------  6 root root      4096 Oct 11 00:06 root
drwxr-xr-x 23 root root       680 Oct 10 23:50 run
drwxr-xr-x  2 root root     12288 Oct 10 23:51 sbin
drwxr-xr-x  2 root root      4096 Apr 27  2018 srv
-rw-------  1 root root 993249280 Jun 24 18:02 swapfile
dr-xr-xr-x 13 root root         0 Oct 11 00:02 sys
drwxrwxrwt  9 root root      4096 Oct 11 00:02 tmp
drwxr-xr-x 10 root root      4096 Jun 24 18:02 usr
drwxr-xr-x 11 root root      4096 Jun 24 18:02 var
lrwxrwxrwx  1 root root        30 Jun 24 18:09 vmlinuz -> boot/vmlinuz-4.15.0-52-generic
lrwxrwxrwx  1 root root        30 Jun 24 18:03 vmlinuz.old -> boot/vmlinuz-4.15.0-20-generic
```

<h3 id="1-3-解压"><a href="#1-3-解压" class="headerlink" title="1.3 解压"></a>1.3 解压</h3>

```bash
tar -xzvf Python-3.7.4.tgz
```

<h3 id="1-4-编译和安装python3-7"><a href="#1-4-编译和安装python3-7" class="headerlink" title="1.4 编译和安装python3.7"></a>1.4 编译和安装python3.7</h3><p>切换到Python源目录并运行configure脚本，该脚本将执行大量检查以确保系统上存在所有依赖项：

```bash
cd Python-3.7.4
./configure --enable-optimizations
```

<p><strong>enable-optimizations选项将通过运行多个测试来优化Python二进制文件，这将使构建过程变慢。</strong><br>然后使用make启动python构建过程：

```bash
make -j
```

<p><strong>make -j后面的数字一般是计算机CPU核心数*2，更方便的，无参就是使用所有核心。</strong></p>
<p>这个过程非常慢，耐心等待……</p>
<p><img src="http://lishengyu.xyz/gif/201910281507243b6d996cf21207bb68f2c003870cf2db.gif" alt></p>
<p>构建完成之后，安装python二进制文件：

```bash
sudo make altinstall
```

<p>这里没有使用标准的<code>make install</code>是因为它会覆盖默认的系统python3二进制文件。</p>
<p>完成之后，Python 3.7已安装并可以使用，输入以下命令进行验证：

```bash
root@Turing:~/Python-3.7.4# python3.7 --version
Python 3.7.4
```

<h3 id="1-5-将python3-7设为默认python环境"><a href="#1-5-将python3-7设为默认python环境" class="headerlink" title="1.5 将python3.7设为默认python环境"></a>1.5 将python3.7设为默认python环境</h3><p>python不同版本对应的路径：

```python
root@Turing:~/Python-3.7.4# which python3
/usr/bin/python3
root@Turing:~/Python-3.7.4# which python3.7
/usr/local/bin/python3.7
```

<p><code>update-alternatives</code>命令用来维护系统命令的符号链接，可以将多个文件链接到同一个符号文件上，并进行管理。使用<code>update-alternatives --install</code>建立链接。

```python
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 8
sudo update-alternatives --install /usr/bin/python python /usr/local/bin/python3.7 4
```

<p>即我们在<code>/usr/bin/python</code>这个目录下，建立一个链接符号为“Python”的链接，这里指定了两个目录，分别是Python3.6和Python3.7的。这里使用python版本后面的数字进行区分，分别是1和2，代表了优先级，数字越大优先级越高，这里明显选择了python3.7！</p>
<p>接下来选择要执行的版本，然后回车就行

```bash
sudo update-alternatives --config python
```
<p>这样就将python3.7设置为默认环境了，输入python可得：

```python
root@Turing:~/Python-3.7.4# python
Python 3.7.4 (default, Oct 11 2019, 01:07:59) 
[GCC 7.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

<h2 id="2-安装一些必要的python包"><a href="#2-安装一些必要的python包" class="headerlink" title="2.安装一些必要的python包"></a>2.安装一些必要的python包</h2><p>首先更新pip：

```python
pip install --upgrade pip
```

<p>python源是阿里云的，速度很快，不需要进行更换，接下来依次安装<code>numpy</code>,<code>scipy</code>,<code>matplotlib</code>即可。</p>
<h3 id="2-1-更换python源"><a href="#2-1-更换python源" class="headerlink" title="2.1 更换python源"></a>2.1 更换python源</h3><p>后面优惠买了百度云，发现百度云没有自己的源，下载python包特别慢，这里就需要更换python源。</p>
<ol>
<li>根目录创建.pip文件：mkdir ~/.pip</li>
<li>创建文件pip.conf：vim .pip/pip.conf</li>
<li>点击“i”键，进入编辑模式，复制信息：

```python
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```
</li>
</ol>
<p>这个更换的是清华的源，清华的源5分钟同步官网一次，建议使用。另附上其他源：<br>清华大学 <a href="https://pypi.tuna.tsinghua.edu.cn/simple/" target="_blank" rel="noopener">https://pypi.tuna.tsinghua.edu.cn/simple/</a><br>阿里云 <a href="http://mirrors.aliyun.com/pypi/simple/" target="_blank" rel="noopener">http://mirrors.aliyun.com/pypi/simple/</a><br>中国科技大学 <a href="https://pypi.mirrors.ustc.edu.cn/simple/" target="_blank" rel="noopener">https://pypi.mirrors.ustc.edu.cn/simple/</a><br>豆瓣(douban) <a href="http://pypi.douban.com/simple/" target="_blank" rel="noopener">http://pypi.douban.com/simple/</a><br>中国科学技术大学 <a href="http://pypi.mirrors.ustc.edu.cn/simple/" target="_blank" rel="noopener">http://pypi.mirrors.ustc.edu.cn/simple/</a></p>
<ol>
<li>点击：“ESC”切换到命令行模式，输入“:wq”保存离开。<h3 id="2-2-TensorFlow2-0"><a href="#2-2-TensorFlow2-0" class="headerlink" title="2.2 TensorFlow2.0"></a>2.2 TensorFlow2.0</h3></li>
</ol>

```python
pip install tensorflow==2.0.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

<p>后面的 -i 表示从国内清华源下载，速度比默认源快很多。服务器上式阿里源，一样很快，就不需要后面的链接了。</p>
<h3 id="2-3-jupyter-notebook"><a href="#2-3-jupyter-notebook" class="headerlink" title="2.3 jupyter notebook"></a>2.3 jupyter notebook</h3><p>直接使用pip安装：

```python
pip install jupyer
```

此时输入`jupyter-notebook`会返回`jupyter: command not found`。
遇到这个状况退出重新登录就好。如果仍有问题可以尝试再次安装：

```bash
sudo apt install jupyter-notebook
```
<p>但这样还是无法正确运行<code>jupyter-notebook</code>，报错的代码是：

```bash
Traceback (most recent call last):
  File "/usr/local/lib/python3.7/site-packages/notebook/services/sessions/sessionmanager.py", line 9, in <module>
    import sqlite3
  File "/usr/local/lib/python3.7/sqlite3/__init__.py", line 23, in <module>
    from sqlite3.dbapi2 import *
  File "/usr/local/lib/python3.7/sqlite3/dbapi2.py", line 27, in <module>
    from _sqlite3 import *
ModuleNotFoundError: No module named '_sqlite3'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/usr/local/bin/jupyter-notebook", line 6, in <module>
    from notebook.notebookapp import main
  File "/usr/local/lib/python3.7/site-packages/notebook/notebookapp.py", line 86, in <module>
    from .services.sessions.sessionmanager import SessionManager
  File "/usr/local/lib/python3.7/site-packages/notebook/services/sessions/sessionmanager.py", line 12, in <module>
    from pysqlite2 import dbapi2 as sqlite3
ModuleNotFoundError: No module named 'pysqlite2'
```
<p>目前还没有找到合适的解决办法，先把jupyter卸载了，找机会再安装吧。</p>
<p>上面的问题在百度云的服务器上并没有发现，直接运行<code>jupyter notebook</code>就能在浏览器上打开了。也不知道阿里云是怎么回事，先在百度云上接着部署吧。</p>
<h4 id="jupyter-notebook-修改配置实现远程访问"><a href="#jupyter-notebook-修改配置实现远程访问" class="headerlink" title="jupyter notebook 修改配置实现远程访问"></a>jupyter notebook 修改配置实现远程访问</h4><ol>
<li><p>生成配置文件</p>

```bash
root:jupyter notebook --generate-config
```

</li>
<li><p>打开ipython，创建一个密文密码</p>

```bash
n [1]: from notebook.auth import passwd
In [2]: passwd()
Enter password: 
Verify password: 
Out[2]: 'sha1:e2797300b176:cb102df65c7b5f2f8e40691f807731b4c149e12e'
```
</li>
</ol>
<p>将<code>Out[2]</code>的输出的密文复制</p>
<ol>
<li>修改配置文件

```bash
root:vim ~/.jupyter/jupyter_notebook_config.py
```

</li>
</ol>
<p>在配置文件下面按照下面要求修改：

```bash
# 重要，允许任何源访问该服务
c.NotebookApp.allow_origin = '*'
c.NotebookApp.ip='*' # 就是设置所有ip皆可访问
c.NotebookApp.password = u'sha:ce...刚才复制的那个密文'
c.NotebookApp.open_browser = False # 禁止自动打开浏览器
c.NotebookApp.port =7000 #随便指定一个端口
# 设置默认jupyter打开目录
c.NotebookApp.notebook_dir = '/python/'
```

<h4 id="jupyter-notebook美化"><a href="#jupyter-notebook美化" class="headerlink" title="jupyter notebook美化"></a>jupyter notebook美化</h4><p>使用<code>pip</code>安装<code>jupyterthemes</code>

```bash

# install jupyterthemes
pip install jupyterthemes

# upgrade to latest version
pip install --upgrade jupyterthemes

```

完成之后，就可以用命令调整<code>jupyter</code>的主题字号以及字体等，可以去看<code>jupyterthemes</code>的<a href="https://github.com/dunovank/jupyter-themes" target="_blank" rel="noopener">文档</a>，很简单，调整几个就可以了。</p>
<p>使用<code>jt -l</code>就能看到主题，这里就不详述了。我的命令是：

```bash
jt -t onedork -f roboto -fs 12 -nfs 12 -tfs 12 -ofs 10 -T -N
```


<p>最后的界面变成了：</p>
<p><img src="http://lishengyu.xyz/jupyter.png" alt></p>
<h4 id="jupyter-后台运行"><a href="#jupyter-后台运行" class="headerlink" title="jupyter 后台运行"></a>jupyter 后台运行</h4><p>一般情况下，使用下面的命令就行：

```bash
# 1.入门级: 
jupyter notebook --allow-root > jupyter.log 2>&1 &
# 2.进阶版: 
nohup jupyter notebook --allow-root > jupyter.log 2>&1 &
```
<p>解释: </p>
<ol>
<li>用&amp;让命令后台运行, 并把标准输出写入<code>jupyter.log</code>中。<code>nohup</code>表示<code>no hang up</code>, 就是不挂起, 于是这个命令执行后即使终端退出, 也不会停止运行.</li>
<li>终止进程<br>执行上面第2条命令, 可以发现关闭终端重新打开后, 用jobs找不到jupyter这个进程了, 于是要用<code>ps -a</code>, 可以显示这个进程的pid。<code>kill -9 pid</code> 终止进程</li>
</ol>
<p>但是这样我是不行的，于是采用了另外一种方法：使用了<code>tmux</code></p>
<p>终端多路复用器（<code>tmux</code>）保持<code>SSH</code>会话在<code>ssh</code>终端关闭后在后台运行：</p>
<ol>
<li>启动ssh终端</li>
<li>输入tmux。它会在同一个终端打开一个窗口。(如果没有安装，使用<code>apt install tmux</code>安装即可)</li>
<li><p>在打开的<code>tmux</code>界面输入<code>jupyter notebook --allow -root</code>启动<code>Jupyter Notebook</code>。打开<code>jupyter notebook</code>。现在，如果SSH终端关闭/终止，它将继续在实例上运行您的笔记本。</p>
</li>
<li><p>如果想在后台关闭<code>jupyter</code>，就在<code>tmux</code>里面重新输入<code>jupyter notebook --allow -root</code>，然后再<code>Ctrl-C</code>就能终止。</p>
</li>
</ol>

      
---
layout: post
title: 创建git仓库
tag: git
---

<p>
服务器端: linux<br/>
客户端: windows xp<br/>
</p>

<h3>服务器端安装并设置git: </h3>
<p>
下载git http://kernel.org/pub/software/scm/git/git-1.7.6.1.tar.bz2<br/>
解压并安装:
<pre>
$ tar -jxvf git-1.7.6.1.tar.bz2
$ cd git-1.7.6.1
$ ./configure -prefix=/usr/local/git
$ make
$ make install
</pre>
配置环境变量:
<pre>
$ cd ~
$ vi .bashrc
</pre>
在末尾添加如下行:
<pre>
export GIT_HOME=/usr/local/git
export PATH=$GIT_HOME/bin:$GIT_HOME/libexec/git-core:$PATH
</pre>
保存并生效：
<pre>
$ source .bashrc
</pre>
</p>
<p>

<h3>在服务器创建一个空的仓库</h3>
<pre>
$ mkdir my.git
$ cd my.git
$ git init --bare
</pre>

<h3>在客户端windows上安装git</h3>
<p>
下载git http://code.google.com/p/msysgit/downloads/list?can=3
安装过程参见 http://help.github.com/win-set-up-git/
</p>

<h3>生成ssh key并设置ssh免密码登录验证</h3>
<pre>
$ ssh-keygen -t rsa -C "your_email@youremail.com"
$ cd .ssh/
$ scp id_rsa.pub git@git-linux:mykey
$ ssh git@git-linux
$ mv mykey .ssh
$ cat mykey >> authorized_keys
$ chomod 600 authorized_keys
$ exit
</pre>
</p>

<h3>初始化my.git仓库</h3>
<p>
windows客户端打开git bash
<pre>
$ mkdir my.git
$ cd my.git
$ git init
$ echo "project initial" > readme
$ git add readme
$ git commit -m 'project initial'
$ git remote add origin git@git-linux:my.git
$ git push origin master
</pre>
到此项目仓库初始化完毕，可以使用git clone了
<pre>
$ git clone git@git-linux:my.git
$ ls
</pre>
之后本地目录会有一个my的文件夹
</p>











---
layout: post
title: "vim的调教日记(1)"
title2: "Install vim8.0 by source codes"
date: 2016-02-17
category: code
tags: vim install source
comments: true
---

# Git到源代码
1. 如果你没有git过vim
{% highlight bash %}
git clone https://github.com/vim/vim.git
{% endhighlight bash %}
如果你有vim的git
{% highlight bash %}
cd vim
git pull
{% endhighlight bash %}
2. 安装vim
{% highlight bash %}
cd src
make distclean # if you build Vim before
make
sudo make install
{% endhighlight bash %}
但是上述方式安装并不理想，由此我参考了下其他的方法
# 站在巨人的肩膀上

1. 从[这里](https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source)可以了解到vim 8.0的源码安装方法
Chiness Translation from the link above:
1) 第一步是预安装相关的库和包
{% highlight bash %}
sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
    libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
    python3-dev ruby-dev lua5.1 lua5.1-dev libperl-dev git
{% endhighlight bash %}
ps:在ubuntu 16.04上,lua包的名字是liblua5.1-dev

对于Fedora 20,相关指令如下:
{% highlight bash %}
sudo yum install -y ruby ruby-devel lua lua-devel luajit \
    luajit-devel ctags git python python-devel \
    python3 python3-devel tcl-devel \
    perl perl-devel perl-ExtUtils-ParseXS \
    perl-ExtUtils-XSpp perl-ExtUtils-CBuilder \
    perl-ExtUtils-Embed
{% endhighlight bash %}

{% highlight bash %}
# symlink xsubpp (perl) from /usr/bin to the perl dir
sudo ln -s /usr/bin/xsubpp /usr/share/perl5/ExtUtils/xsubpp 
{% endhighlight bash %}
此条指令是有关于Fedroa 20的XSubPP安装

2) 第二步是预先卸载之前的vim

更多vimscript细节，请参照[Learn Vimscript the Hard Way](http://learnvimscriptthehardway.stevelosh.com/)

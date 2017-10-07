---
layout: post
title: "vim的调教日记(1)--vim8.0源码安装教程"
title2: "Install vim8.0 by source codes"
date: 2017-01-01
category: code
tags: vim install source
comments: true
---

### Git源代码

1\. 如果你没有git过vim

```bash
git clone https://github.com/vim/vim.git
```

如果你有vim的git

```bash
cd vim
git pull
```

2\. 安装vim

```bash
cd src
make distclean # if you build Vim before
make
sudo make install
```

但是上述方式安装并不理想，由此我参考了下其他的方法

### 站在巨人的肩膀上

1\. 从[这里](https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source)可以了解到vim 8.0的源码安装方法

1) 第一步是预安装相关的库和包

```bash
sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
    libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
    python3-dev ruby-dev lua5.1 lua5.1-dev libperl-dev git
```

ps:在ubuntu 16.04上,lua包的名字是liblua5.1-dev

对于Fedora 20,相关指令如下:

```bash
sudo yum install -y ruby ruby-devel lua lua-devel luajit \
    luajit-devel ctags git python python-devel \
    python3 python3-devel tcl-devel \
    perl perl-devel perl-ExtUtils-ParseXS \
    perl-ExtUtils-XSpp perl-ExtUtils-CBuilder \
    perl-ExtUtils-Embed
```

```bash
# symlink xsubpp (perl) from /usr/bin to the perl dir
sudo ln -s /usr/bin/xsubpp /usr/share/perl5/ExtUtils/xsubpp 
```

此条指令是有关于Fedroa 20的XSubPP安装

2) 第二步是预先卸载之前的vim

```bash
sudo apt-get remove vim vim-runtime gvim
```


或者你需要

```bash
sudo apt-get remove vim-tiny vim-common vim-gui-common vim-nox
```

3) 进行编译和make设定

ps:当你使用python时，请自行确保配置目录的正确性，并对应修改python-config-dir或者python3-config-dir参数

```bash
cd ~
git clone https://github.com/vim/vim.git
cd vim
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp=yes \
            --enable-pythoninterp=yes \
            --with-python-config-dir=/usr/lib/python2.7/config \
            --enable-python3interp=yes \
            --with-python3-config-dir=/usr/lib/python3.5/config \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-gui=gtk2 --enable-cscope --prefix=/usr
make VIMRUNTIMEDIR=/usr/share/vim/vim80
```

如果你安装的是8.0a版本，请修改VIMRUNTIMEDIR=/usr/shar/vim/vim80a

设置完毕之后，直接make就行了

```bash
cd ~/vim
sudo make install
```

到这里vim8.0已经安装完毕了，但是或许你还需要修改你的默认编辑器

```bash
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 1
sudo update-alternatives --set editor /usr/bin/vim
sudo update-alternatives --install /usr/bin/vi vi /usr/bin/vim 1
sudo update-alternatives --set vi /usr/bin/vim
```

更多vimscript细节，请参照[Learn Vimscript the Hard Way](http://learnvimscriptthehardway.stevelosh.com/)

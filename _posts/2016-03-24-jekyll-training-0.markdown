---
layout: post
title: "jekyll的安装笔记(0)"
date: 2016-03-23
category: code
tags: jekyll windows ruby
comments: true
---
由于win10的更新换代，导致了很多之前的jekyll安装方法出现了一些问题。

把我的经验教训，写在这里希望对大家有启发。

### Ruby和Devkit安装

从[这里](http://rubyinstaller.org/downloads/)下载Ruby和对应的Devkit

Ruby无脑安装即可

将Devkit解压，然后在解压的目录下打开命令提示符，执行
```rb
ruby dk.rb init
ruby dk.rb install
```

_由于win10的问题，请把Devkit/bin添加到系统环境变量中_

### jekyll安装以及其他配置

因为GFW的关系，所以我们首先应该更换gems的源
```rb
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
gem sources -l
```

然后我们再安装jekyll
```rb
gem install jekyll
```

但是，如果想要使用别人的模版，这样是往往是不够的

以我的[模版](https://github.com/dirkfabisch/mediator)为例
```bash
git clone https://github.com/dirkfabisch/mediator
```

然后在mediator中执行
```rb
jekyll serve
```

会提示缺少相应gems，一个个手动安装通常是不可行的

_解决办法：_
首先安装bundle，ruby程序安装的神器
```rb
gem install bundle
```


去到在**对应**的目录下，还是GFW的原因，我们先更换bundle的源
```rb
bundle config mirror.https://rubygems.org https://ruby.taobao.org
```

之后就走一个ruby使用bundle的流程
```rb
bundle update && bundle install
bundle exec jekyll serve
```

问题到此得到解决。

* 2016.12.24 更新
在ubuntu下不能使用bundle安装部分gem,后来发现是ruby dev环境配置不正确
错误信息如下

> ERROR:  While executing gem ... (Gem::FilePermissionError)
> 	You don't have write permissions for the /var/lib/gems/2.3.0 directory.
> xacking@ubuntu:~/Blog/TstBlog$ sudo gem install RedCloth -v '4.2.9'
> Building native extensions.  This could take a while...
> ERROR:  Error installing RedCloth:
>  	ERROR: Failed to build gem native extension.
>
> current directory: /var/lib/gems/2.3.0/gems/RedCloth-4.2.9/ext/redcloth_scan  
> /usr/bin/ruby2.3 -r ./siteconf20161214-2465-1hrl24k.rb extconf.rb
> mkmf.rb can't find header files for ruby at /usr/lib/ruby/include/ruby.h
>
> extconf failed, exit code 1
>
> Gem files will remain installed in /var/lib/gems/2.3.0/gems/RedCloth-4.2.9 for inspection.
> Results logged to /var/lib/gems/2.3.0/extensions/x86\_64-linux/2.3.0/RedCloth-4.2.9/gem_make.out


ubuntu下apt-get的安装包版本不是特别一致,导致我ruby环境有问题
给出一个懒惰的解决方案
```shell
sudo apt-get install ruby-dev
```

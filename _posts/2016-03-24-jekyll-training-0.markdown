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

#Ruby和Devkit安装

从[这里](http://rubyinstaller.org/downloads/)下载Ruby和对应的Devkit

Ruby无脑安装即可

将Devkit解压，然后在解压的目录下打开命令提示符，执行

{% highlight ruby %}
ruby dk.rb init
ruby dk.rb install
{% endhighlight ruby %}

_由于win10的问题，请把Devkit/bin添加到系统环境变量中_

#jekyll安装以及其他配置

因为GFW的关系，所以我们首先应该更换gems的源
{% highlight ruby %}
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
gem sources -l
{% endhighlight ruby %}

然后我们再安装jekyll
{% highlight ruby %}
gem install jekyll
{% endhighlight ruby %}

但是，如果想要使用别人的模版，这样是往往是不够的

以我的[模版](https://github.com/dirkfabisch/mediator)为例

{% highlight bash %}
git clone https://github.com/dirkfabisch/mediator
{% endhighlight bash %}

然后在mediator中执行

{% highlight ruby %}
jekyll serve
{% endhighlight ruby %}

会提示缺少相应gems，一个个手动安装通常是不可行的

_解决办法：_
首先安装bundle，ruby程序安装的神器
{% highlight ruby %}
gem install bundle
{% endhighlight ruby %}


去到在**对应**的目录下，还是GFW的原因，我们先更换bundle的源
{% highlight ruby %}
bundle config mirror.https://rubygems.org https://ruby.taobao.org
{% endhighlight ruby %}

之后就走一个ruby使用bundle的流程
{% highlight ruby %}
bundle install
bundle update
bundle exec jekyll serve
{% endhighlight ruby %}

问题到此得到解决。

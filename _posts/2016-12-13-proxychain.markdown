---
layout: post
title:  "proxychain的使用"
date:   2016-12-13
categories: codes
image: /assets/article_images/2016-02-12-hello-world/title.jpg
comments: true
---

在ubuntu下使用ss代理指令是一件麻烦的事情,尤其是ubuntu自带的全局设置还没有那么好用

使用proxychains成为了一种折衷的选择

* 安装proxychains

{% highlight bash %}
sudo apt-get install proxychains
{% endhighlight bash %}

* 编辑proxychains配置

1. poxychains路径位置
{% highlight bash %}
vim /etc/proxychains.conf
{% endhighlight bash %}
2. 修改socks4条目,其中1080为你自己的端口
{% highlight bash %}
socks5 127.0.0.1 1080
{% endhighlight bash %}

* 使用proxychains

{% highlight bash %}
proxychains ...
{% endhighlight bash %}


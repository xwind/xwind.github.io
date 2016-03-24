---
layout: post
title: "jekyll数学扩展"
date: 2016-03-24
category: code
tags: jekyll mathjax
comments: true
---

* 修改\_include/javascripts.html

{% highlight html %}
<script type="text/javascript"
 src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
{% endhighlight html %}

* 打开命令提示符
{% highlight ruby %}
gem install kramdown
{% endhighlight ruby %}

* 修改\_config.yml
{% highlight html %}
markdown: kramdown
{% endhighlight html %}

* 效果测试
$$a^2 + b^2 = c^2$$

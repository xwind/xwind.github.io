---
layout: post
title: "jekyll数学扩展"
date: 2016-03-24
category: code
tags: jekyll mathjax
comments: true
---

* 修改\_include/javascripts.html
```html
<script type="text/javascript"
 src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```

* 打开命令提示符
```rb
gem install kramdown
```

* 修改\_config.yml
```yaml
markdown: kramdown
```

* 效果测试
$$a^2 + b^2 = c^2$$

---
layout: post
title: "Python File To Bytes，And Some IO Problems"
title2: "本文主要讨论 Python IO 操作的技巧"
date: 2017-10-10
category: python
tags: python IO PIL
comments: true
---

### BytesIO, StringIO And RawIO
\\
1\. Raw I/O
操作非文本文件，建议直接使用 Raw IO，不要自己随意 encode，decode

```python
f = open("myfile.jpg", "rb", buffering=0)
```

2\. BytesIO
某些时候，比如使用PIL的时候，我们无法得到文件的 Raw IO，所以往往需要自己动手转化。

现在已经是 PY3 的时代了，用 StringIO 处理其实是不规范的

```python
IM = BytesIO()
image.save(IM, format=self.image.format)  # image 为一个 PIL 文件
src = IM.getvalue().decode('ISO-8859-1')  # 转换为 str
```

3\. StringIO

### Python Imaging Library (PIL)
\\
Python 比较常用的一个图片库（Python Image 的事实标准，[修炼手册请点我](http://effbot.org/imagingbook/image.htm)

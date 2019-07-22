---
layout: post
title:  "python 10 problems"
date:   2018-06-19
tags: python
image: /assets/article_images/2018-01-01-moe-girl.jpg
---

#### Question 1
*what's your differences between "\_\_new\_\_", "\_\_init\_\_" and "\_\_call\_\_"? what's your differences between "cls" and "self"?*

#### Answer 1:
>> \_\_new\_\_: creates the instance of a Class, you use it when you need to control the creation of a new instance. 
>> \_\_new\_\_ accepts "cls" as it's first parameter but \_\_init\_\_ accepts "self". \_\_new\_\_ can return value especially class 

>> \_\_init\_\_: used to initialize the instance variables once the instance is created by \_\_new\_\_. no return value 

>> \_\_call\_\_: like a function call operator. Once you implement \_\_call\_\_ in your Class, you can invoke the Class instance as a function call.

self: instance self,  you can't call class staticmethod\\
cls: class self, you can call class staticmethod

#### Question2
*Singleton Pattern Design with at least 4 methods*

#### Answer2:
1. class with a get\_client method
2. class with \_\_new\_\_ method
3. global instance from your defined class

#### Question3
*Try to design a decorator to disturb/delay async task for avoiding triggering frequency control*

#### Answer3:
```python
# coding: utf-8

import time
import random
import functools


def shuffle_time_gap(func):

    FUNC_DICT = dict()

    @functools.wraps(func)
    def _func(*args, **kws):
        now = int(time.time())
        if FUNC_DICT.get(func.__name__, 0) >= now - 1:
            time_random_gap = random.randint(11, 12) / 1000
            time.sleep(time_random_gap)

        FUNC_DICT[func.__name__] = now
        return func(*args, **kws)

    return _func
```

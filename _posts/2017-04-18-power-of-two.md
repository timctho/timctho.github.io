---
layout     : post
title      : "231. Power of two"
subtitle   : ""
date       : 2017-04-18
author     : "Tim Ho"
tags       : LeetCode LeetCode-Easy
comments   : true
signature  : true
---

## Question
Given an integer, write a function to determine if it is a power of two.

## Solution
1. 第一個想到的解法，是count所有的bit，看bit數是不是1個，當然n要大於0。
{% highlight python %}
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        return (bin(n).count('1') == 1) and (n > 0)
{% endhighlight %}
2. 範例解法用到一個trick，如果是2的次方，n和n-1的binary表示是互斥的，反之亦然
{% highlight python %}
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        return not (n & (n-1)) and (n > 0)
{% endhighlight %}


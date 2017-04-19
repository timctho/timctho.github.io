---
layout     : post
title      : "231. Power of three"
subtitle   : ""
date       : 2017-04-18
author     : "Tim Ho"
tags       : LeetCode LeetCode-Easy
comments   : true
signature  : true
---

## Question
Given an integer, write a function to determine if it is a power of three.

## Solution
1. 一直把數字/3，是3的次方一定會剛好等於1一次。數字大的時候超慢。
{% highlight python %}
class Solution(object):
    def isPowerOfThree(self, n):
        """
        :type n: int
        :rtype: bool
        """      
        while n > 0:
            if n == 1: return True
            n /= 3.
        return False
{% endhighlight %}
2. 承襲1.的想法，但過程中如果變成不是3的倍數其實就不用再做下去了。
{% highlight python %}
class Solution(object):
    def isPowerOfThree(self, n):
        """
        :type n: int
        :rtype: bool
        """      
        while n > 0:
            if n == 1: return True
            if n % 3: return False
            n /= 3         
        return False
{% endhighlight %}
3. 用到log裡面的換底公式，`log(n) / log(3)` 會是一個整數如果n是3的次方。 但注意不是所有底都可以用，因為會碰到float rounding的問題。有人說java用10當底可以，但我在python用又不行，試過用2是可以的。
{% highlight python %}
class Solution(object):
    def isPowerOfThree(self, n):
        """
        :type n: int
        :rtype: bool
        """
        return (n > 0) and (((math.log(n, 2) / math.log(3, 2)) % 1) == 0)
{% endhighlight %}





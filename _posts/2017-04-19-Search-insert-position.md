---
layout     : post
title      : "35. Search Insert Position"
subtitle   : ""
date       : 2017-04-19
author     : "Tim Ho"
tags       : LeetCode LeetCode-Easy
comments   : true
signature  : true
---

## Question
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
You may assume no duplicates in the array.

## Solution
1. 已排序的array，用binary search。 可以加入兩個邊界判斷，也會省掉很多運算。
{% highlight python %}
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left = 0
        right = len(nums)-1

        if target > nums[right]: return right + 1
        if target < nums[left]: return left

        mid = 0
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1

        return left

{% endhighlight %}

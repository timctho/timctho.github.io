---
layout     : post
title      : "83. Remove Duplicates from Sorted List"
subtitle   : ""
date       : 2017-04-19
author     : "Tim Ho"
tags       : LeetCode LeetCode-Easy
comments   : true
signature  : true
---

## Question
Given a sorted linked list, delete all duplicates such that each element appear only once.

## Solution
1. 從list開頭開始，如果現在node val和下一個node val一樣，就可以跳過下一個node。有可能有重複多次的例如1->2->2->2->2->3->4，所以中間要用while判斷。
{% highlight python %}
class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == []: return head

        cur = head
        while cur:
            while cur.next and cur.val == cur.next.val:
                cur.next = cur.next.next
            cur = cur.next
        return head
{% endhighlight %}

---
layout     : post
title      : "437. Path Sum III"
subtitle   : ""
date       : 2017-04-20
author     : "Tim Ho"
tags       : LeetCode LeetCode-Easy
comments   : true
signature  : true
---

## Question
You are given a binary tree in which each node contains an integer value.<br>
Find the number of paths that sum to a given value.<br>
The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).<br>
The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

## Solution
* 以DFS的順序，加總每個node當起點時，可以有幾種可能的path。

{% highlight python %}
class Solution(object):
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: int
        """

        def count_path(node, num):
            if node is None:
                return 0
            return (node.val == num) + count_path(node.left, num - node.val) + count_path(node.right, num - node.val)

        def dfs(root, num):
            if not root:
                return 0
            return count_path(root, num) + dfs(root.left, num) + dfs(root.right, num)

        return dfs(root, sum)
{% endhighlight %}

* 討論區的最快解法，是利用hash table，非常厲害啊，看了好久才看懂。<br>
   想法是紀錄從 `root` 開始到 `current node` 的所有可能path sum，在 `current node` 如果能夠完成一個path，那就是從 `root` 到 `current node` 的sum減掉某個先前存起來的path sum剛好等於 `target`，而準確來說，這條path就是path sum的結尾的 `node` 到 `current node`。<br>
   一樣以DFS的順序走訪整顆tree，走到底返回的時候要記得把經過這個 `node` 的path sum給去掉，因為接下來的 `node` 不會再經過這裡了，留著的話會誤認以為這裡可以走。<br>
   只要從root開始DFS一次就好了，O(N) time，super fast。

```
舉個例子，一顆樹長做 [10,5,-2,3,2,None,11,3,-2,None,1,None,-3] ，DFS順序跟table變化如下。
```
<div align="center">
<img src="{{baseurl}}/images/leet_code/pathSum.png" />
</div>

{% highlight python %}
from collections import defaultdict
class Solution(object):
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: int
        """
        preSum = defaultdict(int)
        preSum[0] = 1

        return self.helper(root, sum, 0, preSum)

    def helper(self, root, target, curSum, preSum):
        if not root:
            return 0

        curSum += root.val
        paths = preSum[curSum - target]
        preSum[curSum] += 1

        paths += self.helper(root.left, target, curSum, preSum)\
                 + self.helper(root.right, target, curSum, preSum)
        preSum[curSum] -= 1

        return paths
{% endhighlight %}

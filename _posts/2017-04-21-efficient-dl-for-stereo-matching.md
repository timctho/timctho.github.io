---
layout     : post
title      : "Efficient Deep Learning For Stereo Matching"
subtitle   : ""
date       : 2017-04-21
author     : "Tim Ho"
tags       : Stereo-Matching CVPR-2016
comments   : true
signature  : true
---

## 前言
之前的CNN-based stereo matching方法

* Patch match: image切成很多個 `patch` ，用Siamese network比較每個patch和另一張圖上的patch是不是一樣，問題是computation cost很高，O(N^2)，N是patch個數。




## 論文想法
這篇將stereo matching當作一個 `multi class` 分類問題，每個class是一個對應的 `disparity` 值。
input是rectified過的image pair，所以每個pixel只需要在水平的方向上做disparity search。

<div align="center">
<img src="{{baseurl}}/images/efdl_stereo_matching/network.png" />
</div>

## Network架構
是一個9層左右的CNN，在測試數據裡根據receptive field的大小比較不同大小network的效能差距。
關鍵是提出了 

`Product Layer` : 將左右image經過 `forward` 後，對 `representation` 做inner product，找 `correlation` 最大的位置，作為matching的結果。

每張image只需要經過一次forward，是它速度快的原因。這個架構和之前介紹用來做tracking的 `Siamese FC` ，概念基本上是一樣的。


## Training
training set的產生：對於left image每個pixel，取一個patch，在right image上取一個 `patch_h * (|disparity| + patch_w) `的search image。

分別經過forward後，一邊output feature dim=`64`，一邊output feature dim=`64*|disparity|`，接著就可以做inner product，經過一個softmax，得到在不同disparity之下的機率值。
Ground truth的值是由下面這個metric所產生，希望smooth而不是非1即0的label，所以是以真實disparity為中心，根據距離給予不同機率。 計算loss時是用cross entropy。

<div align="center">
<img src="{{baseurl}}/images/efdl_stereo_matching/gt.png" />
</div>


在testing時，forward整張image，會output一個HxWx64的cost volume，就像是每個pixel給予一個64 dim的feature，之後就用這個feature來做inner product，省掉了很多重複運算。

不過拿到feature之後如果用pixel-wise的方式找disparity是不會work的，因為如果碰到遮蔽、重複pattern的情況，他就找錯了，整張圖會出現一堆找錯的點，所以需要考慮局部資訊。這篇作者使用了Cost aggregation、Semi-global block matching、Slanted plane等方式。

* Cost aggregation: 就是average pooling。
* Semi-global block matching: 加入和鄰近點的pairwise cost，鼓勵smooth disparity。

<div align="center">
<img src="{{baseurl}}/images/efdl_stereo_matching/semi_global_block_matching.png" />
</div>


## 結果
error略大於目前前段班的 `MC-CNN`、 `Displets v2`，但correlation就是快，thats the price we pay。


<div align="center">
<img src="{{baseurl}}/images/efdl_stereo_matching/kitti2012.png" />
</div>

<div align="center">
<img src="{{baseurl}}/images/efdl_stereo_matching/kitti2.png" />
</div>

---
layout     : post
title      : "Siamese-FC"
subtitle   : "Fully-Convolutional Siamese Networks for Object Tracking"
date       : 2017-04-17
author     : "Tim Ho"
tags       : Deep-Learning Object-Tracking ECCV-2016
comments   : true
signature  : true
---

## 前言
這篇用similarity的方式來解tracking，network是siamese的形式，input一邊為要追蹤`物體的examplar`，另一邊為`要追蹤物體的image`。
在維持一定準確率的表現下達到了realtime tracking。

---

<div align="center">
<img src="{{baseurl}}/images/siamese_fc/network.png" />
</div>

## 論文想法
Siamese network設計為fully convolutional，所以要追蹤物體的image size不會被限制住，小的image output較小的feature map，越大的image就output越大的feature map。 同理examplar的size也是沒有限制的，但paper中為了training時產生mini batch容易一些，有把examplar都resize到同樣大小。

這樣的設計最大的優點就在於每個時間點image只需要`forward一次`，接著找尋物體在畫面中的哪個位置，概念和correlation filter很像，只是對feature map每個位置都做inner product，找尋response最大的地方，所以速度上可以達到realtime。

---

## Network架構
就是`AlexNet`，但為了要fully convolutional，所以把後面的`fc`都拔掉，只用`conv5`。

---

## Training
產生training image pair的方式，是在video t=1時框出物體，之後最多到t=k，取出所有含有物體的image做pair，所以最多產生k組image pair。
因為loss是在feature map上面計算的，這裡有一個參數R，表示在feature map上以要追蹤的物體為中心R以內的距離，都當作是正樣本，其餘當作負樣本，以此計算loss。

<div align="center">
<img src="{{baseurl}}/images/siamese_fc/loss.png" />
</div>


---

## 結果
雖然方法很簡單，表現是相當不錯，特別在速度的部分，VOT2015的前15名tracker，只有這篇突破realtime的需求。

<div align="center">
<img src="{{baseurl}}/images/siamese_fc/voc15.png" />
</div>

<div align="center">
<img src="{{baseurl}}/images/siamese_fc/result.png" />
</div>






---
layout     : post
title      : "Hello Git Page + Jekyll !"
subtitle   : "Git page建立 + Jekyll安裝流程"
date       : 2017-04-15
author     : "Tim Ho"
tags       : GitPage Jekyll
comments   : true
signature  : true
---

### Whats Git Page?
Github除了可以管理、分享程式碼之外，也有提供一個服務叫做Git Page，可以讓你在自己的Github帳號下建立靜態網站(HTML、CSS、JavaScript)，還提供Jekyll幫助你建立靜態網站。 

如果你像我一樣只是想找一個地方記錄、分享自己的學習歷程，我覺得Git Page是一個快速好上手的選擇，套個喜歡的jekyll template，稍微熟悉一下markdown語法，就能開始寫一個漂亮的Blog。

---

### 開始 Git Page
建立Git Page，首先要開一個新的repository。這邊有兩種方式，取決於你的網站想要呈現怎樣的url

(1) repository的名字叫做 `user_name.github.io` ，那之後你的url就會是 `user_name.github.io` ，網站內容直接放在 `master` 中就可以了。

![]({{baseurl}}/images/Git_Page/new_gitpage.png) 

(2) 其他的repository名字，例如叫做 `hello_gitpage`，那之後你的url就會是 `user_name.github.io/hello_gitpage`，而且網站內容不能直接放在 `master`，要另外開一個叫做 `gh-page` 的branch，再放在裡面。


之後到 `repository -> Settings` ，找到Github Pages，把他啟用就可以了，也有一些簡單的template可以套用。

---

### Jekyll
為了方便在本機做網站編輯跟預覽，我們仍然需要安裝Jekyll。 
Jekyll底層是用Ruby開發的，所以先安裝Ruby。

(1) [Ruby官網](http://rubyinstaller.org/downloads/){:target="_blank"} 下載目前最新的2.3.3版本

(2) 同樣在官網，下載版本相對應的Dev-kit

![]({{baseurl}}/images/Git_Page/ruby.png) 

(3) 安裝完Ruby後，就可以用他的 `gem` 這個指令安裝各種package，當然也包括Jekyll。

`gem install jekyll bundler`

到這邊就安裝完所有需要的東西了，然後如果你和我一樣沒什麼寫網站的經驗，google就有很多 [jekyll template](https://github.com/jekyll/jekyll/wiki/Themes){:target="_blank"}，just find one and start to write!









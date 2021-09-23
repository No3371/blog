---
layout: post
title: "Git 客戶端換用 Fork 快到起飛"
tags: git
published: true
language: tw
other_language_versions:
  - en/2021-08-17-fork-goes-brrrrrrr.md=en
---

這兩三年來我一直是忠實的 GitKraken 使用者，我真的很喜歡它的 UI/UX 跟使用體驗，甚至熱情地推薦給很多人——雖然一隻手數得過來，但對我來說已經很多了，畢竟我實在是沒幾個朋友。

但是！GitKraken 是有名地慢，尤其是開啟大 Repo 的時候其效能出奇地差，最早的討論甚至可以追溯到[十年前](https://github.com/git-cola/git-cola/issues/48)。我在一間不算小的公司工作，會碰到一些肥大的專案，有時候光是程式碼就高達數十 mb，在這些專案使用 GitKraken 簡直是一種折磨。

光是顯示單一個檔案的內容就可以跑好幾秒鐘，這完全沒辦法幫它找到正當的理由......說真的，三小？就連 🗒記事本 都比它快，讀取檔案內容根本不需要經由 git 吧？到底在跑什麼？我真的不知道這幾年我哪來的耐心跟它耗。

一直以來， 我時不時都會搜尋替代的 Git 客戶端，希望能找到擁有跟 GitKraken 一樣棒的 UI/UX 的新選擇，這很重要，不然我寧可直接用 Git Cli，就當作順便訓練自己成為 Git 大師。很可惜我一直沒找到，不得不說，GitKraken 的介面難以取代，所以我一直沒嘗試過別的客戶端。

但現在我真的是受不了了，每個點擊都要花好幾秒才有反應，簡直是效率/體驗毀滅者，也像是在羞辱這幾年每年為了 GitKraken 付費的我。所以我去了官方 [GUI Clients](https://git-scm.com/downloads/guis)清單血拚，最後選擇了 [Fork](https://git-fork.com/)。它的官網標榜 `Fast and Friendly`還真是沒在蓋的，就連 UI/UX 都比我想像中還要優秀得多。

順帶一提，有一款叫做 Ungit 用 node js 寫的 web 客戶端，應該是單緒執行，連這東西都跑得比 GitKraken 還快......我的天......

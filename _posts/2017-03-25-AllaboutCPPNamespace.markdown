---
layout: post
title: 關於 C++ Namespace 的那些事
date: 2017-03-25 15:20
comments: true
external-url:
tags: [c++, bash, perl, regex]
---


之前看到一篇文章，
現在還蠻贊同的。

[StackOverflow -- scope of using declaration within a namespace
](http://stackoverflow.com/questions/6175705/scope-of-using-declaration-within-a-namespace)

裡面大概在講：最好不要在 namespace 裏使用 `using foo::blah` 。
因為萬一哪天在自訂 namespace 外面想要 using 該 namespace ，連裡面藏起來的妖魔鬼怪也一起跑出來了。

所以我天真的想說，寫一個 bash script ，讓它幫我把 `using foo::blah` 自動展開成 `foo::blah` ，然後我就崩潰了...
展開的時候匹配做得不好，~~還可能會改到一些不該動的東西~~。
（查一下資料， `sed` 似乎不好做 negative lookahead ，可能要改用 `perl` 比較好？）

~~本來還想改，但小規模用還行，算了！等明年修編譯器的時候再研究吧...~~

改好了 :D

## 後記：
2016-03-25 19:00

後來成功改成使用 `Perl` 來處理了，第一次體驗 `Perl` 的 regex 強大之處。這個版本可以選擇要處理哪個 namespace ，做完以後會清除 `using foo::blah;` 的述句。

## 使用腳本要注意的事
因為這個腳本很單純，只利用 regex 做字串替代，因此將無視所有 Scope 的作用域，替代的範圍是整個文件。

---
腳本：
[展開 using foo::bar 用腳本](https://github.com/peter0749/BashScript/blob/master/remove_using_in_CPP.sh)



---
layout: post
title: "Dropbox と リアルタイム検索"
description: ""
category: 
tags: [Windows]
---
{% include JB/setup %}

僕は Dropbox の有料ユーザーで、40GByte 程度のファイルを Dropbox フォルダーに置いています。
他にも色々同様のサービスはあるのですが、Windows,Linux(Ubuntu),Android で安定的に動くという事で今のところ Dropbox を使い続けています。 

新しいマシンを購入したときや、OS を入れ替えたときに Dropbox をセットアップするするのですが、僕の環境では LAN Sync を有効にしても一日以上は同期に時間がかかります。

あらかじめ、フォルダーの中身をコピーしておけばよいのだろとは思いますが、 それも面倒なので、大体は単純に同期するまで放置しています。
( そういう事をやらなくするために Dropbox を使っているのです。 )

昨日 Windows 7 (US版) のマシン上でもいつもと同じように放置していたのですが、ふと Resource Monitor　を見ると 
MsEpEng.exe が C:\Users\hiroshi\Dropbox\.dropbox.cache\ 上にあるファイルを読み込んでいて Disc Activity のかなりの部分が、埋まっていました。
MsEpEng.exe は Microsoft Security Essentials のリアルタイム検索です。

とりあえず、Dropbox の最初の同期が終わるまでは、ここをチェックしなくても良いとおったので、 
Microsoft Security Essentials の設定で C:\Users\hiroshi\Dropbox\.dropbox.cache スキャン対象から除外しました。


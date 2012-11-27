---
layout: post
title: "Windows 8 Pro の Hyper-V に lubuntu を入れてみました"
description: ""
category: 
tags: ['Lubuntu', 'Windows', 'Hyper-V']
---
{% include JB/setup %}

Windows 8 Pro では [Hyper-V](http://ja.wikipedia.org/wiki/Hyper-V) の機能がサポートされているので、
有効にして [lubuntu](http://lubuntu.net/) をインストールしました。

手順は

1. lubuntu の CD の ISO イメージをダウンロード<a href="#s1">[1]</a>
2. Hyper-V の機能を有効化<a href="#s2">[2]</a>
3. 仮想スイッチを作成<a href="#s3">[3]</a>
4. 仮想マシンを作成<a href="#s4">[4]</a>
5. 仮想マシンの設定<a href="#s4">[4]</a>
6. lubuntu をインストール<a href="#s5">[5]</a>

でした。

## <a name="s1">1. lubuntu の CD の ISO イメージをダウンロード</a>

[lubuntu](http://lubuntu.net/) のサイトより CD の ISO イメージをダウンロードしました。
今回は PC 64bit 版を使いました。

## <a name="s2">2. Hyper-V の機能を有効化</a>

<img src="/assets/images/2012-11/hv1.png" />

コントールパネルの **Windows の機能の有効化または無効化** で Hyper-V を有効にしました。
PC の再起動が必要でした。

## <a name="s3">3. 仮想スイッチを作成</a>

<img src="/assets/images/2012-11/hv2.png" />

**Hyper-V マネージャーを** 立ちあげて(スタートタイルにあります)、仮想スイッチを作成しました。
名前は vs01 にしました。
接続先の仮想スイッチの種類は外部ネットワークとしました。( NAT 接続はないので、
外と通信するためには外部ネットワークにする必要があります。)

## <a name="s4">4. 仮想マシンを作成</a>

<img src="/assets/images/2012-11/hv3.png" />

仮想マシンを作成しました。基本的にはウィザードにしたがって進んでいけばよいのですが、
インストール前に設定を変更するので、後でオペレーティングシステムを
インストールするを選択しました。

## <a name="s4">5. 仮想マシンの設定</a>

<img src="/assets/images/2012-11/hv4.png" />

作成した仮想マシンの、**設定...**  を開きました。
レガシーネットワークアダプタを追加しました。
レガシーネットワークアダプタで仮想スイッチ(S)を先ほど作成した vs01 に設定しました。
既にあったネットワークアダプタは削除しました。

<img src="/assets/images/2012-11/hv5.png" />

IDEコントローラ1のDVDドライブにダウンロードしておいた lubuntu の CD の ISO イメージを指定しました。

## <a name="s5">6. lubuntu をインストール</a>

<img src="/assets/images/2012-11/hv6.png" />

設定画面を閉じて、仮想マシンを**起動..**,**接続...**し lubuntu をインストールしました。
後はインストーラーの指示に従って進んでいくだけです。
今回は、「インストール中にアップデートをダウンロードする」と
「サードパーティーのソフトウエアをダウンロードする」 のどちらもチェックしました。

起動後ターミナルで lsmode | grep hv と打って Hyper-V のモジュールが組み込まれていることを確認しました。

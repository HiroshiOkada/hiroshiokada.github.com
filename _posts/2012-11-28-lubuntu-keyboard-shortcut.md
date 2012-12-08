---
layout: post
title: "Lubuntu の キーボードショートカット"
description: ""
category: 
tags: ['Lubuntu']
---
{% include JB/setup %}

最近、Lubuntu を使用することが多くなってきたので、キーボードショートカットについて調べてみました。

Lubuntu では、ユーザー毎の設定ファイルが、~/.config/openbox/lubuntu-rc.xml
にありました。

ここにキーボードの設定も書かれています。
例えば

    <keybind key="C-A-Left">
      <action name="GoToDesktop">
        <to>left</to>
        <wrap>no</wrap>
      </action>
    </keybind>
というのはCtrlキーとAltキーを押しならがら左矢印を押すと、左側のデスクトップ(ワークスペース)
に行くという意味です。

設定ファイルの書式は Lubuntu のデスクトップ LXDE が使用しているウィンドーマネージャー OpenBox の WiKi [http://openbox.org/wiki/](http://openbox.org/wiki/) を見ると詳しくのっています。

キーバインディングについては、 [Help:Bindings](http://openbox.org/wiki/Help:Bindings) に

動作については [Help:Actions](http://openbox.org/wiki/Help:Actions) に記述されています。



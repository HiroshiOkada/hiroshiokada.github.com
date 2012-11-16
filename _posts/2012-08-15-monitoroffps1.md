---
layout: post
title: "monitoroff.ps1"
description: "ディスプレイの電源を切る PowerShell スクリプト"
category: 
tags: [Windows]
---
{% include JB/setup %}

Windows マシンをスリープやシャットダウンせずに一時的にモニターの電源だけ切りたくなったので、
少しググったらWM_SYSCOMMAND で出来ることがわかりました。

最近 PowerShell を少しずつ使い始めたので、せっかくなので PowerShell で書いてみることにしました。
以下は作成した PowerShell のコマンドレットの内容です。<

### monitoroff.ps1

{% highlight PowerShell %}
# Turn off the display.
# Then, the display will be turned on if a key is pressed. 

$HWND_BROADCAST = -1
$WM_SYSCOMMAND = 0x0112
$SC_MONITORPOWER = 0xF170
$LPARAM_ON = -1
$LPARAM_LOW_POWER = 1
$LPARAM_OFF = 2

$signature = @'
[DllImport("user32.dll")]
public static extern bool PostMessage(
  IntPtr hWnd,
  UInt32 Msg,
  Int32 wParam,
  Int32 lParam);
'@

$postMessage = Add-Type -memberDefinition $signature `
     -Name "Win32PostMessage" `
     -namespace "Win32Functions" `
     -passThru

$postMessage::PostMessage( $HWND_BROADCAST, $WM_SYSCOMMAND, $SC_MONITORPOWER, $LPARAM_OFF) | Out-Null

[Console]::Readkey() | Out-Null

$postMessage::PostMessage( $HWND_BROADCAST, $WM_SYSCOMMAND, $SC_MONITORPOWER, $LPARAM_ON) | Out-Null

$null 
{% endhighlight %}

実行するとモニターが消え、キー入力で復帰します。

Windows 7 と Windows Vista で試しました。

11月15日 追記: Winodws 8 でも動作しました。

なお、Vista で PowerShell のコマンドラインから実行するとなぜかすぐに画面が復帰してしまます。powershell .\monitoroff.ps1 とすれば Vista でも OK でした。<br />
スクリプトを右クリックして PowerShell で実行 で実行する方法ではどちらでも期待通りの動作になりました。



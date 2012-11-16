---
layout: post
title: "poweroff.ps1"
description: "ディスプレイの電源を切る PowerShell スクリプト"
category: 
tags: [Windows]
---
{% include JB/setup %}

{% highlight PowerShell %}

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


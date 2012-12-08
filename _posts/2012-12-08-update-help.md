---
layout: post
title: "PowerShell で Update-Help"
description: ""
category: 
tags: ['PowerShell', 'Windows8']
---
{% include JB/setup %}

Windows 8 の PowerShell で `Get-Help Get-Command` などとヘルプを見ようとすると。

> このコンピューターにこのコマンドレットのヘルプ ファイルは見つかりませんでした。ヘルプの一部だけが表示されています。
-- このコマンドレットを含むモジュールのヘルプ ファイルをダウンロードしてインストールするには、Update-Help を使用してください。

といわれました。

そこで、`Update-Help` を実行してヘルプをインストールするのですが、少しだけ注意点がありました。

*  管理者権限でひらいた PowerShell でないと、一部のヘルプが権限の問題でインストールできない。
*  -Force オプション無しだと Uppdate-Help は一日一回しか更新しない。
*  日本語の Help には無いものもある。

そこで PowerShell を管理者として実行し太字のように入力しました。

<pre style="color:white; background-color:darkblue;">
Windows PowerShell
Copyright (C) 2012 Microsoft Corporation. All rights reserved.

PS C:\Windows\system32&gt; <span style="font-weight:900;">Update-Help -Force -UICulture en-US</span>
PS C:\Windows\system32&gt; <span style="font-weight:900;">Update-Help -Force -UICulture ja-JP</span>
</pre>

赤字のようなエラーが出て、Help の多くの部分は英語になりますが、一応 Help が参照できるようになりました。 

<pre style="color:red; background-color:black;">
Update-Help : UI カルチャ {ja-JP} を使用してモジュール 'Microsoft.PowerShell.Management, Microsoft.PowerShell.Utility,
AppLocker, Appx, BitLocker, BranchCache, CimCmdlets, DirectAccessClientComponents, Dism, DnsClient, Hyper-V, Internatio
nal, iSCSI, ISE, Kds, Microsoft.PowerShell.Diagnostics, Microsoft.PowerShell.Host, Microsoft.PowerShell.Security, Micro
soft.WSMan.Management, MMAgent, MsDtc, NetAdapter, NetConnection, NetLbfo, NetQos, NetSecurity, NetSwitchTeam, NetTCPIP
, NetWNV, NetworkConnectivityStatus, NetworkTransition, PKI, PrintManagement, PSScheduledJob, PSWorkflow, PSWorkflowUti
lity, ScheduledTasks, SecureBoot, SmbShare, SmbWitness, Storage, TroubleshootingPack, TrustedPlatformModule, VpnClient,
 Wdac, WindowsDeveloperLicense, WindowsErrorReporting, Microsoft.PowerShell.Core' のヘルプを更新できませんでした: 次の
パターンに一致する UI カルチャが見つかりませんでした: ja-JP。パターンを確認してから、コマンドをもう一度実行してください
。
発生場所 行:1 文字:1
+ Update-Help -Force -UICulture ja-JP
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (System.Collecti...[System.String]:HashSet`1) [Update-Help]、Exception
    + FullyQualifiedErrorId : HelpCultureNotSupported,Microsoft.PowerShell.Commands.UpdateHelpCommand

</pre>



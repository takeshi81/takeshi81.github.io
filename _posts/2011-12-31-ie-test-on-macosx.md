---
id: 1429
title: MacでWebページ作りながら、Windowsでブラウザチェックする最も快適な方法
date: 2011-12-31T10:00:43+00:00
author: いがらしたけし
layout: post
guid: http://www.indigo-design.org/?p=1429

categories:
  - 仕事
tags:
  - browser
  - design
  - develop
  - Mac
  - remote
  - Web
  - windows
---
たけしです。こんにちは。

ついに2011年も残すところ数時間となってしまいました。皆さんの今年はどんな年でしたか？

早速本題ですが、Mac使いのWeb制作者のちょっとした面倒と言えば、Windowsのブラウザ検証ではないでしょうか。考えられる方法はいくつかありますが、私自身が試してきた方法を取り上げて、長所短所を挙げてゆこうと思います。
  
<!--more-->

### Macの横にWindows機を置く

[<img src="http://farm4.staticflickr.com/3017/2633068270_4d2975c87b_m.jpg" width="240" height="160" alt="pc vs mac" />](http://www.flickr.com/photos/acoustic_punk_sound/2633068270/ "pc vs mac by natashalcd, on Flickr")
  
(photo by natashalcd)

一番わかりやすい方法です。実機で試すので、もっとも確実なやり方です。速度はマシンによりますが、別マシンなので各々おおむね快適に動きます。でも、2つのマシンが机を占拠するので、うさぎ小屋の我が家では置き場に工夫が必要でした。

### 仮想マシン（VM）を使う

[<img src="http://farm4.staticflickr.com/3309/3204713480_3a457e0b90_m.jpg" width="240" height="204" alt="win7-parallels" />](http://www.flickr.com/photos/maui-nui/3204713480/ "win7-parallels by Tarlach, on Flickr")
  
(photo by Tarlach)

しばらく、これがベストソリューションだと考えていた方法がこれ。自分のMacに、Parallels Desktop for Macや、VMWare Fusionをインストールして、Windowsを入れるのです。MacもWindowsも同じ画面で使えます。Drag & Dropだっていけます。

でも、マシンは一つなので、非力なマシンでは動作がかなり遅くなると思います。快適に使おうと思うと結構スペックよいものでないとつらいかもしれません。

### サーバ化したWindowsをMacから遠隔操作する（←イマココ）

[<img src="https://lh6.googleusercontent.com/-hkX-pWiA6d0/Tv3goWDvHYI/AAAAAAAAAUQ/qjVfqUuwdw0/s288/111231_remotedesktop.jpg" height="216" width="288" />](https://picasaweb.google.com/lh/photo/GCauRDDHLR7efmp3e0NfxvDUdFBYrKYna69gqCnW--U?feat=embedwebsite)
  
(photo by takeshi81)

最近たどり着いたのがこれ。まず邪魔にならないところにWindowsマシンを設置（MacBook ProにBootcampでWindows 7を入れて起動している。でも普通のPCでOK）、[リモートデスクトップ接続を許可して](http://windows.microsoft.com/ja-JP/windows7/Connect-to-another-computer-using-Remote-Desktop-Connection)、Macに[Remote Desktop Connection Client for Mac](http://www.microsoft.com/japan/mac/remote-desktop-client)を入れて起動します。ファイヤーウォールの3389番を開けておきましょう。

ネットワーク回線が貧弱だと動きがつらいですが、マシンは別なので、作業中のMacは快適に動きます。Drag & Dropは使えませんが、遠隔のマシンで自分のマシンのフォルダを開いたり、Dropboxのようなサービスを使えば、不便は感じないと思います。

というわけで、今年もお世話になりました。良いお年をお迎えください。

P.S.
  
言い忘れてましたけど、リモートデスクトップ接続される側のPCは、Windows 7だと、Professional、Ultimate、Enterpriseなど上位製品に限られます。Homeバージョンなどの場合はVNCサーバーをインストールするとよいでしょう。

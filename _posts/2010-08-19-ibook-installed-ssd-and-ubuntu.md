---
id: 1006
title: SSDでUbuntuなiBook G4
date: 2010-08-19T15:30:56+00:00
author: いがらしたけし
layout: post
guid: http://indigo-design.dev.test/?p=1006
permalink: /2010/08/ibook-installed-ssd-and-ubuntu/
categories:
  - 仕事
tags:
  - Apple
  - Linux
  - Mac
  - Macintosh
  - Server
  - Ubuntu
  - 仕事
  - 日々
---
<a href="http://photozou.jp/photo/show/120767/46314502"><img src="http://art34.photozou.jp/pub/767/120767/photo/46314502.jpg" alt="ubuntu on ibook" width="240" height="180" /></a>

鳥頭な上にかなりうっかり者のたけしです。こんばんは。どのくらいうっかりかという話をします。 

この間落札したMac mini用にSSDとメモリを取り寄せたのです。で、メモリはよかったのですが、元のHDDとSSDを入れ替えようかな、と思ったその時、SSDの差し込み口がなんと<span style="font-weight:bold;font-size:133%;">IDE</span>ということに気付いてしまいました。Intel miniなんで、HDDの方はどう見てもSATAです。本当にありがとうございました。 

よりにもよってIDEのSSDなどというものを買ってしまった私。途方に暮れても仕方ないので、事の発端であるNAS化していたiBookを例によって分解して壊れたHDDを取り出し、SSDを装着してみました。iBookはIDEなのでもちろんすんなり入りました。 
<!--more-->
さてOSです。今まではMacOSX 10.5 Leopardにしておりました。でも、サーバなのでデスクトップはほとんど使いません。余計なものがいろいろ動かない方がよろしいので、PowerPCでも動くLinuxかBSDでも入れようかと思ったのです。 

ディストリビューションはいろいろ試してみたのですが、結局Ubuntuに落ち着きました。iBookのハードウェアやパワーマネージメントを一通りサポートしているので、モニタの輝度や音量の調整がきちんと出来たからです。インストールも一番簡単でした。 

ちなみにFreeBSDはインストーラの時点でずっこけて入らず、Debianは動くけど輝度が変えられなかったので、コンソールの文字が焼き付きそうでやめました。 

で、一応Apacheの設定なんかもして開発用Webサーバとして使ってますが、結構調子いいんですね、これが。起動は別に速くないですが、Webの表示など読み出し系の仕事は悪くないです。 

いや、捨てるつもりのマシンが思わぬ形で復活してしまった。
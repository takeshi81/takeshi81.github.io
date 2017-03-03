---
id: 939
title: WordPressのインストーラーで毎回接続情報を聞かれる場合は
date: 2010-07-21T02:19:55+00:00
author: いがらしたけし
layout: post
guid: http://indigo-design.dev.test/?p=939
permalink: /2010/07/wordpress-installer/
categories:
  - 仕事
tags:
  - apache
  - Blog
  - Web
  - WordPress
  - 仕事
---
<a href="https://indigo-design.org/wp-content/uploads/2010/07/100720_screen.gif"><img src="https://indigo-design.org/wp-content/uploads/2010/07/100720_screen.gif" alt="WordPressのキャプチャ" width="480" height="224" class="alignnone size-full wp-image-945" /></a>

WordPressの自動アップグレードやプラグインインストーラーはとても便利な物ですが、しばしば「要求された操作を実行するためには、接続情報が必要です」などと表示されてFTPアカウントの入力を求められ、お困りの方も多いかと思います。

原因はいくつかありますが、よくあるのは下記の二つのケースです。
<ol>
	<li>PHPがセーフモードで動作している</li>
	<li>WordPressのファイルの所有権がapacheの所有権と異なる</li>
</ol>
XREA系サーバで動かしている場合は前者でひっかかります。これはCGIモードでPHPを動かすことで回避できます。

後者の場合、必ずなるわけではありませんが、セーフモードでもないのにひっかかる場合、apacheと所有権が異なることで問題が発生することが多いです。MacOSXに入れる場合でも発生することがあります。

この場合はWordPressのPHPファイルとディレクトリをapacheに所有させてしまうのが手っ取り早いです。テーマやプラグインもその他のユーザーに書き込み権限があれば編集も可能です。

参考：
<a href="http://d.hatena.ne.jp/sakaik/20090908/p1">WordPressで「要求された操作を実行するためには、接続情報が必要です」と出る原因とその対処法メモ - sakaikの日々雑感～(T)編</a>
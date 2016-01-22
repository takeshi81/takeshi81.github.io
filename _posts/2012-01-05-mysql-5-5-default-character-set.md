---
id: 1452
title: MySQL 5.5ではdefault-character-setが廃止されてた…
date: 2012-01-05T10:00:27+00:00
author: いがらしたけし
layout: post
guid: http://www.indigo-design.org/?p=1452
permalink: /2012/01/mysql-5-5-default-character-set/
categories:
  - 仕事
tags:
  - db
  - MySQL
  - Server
  - WordPress
---
[<img src="https://lh5.googleusercontent.com/-7DtE734LYHw/TwR5vgXmAyI/AAAAAAAAAUw/XkBqHDpmRqs/s288/mysql.gif" height="149" width="288" />](https://picasaweb.google.com/lh/photo/gcik4d3NGRU9d86p78NCwkI-Gs5g_DIIc8Y78SZjSM8?feat=embedwebsite)

年明けにいきなり風邪でダウンした、たけしです。こんにちは。

このブログを本日新しいサーバに引っ越しさせてみました。さくらのVPSで、昨秋からこつこつ仕込んでいたのですが、新年早々引いた風邪も大分よくなってきたので、WordPressを引っ越しさせることにしたのです。

旧サーバからファイル一式をダウンロード、PHPMyAdminでDBのデータを取り出します。新サーバにファイルを上げて、DBにSQLファイルを流しこめば…これでOKなはず…

と、思っていたら、**記事がほとんど文字化けしてやんの**。参りました。

新サーバのMySQLの文字コードを見ると「latin1」。まあ、そんなことだろうと思い、my.cnfに「default-character-set=utf8」と書いたのですが、今度はMySQLが起動しないんです。あれれ、と思って調べまわった結果がこちらでした。

  1. MySQLのバージョンを5.5にしていた。
  2. 5.5では default-character-set が廃止されていた。

なので、my.cnfの付け足した一文がエラーになっていたわけです。5.5以上をお使いの皆様は「character-set-server」を使うようにしましょう。やれやれ、お疲れ様でした。

なお、今回はこちらの記事を参照させていただきました。ありがとうございます。

[KennyQi PHP Blog: MySQL 5.5で「default-character-set」が使えず文字化けする→「character-set-server」にするとOK](http://kennyqi.com/archives/334.html){.broken_link}

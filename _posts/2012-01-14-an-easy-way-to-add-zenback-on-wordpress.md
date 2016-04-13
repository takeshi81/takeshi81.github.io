---
id: 1494
title: WordPressで簡単にzenbackを導入する方法
date: 2012-01-14T10:00:41+00:00
author: いがらしたけし
layout: post
guid: http://www.indigo-design.org/?p=1494

categories:
  - 仕事
tags:
  - Blog
  - CMS
  - Web
  - WordPress
  - zenback
---
[<img src="https://lh5.googleusercontent.com/-pib9uVazHfY/TxBhbkNW9nI/AAAAAAAAAWI/eo3WNzs5oeo/s800/120114_zenback_logo.gif" height="36" width="186" />](https://picasaweb.google.com/lh/photo/wmH93Ctikne54YQBearIpEI-Gs5g_DIIc8Y78SZjSM8?feat=embedwebsite)

たけしです。こんにちは。

最近よく見かける[zenback](http://zenback.jp/)というウィジェットがあります。

> zenbackはブログパーツです。ブログの記事の下や横に、「TwitterやFacebookなどのソーシャルボタン」「その記事に関係する自分のブログ記事」「その記事に関連するキーワード(関連サイト、zenbackキーワーズへのリンク)」「その記事に関係する他のzenbackユーザーのブログ記事」「その記事についての最新のTwitterのつぶやき」「その記事についてのはてなブックマーク」「その記事にFacebookでいいねを押した友達のプロフィール写真とFacebookコメント」を表示します。

それは面白い。というわけで、早速導入してみました。
  
<!--more-->


  
まず、新規登録してコードを取得します。そして、コードを見ながらWordPressへの導入を考えてみました。その結果、最もシンプルな方法を思いついたので、メモしておきます。

### フッターウィジェットを使う

[<img src="https://lh3.googleusercontent.com/-XEWLATtmi7Y/TxBmmADiZkI/AAAAAAAAAWY/bis2iyUUTp4/s800/120114_wp_widgets.gif" height="135" width="193" />](https://picasaweb.google.com/lh/photo/yVxHbWH7v_hccQjgowvjcEI-Gs5g_DIIc8Y78SZjSM8?feat=embedwebsite)

これはフッターウィジェットに対応したWordPressテーマだけに使える方法なのですが、WordPressの管理画面を開いて、「外観」メニューから「ウィジェット」を選び、「フッターエリア…」となっているところに「テキスト」ウィジェットをドラッグ＆ドロップします。

[<img src="https://lh6.googleusercontent.com/-lv184scJ8cg/TxBhbg9PHZI/AAAAAAAAAWM/L5Tobwdrvn4/s800/120114_zenback.gif" height="538" width="480" />](https://picasaweb.google.com/lh/photo/OpOyBY27DoZbYSRIEXK730I-Gs5g_DIIc8Y78SZjSM8?feat=embedwebsite)

タイトルは適当に設定するか空欄にして、本文部分にzenbackのコードを貼りつけて「保存」ボタンを押します。

以上で、フッターに表示されればOKです。簡単でしょう？テーマによって使えないのが難点ですが、フッターウィジェットが使えるテーマをお使いの方は簡単にzenbackが導入できるので、ぜひお試しください。

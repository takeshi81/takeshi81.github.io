---
id: 1469
title: Google ドキュメントでフォーム送信すると自動返信するスクリプト
date: 2012-01-10T10:00:51+00:00
author: いがらしたけし
layout: post
guid: http://indigo-design.dev.test/?p=1469
permalink: /2012/01/google-apps-script-mailform/
categories:
  - 仕事
tags:
  - Apps Script
  - business
  - form
  - Google
  - mail
  - seminar
  - soho
  - Web
---
<a href="https://picasaweb.google.com/lh/photo/fcDTdCR9OegqU4Z2j7R6gkI-Gs5g_DIIc8Y78SZjSM8?feat=embedwebsite"><img src="https://lh4.googleusercontent.com/-UOeGIzGZ0YA/TwtyEsqSzNI/AAAAAAAAAV0/mdgtj-zNSYg/s800/appsscript-icon.png" height="140" width="140" /></a>

たけしです。こんにちは。

WordPressとおやつの会に申し込まれた方はご存知と思いますが、当会の申し込みフォームは<a href="https://docs.google.com/">Googleドキュメント</a>のフォームを利用しています。

これは便利で、入力されたデータはオンラインでどこからでも確認、編集できますし、入力されたデータをExcel形式やCSV、XMLなどでダウンロードすることもできます。フォームもiframeでブログなどに設置可能で、本当によく出来ています。

ただ、機能としてそれだけなので、フォームに記入、送信したら自動返信したい、など問い合わせフォーム的な使い方は、そのままでは難しいです。

ところがExcelのマクロのような感じで、<a href="http://code.google.com/googleapps/appsscript/">Google Apps Script</a>というJavaScriptのようなスクリプト言語が用意されていて、その機能を使うとメール送信が出来るようになります。実際当会でも使わせていただいているスクリプトを掲載しているページをご紹介します。

<a href="http://creazy.net/2011/03/google_form_mailsend.html">Googleドキュメントのフォーム機能からGoogle Apps Scriptを使ってメール送信 [C!]</a>

フォームを作成して、手順どおりにスクリプトを追加して、トリガーを設定してあげれば設定完了です。実際自分のアドレスを入力して試してみてください。うまくいけばOKです。

これは非常に便利な技なので、皆さんにもおすすめです。フォームメールでお困りなら、ぜひお試しください。
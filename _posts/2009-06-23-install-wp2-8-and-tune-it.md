---
id: 200
title: ブログ引っ越し記：WordPress 2.8 + PDO (SQlite) For WordPress 導入
date: 2009-06-23T02:06:18+00:00
author: いがらしたけし
layout: post
guid: http://indigo-design.dev.test/blog/?p=200
permalink: /2009/06/install-wp2-8-and-tune-it/
categories:
  - 仕事
tags:
  - Blog
  - SQLite
  - Web
  - WordPress
  - 仕事
  - 日々
---
<h3>移転のきっかけ</h3>
今まで3年半くらい<a href="http://blog.fc2.com/">FC2ブログ</a>を使っていたのですが、最近<a title="Wikipedia: アカマイ" href="http://ja.wikipedia.org/wiki/%E3%82%A2%E3%82%AB%E3%83%9E%E3%82%A4%E3%83%BB%E3%83%86%E3%82%AF%E3%83%8E%E3%83%AD%E3%82%B8%E3%83%BC%E3%82%BA">Akamai</a>（アカマイ）使い始めたので広告入れることになったらしいのです。お知らせメールは見逃したらしく、ある日ふと開いた自分のブログが広告だらけになって、あんまりな感じがしたので、そろそろ引っ越し時かと思ったのでした。（今はAkamai切ってテンプレートを差し替えたので、あと30日くらいは広告なしの状態です）

それとは別に、
<ul>
	<li><a href="http://ja.wordpress.org/2009/06/12/wordpress-28-ja/">先日公開されたWordPress 2.8</a>を試したい！</li>
	<li><a href="http://www.sqlite.org/">SQLite</a>をWordPressのデータベースに出来るプラグイン、<a href="http://wordpress.org/extend/plugins/pdo-for-wordpress/">PDO (SQLite) For WordPress</a>を試したい！</li>
</ul>
と昨日ふと思ったので、じゃあ、両方やってみよう！ということにしました。自分のブログを実験台に、WordPress 2.8 + SQLiteというマニアックな構成でブログを立ち上げてみたいと思います。
<!--more-->
<h3>ご注意</h3>
<ul>
	<li>WordPress 2.8は現在自動アップデートでの不具合などが発生しています。導入は慎重に検討して下さい。手動でのアップデートは可能です。バグフィックス版の2.8.1を待ってもよいかもしれません。</li>
	<li>WordPressのデータベースはもちろん<a href="http://www-jp.mysql.com/">MySQL</a>を前提に設計されていますので、SQLiteを利用した場合、特にサードパーティーのプラグインなどの互換性は保証されません。</li>
</ul>
<h3>導入環境</h3>
<ul>
	<li><a href="http://www.coreserver.jp/">CORESERVER</a></li>
	<li>PHP 5.2.5</li>
	<li>MySQL 5.1.20 （今回は使いません）</li>
	<li>SQLite 3.3.7</li>
</ul>
<h3>手順</h3>
<ol>
	<li><a href="http://ja.wordpress.org/">WordPress 2.8</a>をダウンロードします。</li>
	<li><a href="http://wordpress.org/extend/plugins/pdo-for-wordpress/">PDO (SQLite) For WordPress</a>をダウンロードします。</li>
	<li>PDO (SQLite) For WordPressをWordPressに組み込みます。
やり方は<a href="http://www.craft-works.co.jp/blog/archives/40">Craftworks Tech Blog</a>さんの記事を参照するとよいです。
はまり所も書いてあります。</li>
	<li>wp-config-sample.phpをコピーして、wp-config.phpを作成</li>
	<li>wp-config.phpを書き換えます。define('COLLATE',''); の次の行に、
<pre class="decode:1 " >define('DB_TYPE', 'sqlite');    //mysql or sqlite</pre>
と入れます。</li>
	<li>wp-includes/wp-db.php の341行目辺りにある次の行をコメントアウトします。
<pre class="decode:1 " >$this-&gt;dbh = @mysql_connect($dbhost, $dbuser, $dbpassword, true);</pre></li>
	<li>index.phpからWordPressのインストールを始めます。
うまくいけばwp-content/配下にdatabaseディレクトリとDBファイル一式が出来ます。</li>
	<li>WordPressの管理ページでCSSがうまく読み込めてない場合、<a href="http://www.laloopa.com/20090612/wp28-mgmt-page-doesnt-load-css/">La Loopaさんの記事</a>が参考になります。 XREA or CORESERVERな方はご注意。自分もwp-admin/.htaccessを記事通りに作りました。</li>
	<li>きちんとダッシュボードが表示されれば、インストール成功です。お疲れさまでした。</li>
</ol>
<h3>動いてるプラグイン</h3>
<ul>
	<li><a href="http://akismet.com/">Akismet</a></li>
	<li><a href="http://wppluginsj.sourceforge.jp/ktai_style/">Ktai Style</a></li>
	<li><a href="http://suche.pytalhost.de/2008/12/13/wordpress-plugin-simple-google-sitemap-v10">Simple Google Sitemap</a> （後述のプラグインの代替）</li>
</ul>
<h3>動かないプラグイン</h3>
<ul>
	<li><a href="http://www.arnebrachhold.de/projects/wordpress-plugins/google-xml-sitemaps-generator/">Google (XML) Sitemaps Generator for WordPress
</a>SQLiteがいけないのか、メモリが足りないのかはよくわかりませんでした。定番プラグインだけに残念なのですが、前述のプラグインを使えばsitemap.xmlは書き出せます。</li>
</ul>
以上です。Cache系のプラグインは入れていませんが、結構サクサクと表示してくれます。手間がかかるのでおすすめはしませんが、MySQLの速度がボトルネックになっている場合は、解決策の一つになるかもしれません。
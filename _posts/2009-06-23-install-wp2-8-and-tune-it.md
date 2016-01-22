---
id: 200
title: ブログ引っ越し記：WordPress 2.8 + PDO (SQlite) For WordPress 導入
date: 2009-06-23T02:06:18+00:00
author: いがらしたけし
layout: post
guid: http://www.indigo-design.org/blog/?p=200
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
### 移転のきっかけ

今まで3年半くらい[FC2ブログ](http://blog.fc2.com/)を使っていたのですが、最近[Akamai](http://ja.wikipedia.org/wiki/%E3%82%A2%E3%82%AB%E3%83%9E%E3%82%A4%E3%83%BB%E3%83%86%E3%82%AF%E3%83%8E%E3%83%AD%E3%82%B8%E3%83%BC%E3%82%BA "Wikipedia: アカマイ")（アカマイ）使い始めたので広告入れることになったらしいのです。お知らせメールは見逃したらしく、ある日ふと開いた[自分のブログ](http://armadillo75.blog35.fc2.com/){.broken_link}が広告だらけになって、あんまりな感じがしたので、そろそろ引っ越し時かと思ったのでした。（今はAkamai切ってテンプレートを差し替えたので、あと30日くらいは広告なしの状態です）

それとは別に、

  * [先日公開されたWordPress 2.8](http://ja.wordpress.org/2009/06/12/wordpress-28-ja/)を試したい！
  * [SQLite](http://www.sqlite.org/)をWordPressのデータベースに出来るプラグイン、[PDO (SQLite) For WordPress](http://wordpress.org/extend/plugins/pdo-for-wordpress/)を試したい！

と昨日ふと思ったので、じゃあ、両方やってみよう！ということにしました。自分のブログを実験台に、WordPress 2.8 + SQLiteというマニアックな構成でブログを立ち上げてみたいと思います。
  
<!--more-->

### ご注意

  * WordPress 2.8は現在自動アップデートでの不具合などが発生しています。導入は慎重に検討して下さい。手動でのアップデートは可能です。バグフィックス版の2.8.1を待ってもよいかもしれません。
  * WordPressのデータベースはもちろん[MySQL](http://www-jp.mysql.com/)を前提に設計されていますので、SQLiteを利用した場合、特にサードパーティーのプラグインなどの互換性は保証されません。

### 導入環境

  * [CORESERVER](http://www.coreserver.jp/)
  * PHP 5.2.5
  * MySQL 5.1.20 （今回は使いません）
  * SQLite 3.3.7

### 手順

  1. [WordPress 2.8](http://ja.wordpress.org/)をダウンロードします。
  2. [PDO (SQLite) For WordPress](http://wordpress.org/extend/plugins/pdo-for-wordpress/)をダウンロードします。
  3. PDO (SQLite) For WordPressをWordPressに組み込みます。
  
    やり方は[Craftworks Tech Blog](http://www.craft-works.co.jp/blog/archives/40){.broken_link}さんの記事を参照するとよいです。
  
    はまり所も書いてあります。
  4. wp-config-sample.phpをコピーして、wp-config.phpを作成
  5. wp-config.phpを書き換えます。define(&#8216;COLLATE&#8217;,&#8221;); の次の行に、 <pre class="decode:1 " >define('DB_TYPE', 'sqlite');    //mysql or sqlite</pre>
    
    と入れます。</li> 
    
      * wp-includes/wp-db.php の341行目辺りにある次の行をコメントアウトします。 <pre class="decode:1 " >$this-&gt;dbh = @mysql_connect($dbhost, $dbuser, $dbpassword, true);</pre>
    
      * index.phpからWordPressのインストールを始めます。
  
        うまくいけばwp-content/配下にdatabaseディレクトリとDBファイル一式が出来ます。
      * WordPressの管理ページでCSSがうまく読み込めてない場合、[La Loopaさんの記事](http://www.laloopa.com/20090612/wp28-mgmt-page-doesnt-load-css/)が参考になります。 XREA or CORESERVERな方はご注意。自分もwp-admin/.htaccessを記事通りに作りました。
      * きちんとダッシュボードが表示されれば、インストール成功です。お疲れさまでした。</ol> 
    
    ### 動いてるプラグイン
    
      * [Akismet](http://akismet.com/)
      * [Ktai Style](http://wppluginsj.sourceforge.jp/ktai_style/)
      * [Simple Google Sitemap](http://suche.pytalhost.de/2008/12/13/wordpress-plugin-simple-google-sitemap-v10) （後述のプラグインの代替）
    
    ### 動かないプラグイン
    
      * [### 移転のきっかけ

今まで3年半くらい[FC2ブログ](http://blog.fc2.com/)を使っていたのですが、最近[Akamai](http://ja.wikipedia.org/wiki/%E3%82%A2%E3%82%AB%E3%83%9E%E3%82%A4%E3%83%BB%E3%83%86%E3%82%AF%E3%83%8E%E3%83%AD%E3%82%B8%E3%83%BC%E3%82%BA "Wikipedia: アカマイ")（アカマイ）使い始めたので広告入れることになったらしいのです。お知らせメールは見逃したらしく、ある日ふと開いた[自分のブログ](http://armadillo75.blog35.fc2.com/){.broken_link}が広告だらけになって、あんまりな感じがしたので、そろそろ引っ越し時かと思ったのでした。（今はAkamai切ってテンプレートを差し替えたので、あと30日くらいは広告なしの状態です）

それとは別に、

  * [先日公開されたWordPress 2.8](http://ja.wordpress.org/2009/06/12/wordpress-28-ja/)を試したい！
  * [SQLite](http://www.sqlite.org/)をWordPressのデータベースに出来るプラグイン、[PDO (SQLite) For WordPress](http://wordpress.org/extend/plugins/pdo-for-wordpress/)を試したい！

と昨日ふと思ったので、じゃあ、両方やってみよう！ということにしました。自分のブログを実験台に、WordPress 2.8 + SQLiteというマニアックな構成でブログを立ち上げてみたいと思います。
  
<!--more-->

### ご注意

  * WordPress 2.8は現在自動アップデートでの不具合などが発生しています。導入は慎重に検討して下さい。手動でのアップデートは可能です。バグフィックス版の2.8.1を待ってもよいかもしれません。
  * WordPressのデータベースはもちろん[MySQL](http://www-jp.mysql.com/)を前提に設計されていますので、SQLiteを利用した場合、特にサードパーティーのプラグインなどの互換性は保証されません。

### 導入環境

  * [CORESERVER](http://www.coreserver.jp/)
  * PHP 5.2.5
  * MySQL 5.1.20 （今回は使いません）
  * SQLite 3.3.7

### 手順

  1. [WordPress 2.8](http://ja.wordpress.org/)をダウンロードします。
  2. [PDO (SQLite) For WordPress](http://wordpress.org/extend/plugins/pdo-for-wordpress/)をダウンロードします。
  3. PDO (SQLite) For WordPressをWordPressに組み込みます。
  
    やり方は[Craftworks Tech Blog](http://www.craft-works.co.jp/blog/archives/40){.broken_link}さんの記事を参照するとよいです。
  
    はまり所も書いてあります。
  4. wp-config-sample.phpをコピーして、wp-config.phpを作成
  5. wp-config.phpを書き換えます。define(&#8216;COLLATE&#8217;,&#8221;); の次の行に、 <pre class="decode:1 " >define('DB_TYPE', 'sqlite');    //mysql or sqlite</pre>
    
    と入れます。</li> 
    
      * wp-includes/wp-db.php の341行目辺りにある次の行をコメントアウトします。 <pre class="decode:1 " >$this-&gt;dbh = @mysql_connect($dbhost, $dbuser, $dbpassword, true);</pre>
    
      * index.phpからWordPressのインストールを始めます。
  
        うまくいけばwp-content/配下にdatabaseディレクトリとDBファイル一式が出来ます。
      * WordPressの管理ページでCSSがうまく読み込めてない場合、[La Loopaさんの記事](http://www.laloopa.com/20090612/wp28-mgmt-page-doesnt-load-css/)が参考になります。 XREA or CORESERVERな方はご注意。自分もwp-admin/.htaccessを記事通りに作りました。
      * きちんとダッシュボードが表示されれば、インストール成功です。お疲れさまでした。</ol> 
    
    ### 動いてるプラグイン
    
      * [Akismet](http://akismet.com/)
      * [Ktai Style](http://wppluginsj.sourceforge.jp/ktai_style/)
      * [Simple Google Sitemap](http://suche.pytalhost.de/2008/12/13/wordpress-plugin-simple-google-sitemap-v10) （後述のプラグインの代替）
    
    ### 動かないプラグイン
    
      *](http://www.arnebrachhold.de/projects/wordpress-plugins/google-xml-sitemaps-generator/) SQLiteがいけないのか、メモリが足りないのかはよくわかりませんでした。定番プラグインだけに残念なのですが、前述のプラグインを使えばsitemap.xmlは書き出せます。
    
    以上です。Cache系のプラグインは入れていませんが、結構サクサクと表示してくれます。手間がかかるのでおすすめはしませんが、MySQLの速度がボトルネックになっている場合は、解決策の一つになるかもしれません。

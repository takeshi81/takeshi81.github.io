---
id: 999
title: EC-CUBEをMySQLで動かして文字化けが起こるとき
date: 2010-08-09T20:48:22+00:00
author: いがらしたけし
layout: post
guid: http://indigo-design.org/?p=997
permalink: /2010/08/gabled-characters-on-ec-cube-and-mysql/
categories:
  - 仕事
tags:
  - CMS
  - EC-CUBE
  - eCommerce
  - MySQL
  - PHP
  - 仕事
---
<a href="https://indigo-design.org/wp-content/uploads/2010/08/eccube.jpg"><img src="https://indigo-design.org/wp-content/uploads/2010/08/eccube.jpg" alt="eccube" width="236" height="68" class="alignnone size-full wp-image-1022" /></a>

<a href="https://indigo-design.org/2009/07/calculate-consumption-tax/">EC-CUBEの消費税計算の記事</a>は、このブログの人気エントリなのですが、今日は<a href="http://www.ec-cube.net/">EC-CUBE</a>を<a href="http://www.cpi.ad.jp/shared/index.html">CPIの共用サーバ</a>に自力でインストールする時のTipsを（鳥頭な自分のために）書き残しておこうと思います。ちなみにCPI提供のインストーラを使う場合はこの限りではありません。もっと簡単です。
<!--more-->
<h3>1. .htaccessの準備</h3>

CPIはPHPファイルをそのまま設置しても動きません。.htaccessに次のように書きます。

[text]AddHandler x-httpd-php524 .php[/text]

ついでにphp.iniもカスタマイズすることが出来ますので、下のような文を追加することにします。（ユーザーホームにconfというディレクトリを作ってphp.iniを置く場合。設置場所のパスを書く）

[text]suPHP_ConfigPath /usr/home/（ユーザーID）/conf/[/text]

<h3>2. php.iniのカスタマイズ</h3>

次はphp.iniを編集しますが、デフォルトから変更する部分だけ書いておいておけばよいです。

[text]output_handler = mb_output_handler
register_globals = Off
;post_max_size = 8M
magic_quotes_gpc = Off
upload_max_filesize = 5M

;session.use_cookies = 0
;session.use_trans_sid = 1

mbstring.language = Japanese
mbstring.internal_encoding = UTF-8
mbstring.encoding_translation = On[/text]

<h3>3. EC-CUBEをMySQLで動かす時の文字化け対策</h3>

これで普通にインストール出来たりするんですが、管理画面にログインすると「管理者」が「管????」になったり、文字化けが発生するのです。これにはかなり手こずりました。おそらくPHPとMySQLの文字コードがらみでうまくいってないことが想像されるものの、さて、どうしたらよいやらとphpMyAdminとにらめっこしたり、ネットをさまよって十数分。やっと見つけてきたのが、<a href="http://xoops.ec-cube.net/modules/newbb/viewtopic.php?topic_id=2593&amp;forum=11&amp;viewmode=flat&amp;order=ASC&amp;start=10">こちらの記事</a>。

<blockquote>data/class/SC_DbConn.php
の $this-&gt;conn = $objDbConn; の下に
<pre class="lang:php decode:1 " >if ($this-&gt;conn instanceof DB_mysql) {
$this-&gt;conn-&gt;query("SET NAMES 'utf8'");
}</pre>
を追加。

PHP 5.2.4
MySQL 5.0.45
の環境にインストールできました。</blockquote>

素晴らしい…が、ちょっと待って。<a href="http://blog.ohgaki.net/set_namesa_mcb_asc">SET NAMESって使っちゃいかんのではなかったっけ</a>？と、思って調べてみるとこんなことが書いてありました。

<blockquote>・どうすれば安全なのか
PHP5.2.3以降の場合なら　→　mysql_set_charset()を使えばOK
PHP5.0.5以降でmysqliを使用しているなら　→　mysqli_set_charset()を使えばOK
<a href="http://nonn-et-twk.net/twk/why-set-names-in-php-is-bad">PHPからSET NAMESを使わない方が良い理由と対策まとめ - twk @ ふらっと</a></blockquote>

なるほどねえ。というわけで、件の '/data/class/SC_DbConn.php' を開いてみましょう。（下の行番号は1からだけど65行目辺り）

 <pre class="lang:php decode:1 " >
        //MySQL文字化け対策(MySQLで文字化けする場合は以下のコメントアウトをはずして動作確認してみてください。)
        //if (DB_TYPE == 'mysql') {
        //    $objDbConn-&gt;query('SET NAMES utf8');
        //}</pre>

おい、SET NAMES使ってるじゃん…。というわけで、以下のように書き直し。

 <pre class="lang:php decode:1 " >
        //MySQL文字化け対策(MySQLで文字化けする場合は以下のコメントアウトをはずして動作確認してみてください。)
        if (DB_TYPE == 'mysql') {
            mysql_set_charset("utf8");
        }</pre>

これで、一件落着。文字化けもせず、インストールは完了です。

あ、でもまだ本番に近づくにつれて不具合が出るかもしれません。その時は逐一このブログで報告（というか自分用にメモ）したいと思います。
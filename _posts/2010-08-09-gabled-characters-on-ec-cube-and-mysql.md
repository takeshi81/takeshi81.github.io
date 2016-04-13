---
id: 999
title: EC-CUBEをMySQLで動かして文字化けが起こるとき
date: 2010-08-09T20:48:22+00:00
author: いがらしたけし
layout: post
guid: http://www.indigo-design.org/?p=997

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
[<img src="/wp-content/uploads/2010/08/eccube.jpg" alt="eccube" width="236" height="68" class="alignnone size-full wp-image-1022" />](/wp-content/uploads/2010/08/eccube.jpg)

[EC-CUBEの消費税計算の記事](http://www.indigo-design.org/2009/07/calculate-consumption-tax/)は、このブログの人気エントリなのですが、今日は[EC-CUBE](http://www.ec-cube.net/)を[CPIの共用サーバ](http://www.cpi.ad.jp/shared/index.html)に自力でインストールする時のTipsを（鳥頭な自分のために）書き残しておこうと思います。ちなみにCPI提供のインストーラを使う場合はこの限りではありません。もっと簡単です。
  
<!--more-->

### 1. .htaccessの準備

CPIはPHPファイルをそのまま設置しても動きません。.htaccessに次のように書きます。

[text]AddHandler x-httpd-php524 .php[/text]

ついでにphp.iniもカスタマイズすることが出来ますので、下のような文を追加することにします。（ユーザーホームにconfというディレクトリを作ってphp.iniを置く場合。設置場所のパスを書く）

[text]suPHP_ConfigPath /usr/home/（ユーザーID）/conf/[/text]

### 2. php.iniのカスタマイズ

次はphp.iniを編集しますが、デフォルトから変更する部分だけ書いておいておけばよいです。

[text]output\_handler = mb\_output_handler
  
register_globals = Off
  
;post\_max\_size = 8M
  
magic\_quotes\_gpc = Off
  
upload\_max\_filesize = 5M

;session.use_cookies = 0
  
;session.use\_trans\_sid = 1

mbstring.language = Japanese
  
mbstring.internal_encoding = UTF-8
  
mbstring.encoding_translation = On[/text]

### 3. EC-CUBEをMySQLで動かす時の文字化け対策

これで普通にインストール出来たりするんですが、管理画面にログインすると「管理者」が「管????」になったり、文字化けが発生するのです。これにはかなり手こずりました。おそらくPHPとMySQLの文字コードがらみでうまくいってないことが想像されるものの、さて、どうしたらよいやらとphpMyAdminとにらめっこしたり、ネットをさまよって十数分。やっと見つけてきたのが、[こちらの記事](http://xoops.ec-cube.net/modules/newbb/viewtopic.php?topic_id=2593&forum=11&viewmode=flat&order=ASC&start=10)。

> data/class/SC_DbConn.php
  
> の $this->conn = $objDbConn; の下に
> 
> <pre class="lang:php decode:1 " >if ($this-&gt;conn instanceof DB_mysql) {
$this-&gt;conn-&gt;query("SET NAMES 'utf8'");
}</pre>
> 
> を追加。
> 
> PHP 5.2.4
  
> MySQL 5.0.45
  
> の環境にインストールできました。

素晴らしい…が、ちょっと待って。[SET NAMESって使っちゃいかんのではなかったっけ](http://blog.ohgaki.net/set_namesa_mcb_asc)？と、思って調べてみるとこんなことが書いてありました。

> ・どうすれば安全なのか
  
> PHP5.2.3以降の場合なら　→　mysql\_set\_charset()を使えばOK
  
> PHP5.0.5以降でmysqliを使用しているなら　→　mysqli\_set\_charset()を使えばOK
  
> [PHPからSET NAMESを使わない方が良い理由と対策まとめ &#8211; twk @ ふらっと](http://nonn-et-twk.net/twk/why-set-names-in-php-is-bad)

なるほどねえ。というわけで、件の &#8216;/data/class/SC_DbConn.php&#8217; を開いてみましょう。（下の行番号は1からだけど65行目辺り）

<pre class="lang:php decode:1 " >//MySQL文字化け対策(MySQLで文字化けする場合は以下のコメントアウトをはずして動作確認してみてください。)
        //if (DB_TYPE == 'mysql') {
        //    $objDbConn-&gt;query('SET NAMES utf8');
        //}</pre>

おい、SET NAMES使ってるじゃん…。というわけで、以下のように書き直し。

<pre class="lang:php decode:1 " >//MySQL文字化け対策(MySQLで文字化けする場合は以下のコメントアウトをはずして動作確認してみてください。)
        if (DB_TYPE == 'mysql') {
            mysql_set_charset("utf8");
        }</pre>

これで、一件落着。文字化けもせず、インストールは完了です。

あ、でもまだ本番に近づくにつれて不具合が出るかもしれません。その時は逐一このブログで報告（というか自分用にメモ）したいと思います。

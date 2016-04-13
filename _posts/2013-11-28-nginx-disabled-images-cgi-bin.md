---
id: 1800
title: nginxでcgi-bin配下の画像などが表示されない！
date: 2013-11-28T00:58:14+00:00
author: いがらしたけし
layout: post
guid: http://www.indigo-design.org/?p=1800

categories:
  - 仕事
tags:
  - cgi
  - nginx
  - Server
  - Web
---
[<img src="/wp-content/uploads/2013/11/Nginx_logo.gif" alt="Nginx_logo" width="320" height="67" class="alignnone size-full wp-image-1801" />](/wp-content/uploads/2013/11/Nginx_logo.gif)

WebサーバでPerlなどのCGIスクリプトを設置するとき、セキュリティの関係でサーバによっては、cgi-binというディレクトリを利用することがあります。一般的にcgi-binにはスクリプトファイルのみを置くことになっているので、スクリプトから参照したい画像やHTML、スタイルシートなどをcgi-bin配下に置いても表示することは出来ません。

WebサーバがApacheの場合には、「cgi-bin 画像」などで検索すれば対策がわかるのですが、今回はnginxを利用していたので、どうしたらよいかと思案した結果、採った対策をご紹介します。

手法は目新しいものではなく、Apacheでもしばしばあるのですが、画像やHTML、CSSのファイルをWeb公開用のディレクトリ（「www」「htdocs」「web」等）配下に移してしまうものです。

それだけだと参照する場所が変わってしまうので、スクリプトを書き直すか、nginxの設定を変更する必要があります。今回スクリプトは単純なものではなかったので、nginxの設定を変更することにします。

元々 /web/ という公開用ディレクトリ、同じ階層に /cgi-bin/ があって、hoge.cgi、画像を入れた images/ というディレクトリがあったとします。その images/ ディレクトリをごっそり /web/hoge/images/ に移動します。

次に、nginx.conf（場合により sites-available/example.com.vhost など、ご自分の環境に合わせて）に書き加えます。

<pre class="decode:1 " >location /cgi-bin/hoge/images/ {
    alias /var/www/example.com/web/hoge/images/;
}
</pre>

locationはドキュメントルートから書いていきます。aliasはサーバルートから絶対パスで指定します。

こんな感じで今回は対応してみました。もっとスマートなやり方があったら教えてくださいね。

2014/4/26 更新：誤記を訂正しました（site-available → sites-available）。

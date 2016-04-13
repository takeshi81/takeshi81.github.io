---
id: 924
title: 複数のWordPressを統合してみる
date: 2010-07-18T03:08:55+00:00
author: いがらしたけし
excerpt: サーバの移転を機に「ネットワーク」を有効にした一つのWordPressでマルチブログ運用にしてみようと思ったのでした。
layout: post
guid: http://www.indigo-design.org/?p=924

categories:
  - 仕事
tags:
  - Blog
  - Web
  - WordPress
  - 仕事
---
<img src="/wp-content/uploads/2010/07/wordpress-logo-hoz-rgb.gif" alt="wordpress logo" width="384" height="87" class="alignnone size-full wp-image-935" />

WordPressは従来単一のブログしか運用できず、別にWordPress MUというマルチブログ機能を実装したアプリケーションがありました。[しかし、先月リリースされたバージョン3.0で両者は統合し](http://ja.wordpress.org/2010/06/18/thelonious/)、普通のWordPressでも[「ネットワーク」機能を有効にすることで複数のブログを作成、管理することが出来る](http://mage8.com/multiple-blogs-on-wordpress.html)ようになりました。

このサイトのドメイン（indigo-design.org）の下には、このブログの他に、[アビユーズという和小物のネットショップのブログ](http://www.indigo-design.org/habi/)もあって、こちらもWordPressで運用しています。ただ、MUではなく、通常のWordPressを各々、二つ入れていました。二つのブログは開設時期が違ったため、こういう構成になっていたのですが、サーバの移転を機に「ネットワーク」を有効にした一つのWordPressでマルチブログ運用にしてみようと思ったのでした。

### レシピ

まず、すべてのブログのファイルとデータベースをバックアップします。

今回はルートディレクトリで運用しているブログ（このブログ）がありますので、これを存続させて、3.0にアップグレード後、ネットワークを有効にして、子ブログとしてショップブログを新たに開設、記事をインポートすることにします。

やり方は[mage8.comさんの記事](http://mage8.com/multiple-blogs-on-wordpress.html)に従って進めます。ポイントは以下の通りです。

  1. テーマとプラグインの置き場は統合されるので、両ブログで使用しているものを一緒に入れておく。
  2. アップロードしたファイル（wp-content/uploads/\*）の置き場は、子ブログの場合、「wp-content/blogs.dir/(作成したブログのid)/files/\*」に変わる。子ブログの記事をエクスポートして、ファイルをテキストエディタで開いてパスを置換しておき、インポートする。古いファイルは、ごっそり新しいディレクトリに入れる。
  3. ショップブログは以前、http://indigo-design.org/habi/というURLで告知していた。現在はhttp://www.indigo-design.org/habi/であるので、URLの正規化をしたい。今までは放っておけば勝手に書き換わったが、今回古いアドレスでアクセスすると親ブログに飛ばされる事態が発生した。ここは.htaccessにRewriteRuleを書き加えて対処した。
  
    [text]
  
    RewriteCond %{HTTP_HOST} ^indigo-design.org
  
    RewriteRule ^(.*)$ http://www.indigo-design.org/$1 [R=301,L]
  
    [/text] 

あとはそれぞれのブログにテーマとプラグインの設定をすれば出来上がりです。

統合のメリットとしては、今後WordPressの管理画面からの操作だけで、いくらでもブログを増やすことが出来るようになります。これは大きいと思います。私が作業机を間借りしている会社では、実際にプロジェクト管理に利用したりしています。ブラウザで完結するし、画像もほぼ思い通りに貼れるので、メール添付よりもスマートです。

では、皆さんもお試しになってみてください。

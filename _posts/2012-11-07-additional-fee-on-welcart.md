---
id: 1721
title: Welcartで代引手数料以外の手数料を加算する
date: 2012-11-07T12:48:24+00:00
author: いがらしたけし
layout: post
guid: http://indigo-design.org/?p=1721
permalink: /2012/11/additional-fee-on-welcart/
categories:
  - 仕事
tags:
  - Blog
  - business
  - CMS
  - eCommerce
  - PHP
  - Welcart
  - 仕事
---
<a href="https://indigo-design.org/2012/11/additional-fee-on-welcart/%e3%82%b9%e3%82%af%e3%83%aa%e3%83%bc%e3%83%b3%e3%82%b7%e3%83%a7%e3%83%83%e3%83%88-2012-11-07-11-41-22/" rel="attachment wp-att-1722"><img src="https://indigo-design.org/wp-content/uploads/2012/11/77d1623d665da9e2f05661e373bf1410.png" alt="" title="Welcart Logo" width="305" height="85" class="alignnone size-full wp-image-1722" /></a>

忘れそうなので、メモ。<a href="http://www.welcart.com/">Welcart</a>はWordPressをECサイト化する国産のプラグインですが、標準では代引手数料以外の手数料を加算する機能がありません（ver.1.2.1現在。今後対応されるとのことです）。

今構築している<a href="http://www.huhtikuu.jp/">北欧雑貨の通販サイト</a>では、決済方法に代金引換の他、「<a href="http://www.netprotections.com/atobarai/">NP後払い</a>」という決済を利用するので、この支払方法を選択した注文に対して所定の手数料（今回は200円）を商品代金以外に加算したいと思います。

この場合、Welcart側で用意された<a href="http://www.welcart.com/community/archives/1697">フック</a>を利用して、NP後払いを選択した場合だけ手数料を加算する、という処理を、使用するテーマのfunctions.phpに書き加えます（既存のテーマを使っている場合は、<a href="http://wpdocs.sourceforge.jp/%E5%AD%90%E3%83%86%E3%83%BC%E3%83%9E">子テーマ</a>を作ってからfunctions.phpファイルを作成するとよいでしょう）。コードはこんな感じになります。

（追記：2013.12.8 コードを見直しました）
<pre class="decode:1 " >
function my_filter_getCODFee(){
	$args = func_get_args(); //フックからデータを取得
	list ($fee, $payment_name, $amount_by_cod) = $args; //配列を変数にセット
	if ($payment_name == 'NP後払い') {
		$fee = 200;  //支払方法がNP後払いなら、手数料を200円に設定
	}
	return $fee;
}

add_filter('usces_filter_getCODFee', 'my_filter_getCODFee', 10, 3);

function my_filter_cod_label() {
	$text = '代引・後払い手数料'; //カートの手数料表記を書き換える
	return $text;
}

add_filter('usces_filter_cod_label', 'my_filter_cod_label');
</pre>

コードのご利用はご自由にどうぞ。ただし、不具合などの責は負いかねますので、よくテストしてご利用ください。
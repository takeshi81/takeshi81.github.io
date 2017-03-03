---
id: 316
title: '[EC] 続・消費税計算と総額表示'
date: 2009-08-02T01:27:14+00:00
author: いがらしたけし
layout: post
guid: http://indigo-design.org/?p=316
permalink: /2009/08/calculate-consumption-tax-2/
categories:
  - 仕事
tags:
  - eCommerce
  - Web
  - 仕事
---
<a href="https://indigo-design.org/2009/07/calculate-consumption-tax/">前の記事</a>の続きです。

<a href="http://d.hatena.ne.jp/zan-gyo/">「残業プログラマの雑記」</a>のid:zan-gyo様から<a href="http://d.hatena.ne.jp/zan-gyo/20090730/1248947252">追記記事</a>のトラックバックをいただいたので、拝見しました。

<!--more-->
<blockquote>とある商品が複数個購入された場合に端数の累積をどのように扱うかは店舗次第ですが、<span style="text-decoration: underline">一般的には購入者側に負担が少なくなるように処理するのが普通</span>かと思います。

（中略）
<ul>
	<li>端数処理を <strong>切捨て</strong> で行う仕様の場合は単価毎に消費税の端数処理を行い数量で掛けると金額が少なくて済むのでEC-CUBEの現行の仕様で問題ありません。</li>
	<li>端数処理が <strong>四捨五入</strong> か <strong>切り上げ</strong> の場合は単価毎に端数処理を行うと誤差が累積します。</li>
</ul>
今回私が携わったBtoBサイトでは<span style="text-decoration: underline">「税抜き価格入力に対する四捨五入」が条件でしたのでお客様の負担を軽減するためには端数処理の計算方法の変更の必要が発生した</span>というわけです。</blockquote>
なるほど。確かにEC-CUBEの仕様（たまたまローカルに入っていたver.2.3.3で動作を確認しました）によれば、端数処理を「四捨五入」「切り上げ」にした場合、税額が本体価格の5%を超えるケースが発生します。これは購入者側にしてみれば便乗のように見えてしまい、よい印象を与えないと思います。

自分もFileMakerで請求書のデータベースを作る際、税込価格から税額を求める式では「税込金額×消費税率」の<span style="text-decoration: underline">端数を切り捨ててから</span>「税額」を出し、「税込価格−税額」を「本体価格」としました。上記と同じく「税額が5%を超えるのは印象がよくない」という考えからです。
<blockquote>尚、EC-CUBEには４つめの端数処理方法が存在します。大抵のBtoCサイトではこの方式を選択してカスタマイズするのが最も安定する方法かと思います。それは
<ul>
	<li>消費税を０％に指定して</li>
	<li>単価を税込価格で入力する。</li>
</ul>
画面表示時に税額を逆算する必要はありますが仕様として押し付けてしまえば一番無難かもしれません。

引用元: <a href="http://d.hatena.ne.jp/zan-gyo/20090730/1248947252">EC-CUBE 追記 - 残業プログラマの雑記</a></blockquote>
その通りだと思います。総額表示の趣旨からしても、税込価格で取引すべきということですから、消費税分を逆算するのが無難だと思います。
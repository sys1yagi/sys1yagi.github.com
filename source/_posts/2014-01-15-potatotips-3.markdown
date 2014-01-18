---
layout: post
title: "第3回はヤフー開催！ #potatotips で発表されたAndroidのtipsまとめ"
date: 2014-01-15 19:11:45 +0900
comments: true
categories: android potatotips
---

iOSまとめはコチラ→[第3回はヤフー開催！ #potatotips で発表されたiOSのtipsまとめ](http://himaratsu.hatenablog.com/entry/potatotips3)

potatotips 第3回に参加してきました。今回はヤフーオフィスでの開催！
[https://github.com/potatotips/potatotips/wiki/Potatotips-3](https://github.com/potatotips/potatotips/wiki/Potatotips-3)

<blockquote class="twitter-tweet" lang="ja"><p>potatotips#3 in ヤフーさんに参加中！ <a href="https://twitter.com/search?q=%23potatotips&amp;src=hash">#potatotips</a> <a href="http://t.co/sDo41dfCg4">pic.twitter.com/sDo41dfCg4</a></p>&mdash; 所 友太 (@tokorom) <a href="https://twitter.com/tokorom/statuses/423396114457317377">2014, 1月 15</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

<!-- more -->

potatotipsは発表者だけが参加できる、持ち時間1人5分のtips共有会です。
いつもはクックパッド開催していましたが、今回はヤフーさんと合同開催する運びとなりました。三回に一回はクックパッド外での開催にしたいと思っているので「やろうず(^q^)」という方は是非所さんなどに声掛けください。

そんな第3回で発表された9つのAndroidのtipsをまとめます！

##レビューを良くするには
[@rejasupotaro](https://twitter.com/rejasupotaro)さん。

発表はGistで行っていたので、スライドはなし。まとめがブログに→
[アプリの評価を良くするということについて考える](http://rejasupotaro.github.io/blog/2014/01/16/29/)

個人的に気になったのは、レビューダイアログを出すライブラリの存在。こんなんあったんだなー。ほげー。

* iOS: [iRate](https://github.com/nicklockwood/iRate)
* Android: [Android-RateThisApp](https://github.com/kskkbys/Android-RateThisApp)

評価周りはなかなか難しい。個人的にはGoogle Playによく顔を出し、評価コメントにレスしたり、アプリ説明の所で現在やってる事とか注意とかを更新し続けるというのが地道かつ有効な方法かなーと感じているものの、「もっといい方法あるんじゃないか」という気もしている。

あとACRAいいよACRA。

## アプリでもオブジェクト思考エクササイズ

[@shoma2da](https://twitter.com/shoma2da)さん。

<iframe src="http://www.slideshare.net/slideshow/embed_code/30032646" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/shoma2da/potatotips3-shoma2da" title="アプリでもオブジェクト指向エクササイズ（Potatotips#3）" target="_blank">アプリでもオブジェクト指向エクササイズ（Potatotips#3）</a> </strong> from <strong><a href="http://www.slideshare.net/shoma2da" target="_blank">Shoichi Matsuda</a></strong> </div>

ThoughtWorksアンソロジーに書かれているエクササイズらしい。気になる。制約が多い。

[![01](http://ecx.images-amazon.com/images/I/51FOBZPjz-L._BO2,204,203,200_PIsitb-sticker-arrow-click,TopRight,35,-76_AA300_SH20_OU09_.jpg)<br/>ThoughtWorksアンソロジー ―アジャイルとオブジェクト指向によるソフトウェアイノベーション](http://www.amazon.co.jp/dp/487311389X)

実戦にいきなり持ち込むのは危険な香りがするものの、あるテーマをこの制約で実装する「エクササイズマラソン」とかやると面白いかもしれないなと思う。「ひとつのクラスにフィールド2個まで」ってのは脳みそ痺れる。あとAmazonでは値段高騰しててつらぽ。

## Fitting解像度対応β

[@taqoo_negishi](https://twitter.com/tq_ne_jp)さん。

なんと発表はイラレ。レイヤーを切り替えてページ遷移。そっちに気を取られてしまった！
SurfaceViewを使ったゲームアプリを作っていて、画面幅等で倍率を動的に求め、その値を使って画像サイズやタッチ位置を補正する感じにしている。という発表。
UI設計としては正方形に納める事を意識していて、変なサイズの画面が来ても大丈夫にしている。

[@taqoo_negishi](https://twitter.com/tq_ne_jp)さんのアプリはコチラ→[https://play.google.com/store/apps/developer?id=TaQoo](https://play.google.com/store/apps/developer?id=TaQoo)
Cocos2dやUnity等は使わずSurfaceViewでフルスクラッチだそう。イラレで発表していたのでリソース類も自分で作っているのではないかと思う。すげー。

あとイラレすごい。

## ちょっと優しい入力項目

[@sakebook](https://twitter.com/sakebook)さん。

<iframe src="http://www.slideshare.net/slideshow/embed_code/30043058" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/sakebook/ss-30043058" title="ちょっと優しい入力項目" target="_blank">ちょっと優しい入力項目</a> </strong> from <strong><a href="http://www.slideshare.net/sakebook" target="_blank">Shinya Sakemoto</a></strong> </div>

EditTextのフォーカス移動の話。この辺意外と理解が曖昧だったりするのでこういった資料があると非常に捗る。フォーカスまじ大変。バージョンで挙動違うからなーつらい。

## Reflectionを使おう、というお話

[@kobito_kaba](https://twitter.com/kobito_kaba)さん。

AndroidのバージョンチェックしてAPI Levelが足りない場合呼び分けるという処理を書いた時、
Android1.6だとクラスロード時点で存在しないメソッドがあると死ぬ問題があって、このためリフレクションを使って回避できるよねという話。でも今や1.6対応って意味ない。ではどういう時に使うか。

* root取らないといけない時とか

もう一個あったと思いますが忘れてしまいました・・・。
rootの件は、たとえばDNS設定は2.xではふつーに書き換えられたけど、3.x以降では塞がれた、しかしリフレクションによって書き換えが可能に！という話。これでテストも捗る。という。

しかし聞いていると、なんかこう、セキュリティ・ホールでは・・・？という気がしてきた。ちょっと調べてみよう。
リフレクションは便利だけどこわいなーやっぱり。

## TDDでアプリ開発。カバレッジ8%を目指せ（消費税連携！？）
[@tarotaro4](https://twitter.com/tarotaro4)

<iframe src="http://www.slideshare.net/slideshow/embed_code/30039278" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/tkawashita/20140115-potato-tips-no3-android-app-test-development-driven-and" title="20140115 potato tips No.3 Android App Test Development Driven and Jenkins CI Start" target="_blank">20140115 potato tips No.3 Android App Test Development Driven and Jenkins CI Start</a> </strong> from <strong><a href="http://www.slideshare.net/tkawashita" target="_blank">tkawashita </a></strong> </div>

CloudBeesでCIする感じ。CloudBees知らなかったので是非使いたい。emmaは次期Gradle pluginでサポートされるようなので期待。全バリエーションは１回のビルド&テストで6時間かかるらしいのでやはりCIの道は険しい。「ローカルテストは小学生まで」は心に刻んでおきたい。

## KotlinでAndroidアプリ開発！(後編)

[私](https://twitter.com/sys1yagi)です。

<iframe src="http://www.slideshare.net/slideshow/embed_code/30039475" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/bs_yagi/potato03" title="Potato03 KotlinでAndroidアプリ開発(後編)" target="_blank">Potato03 KotlinでAndroidアプリ開発(後編)</a> </strong> from <strong><a href="http://www.slideshare.net/bs_yagi" target="_blank">Toshihiro Yagi</a></strong> </div>

Kotlinｻｲｺｰ！

## Gradleの共通ルーチンをテストする（後編）
[@__gfx__](https://twitter.com/__gfx__)さん。

<iframe src="http://www.slideshare.net/slideshow/embed_code/30039867" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/gorof/potatotips3" title="Gradleだってテストしたい #potatotips" target="_blank">Gradleだってテストしたい #potatotips</a> </strong> from <strong><a href="http://www.slideshare.net/gorof" target="_blank">Goro Fuji</a></strong> </div>	

Gradle周りはガッツリ触ってないのでこういう感じで色々やってみるのはよさそーだなーとｵﾓﾀ。ﾏｸﾛとか書けるんじゃない感ある。もはやGroovyっていうより、Gradleな世界観があって理解が大変だったりする。しかもGradle周りのソースには.javaが混在してて魔界感がある。Power Assertはいいなー。


## AndroidのHTTPライブラリってどれがいいんでしょうか

飛び入り参加の[@ninjinkun](https://twitter.com/ninjinkun)さん。

最近Android界隈に迷い込んだのだとか。よいHTTPライブラリを探していて、

* [Retrofit](http://square.github.io/retrofit/)
* [Volley](https://android.googlesource.com/platform/frameworks/volley)
* [android-async-http](https://github.com/loopj/android-async-http)

とかがよさ気なのかなという話。

[Retrofit](http://square.github.io/retrofit/)知らなかったSquareまじｶｯｹｰ。


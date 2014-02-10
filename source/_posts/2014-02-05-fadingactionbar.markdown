---
layout: post
title: "FadingActionBar -open source libraries #001-"
date: 2014-02-05 22:36:50 +0900
comments: true
categories: android oss
---

　[Androidオープンソースライブラリ徹底活用](http://www.amazon.co.jp/gp/product/4798040029/)の発売以降、続々と新しいライブラリが出てきて、本に載せられなかった分も含めて色々とキャッチアップしていきたいなーと思ったので本に近い形式でライブラリを取り上げていこうかなーと思います。本よりだいぶ砕けた文になると思いますがご了承ください。あと本ではEclipseベースで記述していましたが、ここではAndroid Studioベースで書きます。EclipseでAndroidアプリケーション開発が許されるのは小学生までだと思います。

# FadingActionBar

ActionBarの領域をフェードできるライブラリ

* サポートバージョン: 2.2以上
* License: Apache 2.0
* タイプ: aar, ライブラリプロジェクト
* 公式サイト:[https://github.com/ManuelPeinado/FadingActionBar](https://github.com/ManuelPeinado/FadingActionBar)

* サンプルコード:[https://github.com/sys1yagi/FadingActionBarSample](https://github.com/sys1yagi/FadingActionBarSample)

## 概要

　FadingActionBarはActionBar部分を画面のスクロールにしたがってフェードできるライブラリです。ActionBar部分までコンテンツをオーバーレイさせたい場合に利用できます。また、オーバーレイしたコンテンツ部分をパララックスにする事もできます。

### 動作イメージ

スクロールすると指定した色にActionBarがフェードします。ファーストビューでコンテンツを大きく見せられます。

<img src="/images/2014-02-05-fadingactionbar/01.jpg" width="200px"/>
<img src="/images/2014-02-05-fadingactionbar/02.jpg" width="200px"/>
<img src="/images/2014-02-05-fadingactionbar/03.jpg" width="200px"/>

<!-- more -->

## 導入手順

　FadingActionBarはaar(Android archive)形式をサポートしており、build.gradleのdependenciesに定義するだけでライブラリを利用できます。以下の定義は通常のActionBarでFradingActionBarを利用する場合の設定です。

```groovy
dependencies {
  compile 'com.github.manuelpeinado.fadingactionbar:fadingactionbar:3.1.0'
}
```

　FadingActionBarは通常のActionBarの他に、appcompat-v7のActionBarCompatやActionBarSherlockをサポートしています。ActionBarCompatを使う場合、ActionBarSherlockを使う場合の設定をそれぞれ以下に示します。

### ActionBarCompat

```groovy
dependencies {
  compile 'com.android.support:appcompat-v7:+'
  compile 'com.github.manuelpeinado.fadingactionbar:fadingactionbar-abc:3.1.0'
}
```

### ActionBarSherlock

```groovy
dependencies { 
  compile 'com.github.manuelpeinado.fadingactionbar:fadingactionbar-abs:3.1.0'
}
```

　Eclipseを使う場合は、FadingActionBarをcloneし、ライブラリプロジェクトとして参照してください。

## FadingActionBarを使う

　FadingActionBarは以下の様な画面のスクロールが発生するレイアウトでの利用を想定しています。

* ScrollView
* WebView
* ListView

　ここではActionBarCompatでScrollViewを使う例を解説します。

### テーマの定義をする

　まず、FadingActionBarを利用するにあたって必要なテーマを定義します。通常ActionBarは不透明で、コンテンツ領域はActionBarの表示領域の下部から始まります。これらのスタイルを変更して、背景を透過し、コンテンツ領域にオーバーレイするActionBarにします。

　以下の例では`AppTheme`という名前でActionBarの透過、オーバーレイの定義をしています。

```xml
<resources>

  <style name="Widget.ActionBar" parent="@style/Widget.AppCompat.Light.ActionBar.Solid.Inverse">
  </style>

  <style name="Widget.ActionBar.Transparent">
    <item name="android:background">@android:color/transparent</item>
    <item name="background">@android:color/transparent</item>
  </style>

  <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <item name="actionBarStyle">@style/Widget.ActionBar.Transparent</item>
    <item name="windowActionBarOverlay">true</item>
    <item name="android:windowContentOverlay">@null</item>
  </style>

</resources>

```

　`AppTheme`をAndroidManifest.xmlのapplication要素に設定します。application要素だとアプリケーション内の全てのActivityにテーマが適用されてしまうので、Activity毎に個別に適用したい場合はactivity要素に設定してください。

```xml
<application
    android:icon="@drawable/ic_launcher"
    android:label="@string/app_name"
    android:theme="@style/AppTheme">
    
    <!-- 省略 -->
    
</application>
```

### ヘッダのレイアウトを作成する

　FadingActionBarは、ActionBarにオーバーレイするヘッダ部分と、それ以外のコンテンツ部分を異なるレイアウトで管理します。

<img src="/images/2014-02-05-fadingactionbar/04.jpg" width="400px"/>

　以下のXMLはヘッダに表示するレイアウトの例です。多くの場合大きなImageViewを利用する事になるでしょう。

```xml
<ImageView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:src="@drawable/main_photo"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:scaleType="centerCrop"
    android:adjustViewBounds="true"
    />
```

### コンテンツのレイアウトを作成する

　次にコンテンツのレイアウトを定義します。ここで重要なのは、ヘッダ、コンテンツどちらのレイアウトにも`ScrollView`が登場していない点です。FadingActionBarが自動的に`ScrollView`でこれらのレイアウトをラップするので自分で定義する必要はありません。

```xml
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:background="?android:attr/windowBackground"
    >
  <TextView
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:background="@drawable/shape_header"
      android:padding="10dp"
      android:textStyle="bold"
      android:text="photo by"
      />
  <TextView
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:padding="10dp"
      android:text="http://www.flickr.com/photos/legin101/5480688759"
      />
</LinearLayout>
```


### FadingActionBarHelperでレイアウトを初期化する

　レイアウトの初期化はFadingActionBarHelperクラスを使って行います。FadingActionBarHelperクラスは環境によって異なるパッケージに定義されています。ActionBarCompatを利用する場合は`.extras.actionbarcompat`のFadingActionBarHelperクラスを利用する事になります。

　以下の様にActivityのonCreateメソッドでFadingActionBarHelperクラスを作成し、メソッドチェーンで必要なパラメータをセットします。

```java
import com.manuelpeinado.fadingactionbar.extras.actionbarcompat.FadingActionBarHelper;

//中略
public class MainActivity extends ActionBarActivity {

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    FadingActionBarHelper helper = new FadingActionBarHelper()
      .actionBarBackground(android.R.color.holo_blue_light)
      .headerLayout(R.layout.header_main)
      .contentLayout(R.layout.activity_main);

```

　上記コードで呼び出しているFadingActionBarHelperクラスのメソッドについて以下の表に示します。headerLayoutメソッド及び、contentLayoutメソッドは必ず呼び出してレイアウトの値を設定しなければなりません。

名前|解説|必須
--|--
actionBarBackground(int drawableResId)|フェード後のActionBarの背景を設定できます|×
headerLayout(int layoutId)|ActionBarにオーバーレイするレイアウトを設定できます|○
contentLayout(int layoutId)|ヘッダレイアウトの下部に表示するコンテンツ領域のレイアウトを設定できます|○

　FadingActionBarHelperクラスの初期化が終わったら、initActionBarメソッドを呼び出してActionBarに設定を反映します。その後createViewメソッドを使って画面に表示するViewを作成します。createViewメソッドで取り出せるViewには設定したヘッダとコンテンツのレイアウトが含まれています。

```java
  
    helper.initActionBar(this);
      
    setContentView(helper.createView(this));
  }
```

　実際にcreateViewメソッドで取り出せるViewの[Treeをダンプする](http://visible-true.blogspot.jp/2012/02/view.html)と以下の様な構造である事がわかります。

```
com.manuelpeinado.fadingactionbar.view.RootLayout
 android.widget.FrameLayout
  android.widget.ImageView
  android.view.View
 com.manuelpeinado.fadingactionbar.view.ObservableScrollView
  android.widget.LinearLayout
   android.widget.FrameLayout
   android.widget.LinearLayout
    android.widget.TextView
    android.widget.TextView
```

　これでActionBarにコンテンツをオーバーレイし、ActionBarをスクロールに従ってフェードできる様になります。

## Fragmentで使う

　FragmentでFadingActionBarを利用する場合は、FadingActionBarHelperクラスをonCreateViewメソッドのタイミングで初期化します。これだけでOKです。

```java
public class ParallaxFragment extends Fragment {
  //中略  
  @Override
  public View onCreateView(LayoutInflater inflater, ViewGroup container,
      Bundle savedInstanceState) {
    FadingActionBarHelper fadingActionBarHelper = new FadingActionBarHelper()
        .actionBarBackground(android.R.color.holo_blue_light)
        .headerLayout(R.layout.header_main)
        .contentLayout(R.layout.activity_main);
        
    fadingActionBarHelper.initActionBar(getActivity());
    View view = fadingActionBarHelper.createView(inflater);
    return view;
  }
}
```

## パララックスの設定をする

　FadingActionBarはヘッダ部分をパララックスにできます。FadingActionBarHelperクラスのparallaxメソッドで設定できます。デフォルトではオンになっています。

```java
FadingActionBarHelper helper = new FadingActionBarHelper()
  .parallax(false)
  .actionBarBackground(android.R.color.holo_blue_light)
  .headerLayout(R.layout.header_main)
  .contentLayout(R.layout.activity_main);

```

　パララックス有りと無しでは、以下の様にスクロール時のヘッダの表示が変わります。パララックス有りだとスクロール量より遅めにヘッダ部分がスクロールします。

パララックス有り|パララックス無し
--------|---------
<img src="/images/2014-02-05-fadingactionbar/05.jpg" width="250px"/>|<img src="/images/2014-02-05-fadingactionbar/06.jpg" width="250px"/>

## HeaderOverlayを使う

　ヘッダにボタン等の操作用UIを配置したい場合、パララックスをオンにしているとスクロール時に表示がズレてしまうので管理が大変です。HeaderOverlayを使うと、ヘッダの前面にオーバーレイするViewを追加する事ができ、パララックスの影響を受けないレイアウトを作れます。

　HeaderOverlayはFadingActionBarHelperクラスのheaderOverlayLayoutメソッドでセットできます。

```java
FadingActionBarHelper fadingActionBarHelper = new FadingActionBarHelper()
  .actionBarBackground(android.R.color.holo_blue_light)
  .headerLayout(R.layout.header_main)
  .headerOverlayLayout(R.layout.header_overlay)
  .contentLayout(R.layout.activity_main);
```

　以下の様にスクロールしてもパララックスの影響を受けないViewを追加できます。

<img src="/images/2014-02-05-fadingactionbar/07.jpg" width="250px"/>
<img src="/images/2014-02-05-fadingactionbar/08.jpg" width="250px"/>

## おわりに

　軽めに書くつもりが結構なボリュームになってしまった・・・。FadingActionBarなかなかよさそうですね。ただ自前でテーマ定義する部分は少し面倒です。aar形式なのだし、ライブラリ側に含める事が出来るんじゃないかなぁ・・・と思いました。暇があれば検証&pull reqしてみようかなと思います。


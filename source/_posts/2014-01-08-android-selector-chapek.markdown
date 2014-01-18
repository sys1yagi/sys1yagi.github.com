---
layout: post
title: "SelectorChapek for Androidでselectorを自動生成する"
date: 2014-01-08 23:36:30 +0900
comments: true
categories: android androidstudio plugin
---

カスタムなデザインのボタンを作ろうと思ったら、通常の状態の画像とボタン押下時の画像を用意して、drawableにselectorを定義したxmlを配置して使う事になります。画像の用意はともかく、このselectorのxmlファイルというのがいつもめんどくさいです。大体ググって毎回書き方を調べたりします。

このかったるい作業を簡単にしてくれるのがSelectorChapek for Androidです。

<!-- more -->

## SelectorChapek for Androidをインストールする

SelectorChapek for AndroidはAndroid Studioのpluginです。Github([SelectorChapek for Android](https://github.com/inmite/android-selector-chapek))を見ればもうそのまんま使い方を書いてありますが解説します。

Android Studioを起動して、[Preference]-[Plugins]を開き、`Browse repositories…`を押下してください。

![01](/images/2014-01-08-android-selector-chapek/01.png)

Browse Repositoriesで`SelectorChapek`で絞り込むとpluginが見つかるので、ダブルクリックしてインストールしてください。

![02](/images/2014-01-08-android-selector-chapek/02.png)

## 画像リソースを用意する

SelectorChapek for Androidは命名規則に従った画像リソースを用意する事で、selectorの自動生成を実現します。それぞれの画像リソースのファイル名に、以下の様な状態に対応したサフィックスを付加します。

サフィックス|Drawable state
--------|---------
_normal|(default state)
_pressed|state_pressed
_focused|state_focused
_disabled|state_enabled (false)
_checked|state_checked
_selected|state_selected
_hovered|state_hovered
_checkable|state_checkable
_activated|state_activated
_windowfocused|state_window_focused

シンプルなカスタムボタンであれば以下の様に２つの画像を用意すれば十分でしょう。

```
button_normal.png
button_pressed.png
```

## selectorを生成する

作成した画像をdrawable-xhdpiなどに置き、

![03](/images/2014-01-08-android-selector-chapek/03.png)

ディレクトリを右クリックすると`Generate Android Selectors`という項目が表示されるので選択します。

![04](/images/2014-01-08-android-selector-chapek/04.png)

すると、`drawable/button.xml`が生成されます。楽ちん。

```
<?xml version="1.0" encoding="UTF-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item 
      android:drawable="@drawable/button_normal"
      android:state_pressed="false"/>
    <item 
      android:drawable="@drawable/button_pressed" 
      android:state_pressed="true"/>
</selector>
```

## 条件を複数つける

例えば、disableかつ、pressedとかいった複数の状態を表す場合はサフィックスを連結すれば行えます。

```
button_disabled_pressed.png
```




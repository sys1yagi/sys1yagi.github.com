---
layout: post
title: "Octpressに移行してみる"
date: 2014-01-07 23:06:12 +0900
comments: true
categories: octopress
---

ブログをGithub Pagesに移行しつつ、[Octopress](http://octopress.org/)を導入しました。
OctopressはMarkdownで書くので捗るわー。テーマは[oscailte](https://github.com/coogie/oscailte)を使ってます。

<!-- more -->

## Github Pagesのリポジトリを作る

[GitHub Pages](http://pages.github.com/)を参照してリポジトリ作って下さい。

## Octopressの環境構築

rmvかrbenvを入れて、ruby1.9.3を入れておく。

まずはOctopressの本体をcloneする。

```
git clone git://github.com/imathis/octopress.git octopress
```

Octopressのディレクトリに移動し、bundlerをインストールする。その後`bundle install`で依存するモジュールをインストールする。

```
cd octopress
gem install bundler
rbenv rehash    # rbenvを使っている場合
bundle install
```

以下のコマンドでデフォルトテーマがインストールされる。

```
rake install
```

## ブログ本体を生成し、デプロイする

以下のコマンドでGithub Pagesの設定を行います。リポジトリのURLとかを聞かれます。

```
rake setup_github_pages
```

その後以下のコマンドでブログ本体を生成します。

```
rake generate
```

すると`_deploy`ディレクトリが生成されます。ここにGithub Pagesの.gitが作られます。Github Pagesのリポジトリが空なら以下のコマンドでデプロイできるはずです。

```
rake deploy
```

もし、リポジトリ内になにかファイルがある場合は、`git pull`して不要なファイルを削除して下さい。

## 新しいエントリを作成する

新しいエントリを作成するには以下のコマンドを使います。

```
rake new_post["エントリ名"]
```

以下のパスに新しいMarkdownファイルが生成されます。

```
source/_posts/yyyy-mm-dd-エントリ名.markdown 
```

このファイルを編集して、

```
rake generate
rake deploy
```

で新しいエントリをデプロイできます。


## ブログをプレビューする

書きかけのエントリなどを確認するには以下のコマンドを使います。

```
rake preview
```

4000番でWEBrickが動くので、

```
http://localhost:4000
```
でプレビューを見れます。


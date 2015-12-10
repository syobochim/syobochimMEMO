# Git利用ガイド

## 記載内容

### 書いていること

- 基本的な考え方（リモートリポジトリとローカルリポジトリ、ブランチ）
- 開発をすすめていくなかでの最低限の操作方法
- GitとSubversionの構成管理の考え方の違い(説明のなかで少し出てきます)

### 書いていないこと

- そもそも構成管理とはなにか
- ツールのインストール方法、初期設定方法(環境構築ガイドに書いてあるようなこと)
- 実行コマンド
- 高度な使い方

## 使うツール

### 開発PC

- git
- SourceTree

### リモートリポジトリ

- gitBucket(ブラウザから参照出来る画面です。)

## SubversionとGit

構成管理の考え方についてはSubversionとGitでの差はありません。  
どちらも、開発者はローカルにてソースコードの変更し、リモートリポジトリにソースコードを格納することでソースコードの共有を行います。  
また、ソースコードの変更差分のバージョン管理はリモートリポジトリにて行います。  
  
SubversionとGitでの開発者の操作のながれを２つの図で記載します。  
以下の2つの図を見比べてみても、開発者の操作はほぼかわりません。  
※SubversionにはあってGitにない操作、GitにあってSubversionにない操作を黄色枠で囲っています。  
ただし、**Gitにはローカルリポジトリというものがある**ということを覚えてください。

### Subversionの操作のながれ

<img src="./img/Subversion.png" width="600px">

### Gitの操作のながれ

<img src="./img/Git.png" width="600px">

### ローカルリポジトリとは

ローカルリポジトリとは、開発PC内で（オフラインで）コミットの記録を保管しておける領域です。  
Gitでは、ローカルリポジトリに一度変更差分を登録し、その変更差分をリモートリポジトリに反映していきます。  
リモートリポジトリはgitBucketにて管理しているリポジトリのことです。  
ローカルリポジトリへのソースコード変更の登録は"**自分だけ**"がわかり、  
それをリモートリポジトリへ反映することで"**チームへ**"変更内容を展開することが出来ます。  
操作が"**ローカルリポジトリに対して**"か"**リモートリポジトリに対して**"かを意識しましょう。  
以下解説では、上図のようにローカルリポジトリ(青色の四角)・リモートリポジトリ(オレンジ色の雲)を分けて解説していきます。

## ブランチについて

(Subversionでは開発のために各開発者がブランチをきることはなかったと思いますが、)  
Gitでは各開発者がブランチをきって開発をすすめていきます。  
Gitでは強力なマージ機能があります。そのため、ブランチをきっても、マージする際のコストはあまりかかりません。  
ブランチをわけ、マージする際にレビューする仕組みにすることで、ソースコードの品質を維持することができます。  
PGUT工程中は、主に以下のような種類のブランチができます。

- masterブランチ
  + チームにて管理するブランチ
  + 本番環境へリリースするソースコードを管理する
  + モジュール：ブランチ＝1：1
- developブランチ
  + チームにて管理するブランチ
  + 開発中のソースコードを管理する
  + 既にレビューに合格しているもののみ格納する
  + モジュール：ブランチ＝1：開発拠点数(※開発拠点が一箇所であれば1)
- featureブランチ
  + 開発者が作成し、開発者が削除するブランチ
  + 開発中かつレビュー合格前のソースコードを格納する
  + モジュール：ブランチ＝1：他

### ブランチの概念

gitのブランチは以下のように、矢印を使用した図を用いてブランチの説明をすることが多いです。  
以下の記載方法では、ブランチの時系列を表すことが出来ます。  
ただし、本ドキュメントでは、「ある時点でのリポジトリの状態を断面化したもの」としてブランチを説明していきます。

![](./img/gitFlow.png)

ブランチを切り替えることで、ローカルファイルがブランチごとに変更されていきます。  
今自分がどのブランチにいるのかを意識しましょう。  
なお、上記"Gitの操作の流れ"のイメージ図に記載しましたが、各開発者はまず開発PCのローカルリポジトリのファイルに対して変更を登録していきます。

![](./img/git-branch.png)

## 実際の操作

では、実際の操作方法について記載していきます。  
状況にあわせて以下リンクを参照してください。

### 対象読者

以下全てに当てはまる人を対象読者としています。  
ただし、操作方法リンクに★をつけて補足を記載している箇所は、全員が参照するようにしてください。

- Subversionを利用した開発経験がある。
- Gitを使うのは初めて。
- SourceTreeをインストールしている。

## 操作方法リンク先

[プロジェクト参加のときにやること(clone)](./git/clone.html)

[開発を始めるときにやること(checkout)](./git/checkout.html)
　∟★ブランチの切り方について記載しています。

[開発中にやること(ローカルでの作業)(addとcommit)](./git/commit.html)
　∟★コミットメッセージについて記載しています。

[開発中にやること(リモートブランチへの反映)(push)](./git/push.html)

[レビュー依頼のときにやること(pull request)](./git/pullRequest.html)
　∟★プルリクエストに記載するコメントについて記載しています。
 
[レビューのときにやること(レビュアーが実施)](./git/check.html)

[レビュー指摘対応のときにやること](./git/review.html)

[レビュー合格のときにやること(レビュアーが実施)(merge)](./git/finish.html)
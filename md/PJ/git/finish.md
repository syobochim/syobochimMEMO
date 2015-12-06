# レビュー合格のときにやること(レビュアーが実施)

## 概要

レビューし、内容に問題がなければ、featureブランチをdevelopブランチへマージしましょう。  
developブランチへマージすると、他の開発者に対して変更内容を展開することが出来ます。  
featureブランチはdevelopブランチへのマージ後は不要になるので、削除しましょう。  
残しておくと、どれが既にマージ済みのfeatureブランチなのかわからなくなり、ソースコードの取り込み漏れが発生する可能性があります。

![pullRequest](../img/finish.png)

## 事前準備

- レビュー指摘に全て対応されていること

## 作業内容

① gitBucketの画面を開きます。
② Merge pull requestボタンを押します。

<img src="../img/gitBucket_finish.png" width="700px" border="1">

③ Confirmマージボタンを押します。これがイメージ図の**Merge**です。

<img src="../img/gitBucket_merge.png"  border="1">

④ Delete branchボタンを押して、不要になったブランチを削除しましょう。
※ブランチを削除しても、コミットの記録およびpull requestは"Close"のステータスで残ります。

<img src="../img/gitBucket_deleteBranch.png"  border="1">

## 事後確認

developブランチに変更が反映されています。  
featureブランチが削除されています。  

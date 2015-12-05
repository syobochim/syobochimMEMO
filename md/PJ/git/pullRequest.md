# レビュー依頼のときにやること

## 概要

タスクが完了したら、レビュアーにレビュー依頼を出しましょう。  
gitBucket上でpullRequest機能を使用することで、developブランチとfeatureブランチの差分を確認することが出来ます。  
差分を確認し、pullRequestを作成しましょう。  
レビュアーに対しては、pullRequestのURLをレビュー依頼と共に連携しましょう。  
レビューOKのもののみ、pullRequestページにあるMergeボタンを使用して、developブランチへ反映させます。(レビュアーが実施。)  
※本作業を怠ると、品質が保証されていないソースコードが他の開発者の環境に適用されてしまいます。必ず実施してください。  

**なお、pull requestの説明欄には以下項目を記載してください。**  
(Markdown記法を使用することで、タイトルなどを見やすくすることが出来ます。)

```
## 概要

* なぜこの変更をするのか、
* 課題は何か、
* これによってどう解決されるのか、
* など、この変更に対する概要を記載

## INPUT資料

何をINPUTにしたか
```

![pullRequest](../img/pullRequest.png)

## 事前準備

- クロージング作業を全て完了していること

## 作業内容

① gitBucketの画面をひらきましょう。  
② Pull Requestsのリンクを押します。

<img src="../img/gitBucket_pullRequest.png" width="700px" border="1">

③ New pull requestボタンを押す。

<img src="../img/gitBucket_pullRequest2.png" border="1">

④ baseブランチにdevelopブランチを指定し、headブランチにfeatureブランチを指定する。  
⑤ Create pull requestボタンを押す。

<img src="../img/gitBucket_pullRequest3.png" width="700px" border="1">

⑥ ソースコードの差分が表示されるので、内容を確認してください。レビュー対象のみ、表示されているようにしましょう。  
⑦ レビュー内容を、レビュアーにわかるよう記載しましょう。  

<img src="../img/gitBucket_pullRequest4.png" width="700px" border="1">

⑦ Create pull requestボタンを押してください。これが、イメージ図の**pullRequest**です。  
**Merge pull requestボタンが活性になっていることを確認してください。**  
活性になっていない場合は、『開発中にやること（リモートブランチへの反映）』の章をやり直してください。

### 完了状態

プルリクエストを作成することが出来ました。  
Merge pull requestボタンが活性になっていることを確認してください。  
  
レビュー内容がConversationタグで確認できます。  
対象コミットがCommitsタグで確認できます。  
developとfeatureの差がFile Changedタグでファイル差分を確認する事ができます。
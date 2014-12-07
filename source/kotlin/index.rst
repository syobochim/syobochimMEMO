Kotlin(\*´Д`)ﾊｧﾊｧ
=======================
Kotlinは、IntelliJ IDEAで有名なJetBrainsさんが作ってるプログラミング言語。

静的に型付けされた言語で、JVM上で実行することができる。
また、JavaScriptへの変換もできる。

何よりも名前がかわゆく、女子力が高まる感じが非常に良い言語である。

Kotlinの動かし方
----------------
とりあえず実行するならブラウザで動く `Kotlin Web Demo <http://kotlin-demo.jetbrains.com/>`_ 。
Kotlinお手軽。

ちゃんとやるなら `IntelliJ IDEA <https://www.jetbrains.com/idea/download/>`_ 。
日本だとお髭のイケメンさんがライセンスの販売代理店をやっている。

でも Yosemite で起動するとJava6が無いと怒られる。 `:;(∩´﹏`∩);:`

検索するとさっきの代理店のブログが見つかった。→ http://samuraism.com/2014/10/17/2555
無事起動できた!! `（｀・ω・´）`

IntelliJ IDEA → Preferences... → Plugins → Install JetBrains plugin... ボタン → "kotlin"で探してInstall plugin!!
IntelliJ IDEA再起動してインストール完了 `＼(^o^)／`

後の細かいところは https://sites.google.com/site/tarokotlin/chap2/sec24 に任せたっ!

Hello World!!
---------------------
Hello Worldの例。かわゆさある。

.. code-block:: java

   package hello

   // main関数はパッケージレベルのファンクションで宣言する
   fun main(args: Array<String>) {
     println("Hello World!")
   }
  
Classの定義
---------------------
Classのコンストラクタは１つだけしか定義出来ない
（コンストラクタオーバーロードできない）。
プライマリコンストラクタと呼ばれる。
クラスメンバ変数はval（不変）かvar（可変）で宣言する。

.. code-block:: java

   class Syobochim() {
     val range = 1..10
   }

メソッドはこう書ける。

.. code-block:: java

   fun main(args: Array<String>) {
     val syobochim = Syobochim()
     syobochim.say() // 女子力!
   }

   class Syobochim() {
     fun say() {
       println("女子力!")
     }
   }

staticメソッドは

可視性は

高階関数
---------------------
Kotlinでは高階関数が使える。

.. code-block:: java  

   fun Syobochim.templeatePattern(f : (Int) -> Unit) {
     for(i in this.range) {
       f(i)
     }
   }
  
使用例。

.. code-block:: java  

   fun main(args : Array<String>) {
     val syobo = Syobochim()
     syobo.templeatePattern {
       println("財布ない！")
     }
   }

KotlinからJavaを使う
--------------------

importは

JavaからKotlinを使う
--------------------

jarにまとめて
  
各種情報源
----------

+ `公式サイト <http://kotlinlang.org/>`_
+ `GitHubレポジトリ <https://github.com/JetBrains/kotlin>`_

`@ngsw_taro <https://twitter.com/ngsw_taro>`_ さんが頑張ってるAdvent Calendarと資料。

+ `Kotlin Advent Calendar 2012 (全部俺) JavaプログラマのためのKotlin入門 <https://atnd.org/events/34627>`_
+ `Kotlin Advent Calendar 2013 <http://www.adventar.org/calendars/148>`_
+ `Kotlin Advent Calendar 2014 <http://www.adventar.org/calendars/477>`_

+ `JVM言語のかわいいルーキー Kotlinの紹介 <https://speakerdeck.com/ntaro/jvmyan-yu-falsekawaiiruki-kotlinfalseshao-jie>`_

+ `プログラミング言語Kotlin 解説 <https://sites.google.com/site/tarokotlin/home>`_



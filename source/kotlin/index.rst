Kotlin(\*´Д`)ﾊｧﾊｧ
=======================
Kotlinは、IntelliJ IDEAで有名なJetBrainsさんが作ってるプログラミング言語。

静的に型付けされた言語で、JVM上で実行することができる。
また、JavaScriptへの変換もできる。

何よりも名前がかわゆく、女子力が高まる感じが非常に良い言語である。

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



  

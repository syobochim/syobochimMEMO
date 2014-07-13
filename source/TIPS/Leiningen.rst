============================================
Leiningen
============================================

.. contents:: 目次
   :depth: 2


Jarファイルとして出力する
===============================

- エントリーポイントとなるcore.cljに「:gen-class」をnsの中につける。

.. code-block:: clojure

  (ns first-project.core
    (:gen-class))

|

- project.clj に「:aot」を追加する。

.. code-block:: clojure

  :main first-project.core
  :aot [first-project.core]

|

- コマンド

::

  lein uberjar


Leiningenのバージョンアップ
===============================

::

  lein upgrade


テストを行う
===============================

::

  lein test

::

  lein test <ネーム・スペース>  # 指定されたネーム・スペースのテストを行う


リポジトリの検索
===============================

::

  lein search


REPLを立ち上げる
===============================

::

  lein repl


使い方を表示する
===============================

::

  lein help


特定のタスクの使い方をみる
===============================

::

  lein help <タスク名>


複数のタスクを記述する
===============================

| doから始めることで複数のタスクをカンマ区切りで一度記述することができる
|

- 例）不要なファイルをcleanし、テストを行った後で、jarファイルを作る

::

  lein do clean, test foo.test-core, jar



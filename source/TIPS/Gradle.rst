==============================
Gradle
==============================

.. contents:: 目次
   :depth: 2

初期化
=====================

.. code-block :: sh

  $ gradle init --type java-library


java-libralyの他にも、下記オプションを選択できる。

- basic
- groovy-library
- pom
- scala-library

詳細な説明は、http://www.gradle.org/docs/current/userguide/build_init_plugin.html

|
|

ラッパー
=======================

| ラッパーを使用してGradleを内包して配布することで、使用者がGradleをインストールしていなくても
| すぐにPJを開始することが出来る。
| また、Gradleの使用バージョンを統一させることが出来る。


.. code-block:: groovy

   task wrapper(type: Wrapper) {
       gradleVersion = '2.0'
   }

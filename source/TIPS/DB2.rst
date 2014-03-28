============
DB2
============

.. contents:: 目次
   :depth: 2


コマンドプロンプトからDB2のコマンドラインを起動
============

::

  db2cmd


DB2のバージョンを調べる
============

| コマンドプロンプト上で

::

  db2level


DBへの接続
============

::

  db2start
  db2 connect to sampledb user ユーザ名 using パスワード


DBのパラメータ取得
============

::

  GET DB CFG [FOR データベース別名 ] [SHOW DETAIL]


DBパラメータ変更
============

::

  UPDATE DB CFG FOR [DB名] USING パラメータ名 [設定値]


使用例）

::

  UPDATE DB CFG FOR sampledb USING UTIL_HEAP_SZ 60000


表の一覧取得
============

::

  LIST TABLES [FOR 対象 ]


DBを作成
============

::

  create db sampledb
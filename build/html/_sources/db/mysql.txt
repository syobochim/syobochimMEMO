===========
MYSQL とか SQL とか MEMO
===========

.. contents:: 目次
   :depth: 2

テーブルの一覧を表示
=============

::

  show tables;


データをGroup化する
=============

::

  SELECT col_name, ... FROM tbl_name GROUP BY col_name, ...;

| 集計はグループ単位で行われます。
|

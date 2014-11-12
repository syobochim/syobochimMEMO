syobochimMEMO
=============

いろいろなメモをSphinxドキュメントで残すページ  
  
↓のURLでみれます。  
http://syobochim.github.io/syobochimMEMO/

Usage
-------------

このメモは[Sphinx](http://sphinx-doc.org/)を使用して作成しています。
Sphinxのインストールは[Sphinx-Users.jpのウェブサイト](http://sphinx-users.jp/gettingstarted/index.html#id1)を参照してください。

メモをビルドしてHTMLを生成するにはまず[Basicstrap](http://pythonhosted.org/sphinxjp.themes.basicstrap/)というテーマをインストールしてください。
例えばeasy_installだと次のコマンドでインストールできます。

```sh
easy_install sphinxjp.themes.basicstrap
```

テーマをインストールした状態で次のコマンドを実行すると `docs` にHTMLが出力されます。

```sh
make html
```

ブラウザで `docs/index.html` を開いてください。

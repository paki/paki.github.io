title: rssフィードをつけた
date: 2015-05-28 01:13:56
tags: [hexo]
---

## インストールと設定

[hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed) をインストール

``` bash
$ npm install hexo-generator-feed --save
```

_config.yml に以下を追記

``` yaml
feed:
    type: atom
    path: atom.xml
    limit: 20
```

<!-- more -->

## ついでにテーマもいれかえた

tumblr用の人気テーマ、 [Apollo](https://github.com/sanographix/tumblr/tree/master/apollo) を誰かが hexo のテーマに改変したもの。

``` bash
$ git clone https://github.com/joyceim/hexo-theme-apollo.git themes/apollo
```

## 参考
- [HexoのRSSフィードプラグインを使ってみる](http://qiita.com/f_prg/items/c5a465c79a9980b98495)
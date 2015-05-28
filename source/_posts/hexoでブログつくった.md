title: hexoでブログつくった
date: 2015-05-26 03:43:40
tags: [hexo]
---
## ジェネレータの選定

もともと jekyll でなんかやってみようかと思っていたけど、だいぶ時間があいてしまったのであらためてジェネレータを調査するところから。

静的サイトジェネレータ一覧サイト [Static Site Generators](https://staticsitegenerators.net/) でなんとなくあたりをつけてみる。

[HubPress](http://hubpress.io/) なんかも面白そうだったけど Github Pages に束縛されてしまう…。

結果、 以下の点が気に入ったので [hexo](http://hexo.io/) にすることにした。

- ローカルで確認しやすい
- markdown で投稿できる
- jekyll とか octpress とかよりは新しめ
- npm で管理できる
- テンプレートエンジンの ejs がなんとなくとっつきやすそうだった

※投稿するだけならテンプレートをいじる必要ないです

## 準備

LIGの [hexo紹介記事](http://liginc.co.jp/web/programming/server/104594) を見ながらインストール。
（ちゃんとまとめると執筆にけっこう時間がかかりそうなので、会社のPRも兼ねてとはいえ大変だろうな〜と思う…。ありがとうございます。）

ただ、今回インストールした hexo: 3.1.1 ではデプロイのところでこんなエラーが出る。

``` bash
$ hexo deploy -g
（省略）
ERROR Deployer not found: github
```

適当にググったところ [hexoのissue](https://github.com/hexojs/hexo/issues/1040#issuecomment-104904448)  に解決法があった。

_config.yml の deploy type のとこを編集
``` yaml
deploy:
  type: git # github ではなく git を指定
```

hexo-deployer-git を追加でインストール
``` bash
$ npm install hexo-deployer-git --save
```

これで `$ hexo deploy -g` できるようになる。

そのまま、この記事を書いてデプロイして完了。  
「3分」とはいかなかったけど、シンプルな手順なので wordpress の管理画面開くよりも早くて簡単!!

## 参考

- [所要時間3分!? Github PagesとHEXOで爆速ブログ構築してみよう！](http://liginc.co.jp/web/programming/server/104594)
- [Github Pagesでブログ構築ができる静的サイトジェネレーター総まとめ](http://qiita.com/okmttdhr/items/82ecb0332835472e905f)

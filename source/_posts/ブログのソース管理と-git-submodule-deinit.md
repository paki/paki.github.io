title: ブログのソース管理と git submodule deinit
date: 2015-05-29 01:41:52
tags: [hexo, git]
---

## ソースも git で管理したかった

`$ hexo deploy -g` するとページを生成しつつ公開用に push してくれるが、生成元の markdown ファイルや _config.yaml も git で管理したかった。

というより、ローカルに置いといても無くしちゃうので管理する必要があった。

で、[この記事][a] の最後の段落、「hexo をリポジトリ管理」がまさにやりたいことだったので参考にしてさっそくやってみたのだけれど…。

## init できない

まず、ブログのソースのあるディレクトリで `$ git init` がうまくいかない。

``` bash
$ git init
Reinitialized existing Git repository in {パスはいる}
```

init した覚えないのに…と思いつつ確認してみると、 .gitignore があったので中身を確認してみる。

``` bash
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

なるほど、これは hexo をインストールした時点で用意してくれていたようだ。

## git が入れ子状態

では、ということで add して commit したが、どうもうまくいかない…。

``` bash
$ git commit
On branch master
Changes not staged for commit:
  modified:   themes/apollo (modified content)

no changes added to commit
```

どうも、テーマファイルを追加した際に git clone したので、 git の管理が入れ子になっちゃってるみたいだった。

↓こんな感じ

``` bash
.
├── .git # 親
├── .gitignore
├── _config.yml
（略）
└── themes
    ├── apollo
    │   ├── .git # 子
    │   （略）
    │   └── _config.yaml # 子を clone 後に編集した
    └── landscape
```

とりあえず親ディレクトリから ./themes/apollo/_config.yaml を add してみるが失敗。

``` bash
$ git add ./themes/apollo/_config.yml
fatal: Pathspec './themes/apollo/_config.yml' is in submodule 'themes/apollo'
```

仕方ないので子ディレクトリ上で変更差分を commit する。
これは普通にできた。

## submodule のキャッシュをクリア

submodule の設定なんてした覚えがないけれど、たぶんそういうことになっちゃってるぽいので試しに親ディレクトリで `submodule update` してみるがこれもなんかおかしい。

``` bash
$ git submodule update
No submodule mapping found in .gitmodules for path 'themes/apollo'
```

検索しやすそうなエラーなのですぐに解決策がありそうな、 [それっぽい記事][b] が見つかった。
どうやら submodule のキャッシュを捨てれば良さそうだ。

``` bash
$ git rm --cached themes/apollo/
$ git add themes/apollo/
$ git submodule deinit themes/apollo/
$ git status
```

うまくいった!!

このあと、あらためて `$ git remote add` などをすませて無事に当初の目的を果たした。
（ブログ公開用リポジトリに、別ブランチでソースを push できた）
やれやれ。

[a]:https://harasou.jp/2015/04/28/hexo-setup/ "hexo セットアップメモ"
[b]:http://qiita.com/AtsushiShimo/items/b26c4d2033eb220bb8f9 "Composer install したらgit submodule化してしまった"
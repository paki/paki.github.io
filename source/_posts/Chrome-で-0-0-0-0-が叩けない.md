title: Chrome で 0.0.0.0 が叩けない
date: 2015-05-27 02:09:27
tags:
---
<ins>
## 2015-06-15 追記
いつのまにか直接入力しても検索扱いにならなくなっていた。  
（chrome 43.0.2357.81 にて確認）
</ins>

___

## 検索扱いになってしまう

`hexo server` すると URL が表示される。

``` bash
$ hexo server
INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.
```

この `http://0.0.0.0:4000/` は chrome のアドレスバー（Omnibox）にコピペしても開くことができない。
Omnibox は 0 で始まる文字列をURLとして取り扱わないで、検索キーワードとしてgoogle検索にかけてしまうようだ。

## 解決

デフォルトのブラウザが chrome なら、

``` bash
$ hexo server -o
```

とするか、
サーバ起動後に別タブで

``` bash
$ open http://0.0.0.0:4000/
```

とすれば検索扱いにならずにちゃんと開くことができる。

（とりあえず、`http://127.0.0.1:4000/` や `http://localhost:4000/` としてもいいけどなんとなく指定通りのアドレスで開きたかったので...）

___

この `0.0.0.0` は `127.0.0.1` や `localhost` と同じようなもんだと思ってたんだけど、どうも本来はそのように定義されていないのに習慣的に同じにされちゃってるだけのことみたいらしい。  
なので、むしろ本来は「0.0.0.0を明示的なURLとして扱うほうがバグっぽい」ことになるらしい…。

## 参考

- [Issue 428046:  Omnibox refuses to allow navigation to 0.0.0.0](https://code.google.com/p/chromium/issues/detail?id=428046)
- [Issue 466329: Can't visit 0.0.0.0:4200 URLs with a path (i.e., 0.0.0.0:4200/some_path/file.ext)](https://code.google.com/p/chromium/issues/detail?id=466329)

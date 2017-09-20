title: hexo で日本語パーマリンク
date: 2015-06-16 01:41:08
tags: [hexo]
---
# 404になってしまう
サイト内でリンクを踏むと、日本語を含むアドレスがなぜか404になってしまっていた。  
以前確認した時は問題なかった気がするのだけど…。

<!-- more -->

# 改修
既知の問題らしく、検索したらすぐ答えが出た。  
[ここ](http://atani.github.io/2015/06/hexo%E3%81%A7%E6%97%A5%E6%9C%AC%E8%AA%9E%E3%81%AE%E3%83%91%E3%83%BC%E3%83%9E%E3%83%AA%E3%83%B3%E3%82%AF%E3%82%92%E8%A6%8B%E3%82%8C%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%97%E3%82%88%E3%81%86%EF%BC%81/) に書いてあるとおり対応して確認、問題なく遷移できた!  

## 参考

- [hexoで日本語のパーマリンクを見れるようにしよう！](http://atani.github.io/2015/06/hexo%E3%81%A7%E6%97%A5%E6%9C%AC%E8%AA%9E%E3%81%AE%E3%83%91%E3%83%BC%E3%83%9E%E3%83%AA%E3%83%B3%E3%82%AF%E3%82%92%E8%A6%8B%E3%82%8C%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%97%E3%82%88%E3%81%86%EF%BC%81/)
- [hexo で 404 File not found](https://harasou.jp/2015/05/10/hexo-404-file-not-found/)

<ins>
## 2017-09-21 追記

この問題を解決するプラグイン、 [hexo-filter-permalink-normalization](https://www.npmjs.com/package/hexo-filter-permalink-normalization) が出来ていた。  

### 参考

[hexo の 404 File not found さようなら](https://harasou.jp/2015/06/28/hexo-goodby-404/)
</ins>
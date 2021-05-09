---
layout: post
title:  "ブログを WordPress から GitHub Pages に移行した"
date:   2021-05-09 12:01:20 +0900
categories: Tech
---

ブログを WordPress から GitHub Pages に移行した。

ブログの引越しを何度かやって、ここ数年は AWS の Amazon Lightsail で動かしていた WordPress で運用していたけど、メンテナンスも面倒になってきたので移行を検討し、 GitHub Pages でやってみることにした。

GitHub Pages を選んだのは、技術系のものは GitHub にまとめてみようかなと思った程度で、あんまり意味はない。

GitHub Pages では Jekyll という静的コンテンツを生成するツールが、GitHub Pages の公式ドキュメントでもおすすめされていたので、それを使ってみることにした。

## 初期設定メモ

### GitHub Pages の設定

以下の公式ドキュメントの通りに GitHub Pages 用のリポジトリを作成する。

* [GitHub Pages サイトを作成する - GitHub Docs](https://docs.github.com/ja/pages/getting-started-with-github-pages/creating-a-github-pages-site)

GitHub Pages のリポジトリを Clone して、移動する。

```shell
% git clone ${user}.github.io

% cd ${user}.github.io
```

### Jekyll インストールと起動

Ruby をインストールする。特にバージョンにこだわりはないので、 `ruby-build` とかは入れない。
Docker 使っても良いかもしれない。

```shell
% brew install ruby
```

bundler をインストールする。

```
% gem install bundler
```

`${user}.github.io` ディレクトリ内に `Gemfile` を作成して、以下を記載する。

```
source "https://rubygems.org"
gem 'github-pages', group: :jekyll_plugins
```

gem パッケージをインストールする。

```shell
% bundle install --path vender/bundle
```

起動してみる。

```shell
% bundle exec jekyll serve
```

これで、127.0.0.1:4000 でブラウザから http で参照できる。


### GitHub Pagesのプラグインや Jekyll テーマの設定

GitHub Pages のプラグインや Jekyll テーマの設定を行う。テーマは GitHub Pages 用に用意されているものを使うこともできるが、`jekyll new` で初期化するとデフォルトのテーマである minima が適用されるので、ここでは以下の公式手順を参考に実行する。

* [BundlerでJekyllを使う \| Jekyll • シンプルで、ブログのような、静的サイト](http://jekyllrb-ja.github.io/tutorials/using-jekyll-with-bundler/#jekyll%E9%AA%A8%E6%A0%BC%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B)

`${user}.github.io` ディレクトリ直下で以下を実行する。すでにファイルなどがあると失敗するので `--force` オプションを付与し、bundle は別で実行させるため `--skip-bundle` オプションを付与する。

```
 % bundle exec jekyll new --force --skip-bundle .
 ```

これをやるとファイルが色々生成され、Gemfile も書き換わる。`bundle install` を実行する。

```shell
% bundle install --path vender/bundle
```


### 細かい設定

`_config.yml` や `_layouts/`, `_includes`, `_sass/ 配下などのファイルを好みに合わせて調整する。詳細の記載は省く。


## まとめ

ブログを GitHub Pages へ移行することにしたので、その際にやったことなどを簡単に書いた。


## 参考

* [GitHub Pages を使ってみる - GitHub Docs](https://docs.github.com/ja/pages/getting-started-with-github-pages)
* [GitHub PagesとJekyllについて - GitHub Docs](https://docs.github.com/ja/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)
* [BundlerでJekyllを使う \| Jekyll • シンプルで、ブログのような、静的サイト](http://jekyllrb-ja.github.io/tutorials/using-jekyll-with-bundler/)
* [jekyll/minima: Minima is a one-size-fits-all Jekyll theme for writers.](https://github.com/jekyll/minima)
* [GitHub Pagesでブログを運用し始めてから4年くらいたった \| Masamichi Ueta](https://masamichi.me/development/2019/12/14/github-pages-blog.html)
* [GitHub Pagesで無料ブログを作成する - Part3 Jekyllの設定をカスタマイズする \| Masamichi Ueta](https://masamichi.me/development/2020/05/28/github-pages-blog-part3-cutomize-setting.html)
* [Welcome to my Top Page \| netchira.github.io](https://netchira.github.io)
* [GithubPagesでjekyllを使ってみよう。 - Qiita](https://qiita.com/OriverK/items/ce48102c66c9fa97b33e)
* [GitHub PagesにJekyllを使っていい感じのページを作る例 - Qiita](https://qiita.com/stkdev/items/0e2df27736acbea9bd26)

---
layout: post
title: MaterialDesignカラーを適用したJekyllテーマ「Materi」
tags: [jekyll]
image:  'https://raw.githubusercontent.com/ogaclejapan/materi-for-jekyll/master/art/materi_device_art.png'
---

昨年末、久々にブログを書いてみたら自ら作った[Bootstrap臭のテーマ][jekyllstrap]に飽きてしまったので、
巷で流行りのマテリアルデザイン風なカラーリングで[Jekyll][jekyll]のテーマを作ってみました。

[![art][materi-art]]("https://github.com/ogaclejapan/materi-for-jekyll")


## Materi for Jekyll

以前にBootstrapベースのJekyllテーマを作ったときは一からすべて作りましたが、
今回は[m3xm][hikari-author]さんがGitHubで公開している「[Hikari][hikari]」というテーマが個人的にシンプルで良さげだったので、
これをforkしてMaterialDesignっぽいスタイルやいくつか機能を追加したり、カスタマイズしてみました。

<https://github.com/ogaclejapan/materi-for-jekyll>


### 主な特徴

* マテリアルデザインっぽい背景色やテキスト色を採用
* 本文にGoogle Noto Font、それ以外の部分にUbuntu系Fontを採用
* タグ一覧、タグ毎の記事一覧ページを生成(後述する補足を参照のこと)
* sitemap.xml, robots.txt, 404ページを生成
* OGP, Twitter Cardsのmetaタグ対応(記事ページのみ)
* テーマにあったfaviconをデフォルトで用意


使い方は他のJekyllテーマと同様リポジトリをcloneして使うと非常に簡単です。
使ってみたいと思ったら、ぜひGitHubスターをポチってくださいな☆（ゝω・）vｷｬﾋﾟ


#### 補足: ローカルに試すには？

[Bundler][bundler]で必要なgemファイルはすべてインストールできます。
RubyとRubyGemsが入っていればBundlerをインストールして実行するだけで簡単に起動できます。

```bash
git clone https://github.com/ogaclejapan/materi-for-jekyll.git
cd materi-for-jekyll

gem install bundler

bundle install
bundle exec jekyll serve -w
# Server running http://localhost:4000/materi-for-jekyll/

```


#### 補足: タグページを生成するには？

GitHub Pages上ではJekyllのプラグインが動かない仕様のため、
プラグインを使わずに生成できる方法を採用しています。
そのため、生成するためのテンプレートファイルを手動で用意する必要があります。


Jekyllにはタグをつけるための機能が標準で実装されています。
`tags`という属性にタグを一意に表すキー文字列を定義してください。

```yaml
---
layout: post
title: MaterialDesignカラーを適用したJekyllテーマ「Materi」
tags: [jekyll]
---
```

次に、`data/tags.yml`に先ほど定義したキー文字列と表示するタグ名を定義します。
記事ページ内のタグリンクを有効にするかどうかをこの定義で制御してます。

```yaml
# To generate the tag page will need to be defined here

jekyll:
  name: Jekyll
```

最後に、タグ付けされた記事一覧を生成するためのテンプレートファイルを作ります。
テンプレートは`tags/*`配下に作成してください。

* e.g. `tags/jekyll.md`

```yaml
---
layout: tag
title: 'Tags: Jekyll'
tag: jekyll
permalink: tags/jekyll/
---
```

attribute | value
:----|:----
layout | 必ず'tag'固定にしてください
title | htmlのtitleタグに表示する文字列
tag | 記事に定義したタグのキー文字列
permalink | 'tags/(タグのキー文字列)/'

タグキー文字列の冗長な記述が多いのでほんとは自動生成できれば一番いいんですが、
Jekyllではプラグインを使わないとファイルを生成できないので残念なところです。

自前でRakeファイルにこの辺を処理するタスクを定義しておくと、多少手間が省けるかもですね。


#### 補足: WebFontを変更するには？

デフォルトでは英語圏でも使えるようなWebFontを採用しています。

* 本文: [Noto Serif][webfont-noto-serif]
* 本文のコード部分: [Ubuntu Mono][webfont-ubuntu-mono]
* それ以外: [Ubuntu][webfont-ubuntu]


このブログは日本語向けなので[Google Noto Japanese][webfont-noto-japanese]に一部変更しています。
日本語のWebFontはサイズが大きいのでパフォーマンス面ではよくないですが、読みやすさ重視で採用しました。


フォントを変更するには以下の２ファイルを編集してください。

`_includes/link_your_font.html`  
`_sass/base/_your_font_family.scss`


[jekyll]: http://jekyllrb.com/
[jekyllstrap]: https://github.com/ogaclejapan/jekyllstrap
[hikari]: https://github.com/m3xm/hikari-for-Jekyll
[hikari-author]: https://github.com/m3xm
[bundler]: http://bundler.io/
[webfont-noto-serif]: https://www.google.com/fonts/specimen/Noto+Serif
[webfont-noto-japanese]: http://www.google.com/fonts/earlyaccess
[webfont-ubuntu]: https://www.google.com/fonts/specimen/Ubuntu
[webfont-ubuntu-mono]: https://www.google.com/fonts/specimen/Ubuntu+Mono

[materi-art]: https://raw.githubusercontent.com/ogaclejapan/materi-for-jekyll/master/art/materi_device_art.png


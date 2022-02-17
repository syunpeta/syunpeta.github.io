---
layout: post
title: Github pagesをjekyllで作る際のエラー
gh-repo: daattali/beautiful-jekyll
tags: [Ruby,プログラミング]
thumbnail-img: /assets/img/ruby.png
comments: true
---
jekyllとGithub pagesを用いてサイトを立ち上げる際に躓いた点を紹介します。

## jekyllでGithub pagesを作る方法
jekyll(ジキル)はRuby製の静的サイトジェネレーターです。  
手軽にサイトが作れるのが利点でGithub pages(Githubのポスティングサービス)などと組み合わせてよく使用されます。  
また、jekyllで作成するサイトはマークダウン方式で書くことができ、慣れている人は通常の方法で作成するより記述が楽というのも利点です。  
このサイトもjekyllのbeautiful-jekyllというテーマを用いて作成されています。  
  


jekyllとGithub pagesを用いてウェブサイトを作成する方法は以下のサイトで詳しく説明されています。↓↓↓  
[ゼロからわかる！GitHub Pagesを使った自前無料ブログの作り方（Jekyll）](https://qiita.com/madoreenu/items/b47833bf785562c77819)

## Rubyインストール時の注意点
上のサイトを参考にして進めればほとんど困ることはないのですが、一つドツボにはまったことがあります。 
それはRubyのバージョンです。
  

まず[Rubyインストーラ](https://rubyinstaller.org/downloads/)に飛んで現在のRubyのバージョンを確認してみてください。  
現在(2022-02-07)のRuby+Devkitのバージョンは3.1.0-1(x64)が最新で、⇒のついているバージョンは3.0.3-1(x64)になります。  
jekyllの対応バージョンは2.5.0以上と[公式サイト](http://jekyllrb-ja.github.io/docs/installation/)に記載されていますので、⇒のついているバージョンを選びがちですがこれをインストールするとローカルでbundle exec jekyll serveをする際にエラーを吐きます(明確にこれが原因かはわかりませんが)。  
  
自分の環境ではRubyのバージョンを2.6.9(x64)に落としたところうまく動作するようになりました。  
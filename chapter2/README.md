# NAME

chapter2 - 手軽にクローラを作りながら楽しむ

```
Unix のコマンドアプリ Wget をつかって手を動かしながらスクレイピングの世界を楽しんでみます
この資料では環境構築はMacのみの紹介とします
```

# SECTION1

___Wget コマンドを使えるようにする___

- 前提条件
    - Unix系のコマンドライン操作の知識
    - Macのターミナルの使い方の知識
    - homebrew についての知識
    - homebrew インストール済み

下記ターミナルで実行

```
(基本的には最新の状態がのぞましい)
$ brew update && brew upgrade

(mac には wget はインストールされていないでのインストール)
$ brew install wget

(使い方の詳細はドキュメントを頑張って読む)
$ man wget

(PyconKyushu サイトの画像をダウンロードしてみる)
$ wget https://kyushu.pycon.jp/2020/images/main_image.png
```

# SECTION2

___Wget コマンドを使いながら覚える___

ネット上の画像ファイルをダウンロードする

```
(作業用にtutorialというディレクトリを用意することにする)
$ mkdir ~/tutorial
$ cd ~/tutorial

(PyconKyushu サイトの画像をダウンロードしてみる)
$ wget https://kyushu.pycon.jp/2020/images/main_image.png

(ホームディレクトリ配下のmain_image.pngがダウンロードされた)
$ ls -l
...
-rw-r--r--   1 yk  staff  128992  1 13 12:17 main_image.png
...
```

_ちなみにPyConKyushu 2020 は熊本で5/23に開催予定です!_

ネット上のhtml形式のシンプルテキストを1ページ分ダウンロードする

```
(PyconKyushu サイトをダウンロードしてみる)
$ wget https://kyushu.pycon.jp/2020/

(こちらがダウンロードされた)
$ ls -l
...
-rw-r--r--@ 1 yk  staff   17538  1 13 12:17 index.html
...

(PyconKyushu サイトを再起的にダウンロードしてみる)
$ wget -r https://kyushu.pycon.jp/2020/

(ディレクトリの中に参照されているファイルも一式ダウンロード)
$ ls -l
...
drwxr-xr-x  4 yk  staff     128  1 17 16:56 kyushu.pycon.jp
...
```

ダウンロードしたものをwebブラウザで確認してみる

```
(このファイルには参照しているcssがないのでまともに表示できない)
$ open index.html

(こちらファイルには参照しているcssなどが存在するので表示できる)
$ open kyushu.pycon.jp/2020/index.html
```

# SECTION3

___欲しい情報を抽出する___

今回はダウンロードしたページに含まれている外部リンクのみを抽出

今回活用するコマンドは`cat`と`grep`

```
(ダウンロードしたファイルは沢山のhtmlタグが存在する)
$ cat kyushu.pycon.jp/2020/index.html

(リンクは <a href="...">...</a> で囲まれている)
$ cat kyushu.pycon.jp/2020/index.html | grep '<a href='

(外部リンクは http で始まっている)
$ cat kyushu.pycon.jp/2020/index.html | grep '<a href="http'
```

# SEE ALSO

-
-
-

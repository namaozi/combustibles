# Docker超入門チュートリアル

先日チームでrailsプロジェクトを始めるという経験がありまして、その際に開発環境・本版環境をDockerを使いましたので、アウトプットとしてメモを残しておきます。

# 前置き
私はサーバーやネットワーク、OSの知識が非常に乏しく、ものすごくふんわりとした理解しか得られていません。今回はふんわりとした状態で記事を書こうと思います。
また、

コードはGitHubに公開しておりますのでよろしければご参照ください。

# Dockerってなんなの？
VM（みたいなもの）のすごいやつです。
環境を構築してパッケージ化してアップロードして配布などができ、
全体的にVagrantと似ていると思います。

# 準備
今回Macを対象に書きますが、Windowsでも最新のDocker for Windowsをダウンロードすれば同様に出来るはずです。

## Docker for Macをインストール
公式サイトからDocker for Macをインストールしましょう。

メニューバーにくじらのアイコンが表れ、「」と表示されればOKです。


## まず知るべきこと

## 使い方の流れ
使用方法の概要から掴んでみましょう。
「Dockerfile」 -> 「Docker イメージ」 -> 「Docker コンテナ」

それではまず例としてrubyをインストールしただけのdockerコンテナを作ってみましょう。

### 1.Dockerfileを作る
まずは最もシンプルな使い方をしてみましょう。
適当なディレクトリに「Dockerfile」というファイルを作り、以下のように書いてください。

``` Dockerfile
BASE ruby:2.4.1
```

`BASE イメージ名:バージョン` で、作成するイメージのベースを指定できます。ベースイメージは[Docker公式サイト]()に多数公開されており、これらを指定することで、いろいろなソフトウェアをインストールされた環境をそのまま利用できます。

### 2.Dockerイメージを作る
これをもとに「Dockerイメージ」を作ってみましょう。
以下のコマンドを実行してください。

`$ docker build --name test-image`

するとDockerfileをもとにDockerイメージが作られます。buildコマンドを使っているので「ビルドする」ともいいます。

作ったイメージを確認してみましょう。以下のコマンドを実行してください。

`$ docker images`

するとこんな風に表示されます。imageは指定しないとランダムで名前が付けられるようです。

### 3.Dockerコンテナを作る
では先程作ったDockerイメージをコンテナにしてみましょう。

`$ docker run test-image test-container`

このように表示され、コンテナの作成に成功しました。では作ったコンテナを確認してみましょう。

`$ docker ps`

するとこのように表示され、コンテナが正常に作られたことが分かると思います。

### 4.作ったコンテナ上でコマンドを動かす
それではコンテナにrubyがインストールされているのか確認してみましょう。

`$ docker exec test-container ruby -e 'puts "hello!"'`

これで"hello"と表示されたでしょうか？

ちなみにコンテナにアクセスして自由にコマンドを打つには、以下のようにオプションをつけてbashなどのシェルを指定すればOKです。

`$ docker exec -it test-container bash`

# まとめ

これでDockerfileからDockerイメージを作り、DockerイメージからDockerコンテナを作る流れが体験できたと思います。

次はRailsが動くコンテナを作ってみたいと思います。


## DockerとVagrantとの違い
後日Vagrantを触った時に感じたDockerとVagrantの違いを書いていきます。

### 自動的にマウントされない
Vagrantでは、Vagrantファイル

##



# 特徴
イメージの差分がレイヤで管理されていることだと思います。
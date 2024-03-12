---
title: 'Docker Compose V2 をとりあえず入れてみた'
emoji: '🐳'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['windows', 'wsl2', 'docker']
published: true
published_at: 2022-08-20 14:50
---

## 前提

-   `docker run --d hello-world` が動く

## 僕の認知は遅かった。

`docker-compose` コマンドを僕は知らない状態で `docker` に触れました。  
少し調べてみると `V1` と `V2` なるものがあり、 二〇二三年には `V1` なくしていきた方向らしいですね。  
そら、`docker-compose`と打つのと`docker compose`とでは打ちやすさに雲泥の差がありますよね。（本当にそこなのか？）  
`doc` `tab` `com` `tab` で入力したいものです。（ほんとうに？？？）

詳しいことはよくわかっていないけれど、とりあえず最新の方がいいっしょ。（一応ちゃんと調べます）  
時代は変わるものだ精神で入れていきます。（それでよいのか？）

## `Docker Compose V2` インストール

1. まずはプラグインを入れる場所の確保

    ```bash
    sudo mkdir -p /usr/local/lib/docker/cli-plugins
    ```

1. 次にプラグインをダウンロード

    ```bash
    sudo curl -SL https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose
    ```

1. そしてダウンロードしたプラグインを使えるようにするために実行権限を付与

    ```bash
    sudo chmod a+x /usr/local/lib/docker/cli-plugins/docker-compose
    ```

たったこれだけだというのか ...!!

## エイリアス作成

### 前提

-   `wsl2` を `vscode` で開ける（別に `vim` 等でも可。お好きなエディターで修正して保存できれば）
-   `.bash_aliases` が読み込まれる設定を `.bashrc` で行われている（`wsl2` `Ubuntu` は初期でそうなっていました）

とりあえずコマンドラインで `tab` しても出てこないことに気づいたので、エイリアスだけ作っておこうと思いました。

1. ホームディレクトリへ移動

    ```bash
    cd
    ```

1. `vscode` でファイル修正

    ```bash
    code .bash_aliases
    ```

    下記のように書いて保存

    ```.bash_aliases
    # Docker の独自エイリアス
    alias d='docker'
    alias dc='docker compose'
    alias dcps='docker compose ps'
    alias dcud='docker compose up -d'
    alias dcudb='docker compose up -d --build'
    alias dce='docker compose exec'
    alias dcl='docker compose logs'
    alias dcd='docker compose down'
    alias dcbnc='docker compose build --no-cache'
    ```

    `ctrl` + `s` で保存

1. 確認する  
   シェルからログアウト後、再度ログインして、上記コマンド一覧を行ってみる。  
   確認できれば完了

    ```bash
    d
    ```

`d` だけで `docker` が動くのは快適すぎて、もう無理だ。  
コマンド忘れそう。  
ありがとうございました。

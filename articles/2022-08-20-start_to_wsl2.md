---
title: 'windows で開発するのはこれっきり辞めようと試みてみた。'
emoji: '🐋'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['windows', 'wsl2', 'docker']
published: true
published_at: 2022-08-20 14:17
---

## 1. `Windows PowerShell` から `wsl2` をインストール

```powershell
wsl --install
```

僕は `docker` と `wsl2` がすでに入っていたので、下記の手順を踏んでからやりました。

1. `docker for windows` をアンインストール
1. `wsl` を無効化  
   ![2022-08-20-start_to_wsl2-windows_menu](/images/2022-08-20-start_to_wsl2/windows_menu.png)  
   ![2022-08-20-start_to_wsl2-windows_menu](/images/2022-08-20-start_to_wsl2/windows_function_menu.png)
1. 再起動

---

## 2. `wsl2` 内で `docker` をインストール

`wsl` のインストールが終わり再起動をすると自動でターミナルが動いてくれました。  
ユーザー名とパスワードを新規作成できるよう、任意の値を設定します。

`docker` の公式のコマンド通りやるだけです！  
参考: <https://docs.docker.com/engine/install/ubuntu/>

### リポジトリ追加

1. アップデート

    ```bash
    sudo apt update -y && sudo apt upgrade -y
    ```

1. 必要なものをインストール

    ```bash
    sudo apt-get install \
        ca-certificates \
        curl \
        gnupg \
        lsb-release
    ```

1. 公式の `GPG` キーを取得しておく場所を確保

    ```bash
    sudo mkdir -p /etc/apt/keyrings
    ```

1. ダウンロードして配置

    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    ```

    **※ディストリビューションは `Ubuntu` 前提です。**

1. リポジトリをセットアップすると。

    ```bash
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    ```

### install docker engine

1. どっかーえんじんをいんすとおおる

    ```bash
    sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    sudo apt update
    ```

1. 起動確認

    ```bash
    sudo docker container run --rm hello-world
    ```

    この時エラーになったのでとりあえず `wsl` を再起動したら治りました。

### sudo なんてつけていられない場合

```bash
sudo groupadd docker
```

なんか、すでに存在するとか言われました。。。過去にやったやつ何か影響している・・・？

```bash
sudo usermod -aG docker $USER
```

とりあえずこれで `Docker Engine` が入ったと！よしよし。  
次回は `docker compose V2` を入れていきます。  
ありがとうございました！

## 参考

-   <https://docs.docker.com/engine/install/ubuntu/>
-   <https://footloose-engineer.com/wsl2-ubuntu-docker-compose-setup/#toc3>
-   <https://zenn.dev/fehde/articles/ea0e8a0a0a1de4>
-   <https://chusotsu-program.com/1%E8%A1%8C%E3%81%AE%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%A7mkdir%E3%81%A8cd%E3%82%92%E5%90%8C%E6%99%82%E3%81%AB%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95/>
-   <https://qiita.com/wakki_haya/items/a00ecdc231e131b4d18d>

誠に勝手ながら、参考に致しました。  
皆さんこんな僕でも分かりやすい記事をありがとうございます！！

## 後書き

元々 `docker` に興味はあったのだけれど、なかなか手を出せていなかったところ仕事で使う時がついにやってきてしまった。  
そのためにはまず慣れておきたいと思ってちょっとずつ手を出し始めてきたころのこと・・・

さっき気づいた。あれ？ `Windows Terminal` に `WSL` なくね・・・？  
すなわち、 `wt` に `Ubuntu` の項目ないやん！  
**※出ていなかった時点の画像のスクショはありません。**

設定を追記すれば何とかなりそうなものの、新しく入れなおした方が速そうだと思った。  
それならいっそのこと作業ログを残しつつ心機一転しようと思った。  
やっぱり `windows` の中はゲームだけでいっか（？）という淡い気持ちもあったりなかったり。

### 余談

記事を書いたことで、スクリーンショットのショートカットに `win` + `alt` + `Print Screen` があることを最近知りました。  
僕の環境はトリプルモニターなので `win` + `shift` + `s` の後、ウインドウ選択していました。  
まぁ、あんまりスクショする機会もないかもしれませんが笑  
仕事では重宝しそうなので覚えておきます。てか、 `win` + `Print Screen` ってデュアルモニター以上の時に使用することあるんですか？？

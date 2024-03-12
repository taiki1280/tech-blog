---
title: 'ふと二年ぶりに Discord を覗いてみたら・・・'
emoji: '🎮'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['discord', 'python']
published: true
published_at: 2022-12-02 03:57
---

## あれ？なんか実行できなくなってるぞ

専門学生時代に作った `discord bot` を掘り起こしてみた。  
まずは、酷すぎる過去の自分のソースコードとコミットログに落胆した。  
とりあえず `docker` 化して実行を試みたところ・・・・動かないではないか。  
僕が過去に一生懸命書いたコードが。。。でも、割と頑張ってんな。過去の僕。  
諸々、以下の点とかとくに突っ込みどころ多いけれど、成長を感じる。

1. ディレクトリ構造がやべえ点
1. `db` を知らなかったがゆえにすべてを `excel` でローカル管理している点

ありがとう今の僕。と感傷に浸りとりあえず三時間ほど詳細を調べた。

### 調べてみて分かったこと

1. `discord.py` のアプデで従来の書き方ができなくなっていたこと
1. `python` バージョン `3.7` 以前はサポート終了していたこと
1. `discord.py` が開発終了したこと
1. 開発再開していたこと

**I can only say Oh my god.**  
オーマイゴッドとしか言えん！！  
とりあえず `Hello World` までした。（それだけで時間かかった・・・）

## 仕様が変わってた内容メモ

```python
# 従来の書き方は使えなくなったらしい。そりゃ2年もたてば変わるか。
# client = discord.Client()

# 面倒だったら全許可でも良い
# intents = discord.Intents.all()

intents = discord.Intents.default()
# メッセージの取得許可
intents.message_content = True
client = discord.Client(intents=intents)
```

`bot` とダイレクトメッセージの時は無くても大丈夫だったが、  
何かしらのサーバーに `bot` を招待したいとなると「`default()` → `all()` にする」または「下記の追記」が必要だった。

```python
intents.message_content = True
```

また `discord` `bot` 設定もいくつか必要になってた。色々あったんやね。。

参考（`API` リファレンス）: <https://discordpy.readthedocs.io/ja/latest/api.html#discord.Intents.all>

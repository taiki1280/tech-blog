---
title: 'hyper-v linux ボリューム変更'
emoji: '👌'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: []
published: true
published_at: 2024-03-20 21:49
---

```zsh
# 空き容量確認
df -h
# パス確認
sudo lvdisplay
# LV Path → /dev/ubuntu-vg/ubuntu-lv
# 空いているボリュームを全て埋める
sudo lvextend -l+100%FREE /dev/ubuntu-vg/ubuntu-lv
# 変更後
sudo lvdisplay
```

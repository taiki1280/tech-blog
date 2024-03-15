---
title: "markdown-pdf 修正"
emoji: "📚"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ['vscode']
published: false
---

1. ユーザー直下の `\.vscode\extensions\yzane.markdown-pdf-1.5.0\extension.js` を修正
    `options` 変数内に以下を追加

   ```js
   ignoreDefaultArgs: ['--disable-extensions'],
   ```

![image.png](/images/2024-03-15-fix_markdown_pdf/image.png)

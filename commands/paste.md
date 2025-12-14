---
description: クリップボードの内容を貼り付け
argument-hint: [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_paste
---

クリップボードの内容を貼り付けます（Ctrl+V）。

**引数**
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `browser` を解析
2. `mcp__native-browser-control__chrome_paste` を呼び出す
   - `browser`: 解析した値（省略時は "chrome"）
3. 貼り付け完了を確認

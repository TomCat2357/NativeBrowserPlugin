---
description: HTMLソースを取得
argument-hint: [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_get_page_source
---

現在のページのHTMLソースを取得します。

**引数**
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `browser` を解析
2. `mcp__native-browser-control__chrome_get_page_source` を呼び出す
   - `browser`: 解析した値（省略時は "chrome"）
3. 取得したHTMLソースを表示

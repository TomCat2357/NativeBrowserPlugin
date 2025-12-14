---
description: 選択中のテキストをコピー
argument-hint: [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_copy_selected
---

選択中のテキストをコピーして取得します（Ctrl+C）。

**引数**
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `browser` を解析
2. `mcp__native-browser-control__chrome_copy_selected` を呼び出す
   - `browser`: 解析した値（省略時は "chrome"）
3. コピーしたテキストを表示

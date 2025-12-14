---
description: ページ内検索
argument-hint: <text> [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_find_text
---

ページ内検索を開いてテキストを検索します（Ctrl+F）。

**引数**
- `text`: 検索するテキスト（必須）
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `text`, `browser` を解析
2. `text` が無ければ usage を出して終了
3. `mcp__native-browser-control__chrome_find_text` を呼び出す
   - `text`: 解析したテキスト
   - `browser`: 解析した値（省略時は "chrome"）
4. 検索実行を確認

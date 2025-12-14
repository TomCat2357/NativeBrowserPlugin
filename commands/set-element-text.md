---
description: 要素のテキストを設定
argument-hint: <index> <text> [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_set_element_text
---

スキャンした要素のテキストを設定します（先にchrome_scan_elementsを実行してください）。

**引数**
- `index`: テキストを設定する要素のインデックス（必須）
- `text`: 設定するテキスト（必須）
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `index`, `text`, `browser` を解析
2. `index`, `text` が無ければ usage を出して終了
3. `mcp__native-browser-control__chrome_set_element_text` を呼び出す
   - `index`: 整数値
   - `text`: 解析したテキスト
   - `browser`: 解析した値（省略時は "chrome"）
4. テキスト設定完了を確認
5. 注意: 設定前に `/browser:scan-elements` でEdit要素のインデックスを確認すること

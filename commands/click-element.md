---
description: 要素をインデックスでクリック
argument-hint: <index> [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_click_element
---

スキャンした要素をインデックスでクリックします（先にchrome_scan_elementsを実行してください）。

**引数**
- `index`: クリックする要素のインデックス（必須）
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `index`, `browser` を解析
2. `index` が無ければ usage を出して終了
3. `mcp__native-browser-control__chrome_click_element` を呼び出す
   - `index`: 整数値
   - `browser`: 解析した値（省略時は "chrome"）
4. クリック完了を確認
5. 必要に応じて `/browser:wait` でページ更新を待機
6. 注意: クリック前に `/browser:scan-elements` でインデックスを確認すること

---
description: スキャンした要素をタイプ別に集計
argument-hint: [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_elements_summary
---

直近にスキャンした要素をタイプ別に集計して表示します（先にchrome_scan_elementsを実行してください）。

**引数**
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `browser` を解析
2. `mcp__native-browser-control__chrome_elements_summary` を呼び出す
   - `browser`: 解析した値（省略時は "chrome"）
3. コントロールタイプ別の集計結果を表示
4. 注意: 先に `/browser:scan-elements` を実行してください。スキャン前に実行するとエラーになります。

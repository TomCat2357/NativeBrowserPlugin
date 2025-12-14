---
description: 指定URLに移動
argument-hint: <url> [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_navigate
---

指定したURLに移動します。

**引数**
- `url`: 移動先のURL（必須）
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `url`, `browser` を解析
2. `url` が無ければ usage を出して終了
3. `mcp__native-browser-control__chrome_navigate` を呼び出す
   - `url`: 解析したURL
   - `browser`: 解析した値（省略時は "chrome"）
4. ナビゲーション完了を確認
5. ページロード待機として `/browser:wait 2` を推奨

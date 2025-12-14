---
description: ページをスクロール
argument-hint: <direction> [browser=chrome|edge] [amount=500]
allowed-tools: mcp__native-browser-control__chrome_scroll
---

ページをスクロールします。

**引数**
- `direction`: スクロール方向（down, up, top, bottom, page_down, page_up、必須）
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）
- `amount`: スクロール量（down/upの場合のみ、省略時: 500）

**手順**
1. 引数から `direction`, `browser`, `amount` を解析
2. `direction` が無ければ usage を出して終了
3. `mcp__native-browser-control__chrome_scroll` を呼び出す
   - `direction`: 解析した方向
   - `browser`: 解析した値（省略時は "chrome"）
   - `amount`: 整数値（省略時は 500、directionがdownまたはupの場合のみ）
4. スクロール完了を確認

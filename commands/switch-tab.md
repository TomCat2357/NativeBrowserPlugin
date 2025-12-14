---
description: タブを切り替え
argument-hint: <direction> [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_switch_tab
---

タブを切り替えます。

**引数**
- `direction`: 切り替え方向（next または previous、必須）
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `direction`, `browser` を解析
2. `direction` が無ければ usage を出して終了
3. `mcp__native-browser-control__chrome_switch_tab` を呼び出す
   - `direction`: 解析した方向
   - `browser`: 解析した値（省略時は "chrome"）
4. タブ切り替えを確認

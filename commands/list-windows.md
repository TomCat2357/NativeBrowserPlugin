---
description: 起動中のブラウザウィンドウ一覧を取得
argument-hint: [browser=chrome|edge] [require_visible=true|false] [exclude_minimized=true|false]
allowed-tools: mcp__native-browser-control__chrome_list_browser_windows
---

起動中のブラウザウィンドウ一覧を取得します。

**引数**
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）
- `require_visible`: 可視ウィンドウのみ対象（true/false、省略時: false）
- `exclude_minimized`: 最小化されたウィンドウを除外（true/false、省略時: false）

**手順**
1. 引数から `browser`, `require_visible`, `exclude_minimized` を解析
2. `mcp__native-browser-control__chrome_list_browser_windows` を呼び出す
   - `browser`: 解析した値（省略時は "chrome"）
   - `require_visible`: boolean値
   - `exclude_minimized`: boolean値
3. 結果をインデックス付きで表示
4. 次のアクションとして `/browser:connect <index>` を案内

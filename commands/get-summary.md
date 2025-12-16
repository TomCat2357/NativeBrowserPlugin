---
description: ブラウザの状態概要を取得
argument-hint: [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_get_browser_summary
---

ブラウザの現在の状態を一括で取得します。

**引数**
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `browser` を解析
2. `mcp__native-browser-control__chrome_get_browser_summary` を呼び出す
   - `browser`: 解析した値（省略時は "chrome"）
3. 取得した概要情報を表示：
   - URL/タイトル
   - ウィンドウ状態（最小化/通常/最大化、可視/不可視）
   - 位置・サイズ情報（rect）
   - descendants要素の統計情報（総数、可視/不可視の内訳とコントロールタイプ別集計）

**使用例**
- `/browser:get-summary` - Chromeの状態概要を取得
- `/browser:get-summary browser=edge` - Edgeの状態概要を取得

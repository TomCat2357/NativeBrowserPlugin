---
description: ズーム操作
argument-hint: <action> [browser=chrome|edge]
allowed-tools: mcp__native-browser-control__chrome_zoom
---

ズーム操作を行います。

**引数**
- `action`: ズーム操作（in=拡大、out=縮小、reset=リセット、必須）
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）

**手順**
1. 引数から `action`, `browser` を解析
2. `action` が無ければ usage を出して終了
3. `mcp__native-browser-control__chrome_zoom` を呼び出す
   - `action`: 解析したアクション
   - `browser`: 解析した値（省略時は "chrome"）
4. ズーム操作完了を確認

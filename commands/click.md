---
description: 座標でクリック
argument-hint: <x> <y> [browser=chrome|edge] [click_type=single|double|right]
allowed-tools: mcp__native-browser-control__chrome_click
---

指定した座標をクリックします（ウィンドウ相対座標）。

**引数**
- `x`: X座標（必須）
- `y`: Y座標（必須）
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）
- `click_type`: クリックの種類（single, double, right、省略時: single）

**手順**
1. 引数から `x`, `y`, `browser`, `click_type` を解析
2. `x`, `y` が無ければ usage を出して終了
3. `mcp__native-browser-control__chrome_click` を呼び出す
   - `x`: 整数値
   - `y`: 整数値
   - `browser`: 解析した値（省略時は "chrome"）
   - `click_type`: 解析した値（省略時は "single"）
4. クリック完了を確認
5. 注意: DPI設定により座標がずれる場合がある。要素ベースのクリックを推奨。

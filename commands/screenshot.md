---
description: ブラウザウィンドウを撮影
argument-hint: [browser=chrome|edge] [format=PNG|JPEG] [quality=90]
allowed-tools: mcp__native-browser-control__chrome_screenshot
---

ブラウザウィンドウのスクリーンショットを撮影します（base64エンコードされた画像を返します）。

**引数**
- `browser`: 対象ブラウザ（chrome または edge、省略時: chrome）
- `format`: 画像フォーマット（PNG または JPEG、省略時: PNG）
- `quality`: JPEG品質（1-100、省略時: 90）※formatがJPEGの場合のみ有効

**手順**
1. 引数から `browser`, `format`, `quality` を解析
2. `mcp__native-browser-control__chrome_screenshot` を呼び出す
   - `browser`: 解析した値（省略時は "chrome"）
   - `format`: 解析した値（省略時は "PNG"）
   - `quality`: 整数値（省略時は 90、formatがJPEGの場合のみ）
3. 撮影した画像を表示

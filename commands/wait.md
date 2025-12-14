---
description: 指定秒数待機
argument-hint: [seconds=2]
allowed-tools: mcp__native-browser-control__chrome_wait
---

指定した秒数待機します。

**引数**
- `seconds`: 待機秒数（数値、省略時: 2）

**手順**
1. 引数から `seconds` を解析（数値型）
2. `mcp__native-browser-control__chrome_wait` を呼び出す
   - `seconds`: 解析した値（省略時は 2）
3. 待機完了を確認

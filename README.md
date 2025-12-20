# Native Browser Control Plugin

Claude Code から NativeBrowserControl MCP サーバーを使いやすくするためのプラグインです。

## できること

NativeBrowserControl は、Windows の UI Automation を使って Selenium なしで Chrome / Edge を直接操作する MCP サーバーです。このプラグインは、そのツールを簡単に実行できるようにします。

### スラッシュコマンド（全26個）

#### ブラウザ接続・管理
- `/browser:list-windows` - 起動中のブラウザウィンドウ一覧を取得
- `/browser:connect` - 指定ブラウザに接続（未起動なら起動）
- `/browser:wait` - 指定秒数待機

#### ナビゲーション
- `/browser:navigate` - 指定URLに移動
- `/browser:get-url` - 現在のページURLを取得
- `/browser:get-title` - 現在のページタイトルを取得
- `/browser:back` - 前のページに戻る
- `/browser:forward` - 次のページに進む
- `/browser:refresh` - ページをリロード

#### スクリーンショット
- `/browser:screenshot` - ブラウザウィンドウを撮影
- `/browser:full-screenshot` - 画面全体を撮影

#### コンテンツ取得
- `/browser:get-page-text` - ページ全体のテキストを取得
- `/browser:get-page-source` - HTMLソースを取得

#### テキスト入力・検索
- `/browser:type-text` - テキストを入力
- `/browser:find-text` - ページ内検索

#### スクロール
- `/browser:scroll` - ページをスクロール

#### タブ操作
- `/browser:new-tab` - 新しいタブを開く
- `/browser:close-tab` - 現在のタブを閉じる
- `/browser:switch-tab` - タブを切り替え

#### ズーム
- `/browser:zoom` - ズーム操作

#### クリック操作
- `/browser:click` - 座標でクリック

#### 要素操作（重要）
- `/browser:scan-elements` - ページ上の要素をスキャン
- `/browser:click-element` - 要素をインデックスでクリック
- `/browser:set-element-text` - 要素のテキストを設定

#### クリップボード
- `/browser:copy-selected` - 選択中のテキストをコピー
- `/browser:paste` - クリップボードの内容を貼り付け

### Skill

- **native-browser-usage**: NativeBrowserControl の使い方、Tips、ベストプラクティスを提供

## 前提条件

- Windows 環境
- Chrome または Edge がインストールされていること
- NativeBrowserControl MCP サーバーが `.mcp.json` に設定されていること

## セットアップ

### 1. プラグインのインストール

#### 方法1: マーケットプレイスからインストール（推奨）

Claude Code でマーケットプレイスを追加し、プラグインをインストールします：

```bash
# マーケットプレイスを追加
/plugin marketplace add TomCat2357/NativeBrowserControl

# プラグインをインストール
/plugin install native-browser-control
```

#### 方法2: ローカルからインストール（開発者向け）

リポジトリをクローンして、ローカルからプラグインを読み込みます：

```bash
# リポジトリをクローン
git clone https://github.com/TomCat2357/NativeBrowserPlugin.git

# Claude Code でローカルプラグインとして読み込み
/plugin install ./NativeBrowserPlugin
```

#### 方法3: ZIPダウンロードからインストール（SSH/Git接続不可環境向け）

会社のセキュリティポリシー等でSSHやGit接続ができない場合は、ZIPファイルをダウンロードしてインストールできます：

1. ブラウザで [GitHubリポジトリ](https://github.com/TomCat2357/NativeBrowserPlugin) にアクセス
2. 緑色の「Code」ボタン → 「Download ZIP」をクリック
3. ダウンロードしたZIPを展開

```bash
# 展開したフォルダからローカルマーケットプレイスとして追加
/plugin marketplace add ./NativeBrowserPlugin-master

# ローカル版プラグインをインストール
/plugin install native-browser-control-local@native-browser-control-tools
```

または直接インストール：
```bash
/plugin install ./NativeBrowserPlugin-master
```

### 2. MCP サーバーの設定

プラグインをインストールしたら、NativeBrowserControl MCP サーバーを設定します：

```bash
/add-to-config
```

このコマンドを実行すると、インストール方法（uvx / pip-editable / script）を選択し、必要な情報を入力することで、自動的に設定ファイル（`~/.claude.json` または `~/.codex/config.toml`）に MCP サーバーの設定が追加されます。

**推奨設定**: uvx を使用した GitHub からの直接実行（インストール不要で常に最新版を使用できます）

## 使い方の例

### 基本的な流れ

1. ブラウザに接続
```
/browser:connect
```

2. URLに移動
```
/browser:navigate https://example.com
```

3. スクリーンショットで確認
```
/browser:screenshot
```

4. 要素をスキャンしてボタンをクリック
```
/browser:scan-elements
/browser:click-element 42
```

## 注意事項

- 実ブラウザウィンドウを前面化・最大化して操作するため、実行中は手動操作に影響します
- DPI 設定や仮想デスクトップ構成によっては座標がずれることがあります
- `chrome_scan_elements` 実行後に取得したインデックスを `chrome_click_element` で利用してください

## 拡張性

このプラグインは将来の拡張を見込んで設計されています：

- `skills/native-browser-usage/references/` - 詳細なリファレンスドキュメントを追加可能
- `skills/native-browser-usage/examples/` - 実用的な使用例を追加可能

## ライセンス

MIT

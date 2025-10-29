# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

このリポジトリは、生成AIプロンプト活用による業務効率化をテーマとした日本語プレゼンテーションサイトです。単一のHTMLファイル（`index.html`）で実装されたスライドショー形式のプレゼンテーションです。

## 技術スタック

- **純粋なHTML/CSS/JavaScript**: ビルドツールやフレームワークは不要
- **外部依存**: Font Awesome 6.4.0（CDN経由）のみ
- **デザインシステム**: Atlassian Design Colorsをベースにしたカスタムカラーパレット

## プロジェクト構成

```
presentation-zou/
├── index.html          # メインプレゼンテーションファイル（全スライド含む）
└── img/               # プレゼンテーション画像
    ├── c-table_logo.png
    ├── image-1.png
    ├── image-2.png
    ├── image-3.png
    ├── image.png
    ├── yano_after.png
    └── yano_before.jpg
```

## ローカル開発

プレゼンテーションを表示するには、以下のいずれかの方法を使用:

```bash
# Python 3の場合
python -m http.server 8000

# Python 2の場合
python -m SimpleHTTPServer 8000

# Node.jsのhttp-serverを使用
npx http-server -p 8000
```

その後、ブラウザで `http://localhost:8000` にアクセス。

## アーキテクチャ

### スライド構造

- 全28スライドが単一HTMLファイル内に定義
- 各スライドは `.slide` クラスを持つdiv要素
- JavaScriptで `active` クラスを切り替えてスライド表示を制御
- スライド間のナビゲーションはアニメーション効果付き（`slideIn` keyframes）

### ナビゲーション機能

- **キーボード操作**:
  - 右矢印/スペース: 次へ
  - 左矢印: 前へ
  - Home: 最初のスライドへ
  - End: 最後のスライドへ
- **タッチ/スワイプ**: モバイルデバイスでのスワイプジェスチャー対応
- **ボタン**: 画面下部の前へ/次へボタン

### UI要素

- **プログレスバー**: 画面上部に表示、進行状況を可視化
- **スライド番号**: 右上に「現在のスライド / 総スライド数」を表示
- **コピーボタン**: 全てのコードブロックにコピー機能を自動追加（`addCopyButtons()`）

## スタイリングシステム

### CSS変数（:root）

主要なカラーパレット:
- `--primary-color: #0052CC` - プライマリブルー
- `--secondary-color: #36B37E` - 成功グリーン
- `--accent-color: #FF5630` - アクセントレッド
- `--text-color: #172B4D` - メインテキスト
- `--light-bg: #F4F5F7` - 背景色

### 主要なコンポーネントクラス

- `.title-slide`: タイトルスライド専用スタイル
- `.comparison`: 2カラム比較レイアウト
- `.feature-grid`: グリッドレイアウト（特徴表示用）
- `.card`: カードコンポーネント（success/warning/error バリアント）
- `.highlight-box`: 重要情報のハイライト表示
- `.prompt-example` / `.output-example`: プロンプトと出力の例示

## コンテンツ編集

### 新しいスライドの追加

1. `<div class="slide">` 要素を追加
2. 必要なHTMLコンテンツを記述
3. JavaScriptの `totalSlides` は自動計算されるため、手動更新不要

### スライドの順序変更

HTMLファイル内のスライド順序を直接変更するだけでOK

### 画像の管理

- 全ての画像は `/img/` ディレクトリに配置
- 画像パスは絶対パス（`/img/filename.ext`）で参照
- 画像追加時は `/img/` ディレクトリに配置し、HTMLで参照

## 日本語コンテンツ

このプレゼンテーションは完全に日本語で記述されています。以下のトピックをカバー:

1. プロンプトエンジニアリングの基礎
2. 効果的なプロンプトの5要素フレームワーク
3. Markdown形式での出力指定
4. ChatGPT Thinking modeの活用
5. NotebookLMとNano Bananaの紹介

コンテンツ編集時は日本語の文脈とビジネス用途を考慮すること。

## 注意事項

- このリポジトリは静的なプレゼンテーションサイトであり、バックエンドやビルドプロセスは不要
- スタイルとスクリプトはすべてindex.html内にインライン記述
- レスポンシブデザインは実装されていない（PC専用設計）
- コードの変更後は、ブラウザでリロードして確認

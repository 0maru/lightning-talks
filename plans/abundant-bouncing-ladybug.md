# Claude Code ベストプラクティス勉強会スライド作成計画

## 概要

GitHub issue #3の要件に基づき、Claude Codeのベストプラクティスを解説する勉強会用スライド（42枚）をSlidevで作成します。

**プロジェクト名**: `claude-code-best-practices`
**形式**: Web版（Slidev）+ PDF出力
**言語**: 日本語
**スライド枚数**: 42枚

## ディレクトリ構造

```
claude-code-best-practices/
├── .gitignore
├── .npmrc
├── README.md
├── package.json
├── slides.md                    # メインスライドファイル（42枚すべて）
├── styles/
│   ├── index.ts                 # CSSエントリポイント
│   └── custom.css               # カスタムカラーテーマとフォント設定
├── components/
│   ├── SectionTitle.vue         # ダーク背景のセクションタイトル用
│   ├── CodeBlock.vue            # カスタムコードブロック
│   └── ComparisonTable.vue      # 比較表用コンポーネント
├── public/
│   └── images/                  # スクリーンショットや図解
└── snippets/                    # コードスニペット
    ├── claude-md-example.md
    ├── skill-template.md
    └── hook-examples.sh
```

## 実装手順

### Phase 1: プロジェクトセットアップ

1. **ディレクトリとpackage.json作成**
   ```bash
   mkdir claude-code-best-practices
   cd claude-code-best-practices
   ```

2. **package.json**（最新の@slidev/cli ^0.50.0-beta.5を使用）
   ```json
   {
     "name": "claude-code-best-practices",
     "type": "module",
     "private": true,
     "scripts": {
       "build": "slidev build",
       "dev": "slidev --open",
       "export": "slidev export"
     },
     "dependencies": {
       "@slidev/cli": "^0.50.0-beta.5",
       "@slidev/theme-default": "latest",
       "@slidev/theme-seriph": "latest",
       "vue": "^3.5.12"
     },
     "devDependencies": {
       "playwright-chromium": "^1.50.1"
     }
   }
   ```

3. **基本設定ファイル**
   - `.gitignore`: node_modules, dist, .slidev等を除外
   - `.npmrc`: shamefully-hoist=true, auto-install-peers=true
   - `README.md`: プロジェクト説明と起動方法

4. **依存関係インストール**
   ```bash
   pnpm install
   ```

### Phase 2: テーマとスタイル設定

1. **styles/custom.css作成**（カラーテーマ実装）
   ```css
   :root {
     /* Anthropic Brand Colors */
     --claude-dark-bg: #1A1A2E;
     --claude-light-bg: #F5F5F0;
     --claude-accent: #D97757;
     --claude-code-bg: #2D2D3F;
     --claude-code-text: #E8E8E8;
     --claude-subtle: #8B8B9E;

     /* Slidev Override */
     --slidev-theme-primary: var(--claude-accent);
     --slidev-code-background: var(--claude-code-bg);
   }

   /* Light background (default) */
   .slidev-layout {
     background-color: var(--claude-light-bg);
     color: #1A1A2E;
   }

   /* Dark section */
   .slidev-layout.dark-section {
     background-color: var(--claude-dark-bg);
     color: #FFFFFF;
   }

   /* Code blocks */
   .slidev-code {
     background-color: var(--claude-code-bg) !important;
     border-radius: 8px;
     padding: 1.5rem !important;
   }

   /* Slide numbers */
   .slidev-page-number {
     font-size: 10pt;
     color: var(--claude-subtle);
   }
   ```

2. **styles/index.ts作成**
   ```typescript
   import './custom.css'
   ```

3. **slides.md frontmatter設定**
   ```yaml
   ---
   theme: seriph
   title: Claude Code ベストプラクティス
   class: text-center
   transition: slide-left
   mdc: true
   colorSchema: light
   fonts:
     sans: 'Calibri, Arial, sans-serif'
     serif: 'Arial Black, Arial, sans-serif'
     mono: 'Consolas, Monaco, "Courier New", monospace'
     provider: 'none'
   lineNumbers: true
   aspectRatio: '16/9'
   ---
   ```

4. **動作確認**
   ```bash
   pnpm run dev
   ```

### Phase 3: スライド内容の実装（42枚）

**セクション別スライド構成**（issue #3より）:

1. **イントロ（3枚）** - スライド1-3
   - タイトル（ダーク背景）
   - 今日のゴール
   - 全体マップ（図解）

2. **コンテキストウィンドウ（5枚）** - スライド4-8
   - セクションタイトル（ダーク背景）
   - 最も重要な制約
   - 対処法（3カラム）
   - フィードバックループ（図解）
   - セルフチェックの威力

3. **CLAUDE.md（6枚）** - スライド9-14
   - セクションタイトル（ダーク背景）
   - メモリの4階層（図解）
   - 何を書くべきか（2カラム）
   - インポート構文（コードブロック）
   - ハンズオン手順
   - ベストプラクティスまとめ

4. **Skills（7枚）** - スライド15-21
   - セクションタイトル（ダーク背景）
   - Skillsとは
   - Skillの構造（ディレクトリ図解）
   - SKILL.mdの書き方（コードブロック）
   - スコープの違い（2カラム）
   - ハンズオン手順
   - Tips & 注意点

5. **Hooks（8枚）** - スライド22-29
   - セクションタイトル（ダーク背景）
   - Hooksの3タイプ（3カラム）
   - イベント一覧（テーブル）
   - commandフック実例
   - promptフック実例
   - agentフック実例
   - ハンズオン手順
   - ベストプラクティス

6. **Subagents & Plugins（11枚）** - スライド30-40
   - Subagentsセクションタイトル（ダーク背景）
   - Subagentsとは
   - 使い分け（フローチャート）
   - 実例
   - ハンズオン手順
   - Pluginsセクションタイトル（ダーク背景）
   - Pluginの構造
   - 配布方法
   - 既存プラグイン紹介
   - ハンズオン手順

7. **まとめ（2枚）** - スライド41-42
   - 意思決定フローチャート
   - 今週のアクション

**実装のポイント**:
- セクションごとにコミット
- 連続するスライドで同じレイアウトを避ける
- すべてのスライドにビジュアル要素（コード、テーブル、図解）を含める
- コメントでスライド番号を明記（管理容易性）

### Phase 4: カスタムコンポーネント作成

1. **components/SectionTitle.vue**
   - ダーク背景（#1A1A2E）
   - タイトル + サブタイトル
   - センタリング

2. **components/CodeBlock.vue**
   - カスタムコードブロック
   - タイトル付き
   - ダーク背景（#2D2D3F）、Consolasフォント

3. **components/ComparisonTable.vue**
   - Do's/Don'ts用
   - 2カラムレイアウト
   - アイコン付き

### Phase 5: 最終調整

1. **全体レビュー**
   - 42枚すべてのスライド確認
   - レイアウトの多様性確認
   - カラーテーマの一貫性確認
   - フォントサイズ・可読性確認

2. **ビルドとエクスポート**
   ```bash
   pnpm run build    # 本番ビルド
   pnpm run export   # PDF出力
   ```

## 重要ファイル

実装時に作成・編集が必要な主要ファイル:

1. **[claude-code-best-practices/slides.md](claude-code-best-practices/slides.md)**
   - 42枚すべてのスライド内容
   - frontmatterでテーマ・フォント・カラー設定
   - 最も重要なファイル

2. **[claude-code-best-practices/styles/custom.css](claude-code-best-practices/styles/custom.css)**
   - Anthropicブランドカラー（#1A1A2E, #F5F5F0, #D97757）
   - コードブロックスタイル（#2D2D3F背景）
   - スライド番号スタイル

3. **[claude-code-best-practices/package.json](claude-code-best-practices/package.json)**
   - @slidev/cli ^0.50.0-beta.5
   - ビルド・開発・エクスポートスクリプト
   - playwright-chromium（PDF出力用）

4. **[claude-code-best-practices/components/SectionTitle.vue](claude-code-best-practices/components/SectionTitle.vue)**
   - ダーク背景のセクションタイトル
   - 7つのセクションで使用

5. **[claude-code-best-practices/components/ComparisonTable.vue](claude-code-best-practices/components/ComparisonTable.vue)**
   - Do's/Don'ts、3カラム比較表
   - 複数スライドで再利用

## カラーパレット（issue #3より）

| 用途 | カラーコード | 説明 |
|------|-------------|------|
| ダーク背景 | #1A1A2E | セクションタイトル用 |
| ライト背景 | #F5F5F0 | コンテンツスライド用 |
| アクセント | #D97757 | Anthropicオレンジ |
| コードブロック背景 | #2D2D3F | コード表示用 |
| コードブロック文字 | #E8E8E8 | コード表示用 |
| サブテキスト | #8B8B9E | 補足・スライド番号用 |

## フォント設定

| 用途 | フォント |
|------|---------|
| ヘッダー | Arial Black |
| ボディ | Calibri |
| コード | Consolas |

※すべてシステムフォント（追加インストール不要）

## 検証方法

### ローカル確認
```bash
cd claude-code-best-practices
pnpm install
pnpm run dev
```
- http://localhost:3030 で確認
- カラーテーマの表示確認
- フォントの表示確認
- 各スライドのレイアウト確認

### ビルド確認
```bash
pnpm run build
```
- `dist/` ディレクトリの生成確認
- ビルドエラーがないか確認

### PDF出力
```bash
pnpm run export
```
- `slides-export.pdf` の生成確認
- PDF内のカラー・フォント確認

## 参考: 既存プロジェクト

- [claude-mcp/](../claude-mcp/) - MCP関連スライド、構造の参考
- [modern-css/](../modern-css/) - カスタムスタイリングの例
- [react-v0-hands-on/](../react-v0-hands-on/) - 最新版Slidev使用例

## 注意事項

1. **レイアウトの多様性**: 連続するスライドで同じレイアウトを避ける
2. **ビジュアル要素必須**: すべてのスライドにコード・テーブル・図解のいずれかを含める
3. **スライド番号**: 右下に10pt、#8B8B9Eで表示
4. **フォント**: システムフォントを使用（Arial Black, Calibri, Consolas）
5. **カラー一貫性**: CSS変数で統一的に管理
6. **ハンズオン**: ステップバイステップの番号付きリスト + コード例

## 実装後の展開

1. **勉強会での使用**: Web版をブラウザで表示（プレゼンターモード対応）
2. **PDF配布**: `pnpm run export`で生成したPDFを配布
3. **継続更新**: 勉強会後のフィードバックを反映

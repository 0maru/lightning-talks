# Claude Code ベストプラクティス

Claude Codeのベストプラクティスを解説する勉強会用スライドです。

## 技術スタック

- **Slidev**: プレゼンテーションフレームワーク
- **Vue 3**: コンポーネント開発
- **TypeScript**: 型安全性

## 起動方法

### 開発環境

```bash
pnpm install
pnpm run dev
```

http://localhost:3030 でスライドを確認できます。

### ビルド

```bash
pnpm run build
```

`dist/` ディレクトリに本番用ファイルが生成されます。

### PDF出力

```bash
pnpm run export
```

`slides-export.pdf` が生成されます。

## スライド構成

全42枚のスライドで構成されています:

1. **イントロ** (3枚)
2. **コンテキストウィンドウ** (5枚)
3. **CLAUDE.md** (6枚)
4. **Skills** (7枚)
5. **Hooks** (8枚)
6. **Subagents & Plugins** (11枚)
7. **まとめ** (2枚)

## カラーテーマ

Anthropicブランドカラーを使用:

- ダーク背景: `#1A1A2E`
- ライト背景: `#F5F5F0`
- アクセント: `#D97757`
- コードブロック背景: `#2D2D3F`

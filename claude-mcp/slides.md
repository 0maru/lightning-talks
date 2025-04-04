---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
---

# Deno でMCP サーバーを作成する

---

# Deno とは？


- Ryan Dahl（Node.jsの創始者）によって開発された新しいJavaScriptランタイム
- Node.jsの「設計上の後悔」を修正するために作られた
- 安全性第一のアプローチ：デフォルトでセキュアな環境
- TypeScriptをネイティブサポート
- ブラウザと互換性のあるAPIを採用
- 依存関係管理の合理化: package.jsonやnpm/yarnは不要

---

# なぜDeno?

- セキュリティ：デフォルトで安全（ファイルシステム、ネットワークへのアクセスは明示的な許可が必要）
- TypeScriptのネイティブサポート（トランスパイラ不要）
- 標準ライブラリが充実
- モダンなAPIとPromiseベースの設計
- シンプルな依存関係管理（URL直接インポート）
- 開発者体験の向上：フォーマッター、リンター、テストランナーなどが組み込み済み
- シングルバイナリですぐに実行可能

**セキュリティ：デフォルトで安全**が今回の採用理由


---

# セキュリティ的にデフォルトで安全とは？

明示的にオプションを指定しないと下記の機能が使用できない

- ファイルシステムへの読み書き（--allow-read、--allow-writeフラグが必要）
- ネットワーク通信（--allow-netフラグが必要）
- 環境変数の参照（--allow-envフラグが必要）
- サブプロセスの実行（--allow-runフラグが必要）

さらにV8エンジンのサンドボックス環境で実行されるので、OSのリソースへのアクセスは制限されている

--

# MCP とは？

---

# 準備
 
 Claude Desktop とDeno のインストール

```
brew install claude
brew install deno
```

---

# MCPプロジェクトを作成する

---

# 最低限のコードを書いてClaude にMCPサーバを接続する

---

# Redash に接続するコードを書く

---

# Claude経由でRedash の操作を行う


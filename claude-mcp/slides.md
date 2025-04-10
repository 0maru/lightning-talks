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

# Model Context Protocol

---
layout: default
---

## Model Context Protocol（MCP）とは

MCPと省略した形で書かれる事が多い  
Anthoropic社が策定した、AIモデルとアプリケーション間の通信を行うためのプロトコル

Claude Desktop やVS Code、Cline、Cursor などが対応している

---
layout: image

image: ./assets/mcp-architecture.png
---

---

## 仕組み

MCP Client（Claude Desktopなど） とMCP Server がありこの間は標準入出かStreamable HTTPで通信を行う  
メッセージはJSON-RPC形式でやり取りされる  
プロンプトが送信されると、LLM が登録されているMCPを確認して、使用するかを判断してくれる  
→LLMの判断なので、似た機能があったりすると意図しない動作をすることがある  

ツールによってはMCP の有効、無効を管理できるものも出てきている  

---


## MCP の機能

- Prompt
  - 
- Tools
  - 
- Sampling
  - 
- Roots
  -
- Transports
  -

---

## MCP利用時における注意点

### セキュリティ

ローカル環境でプログラムを動かすことになるので、悪意を持ったプログラムが埋め込まれているかもしれない  
GitHubやAWS公式のMCPの利用に留めるか、自作したMCPの利用に留めるのがベストだと思う  

### 使うとき

LLM による解釈が挟まって操作されるので、操作が完璧ではない  
LLMに対してコンテキストを与える事ができるので、最新のドキュメントを与える使い方は知識が増えるので良き

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


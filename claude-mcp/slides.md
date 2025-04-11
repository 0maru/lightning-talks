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
ユーザーのプロンプトからLLMが関連するMCPの機能が必要と判断した場合に、MCPサーバを使用する仕組み
→コンテキスト解釈に基づく判断なので似た機能があったりすると意図しない動作をすることがある  

ツールによってはMCP の有効、無効を管理できるものも出てきている  

---


## MCP の機能

- Resources
  - サーバからLLMにデータとコンテンツを公開する
  - LLM にコンテキストを与えている
- Prompts
  - 再利用可能なプロンプトテンプレート、ワークフローを作成する
  - 簡単にLLMを使用できるようにする手段（引数を受け入れる、UIを用意する）

---

## MCP の機能 - 2

- Tools
  - LLM がサーバ経由でアクションを行えるようにする
  - チャットで操作するアプリのようなもの
- Sampling
  - 人とLLMが複数回のやり取りを行うことで精度を高める
  - サーバからのレスポンスでLLMに指示を出して、その結果を人に返す
  - サーバのレスポンスでモデルの指定やパラメータの指定もできる
  - データ作成側が考える最適なLLMを使わせる事ができる
  - いわゆるエージェント的なこと
  - 例：AWSコスト分析ツールがデータを取得→LLMが分析→ユーザーに最適化提案
 
https://modelcontextprotocol.io/clients

---

## MCP利用時における注意点

### セキュリティ

ローカル環境でプログラムを動かすことになるので、悪意を持ったプログラムが埋め込まれているかもしれない  
GitHubやAWS公式のMCPの利用に留めるか、自作したMCPの利用に留めるのがベスト  

### 使うとき

LLM による解釈が挟まって操作されるので、操作が完璧ではない  
LLMに対してコンテキストを与える事ができるので、最新のドキュメントを与える使い方は知識が増えるので良き

---

## MCP を使ってみる

Claude Desktop のインストール

```shell
brew install claude
```

---

## AWS Documentation MCP Server の起動準備

Python で実装されたMCP Serverなのでuvをインストールしておく


```shell
brew install uv
uv python install 3.13
```

```shell
uvx awslabs.aws-documentation-mcp-server@latest
```

---

## Claude Desktop への登録

1. Claude Desktop を起動して cmd + , で設定画面を開く  
2. Developer をクリック
3. Edit config をクリック
4. Finderが開くので、claude_desktop_config.json を開く

---

## MCP Server の登録

```json
{
  // ... その他
  "mcpServers": {
    "awslabs.aws-documentation-mcp-server": {
        "command": "/opt/homebrew/bin/uvx",
        "args": ["awslabs.aws-documentation-mcp-server@latest"],
        "env": {
          "FASTMCP_LOG_LEVEL": "ERROR"
        },
        "disabled": false,
        "autoApprove": []
    }
  }
  // ... その他
}
```

保存したら Claude Desktop を再起動してください  
uv のパスは　`which uv` で確認してください

---

layout: image

image: CleanShot 2025-04-11 at 01.27.55.png

---

## 登録の確認

---

## 動作させてみる

```
EC2インスタンスの命名規則はありますか
```

```
Allow tool from “awslabs.aws-documentation-mcp-server” (local)?
```

というメッセージが出てきたら、MCP Server が起動している証拠です  
Allow for this chat か Allow Once をクリックするとMCP Server が有効になります  

---

## AWS MCP を使用する理由

Claude やChatGPT は最新の情報も持っているわけではなく、知識はカットオフがされている。  
AWSのドキュメントは常に最新の情報が更新されているので、MCP Server をLLMに情報を与えることで、最新の情報までを考慮した回答ができる。  

- AWS CDK MCP Server 
  - AWS CDKのドキュメントやベストプラクティスを提供
- Cost Analysis MCP Server
  - AWSサービスのコスト分析機能を提供
等がある

---

## GitHub MCP Server の登録

YOUR_TOKEN にはGitHubのPersonal Access Tokenを入れてください
gh auth token でも取得できます

```json
"github": {
  "command": "docker",
  "args": [
    "run",
    "-i",
    "--rm",
    "-e",
    "GITHUB_PERSONAL_ACCESS_TOKEN",
    "ghcr.io/github/github-mcp-server"
  ],
  "env": {
    "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
  }
}
```

---

## GitHub MCP Server を使ってみる

```
私のGitHubアカウントは？
```

```
ブログ用のリポジトリを作成して。リポジトリ名はblog
```

---

GitHub MCP Server をVS Code やJetBrains IDE に登録することで、AI経由でコミットしてPRを作成することもできる  
API経由で行えてインタフェースが定義されているので間違いにくい  
登録されているAPIだけを使えば、存在しない機能を使いような事にならない  

---

# MCP Server を作ってみよう

---

## Deno とは？

- Ryan Dahl（Node.jsの創始者）によって開発された新しいJavaScriptランタイム
- Node.jsの「設計上の後悔」を修正するために作られた
- 安全性第一のアプローチ：デフォルトでセキュアな環境
- TypeScriptをネイティブサポート
- ブラウザと互換性のあるAPIを採用
- 依存関係管理の合理化: package.jsonやnpm/yarnは不要

---

## なぜDeno?

- セキュリティ：デフォルトで安全（ファイルシステム、ネットワークへのアクセスは明示的な許可が必要）
- TypeScriptのネイティブサポート（トランスパイラ不要）
- 標準ライブラリが充実
- モダンなAPIとPromiseベースの設計
- シンプルな依存関係管理（URL直接インポート）
- 開発者体験の向上：フォーマッター、リンター、テストランナーなどが組み込み済み
- シングルバイナリですぐに実行可能

**セキュリティ：デフォルトで安全**が今回の採用理由


---

## セキュリティ的にデフォルトで安全とは？

明示的にオプションを指定しないと下記の機能が使用できない

- ファイルシステムへの読み書き（--allow-read、--allow-writeフラグが必要）
- ネットワーク通信（--allow-netフラグが必要）
- 環境変数の参照（--allow-envフラグが必要）
- サブプロセスの実行（--allow-runフラグが必要）

さらにV8エンジンのサンドボックス環境で実行されるので、OSのリソースへのアクセスは制限されている

---

## 準備
 
Deno のインストール

```
brew install deno
```

---

# # MCPプロジェクトを作成する

redash-mcp-server という名前でプロジェクトを作成する  
せっかくなのでClaude Desktop で作成してみてください

```
mcp-server-sample という名前のプライベートリポジトリを作成してください
```

---

## リポジトリをクローンする

---

## 最低限のコードを書いてClaude にMCPサーバを接続する

```typescript
import { McpServer } from "npm:@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "npm:@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "npm:zod";

const server = new McpServer({
  name: "mcp-server-sample",
  version: "1.0.0",
});

server.tool(
  "double_number",
  "与えられた数値を2倍にする",
  {num: z.number().describe("数値")},
  ({num}) => ({
    content: [{type: "text", text: (num * 2).toString()}]
  }),
);

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("Example MCP Server running on stdio");
}

main();
```

---

## Claude Desktop に登録する

```json
"mcp-server-sample": {
  "command": "/opt/homebrew/bin/deno",
  "args": [
    "run",
    "/Users/3maru/workspaces/github.com/0maru/mcp-server-sample/main.ts",
  ],
  "disabled": false,
  "autoApprove": []
}
```

---
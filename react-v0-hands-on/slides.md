---
theme: default
title: Vercel v0 を使用したECサイトのフロントエンド開発 
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
overviewSnapshots: true
---

# Vercel v0 を使用したECサイトのフロントエンド開発

---

# v0 とは？？

AI を活用してUIとコードの生成をおこなうツール  
Next.js の開発を行うVercel が提供する生成AIサービス  

---

# v0 を使ってECサイトを作ってみる

---

# Next.js のプロジェクトを作成する

```bash
npx create-next-app@latest
```

https://nextjs.org/

コマンドを実行したらプロジェクト名以外すべて「Enter」で進める

```txt
What is your project named? my-app
Would you like to use TypeScript? No / Yes
Would you like to use ESLint? No / Yes
Would you like to use Tailwind CSS? No / Yes
Would you like your code inside a `src/` directory? No / Yes
Would you like to use App Router? (recommended) No / Yes
Would you like to use Turbopack for `next dev`?  No / Yes
Would you like to customize the import alias (`@/*` by default)? No / Yes
What import alias would you like configured? @/*
```

## Reactのバージョンを18に下げる

```bash
npm i react@18 react-dom@18
```

---

# Next.js の起動確認

dev サーバーを起動してブラウザで確認する

```bash
npm run dev
```

http://localhost:3000/

---

# v0 で使用される依存関係の追加

## lucide-react（アイコン）

```bash
npm install lucide-react
```


## shadcn-ui（UIライブラリ）

```bash
npx shadcn-ui@latest init
```

実行したら残りすべて「Enter」 で進める  

今後使用するので下記のURL開いてブラウザのタブに残す  
https://ui.shadcn.com/docs/components/accordion

---

# v0 にアクセスしてみる

https://v0.dev/

Vercel のアカウントにログインが必要  
以前にVercel使う勉強会をやったのでアカウントはあるはず  

---

# ECサイトのトップページを作成する

プロンプトにECサイトのトップページを作ってくれと書き込んで実行する

入れてほしいワード
1. 商品一覧ページ
2. 商品詳細ページ

--- 

# 出てきたコードをコピペしてapp/page.tsxに貼り付ける

画面右上のコピーボタンを押して、貼り付ける

エディターの上部に行くとインポートエラーがある

---

# コンポーネントを追加する

shadcn-ui で提供されているコンポーネントを追加する

shadcn-ui はヘッドレスUIフレームワークで、コンポーネント毎にインポートすることができる。  
ボタンをインポートしてファイル名を変えたら、ログインボタン、カートに追加ボタンなど無限に作ることができる。   
ロジックをコンポーネントからできる限り切り出していたら、フレームワークの更新があっても新しくボタンをインポートして必要な分だけ書き換えたら、最新のフレームワークに則ったコンポーネントができるはず...


```bash
npx shadcn@latest add xxx
```

追加後、ブラウザで確認するとエラーなく画面が表示されているはず

---

# リファクタリング
コンポーネントに分かれていないとメンテナンス性であったり、再利用性が下がるので、コンポーネントに分ける。

<header>から</header>までを選択して、右クリックして「Extract Component」を選択する

---

# 商品一覧ページと商品詳細ページを作成する

コード自体はv0に作ってもらうので、貼り付け先のファイルを作成する

`app/products/page.tsx` と `app/products/[id]/page.tsx` を作成する。

---

# 商品一覧ページのコードを作成してもらう

---

# 商品詳細ページのコードを作成してもらう

---


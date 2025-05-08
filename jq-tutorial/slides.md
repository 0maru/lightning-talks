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
# take snapshot for each slide in the overview
overviewSnapshots: true
---

# jq とcurl で遊んでみよう

---

## curl コマンドとは??

HTTP/HTTPS をはじめ FTP, SFTP, SMTP
など多数のプロトコルに対応したコマンドラインツール

インストールの確認

```bash
which curl
```

---

## curl を最新のバージョンにアップデートする

```bash
which curl
```

結果が`/usr/bin/curl` になっている場合にはmacOSにバンドルされているcurl
が使用されています。 アップデートしたいのでbrew からインストールしてbrew
でインストールしたcurlを使用するように書き換えます。

インストール方法

```bash
brew install curl
```

curl をリンクさせる

```bash
brew link curl --force
```

新しいターミナルのタブで 8.13.0 になっていたらbrew でインストールできるcurl
の最新版

```bash
curl -V
```

---

## curl を使ってみる

グローバルIPを取得する

```bash
curl 'https://inet-ip.info'
```

GitHub APIを使ってIssue を取得する

```bash
curl 'https://api.github.com/repos/0maru/twitter_login/issues'
```

POST通信を行う

```bash
curl -X POST https://httpbin.org/post \
     -H "Content-Type: application/json" \
     -d '{"message": "こんにちは"}'
```

---

## jq コマンドとは??

JSON のsed コマンドのようなもの\
フィルタや変形、集計も行える\
標準入力が読み取れるので複数のコマンドを組み合わせることで強力なコマンドになる

---

## jq を使ってみる-1

レスポンスをjq で整形する

```bash
curl 'https://api.github.com/repos/0maru/twitter_login/issues' | jq
```

レスポンスから特定のkeyを持つvalueを取得する

```bash
curl 'https://api.github.com/repos/0maru/twitter_login/issues' | jq '.[].title'

curl 'https://api.github.com/repos/0maru/twitter_login/issues' | jq '.[] | [.number, .title]'
```

---

## jq を使ってみる-2

sales_2024.json を保存して、保存したファイルがあるディレクトリに移動する

```
jq . sales_2024.json

jq '[.[].total]' -r sales_2024.json

jq '[.[].total] | add' -r sales_2024.json
```

---

## ブラウザ上からcurlコマンドを取得する

1. DevTools を開く
2. Network タブを開く
3. Copy → Copy as cURL をクリック

cURL
コマンドがコピーできたのでターミナルに貼り付けたら何度もAPI通信を行う事ができる\
unit test やintegration test
で動作を担保するべきだが、初めてプログラムの動作チェックやSentry
で発生したエラーと同じリクエストを送って、動作を確認することができる。\
モバイルアプリからのリクエストをcURLコマンドで貰い、アプリからのリクエストをシミュレートする事もできる。

---

## Postman を使ってAPIリクエストを送る

Postman とはGUI でAPI通信ができるクライアントツール

```bash
brew install postman
```

---

## curl からPostman のリクエストを作成する

ブラウザ上からcurlコマンドを取得する と同じ手順でcURLコマンドをコピーしてURL
の項目に貼り付けると手書きしなくてもPostmanのリクエストが作成できる

---

## 今後の活用方法

curl
でリクエストを送って、jqでレスポンスを見ることができるのでUIやテストを書く前でもAPIのレスポンスが見れる、共有できる

HTTPie を使うのも良き (内部ではPython のrequestsが使用されている)\
※curl なら急に共有されてもmacOS を使用していたら実行できるがHTTPie
は事前にインストールが必要

手元で検証する段階はHTTPieでやって

```bash
# CLI ツール
brew install httpie
# GUI アプリケーション
brew install --cask httpie
```

curl とhttpie の比較

```bash
curl -X POST https://httpbin.org/post \
     -H "Content-Type: application/json" \
     -d '{"message": "こんにちは"}' | jq

https POST https://httpbin.org/post message=こんにちは
```

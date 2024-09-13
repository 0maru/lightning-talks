---
theme: apple-basic
title: 'DuckDBと触れ合ってみよう'
lineNumbers: true
layout: intro
---

# DuckDB と触れ合ってみよう

---

# Duckdbとは？？
　
2024-06-03 に 1.0.0がリリースされたオープンソースの列指向リレーショナル データベース管理システム  
静的ライブラリとして提供されている  
依存しているものはないので、duckdbさえインストールしたら使える  
ビルドにはCMake、Python3、およびC++11準拠コンパイラさえあればビルドができる  

https://github.com/duckdb/duckdb

2024-09-09　に 1.1.0 がリリースされた

初回リリースは2019年

---

# DuckDBのインストール

```
brew install duckdb
```

インストールすればわかるが本当に依存しているものがない

---

# クライアントAPI

公式からいくつかの言語でクライアントAPIが提供されている

- Java
- Node.js
- Python
- Rust
- WebAssembly (Wasm)
etc...

https://duckdb.org/docs/api/overview


### Python の使用例

```
import duckdb

duckdb.sql("SELECT 42").show()
```

---

# DuckDB-Wasm

DuckDBはWebAssembly にコンパイルされているので、ブラウザ上でも実行することができる

https://duckdb.org/docs/api/wasm/overview

（やるひとがいるかは置いておいて）外部ファイルを読み込んで結果を出すことができるので、ブラウザ上だけで集計した結果を表示することも可能。
ファイルが取れればいいから、APIが無いからサーバ負荷やDB負荷は抑えられそう？？

---

# 外部ファイルの読み込み

CSVやJSONファイルを読み込んでテーブルの代わりに使用することができる  
スキーマは自動的に作成される  
自分で指定することも可能  


## CSVファイルの読み込み

```
SELECT * FROM 'data.csv';
```

## JSONファイルの読み込み

```
SELECT * FROM 'todos.json';
```

---

# 複数の外部ファイルを読み込む

1つのファイルだけでなく、複数のファイルを読み込むこともできる
Unix 形式のパス名のパターン展開が使用できる

```
import glob
>> glob.glob('./[0-9].*')
['./1.gif', './2.txt']
>> glob.glob('*.gif')
['1.gif', 'card.gif']
>> glob.glob('**/*.txt', recursive=True)
['2.txt', 'sub/3.txt']
```

## downloadsにある複数のファイルを読み込む

```
SELECT * FROM 'downloads/*.csv';
```

## 羅列した複数のファイルを読み込む

```
SELECT * FROM read_csv(['202408.csv', '202409.csv']);
```

---

# Extension

公式で対応していない形式のファイルを拡張機能を使うことによって読み込むこともできる  
  
https://duckdb.org/docs/extensions/overview  
  
S3 API Supportなどもあり、AWS S3 にあるファイルを使って分析などもできる

---

# 使い方

PostgreSQL のパーサがベースで、構文が拡張されている  
PostgreSQL でできることはある程度できるので分析などで困ることはほとんど無いはす

---

# ファイルを使ってSQLを書いてみる

```
SELECT * FROM 'downloads/20240913.csv'
```

※ファイルの拡張子は必須
もしネットワーク上のファイルを使う場合に、拡張子が存在しないときは専用関数を使用することで読み込むことができる

```
SELECT * FROM read_json_auto('');
```

```
SELECT * FROM * read_csv_auto('');
```

---

# どういう使い方をしているのか

主にスキマも会計処理の確認に使用している  
数万行あって検索が遅かったり、問題があったときに特定の商品に限って売上などを確認するのに使用する


---
theme: seriph
title: 入門 ビットボード
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

# 入門 ビットボード

--- 

# ビットボードとは？

- オセロやチェス、将棋などの盤面をビット配列で表したもの
- 64ビット整数の場合、オセロ・チェス(8x8)なら1個の変数で管理できる
- 将棋(9x9)なら2個の変数で管理できる

---

# ビット配列とは

- 0と1の2値を持つ配列

---

# 今回の資料について

- 扱う数字は符号なし整数（unsigned integer）を使う

---

# オセロの盤面管理に必要な項目について考えてみる

- マスの数は8x8
- マスには白、黒、空の3つの状態がある
- 置けるマスかどうかの判定（合法手の判定）
- ゲーム終了条件の判定


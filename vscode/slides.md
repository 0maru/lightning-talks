---
# You can also start simply with 'default'
theme: seriph
title: VS Codeへの移り方
info: 
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---

# VS Codeへの移り方

---
transition: fade-out
---

# 個人的なおすすめの設定

- "editor.minimap.enabled": false, // ミニマップを非表示にする
- "editor.renderLineHighlight": "all", // 選択行の行番号をハイライトする
- "editor.cursorBlinking": "smooth", // カーソルが滑らかに点滅するように
- "editor.bracketPairColorization.enabled": true // 括弧の対応を色付ける
- "editor.renderWhitespace": "all", // 空白を表示する
- "window.title": "", // タイトルを設定しない

---

# おすすめのキーバインド

## ファイル作成

## フォルダ作成


---


# おすすめの拡張機能（必須級）

## EditorConfig for VS Code

これがないとeditorconfigの設定が反映されません...

## Prettier - Code formatter
  
フォーマッターが存在しないとコードのフォーマットができないので、jsだけじゃなくjsonなどのフォーマットもできるように入れておく

## GitLens - Git supercharged

エディターの Git統合を強化してくれる

---

# IntelliJ のキーマップが使いたい

IntelliJ IDEA Keybindings を使うとIntelliJ のキーマップが使用できます  

k--kato.intellij-idea-keybindings  

---

# .code-workspace のススメ

code-workspaceとは?

code-workspaceはVS Codeのプロジェクトを管理するためのファイル
複数のリポジトリを１つのエディタで見たり、このワークスペース専用の設定などができる

# VS Code の問題点

フロントエンドもバックエンドも開発するし、担当プロジェクトが多いエンジニアがほとんど  
PycharmやWebStormのようにアプリが別れている場合には、アプリを切り替えればバックエンド、フロントエンドのコードを表に持ってこれたが、VS Codeではどの環境でも同じVS Codeになっている。


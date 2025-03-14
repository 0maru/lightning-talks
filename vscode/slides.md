---
# You can also start simply with 'default'
theme: seriph
title: VS Codeへの移り方
info: ””
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

## インストールしましょう

個人的にはIndiders版（ベータ版）がおすすめ

```
brew install visual-studio-code@insiders
```

安定版がいいならこれ

```
brew install visual-studio-code
```

---

## 起動してみる


--- 

## Copilot, Copilot Chat のインストール


cmd + shift + p でコマンドパレットを開いて Extensions: Install Extensions を選択

shift + cmd + x  

で Extesions を開いて検索してインストールする

---

## copilot の設定

画面右下の「Sign In to Use Copilot」をクリック

---

## Copilot Chat

質問をすると回答をくれる

必要なコードをコピーして貼り付けて終わり

---

## Copilot EDIT

Editモード、Agentモードがある

### Editモード

編集するファイルを選択してコンテキストとプロンプトを提供するとコード編集を提案してくれるので、その変更を受け入れる・受け入れないを選択する

### Agentモード

編集リクエストに対してCopilot が自律的に必要なタスクと関連ファイルを探し、コード編集やターミナルでのコマンド実行を提案し、継続的に反復する

---

# 個人的なおすすめの設定

- "editor.minimap.enabled": false, // ミニマップを非表示にする
- "editor.renderLineHighlight": "all", // 選択行の行番号をハイライトする
- "editor.cursorBlinking": "smooth", // カーソルが滑らかに点滅するように
- "editor.bracketPairColorization.enabled": true // 括弧の対応を色付ける
- "editor.renderWhitespace": "all", // 空白を表示する
- "window.title": "", // タイトルを設定しない
- "editor.formatOnSave": true // 保存時に自動フォーマット
- "editor.linkedEditing": true // HTMLタグなどの関連要素を同時編集
- "workbench.editor.enablePreview": false // プレビューモードを無効化
- "workbench.editor.revealIfOpen": true // 既に開いているファイルを再度開こうとすると、そのタブにフォーカス


タイトルを設定しないは後で回収します

---

## 設定することをおすすめするキーバインド

### ファイル作成

explorer.newFile

### フォルダ作成

explorer.newFolder

### Exploer タブを開く

workbench.view.explorer

---

## おすすめの拡張機能（必須級）

### EditorConfig for VS Code

これがないとeditorconfigの設定が反映されません...

### Prettier - Code formatter
  
フォーマッターが存在しないとコードのフォーマットができないので、jsだけじゃなくjsonなどのフォーマットもできるように入れておく

### GitLens - Git supercharged

エディターの Git統合を強化してくれる

---

## IntelliJ のキーマップが使いたい

IntelliJ IDEA Keybindings を使うとIntelliJ のキーマップが使用できます  

k--kato.intellij-idea-keybindings  

---

## .code-workspace のススメ

code-workspaceとは?

code-workspaceはVS Codeのプロジェクトを管理するためのファイル
複数のリポジトリを１つのエディタで見たり、このワークスペース専用の設定などができる

### VS Code の問題点

フロントエンドもバックエンドも開発するし、担当プロジェクトが多いエンジニアがほとんど  
PycharmやWebStormのようにアプリが別れている場合には、アプリを切り替えればバックエンド、フロントエンドのコードを表に持ってこれたが、VS Codeではどの環境でも同じVS Codeになっている。

---

## ワークスペースの作り方

File > Add Folder to Workspace でワークスペースに追加して保存する

すでにエディタを開いていて、追加したいなら `code -a .` で追加もできる

---

### 例

```json
{
  "folders": [
    {
      "name": "yyyyy-client",
      "path": "../../xxxxxx-zzzzz/yyyyy-client"
    },
    {
      "name": "xxxxxx-blog",
      "path": "../../xxxxxx-zzzzz/xxxxxx-blog"
    },
    {
      "name": "xxxxxx-id",
      "path": "../../xxxxxx-zzzzz/xxxxxx-id"
    },
  ],
  "settings": {
    "window.title": "ぷぷぷぷろじぇくとめい",
    "files.autoSave": "afterDelay",
    "workbench.colorCustomizations": {
      "titleBar.activeBackground": "#f830dd",
      "titleBar.activeForeground": "#ffffff",
      "titleBar.inactiveBackground": "#f830dd",
      "titleBar.inactiveForeground": "#ffffff"
    }
  }
}
```

---

### code-workspace 

window.title を設定することで、Mission Control のときにアプリのタイトルがwindow.titile で設定した値になる  
titleBar の色も変えているので、titleBar の色でプロジェクトを判別することもできる  

ビルドの設定もかけるので、個人の設定を書いたり、１つのタスクを実行することで複数のタスクを実行するような設定もかける  

---

### おすすめの管理法

プライベートリポジトリにcode-workspace ファイルをまとめたリポジトリを作成する

開くときはそのリポジトリに移動してcode xxxxxx.code-workspace で開くことができる

---

### Cursor  

https://www.cursor.com/ja

VSCodeのFork  
ChatGPT の方が使用していて火がついた


### Windsurf

https://codeium.com/windsurf

Codeium製の独自IDE  
全ファイル認識してと自動でタグ付けしてくれる  
→コンテキストが充実する

### Trae 

https://www.trae.ai/

ByteDance が開発しているエディタ  
VSCodeのFork  
Claude-3.5-Sonnet が無料で使える


---
align: center
---
# 一番大切なことは無理やり使うこと

---

## おわり



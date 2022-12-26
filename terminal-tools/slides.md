---
# try also 'default' to start simple
theme: apple-basic
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
# highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS
css: unocss
---
---
layout: intro
---

# ターミナルの歩き方

---

# ターミナルって使いますか？

<div style="display:flex">
  <img src="/terminal-01.png" />
  <img src="/terminal-02.png" />
</div>

Terminal, iTerm2, Wrap, wezterm, alacritty, kitty, IDEのターミナル...

<style>
img {
  width: 50%;
  padding: 16px;
  object-fit: contain;
}
</style>

---

# コマンドの実行

Git の操作

```bash
git checkout -t feature/auth
```

デプロイ
```bash
fab dev deploy:feature/auth
```

スクリプトの実行
```bash
npm run dev
```

---

# コマンドの実行が...

Git の操作
```bash
igt checkout -t feature/auth
```

デプロイ
```bash
fab dev drploy:feature/auth
```

スクリプトの実行
```bash
mpm run dev
```

## タイポぉぉぉぉ

---
layout: intro
---

## タイピングの回数が減ればタイポが減る

---
layout: intro
---

## タイピングを減らすためには？？

---

## 1. 補完を使う
　
## 2. 手順書からコマンドをコピペで実行する
　
## 3. 長いコマンドをまとめたスクリプトを実行する

---
layout: intro
---

# 実行履歴からコマンドを検索して実行する

---

# interactive filtering tool

## fzf

https://github.com/junegunn/fzf

## peco

https://github.com/peco/peco

---

# 次世代のツールを使う

## exa (ls)

https://github.com/ogham/exa

## ripgrep (grep)

https://github.com/BurntSushi/ripgrep

## bat (cat)

https://github.com/sharkdp/bat

## fd (find)

https://github.com/sharkdp/fd

--- 

# お便利ツールを使う

## ghq (git)

https://github.com/x-motemen/ghq

## zoxide　(cd)

https://github.com/ajeetdsouza/zoxide

## asdf　(ooEnv)

https://github.com/asdf-vm/asdf

--- 

# これらのツールのセットアップを助けてくれるツール

## Homebrew

https://github.com/Homebrew/brew

-> Brew Bundle

## mackup (設定ファイルの同期)

https://github.com/lra/mackup
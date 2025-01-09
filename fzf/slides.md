---
# You can also start simply with 'default'
theme: seriph
# some information about your slides (markdown enabled)
title: fzf
info:
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# fzf

---

# What is fzf?

fzf is a general-purpose command-line fuzzy finder.

fuzzy finder 「あいまい検索」
Intellij のshift shift のようなもの

単体で使うこともできるがgit やpackage.json と組み合わせて便利になる

---

# 注意


今回の内容は個人の環境をできるだけ変更しないように進めます  
ターミナルのタブは閉じないように気をつけてください  
何箇所か.zshrc などに記述する箇所がありますが、環境を今のまま保ちたい方は見ているだけにしてください

---

# とりあえずインストール

```bash
brew install fzf
```

https://github.com/junegunn/fzf

---

# fzf を実行してみる

```bash
fzf
```

---

# 別のコマンドを組み合わせてfzf を実行してみる

```bash
find * -type f | fzf > selected
```

`find * -type f` で現在のディレクトリ以下にあるフォルダ一覧を取得して、`|`（パイプ）でfzf に渡して「あいまい検索」を行う

- カーソルの移動は上下の矢印キー or ctrl-k, ctrl-j
- Enter で決定
- ctrl-c, ctrl-g, ecs で終了

```
cat package.json | jq -r '.scripts | keys[] ' | sort | fzf
```

package.json のscripts を取得して実行可能なスクリプトを表示する  
（実行するにはnpm run などに値を渡す必要があります）  
npmだったりyarnだったりpnpm のプロジェクトがある場合には ni を使うとどの環境でも動作させられます    
（fab でも使えたら便利だと思ったが、まだできていない。fab --shortlist 使うとタスクは取れるので、１つで良ければ実行まではできる。fzf を環境、実行を選ぶようなスクリプトにしたらできそう）

---

# シェル統合を試してみる-1

コマンドラインで各々使用しているシェルに合わせてコマンドを実行してください

## zsh

```bash
source <(fzf --zsh)
```

## bash

```bash
eval "$(fzf --bash)"
```

## fish

```bash
fzf --fish | source
```

---

# シェル統合を試してみる-2

- ctrl-t
  -  ファイル、ディレクトリ検索
- ctrl-r
  - コマンド履歴(history)検索
- alt-c
  - フォルダ検索 + ディレクトリ移動

キーバインドがぶつかって動作しない場合があります。

---

# シェル統合を試してみる-3

cd できる先を選ぶ

```bash
cd **<TAB>
```

vim で開くファイルを選ぶ

```bash
vim **<TAB>
```

ssh する先を選ぶ

```bash
ssh **<TAB>
```

---

# ghq を合わせてgit を便利にする

ghq とはgit のリポジトリを管理するツール

## とりあえずインストール
```bash
brew install ghq
```

---

# リポジトリを取得

```bash
ghq get torico-tokyo/torico_id_login
```

ghq には　get（取得）、　list（一覧表示）、　rm (ローカルのリポジトリの削除)などができる

---

# fzf と組み合わせてみる

ghq list で表示したリポジトリ一覧から選択してcd する

```bash
cd $(ghq list -p | fzf)
```

ghq list -p でフルパスで表示されるので簡単にcd できる

ブランチを切り替える
```bash
git switch $(git branch | fzf)
```

---

# 関数とキーバインドを組み合わせてショートカットでブランチの切り替えを行う（ファイル書き込みあり）

```
vim ~/.zshrc
```

```bash
function ghq-fzf() {
  local src=$(ghq list | fzf --preview "cat $(ghq root)/{}/README.*")
  if [ -n "$src" ]; then
    BUFFER="cd $(ghq root)/$src"
    zle accept-line
  fi
  zle -R -c
}
```

`:qw` で保存して終了

```bash
source ~/.zshrc
ghq-fzf
```

と入力してEnter を押す

---

# ブランチを切り替える（ファイル書き込みあり）

```bash
vim ~/.zshrc
```


```bash
function git-branches-fzf() {
  local branch=$(
    git branch -a |
    fzf --preview="echo {} | tr -d ' *' | xargs git plog --color=always" |
    head -n 1 |
    perl -pe "s/\s//g; s/\*//g; s/remotes\/origin\///g"
  )
  if [ -n "$branch" ]; then
    BUFFER="git switch $branch"
    zle accept-line
  fi
  zle -R -c
}
```

`:qw` で保存して終了

```bash
source ~/.zshrc
git-branches-fzf
```

---

# ショートカット登録する（ファイル書き込みあり）


```bash
vim ~/.zshrc
```

```bash
zle -N ghq-fzf
bindkey '^g' ghq-fzf
```

`:qw` で保存して終了

ctrl-g でghq-fzf を実行できる

zle（Zsh Line Editor） とはキーバインディングの管理や入力補完ができるツール

---

# fzf, ghq のアンインストール

使わない方は下記のコマンドでアンインストールしてお掃除してください

```bash
brew uninstall fzf ghq
```

---
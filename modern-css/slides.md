---
# try also 'default' to start simple
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
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# duration of the presentation
duration: 35min
---

# モダンCSS　2025ver

---

## 中央寄せはどうやる？？

![中央寄せはどうやる？？](/center.png)

```html
<body>
  <div class="flex items-center bg-red-400 min-h-25">
    <button class="bg-blue-400">ok</button>
  </div>
</body>
```

---

## Flexboxを使う

```html
<style>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
```

### Tailwind CSSを使うと

```html
<body>
  <div class="bg-red-400 min-h-25 flex items-center justify-center">
    <button class="bg-blue-400">ok</button>
  </div>
</body>
```

---

## Gridを使う

grid を使うと2つのクラスで中央寄せができる

```html
<style>
.container {
  display: grid;
  place-items: center;
}
</style>
```

### Tailwind CSSを使うと

```html
<body>
  <div class="bg-red-400 min-h-25 grid place-content-center">
    <button class="bg-blue-400">ok</button>
  </div>
</body>
```

---
layout: image-left

image: /subgrid.png
---

## 商品カードどうやって作る??

- タイトルは長い短いがある
- 発売日や価格が未定の商品が混ざる

などで要素数が合わない・高さがことなる事がある

---

## 各要素に高さを指定して揃える

```html
<style>
.card {
  height: 300px;
}

.title {
  height: 50px;
}
.price {
  height: 30px;
}
</style>
```

---

## subgrid を使う

```html

```

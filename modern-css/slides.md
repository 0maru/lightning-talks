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

### 垂直方向の縦寄せ

align-content:center で縦に寄せることができる

```html
<body>
  <div class="bg-red-400 min-h-25 content-center">
    <button class="bg-blue-400">ok</button>
  </div>
</body>
```

---

### position の指定どうやる？

```css
.overlay {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
```

は４行でかける

---

### inset を使う

```css
.overlay {
  position: absolute;
  inset: 0;
}
```

がすべてに0を指定していたものと同じ。  
0は1でも２何でも好きな数字にできる

---

### 要素がある、なしでスタイルが変わる

コーポレートサイトのサービス一覧ページとか  
css をif の条件で切り分ける

---

### :has() 擬似クラスを使う

```html
<body>
</body>
<style>
.card:has(.image) {
  border-color: green;
}
</style>
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

微調整多くなるし、要素が無い箇所とか考えたりすると難しい...

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

## Subgrid を使う

```html
<style>
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 16px;
}

.card {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 4;
}
</style>
```

---

### カルーセルはどうやって実装する？？

#### カルーセルの実装案

swiper などのライブラリを使う？？  
JSで簡易的なものを作る

---

### CSS Scroll Snap で実装する

css の scroll-snap-type を使うと簡単にカルーセルが実装できる
漫画全巻のビューアがscroll snapで実装されている

```html
<style>
  .carousel {
    display: flex;
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    scroll-behavior: smooth;
    gap: 1rem;
    scrollbar-width: none;
  }

  .carousel::-webkit-scrollbar {
    display: none;
  }

  .carousel-item {
    scroll-snap-align: start;
    scroll-snap-stop: always;
    flex: 0 0 100%;
  }
</style>
```

---

### diaglo はどうやって実装する??

#### 実装案

nuxt, next はらv-show とかv-if で表示して、div にinset-0 とか指定して実装？？
hidden にしていたのをabsolute にして表示？？

---

### dialog 要素を使う

document.getElementById('dialog のID').showModal() でモーダル表示できる  
this.closest('dialog').close() で閉じることができる

---

### 実装例

```html
<style>
dialog::backdrop {
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(4px);
}

/* アニメーション */
dialog[open] {
  animation: slideIn 0.3s ease-out;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
```

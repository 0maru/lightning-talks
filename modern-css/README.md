# モダンCSS　2025ver

subgrid のやつ

```html
<!DOCTYPE html>
<html lang="ja">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
  <title>modern css</title>
</head>

<body>
  <main class="flex gap-8">
    <div class="w-30">
      <img src="https://ebook.mangazenkan.com/pubridge/BT0000206277/005/cover.jpg" />
      <p>アカメが斬る！5巻</p>
      <button class="bg-sky-400 text-white">
        カートに入れる
      </button>
    </div>
    <div class="w-30">
      <img src="https://ebook.mangazenkan.com/pubridge/BT0000484849/006/cover.jpg" />
      <p>とんでもスキルで異世界放浪メシ 6</p>
      <button class="bg-sky-400 text-white">
        カートに入れる
      </button>
    </div>
    <div class="w-30">
      <img
        src="https://dip6t338iqjb9.cloudfront.net/image/resize/?quality=90&width=260&url=/upload/save_image/567/M8190470056_detail.jpg&12" />
      <p>デッドデッドデーモンズデデデデデストラクション (1-12巻 全巻)</p>
      <button class="bg-sky-400 text-white">
        カートに入れる
      </button>
    </div>
  </main>
</body>

</html>
```

subgrid

```html
<!DOCTYPE html>
<html lang="ja">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
  <title>modern css</title>
</head>

<body>
  <main class="grid grid-cols-12 gap-8">
    <div class="col-span-2 grid grid-rows-subgrid row-span-4 gap-2">
      <img class="w-40" src="https://ebook.mangazenkan.com/pubridge/BT0000206277/005/cover.jpg" />
      <p>アカメが斬る！5巻</p>
      <p>1000円</p>
      <button class="h-10 bg-sky-400 text-white">
        カートに入れる
      </button>
    </div>
    <div class="col-span-2 grid grid-rows-subgrid row-span-4 gap-2">
      <img class="w-40" src="https://ebook.mangazenkan.com/pubridge/BT0000484849/006/cover.jpg" />
      <p>とんでもスキルで異世界放浪メシ 6</p>
      <p></p>
      <button class="h-10 bg-sky-400 text-white">
        カートに入れる
      </button>
    </div>
    <div class="col-span-2 grid grid-rows-subgrid row-span-4 gap-2">
      <img class="w-40"
        src="https://dip6t338iqjb9.cloudfront.net/image/resize/?quality=90&width=260&url=/upload/save_image/567/M8190470056_detail.jpg&12" />
      <p>デッドデッドデーモンズデデデデデストラクション (1-12巻 全巻)</p>
      <p></p>
      <button class="h-10 bg-sky-400 text-white">
        カートに入れる
      </button>
    </div>
  </main>
</body>

</html>
```

CSS Scroll Snap

```html
<!DOCTYPE html>
<html lang="ja">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
  <title>modern css</title>
</head>

<body>
  <div class="carousel">
    <div class="carousel-item bg-red-500 h-64 flex items-center justify-center text-white text-2xl">Item 1</div>
    <div class="carousel-item bg-green-500 h-64 flex items-center justify-center text-white text-2xl">Item 2</div>
    <div class="carousel-item bg-blue-500 h-64 flex items-center justify-center text-white text-2xl">Item 3</div>
    <div class="carousel-item bg-yellow-500 h-64 flex items-center justify-center text-white text-2xl">Item 4</div>
    <div class="carousel-item bg-purple-500 h-64 flex items-center justify-center text-white text-2xl">Item 5</div>
  </div>

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
</body>

</html>
```

has()

```html
<!DOCTYPE html>
<html lang="ja">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
  <title>modern css</title>
</head>

<body>
  <div class="card has-[img.image]:bg-yellow-200 p-4 border m-4">
    <p>カード</p>
    <img class="image w-30" src="https://img.mangaoh.jp/img/product/_w600/826/826648_w600.jpg" />
  </div>
  <div class="card">
    <p>カード2</p>
  </div>
</body>

</html>
```

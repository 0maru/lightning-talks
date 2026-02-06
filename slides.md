---
marp: true
theme: custom
paginate: true
backgroundColor: #0f172a
color: #f1f5f9
---

<style>
/* カスタムテーマ */
section {
  font-family: 'Noto Sans JP', 'Arial', sans-serif;
  padding: 40px 60px;
}

h1 {
  color: #f1f5f9;
  font-size: 2.2em;
  margin-bottom: 0.5em;
}

h2 {
  color: #94a3b8;
  font-size: 1.4em;
}

code {
  background: #1e293b;
  color: #22d3ee;
  padding: 2px 8px;
  border-radius: 4px;
}

pre {
  background: #1e293b;
  border-radius: 8px;
  padding: 16px;
}

/* Era colors */
.spa { color: #f59e0b; }
.ssr { color: #8b5cf6; }
.isr { color: #10b981; }
.accent { color: #3b82f6; }

/* Badge */
.badge {
  display: inline-block;
  background: #3b82f6;
  color: #fff;
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 0.7em;
  font-weight: bold;
}

/* Card */
.card {
  background: #1e293b;
  border-radius: 12px;
  padding: 20px;
  margin: 10px 0;
}

/* Timeline bar */
.timeline-bar {
  display: flex;
  height: 6px;
  border-radius: 3px;
  overflow: hidden;
  margin: 20px 0;
}

/* Table styling */
table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.85em;
}

th {
  background: #334155;
  padding: 12px;
  text-align: center;
}

td {
  background: #1e293b;
  padding: 10px 12px;
  text-align: center;
  border-bottom: 1px solid #334155;
}

/* Title slide */
section.title {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

section.title h1 {
  font-size: 2.8em;
  line-height: 1.2;
}
</style>

<!-- _class: title -->

# Webキャッシュ戦略の<br>変遷を理解する

<p class="accent" style="font-size: 0.9em; margin-top: 20px;">SPA → SSR → ISR/Edge</p>

<div class="timeline-bar" style="position: absolute; bottom: 100px; left: 60px; right: 60px;">
  <div style="flex: 1; background: #f59e0b;"></div>
  <div style="flex: 1; background: #8b5cf6;"></div>
  <div style="flex: 1; background: #10b981;"></div>
</div>

<p style="color: #64748b; font-size: 0.6em; position: absolute; bottom: 40px; right: 60px;">TECH LT • 2025.01</p>

---

# アジェンダ

<div style="display: grid; gap: 20px; margin-top: 20px;">

<div style="display: flex; gap: 16px; align-items: flex-start;">
  <div style="background: #f59e0b; color: #0f172a; width: 40px; height: 40px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; flex-shrink: 0;">1</div>
  <div>
    <p style="margin: 0; font-weight: bold;">SPA時代（2013〜2018）</p>
    <p style="margin: 0; color: #94a3b8; font-size: 0.85em;">クライアントサイドレンダリングとimmutableアセット戦略</p>
  </div>
</div>

<div style="display: flex; gap: 16px; align-items: flex-start;">
  <div style="background: #8b5cf6; color: #fff; width: 40px; height: 40px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; flex-shrink: 0;">2</div>
  <div>
    <p style="margin: 0; font-weight: bold;">SSR/Jamstack時代（2016〜2019）</p>
    <p style="margin: 0; color: #94a3b8; font-size: 0.85em;">サーバーサイドレンダリング回帰と静的サイト生成</p>
  </div>
</div>

<div style="display: flex; gap: 16px; align-items: flex-start;">
  <div style="background: #10b981; color: #fff; width: 40px; height: 40px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; flex-shrink: 0;">3</div>
  <div>
    <p style="margin: 0; font-weight: bold;">ISR/Edge時代（2020〜現在）</p>
    <p style="margin: 0; color: #94a3b8; font-size: 0.85em;">stale-while-revalidateとEdge Computeの活用</p>
  </div>
</div>

<div style="display: flex; gap: 16px; align-items: flex-start;">
  <div style="background: #3b82f6; color: #fff; width: 40px; height: 40px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; flex-shrink: 0;">4</div>
  <div>
    <p style="margin: 0; font-weight: bold;">まとめ</p>
    <p style="margin: 0; color: #94a3b8; font-size: 0.85em;">各時代の比較と今後の展望</p>
  </div>
</div>

</div>

---

<!-- _header: '<span class="badge" style="background: #f59e0b; color: #0f172a;">ERA 1</span>' -->

# <span class="spa">SPA時代</span>（2013〜2018）

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 20px;">

<div>

### 背景

React（2013）、Vue（2014）の登場により、クライアントサイドでUIを構築するSPAが主流に

### 主な技術スタック

`React` `Vue.js` `Angular` `webpack` `REST API`

</div>

<div class="card">

### アーキテクチャ

```
┌─────────────────────────┐
│  Browser                │
│  ├─ React/Vue           │
│  ├─ Router              │
│  └─ State (Redux/Vuex)  │
└───────────┬─────────────┘
            │ API Request
            ▼
┌─────────────────────────┐
│  Server                 │
│  ├─ Empty HTML Shell    │
│  └─ JSON API            │
└─────────────────────────┘
```

</div>

</div>

---

# SPA時代のキャッシュ戦略

<div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; margin-top: 20px;">

<div class="card" style="border-top: 3px solid #ef4444;">

### index.html
空のシェル - キャッシュ短め

```http
Cache-Control: no-cache
```

</div>

<div class="card" style="border-top: 3px solid #10b981;">

### app.[hash].js
content hash付き - 永続キャッシュ

```http
Cache-Control: 
max-age=31536000, immutable
```

</div>

<div class="card" style="border-top: 3px solid #3b82f6;">

### API Response
動的データ

```javascript
// Redux/Vuex で
// メモリキャッシュ
```

</div>

</div>

<div class="card" style="border-left: 4px solid #f59e0b; margin-top: 20px;">

### 💡 Service Worker の登場（2015〜）

ブラウザ側でプログラマブルなキャッシュ制御が可能に。Cache-First / Network-First などの戦略を **Workbox** で実装

</div>

---

# SPA時代の課題

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 20px;">

<div>

<div class="card" style="border-left: 4px solid #ef4444; margin-bottom: 16px;">

### ⚠️ 初回表示の遅さ

JSバンドルのダウンロード・パース・実行が完了するまでコンテンツが表示されない

</div>

<div class="card" style="border-left: 4px solid #ef4444;">

### ⚠️ SEO問題

クローラーがJSを実行できないとコンテンツを認識できない。OGP取得も困難

</div>

</div>

<div class="card">

### レンダリングフロー

```
1. 空のHTML受信
      ↓
2. JS/CSSダウンロード
      ↓
3. JSパース・実行
      ↓
4. APIデータ取得
      ↓
5. コンテンツ表示 ✓
```

🐢 ユーザーはここまで待つ必要あり

</div>

</div>

---

<!-- _header: '<span class="badge" style="background: #8b5cf6;">ERA 2</span>' -->

# <span class="ssr">SSR/Jamstack時代</span>（2016〜2019）

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 20px;">

<div>

### なぜSSRが復活したか

SPAの「初回表示の遅さ」「SEO問題」を解決するため、サーバーでHTMLを生成して返す方式が再注目

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-top: 16px;">

<div class="card" style="border: 1px solid #8b5cf6; padding: 14px;">
<p class="ssr" style="margin: 0; font-weight: bold; font-size: 0.9em;">SSR</p>
<p style="margin: 4px 0 0 0; font-size: 0.8em;">リクエスト毎にサーバーでレンダリング</p>
<p style="margin: 8px 0 0 0; font-size: 0.7em; color: #94a3b8;">Next.js / Nuxt.js</p>
</div>

<div class="card" style="border: 1px solid #10b981; padding: 14px;">
<p class="isr" style="margin: 0; font-weight: bold; font-size: 0.9em;">SSG (Jamstack)</p>
<p style="margin: 4px 0 0 0; font-size: 0.8em;">ビルド時に全ページを静的生成</p>
<p style="margin: 8px 0 0 0; font-size: 0.7em; color: #94a3b8;">Gatsby / Hugo</p>
</div>

</div>

</div>

<div class="card">

### SSR フロー
```
Request → [Server Render] → HTML
```

### SSG フロー
```
[Build] → Static HTML → [CDN] → User
```

### ✓ 解決されたこと

初回表示でコンテンツが含まれたHTMLが返る
→ **高速表示 & SEO対応**

</div>

</div>

---

# SSR/Jamstack時代のキャッシュ戦略

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 20px;">

<div class="card" style="border-top: 3px solid #8b5cf6;">

### SSRのキャッシュ課題

**問題点**: リクエスト毎にレンダリング = 高負荷

**対策**:
- Varyヘッダーでのキャッシュ分岐
- ページ単位での短いTTL設定
- パーソナライズ部分のみCSR

</div>

<div class="card" style="border-top: 3px solid #10b981;">

### Jamstackの戦略

**シンプルな解決策**: 全ページをビルド時に生成してCDNに配置

**デプロイフロー**:
```
git push → Build → CDN Deploy → Purge
```

100%キャッシュヒット可能！

</div>

</div>

<div class="card" style="background: linear-gradient(90deg, rgba(59,130,246,0.1), transparent); border: 1px solid #3b82f6; margin-top: 16px; text-align: center;">

### CDNキャッシュの活用が本格化

`User` → `CDN Edge (Cache Hit!)` → ~~Origin~~

</div>

---

# SSR/Jamstack時代の課題

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 20px;">

<div class="card" style="border-top: 3px solid #8b5cf6;">

### SSRの課題

- ⚠️ **サーバー負荷** - リクエスト毎にレンダリング処理
- ⚠️ **TTFB悪化** - レンダリング完了まで待機
- ⚠️ **コスト** - 常時稼働のサーバーが必要

</div>

<div class="card" style="border-top: 3px solid #10b981;">

### Jamstackの課題

- ⚠️ **ビルド時間** - ページ数に比例して増加
- ⚠️ **更新頻度の制限** - 頻繁な更新には全ビルド
- ⚠️ **動的コンテンツ** - パーソナライズに弱い

</div>

</div>

<div class="card" style="border: 1px solid #ef4444; background: rgba(239,68,68,0.1); margin-top: 16px;">

### 💡 ECサイトでの問題例

商品数が **10万点** あるECサイトでは、1商品の価格変更のために全ページを再ビルドするのは現実的ではない

</div>

<p style="text-align: center; margin-top: 16px; color: #94a3b8;">これらの課題を解決するために... → <span class="isr" style="font-weight: bold;">ISR/Edgeの登場</span></p>

---

<!-- _header: '<span class="badge" style="background: #10b981;">ERA 3</span>' -->

# <span class="isr">ISR/Edge時代</span>（2020〜現在）

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 20px;">

<div>

<div class="card" style="border-left: 4px solid #10b981; margin-bottom: 16px;">

### ISR（Incremental Static Regeneration）

Next.js 9.5（2020年7月）で導入。静的生成の高速さとSSRの鮮度を両立

</div>

<div class="card" style="margin-bottom: 16px;">

### stale-while-revalidate パターン

```http
Cache-Control: 
max-age=1, stale-while-revalidate=59
```

古いキャッシュを即座に返しつつ、バックグラウンドで再生成

</div>

<div class="card">

### Edge Computeの成熟

`Cloudflare Workers` `Vercel Edge` `CloudFront Functions`

</div>

</div>

<div class="card">

### ISR の動作フロー

**1. 初回アクセス**
オンデマンドで生成 → キャッシュ保存

**2. 2回目以降**
キャッシュから即座にレスポンス

**3. revalidate時間経過後**
古いキャッシュを返却（ユーザーは待たない）

**4. バックグラウンド再生成**
次回アクセス時は新しいコンテンツ

---

🚀 **ユーザーは常に即座にレスポンスを受け取る**

</div>

</div>

---

# 現代のキャッシュ戦略

<div class="card" style="text-align: center; padding: 16px; margin-bottom: 16px;">

### 多層キャッシュアーキテクチャ

`Browser (Service Worker)` → `Edge / CDN (KV Store / ISR)` → `Origin (Redis / DB)`

</div>

<div style="display: grid; grid-template-columns: 2fr 1fr; gap: 16px;">

<div>

### コンテンツ別キャッシュ戦略

| コンテンツ | 戦略 | TTL例 |
|---|---|---|
| 静的アセット | immutable | 1年 |
| 商品一覧 | ISR | 60秒 |
| 商品詳細 | SWR | 1秒 + 59秒 |
| カート・決済 | no-store | キャッシュなし |

</div>

<div class="card">

### Edgeでできること

- ✓ キャッシュキー制御
- ✓ A/Bテスト
- ✓ 認証チェック
- ✓ 地域別コンテンツ
- ✓ Bot検出

</div>

</div>

---

# 時代の比較

|  | <span class="spa">SPA</span> | <span class="ssr">SSR/SSG</span> | <span class="isr">ISR/Edge</span> |
|---|:---:|:---:|:---:|
| キャッシュ対象 | JS/CSSアセット | 静的HTML全体 | 動的HTML + Edge処理 |
| 初回表示速度 | △ 遅い | ○ 普通〜速い | ◎ 常に高速 |
| 更新反映 | ◎ 即時（API経由） | △ 再ビルド必要 | ◎ 自動再生成 |
| SEO | △ 要対策 | ◎ 良好 | ◎ 良好 |
| オリジン負荷 | ○ API負荷あり | ○ SSRは高負荷 | ◎ Edgeで分散 |
| 実装複雑さ | ○ シンプル | ○ やや複雑 | △ 設計が重要 |

<div class="card" style="border: 1px solid #3b82f6; background: rgba(59,130,246,0.1); text-align: center; margin-top: 16px;">

💡 ISRは「過去の手法の良いとこ取り」をフレームワークが抽象化したもの

</div>

---

# まとめ

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-top: 20px;">

<div class="card" style="border-left: 4px solid #3b82f6;">

### キャッシュ戦略の進化

「静的 vs 動的」の二択から、ISR/SWRで両方の利点を得られる時代に。キャッシュの設計次第でUXとコストを大きく改善可能

</div>

<div class="card" style="border-left: 4px solid #10b981;">

### Edgeの活用

単なるキャッシュから「処理もできるエッジ」へ。Core Web Vitals対応、オリジン負荷軽減、コスト削減の鍵

</div>

</div>

<div class="card" style="margin-top: 20px;">

### 🚀 明日から試せること

1. コンテンツごとのキャッシュTTLを見直す
2. stale-while-revalidateの導入検討
3. Nuxt 3 Hybrid Renderingの検証
4. CloudFront Functions活用の検討

</div>

<p style="text-align: center; margin-top: 30px; color: #94a3b8;">— ご質問・ディスカッション —</p>

---

<!-- _class: title -->
<!-- _paginate: false -->

# Thank You!

<p style="color: #94a3b8; font-size: 0.8em; margin-top: 40px;">参考: Next.js Docs, Vercel Blog, Cloudflare Docs, web.dev</p>

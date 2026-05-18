# HVILE — design-furniture-nordic Spec

**Status:** Approved  
**Author:** torifo  
**Created:** 2026-05-19  
**Updated:** 2026-05-19

---

## 1. Overview

### Problem Statement
北欧インテリアに共感するデザイン志向の大人（30–45歳）が訪れる家具店サイトは「清潔感はあるがどこも同じ」か「オシャレすぎて購入導線が弱い」かに分かれており、静謐さと購買意欲を両立するデザインは少ない。

### Goal
"Hvile"（ノルウェー語：安らぎ）という架空の北欧家具店のランディングページを実装し、Kinfolk誌的エディトリアル余白・Cormorant Garamondの品格・暖色ベースライトテーマが生む「選ばれた静けさ」を検証する。

### Non-Goals
- カート・決済機能
- CMS連携
- ユーザー認証

### Background
- HVILEは本デザイン研究のために作成した架空ブランドであり、実在のブランド・店舗・商品ではない
- `design-furniture-nordic` リポジトリ予定
- apparelシリーズとは別カテゴリ（家具）の研究第1作

---

## 2. Persona

| 属性 | 詳細 |
|------|------|
| 年齢 | 30–45歳 |
| 志向 | デザイン意識が高い、素材と機能美を重視 |
| 購買姿勢 | 長く使えるものへの投資として家具を選ぶ |
| 共鳴する価値 | サステナビリティ、職人技、自然素材、静けさ |
| 嫌うもの | 過剰な情報、装飾的すぎるUI、コピペ的スカンジナビアデザイン |

---

## 3. User Stories

| ID | Persona | Want to | So that |
|----|---------|---------|---------|
| US-01 | 北欧ライフスタイル層 | 開いた瞬間にブランドの哲学と品格を感じたい | 「自分の美意識に合う」と確信できる |
| US-02 | 同上 | 商品を生活シーンの中で確認したい | 実際の空間に置いた時のイメージができる |
| US-03 | 同上 | ブランドの素材哲学を知りたい | 購入の判断基準として使える |
| US-04 | 同上 | PCでもモバイルでも同じ静謐感を得たい | デバイスに関わらず体験が一貫している |

---

## 4. Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | ページロードアニメーション（ダーク背景×セリフブランド名） | P0 |
| FR-02 | SVG grain固定オーバーレイ（opacity 0.025、ウッドテクスチャ感） | P0 |
| FR-03 | カスタムカーソル（ウォームドット+追従リング） | P0 |
| FR-04 | スプリットヒーロー（左：エディトリアルテキスト、右：北欧インテリア写真） | P0 |
| FR-05 | 商品グリッド（12カラムアシンメトリック、4商品） | P0 |
| FR-06 | マーキー（素材キーワード、セリフ体、スロー） | P1 |
| FR-07 | フィロソフィーセクション（ダーク背景、大型引用、縦書きラベル） | P1 |
| FR-08 | マテリアルセクション（2×2グリッド、画像オーバーレイ） | P1 |
| FR-09 | フィーチャーストリップ（3カラム） | P2 |
| FR-10 | スクロールリビールアニメーション | P1 |
| FR-11 | ナビ（スクロールでbg+blur） | P0 |
| FR-12 | モバイルファースト対応（375px基準） | P0 |

---

## 5. Design System

### Color Palette
```css
--bg:        #F7F3ED;   /* ウォームリネン */
--bg-sub:    #F0E9DF;   /* やや深いクリーム */
--bg-dark:   #1C1915;   /* 暗い木炭（ダークセクション） */
--fg:        #1A1712;   /* リッチチャコール */
--fg-muted:  #8B7A69;   /* ウォームミュート */
--fg-light:  #C4B5A5;   /* ライトトーン */
--border:    #D8CEBC;   /* サトル境界線 */
--accent:    #3A5537;   /* ディープノルディックセージ */
--warm:      #B5703A;   /* ウォームオーク（ドット・アクセント） */
```

### Typography
```css
--font-serif: 'Cormorant Garamond', Georgia, serif;   /* エディトリアル品格 */
--font-sans:  'Outfit', sans-serif;                   /* ジオメトリッククリーン */
```
- Google Fonts CDN: Cormorant Garamond, Outfit

### Motion
```css
--ease:     cubic-bezier(0.25, 0.46, 0.45, 0.94);
--ease-out: cubic-bezier(0.16, 1, 0.3, 1);
/* hero: slideUp 1s stagger 0.15s */
/* reveal: fade+translate 0.9s */
/* cursor ring: lag 0.1 (RAF loop) */
/* image settle: scale 1.05→1 over 8s */
```

---

## 6. Architecture

```
index.html
├── .loader              # ダーク背景×セリフ名×垂直ライン
├── .grain               # SVG noise fixed overlay
├── .cursor-dot / .cursor-ring
├── nav                  # ロゴ左、リンク右
├── .hero                # 2カラムスプリット
│   ├── .hero-left       # 見出し・CTA
│   └── .hero-right      # インテリア写真
├── .section#collection  # 商品グリッド
├── .marquee-wrap        # 素材マーキー
├── .philosophy          # ダーク引用セクション
├── .section#materials   # 2×2マテリアルグリッド
├── .features            # 3カラムストリップ
└── footer
```

---

## 7. Key Design Decisions

| Decision | Chosen | Rationale |
|----------|--------|-----------|
| テーマ | ライト（ウォームリネン） | 北欧の自然光・木材感を体現 |
| ヒーロー | スプリット2カラム | Kinfolk的エディトリアル感。全面写真より静けさが出る |
| Display font | Cormorant Garamond | 品格×エディトリアル。セリフで素材感と長さを表現 |
| Body font | Outfit | ジオメトリックで清潔感。Inter/DM Sansを避けた |
| アクセント | ディープセージ #3A5537 | 北欧の森・自然への参照。ライムやレッドを避けた |
| サブアクセント | ウォームオーク #B5703A | 木材・テラコッタ。カーソルドット・セクション詳細 |
| フィロソフィー | ダーク背景反転 | ライト背景から反転してリズムを作る |
| Grain | opacity 0.025 | ウッドテクスチャ的質感。主張しすぎない |

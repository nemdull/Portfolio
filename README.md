# ポートフォリオ集（静的サイト）

本リポジトリは、静的なWeb制作物のポートフォリオ集です。個人ポートフォリオの「Website」と、企業LPを想定したUIデモ「TheCompany」を含みます。いずれも素の HTML/CSS/JavaScript で構成されています。

## プロジェクト概要

- `Website`: 個人ポートフォリオサイト（トップ/Portfolio/About/Contact）。基本レイアウトとモバイル向けメディアクエリ対応を含む。
- `TheCompany`: 企業LP想定のUIデモ。スライダーやスクロールアニメーション、ニュースリスト、料金表、アクセス（Google マップ埋め込み）、問い合わせフォームUIを実装。

## 技術スタック

- 言語: HTML, CSS, JavaScript（バンドラ/ビルドツールなし）
- ライブラリ（同梱/参照）:
  - Swiper 4.5.0（タッチスライダー）: `TheCompany/js/swiper.js`, `TheCompany/CSS/swiper.css`
  - WOW.js 1.1.3（スクロールアニメーション）: `TheCompany/js/wow.min.js`, `new WOW().init()` を `index.html` 下部で実行
  - animate.css（アニメーションクラス）: `TheCompany/CSS/animate.css`
  - Google Fonts（Bitter）: `Website/portfolio.html` で参照
  - Google Maps 埋め込み iframe: `TheCompany/index.html` の Access セクション
- 画像/アセット: `Website/images/*`, `TheCompany/images/*`

## 主な機能

- ナビゲーション: 固定ヘッダー内のアンカーリンクで各セクションへ移動（`TheCompany/index.html`）。
- ヒーローセクション: Swiper 用マークアップを実装（初期化スクリプトの追加で動作）。
- スクロールアニメーション: `wow` クラス＋`animate.css` により各要素が段階的に表示。
- コンテンツセクション: Card（カードグリッド）、News（ニュース一覧）、Price（料金表）、Access（地図/住所）、Contact（問い合わせUI）。
- ポートフォリオ表示: `Website/portfolio.html` に制作物サムネイルと説明を配置。
- レスポンシブ対応（Website）: `@media (max-width: 600px)` によるスマホ最適化（ナビ/レイアウト調整）。

## 設計・実装の工夫（読み取れる点）

- 素の HTML/CSS による段組・余白設計と、セクションごとの ID/クラス設計。
- `Website/css/style.css` にレスポンシブ用のメディアクエリを集約し、主要レイアウトを簡潔に制御。
- 同一アセット規約（画像ディレクトリ、CSS/JS の分離）で、2プロジェクトともに構造が明瞭。
- WOW.js＋animate.css を用いた、直感的なクラス設計でのアニメーション適用。

## セットアップ & 動作確認

ローカルで静的ファイルを開くだけで閲覧可能です。ブラウザのローカルファイル制限を避けたい場合は簡易サーバを使うと安全です。

- 方法A（直接開く）
  - `Website/index.html` をブラウザで開く
  - `TheCompany/index.html` をブラウザで開く

- 方法B（簡易サーバで配信）
  - リポジトリルートで実行: `python3 -m http.server 8000`
  - `http://localhost:8000/Website/index.html`
  - `http://localhost:8000/TheCompany/index.html`

動作確認の観点例:

- `TheCompany` の各セクション（Card/News/Price/Access/Contact）にナビから移動できるか。
- WOW.js によるアニメーションがスクロールで発火するか。
- `Website` のモバイル幅でのレイアウト崩れがないか（600px 以下）。
- Google マップの埋め込みが表示されるか（ネットワーク接続が必要）。

## 改善ポイント / TODO（リポジトリからの事実ベース）

設計/マークアップ

- 重複 ID の使用: `TheCompany/index.html` 内で `id="item"` が複数回使用（ID は一意にする）。
- ラベル/フォーム属性: `Contact` のラジオボタンに `name` が未設定、`id` と `for` による関連付けが未実装。
- フォーム挙動: action/method が未設定のため送信はダミー。入力検証/エラーメッセージも未実装。
- アクセシビリティ: 多くの `<img>` に `alt` が未設定。装飾画像は空 alt、意味のある画像は説明を付与。
- 外部リンク: `target="_blank"` を用いる場合は `rel="noopener noreferrer"` の付与を検討。

スタイル/レスポンシブ

- `TheCompany` は 1366px 固定幅の指定が多く、モバイル最適化が未実装。ブレークポイント設計と可変レイアウト化を推奨。
- 共通余白/タイポグラフィのスケール定義（CSS 変数）により再利用性を向上可。

挙動/JS

- Swiper 初期化の未実装: マークアップとライブラリは同梱されているが、`new Swiper('.swiper-container', { ... })` が未記述のためスライダーが動作しない。
- WOW.js 発火は実装済みだが、オフセット/デュレーション等の最適化余地あり。

パフォーマンス

- 画像の最適化（解像度/圧縮）と `loading="lazy"` の付与で初期表示を改善可。
- CSS/JS のミニファイ（`styles.css`/`swiper.css`）や不要コードの削減。

ドキュメント/運用

- GitHub Pages でのホスティング手順や、利用ライブラリのライセンス/出典の明記が未記載。
- CI/CD が未整備。HTML/CSS の Lint（例: `htmlhint`, `stylelint`）や Lighthouse レポートの自動化を検討。

テスト

- 自動テストは未実装。ビジュアルリグレッション（Percy 等）や Lighthouse のスコア監視を導入可能。

## ディレクトリ

- `Website/`: 個人ポートフォリオ（`index.html`, `about.html`, `contact.html`, `portfolio.html`, `css/style.css`, `images/*`）
- `TheCompany/`: 企業LP想定（`index.html`, `CSS/*.css`, `js/*.js`, `images/*`）

## 強調ポイント（本リポジトリで示しているスキル）

- 素の HTML/CSS/JS による UI 実装力（レイアウト、ナビ、ホバー、セクション設計）。
- アニメーション表現の導入（WOW.js＋animate.css）。
- 外部ライブラリの取り込み・統合（Swiper/Google Fonts/Google Maps）。
- レスポンシブ配慮（`Website` でのメディアクエリ適用）。

## 閲覧方法（クイック）

- `TheCompany/index.html`
- `Website/index.html`

必要に応じて簡易サーバ: `python3 -m http.server 8000`

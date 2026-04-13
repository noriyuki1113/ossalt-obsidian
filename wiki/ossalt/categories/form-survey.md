# フォーム・アンケート — OSSカテゴリ概要

> フォーム作成・アンケート収集・リード獲得。Typeform 代替として近年 OSS が充実してきたカテゴリ。

タグ: `#category` `#form` `#Typeform代替`
最終更新: 2026-04-13

---

## カテゴリ概要

フォームは「静的な問い合わせフォーム」から「対話型アンケート（Typeform 系）」「プロダクト内フィードバック収集」まで幅広い。SaaS の回答数課金モデルに不満を持つ層に OSS 代替が刺さる。

---

## 代表的 OSS ツール

| ツール | 特徴 | セルフホスト難易度 |
|---|---|---|
| Formbricks | プロダクト内サーベイ・Typeform 風のフロー作成 | 低〜中 |
| Typebot | チャットボット型フォーム・Typeform に近い UX | 低〜中 |
| Tally (OSS代替候補) | Notion 風のフォームビルダー（クラウドのみ） | — |
| Formie | PHP ベース・WordPress プラグインとしても使用可 | 中 |

---

## 代替する商用 SaaS

| 商用SaaS | 月額目安 | 主な差異 |
|---|---|---|
| Typeform | $25〜$83/月 | Formbricks / Typebot がセルフホストで代替 |
| SurveyMonkey | $25〜$75/月 | 機能は劣るが基本的な収集は OSS で十分 |
| Tally | $0〜$29/月 | Typebot がビジュアル的に近い |

---

## 典型的なユースケース

- SaaS プロダクト内のユーザーフィードバック収集（Formbricks）
- LP からリード獲得するための対話型フォーム（Typebot）
- カスタマーサポートチケット入力・問い合わせフォームの置き換え

---

## 収益化への示唆（ossalt.jp）

- **コンテンツ価値**: Typeform の価格が上がるたびに移行先検索が増える。タイムリーな比較記事が有効。
- **ビジネス機会**: Formbricks セットアップ代行 + SaaS プロダクトへの埋め込み実装サービス
- **訴求ポイント**: 「回答数無制限でゼロコスト」が中小企業・個人サイト運営者に響く

---

## 実装上の注意

- Formbricks は Next.js ベース。Vercel + Supabase で動かすパターンが安定している。
- Typebot は Node.js + PostgreSQL + S3 互換ストレージが必要。
- どちらもメール通知設定（SMTP）が必要なため、Resend との組み合わせを推奨。

---

## 関連ノート

- [wiki/ossalt/_index.md](../_index.md)
- [crm](./crm.md)
- [monitoring](./monitoring.md)

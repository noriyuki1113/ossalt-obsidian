# SaaS・マイクロSaaSアイデア — インデックス

自分が作るプロダクトのアイデア・設計・収益化・スタック。

---

## 戦略メモ

- **ターゲット市場**: 日本語市場 × インディーハッカー・スモールビジネス
- **収益化優先**: アイデア段階から収益モデルを定義する
- **スタック原則**: Lovable + Supabase + Stripe + Vercel を標準スタックとする
- **MVP 定義**: 課金が発生するまでの最小構成

---

## アイデアノート

| ノート | 状態 | 収益モデル |
|---|---|---|
| [AIニュース要約アプリ](./ideas/AIニュース要約アプリ.md) | MVP設計中 | サブスクリプション |

### 追加予定スロット
- `OSS比較ツール.md` — ossalt.jp の有料機能版
- `プロンプト管理SaaS.md` — チーム向けプロンプト資産管理

---

## MVP 候補

アイデアから MVP 設計に昇格したプロダクト。

| ノート | 目標MRR | 次のアクション |
|---|---|---|
| [AIニュース要約アプリ MVP](./mvp/AIニュース要約アプリ MVP.md) | ¥50,000（6ヶ月） | LP作成 → 事前登録50人 |

---

## 収益化パターン

> `wiki/apps/monetization/` 以下に作成予定

繰り返し使える収益化パターンをまとめる予定。

---

## スタック設計

> `wiki/apps/stack/` 以下に作成予定

採用技術の選定理由・ベストプラクティスをまとめる予定。

---

## 標準スタック

```
フロントエンド:  Next.js (Lovable生成) + Tailwind CSS
バックエンド:    Supabase (DB + Auth + Edge Functions)
決済:           Stripe
デプロイ:       Vercel
ドメイン:       Cloudflare
メール:         Resend
```

---

## 関連リンク

- [wiki/index.md](../index.md)
- [wiki/hot.md](../hot.md)
- [wiki/systems/_index.md](../systems/_index.md)
- [_templates/app-idea.md](../../_templates/app-idea.md)

---

*最終更新: 2026-04-13*

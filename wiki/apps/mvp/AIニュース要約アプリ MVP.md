# AIニュース要約アプリ — MVP 設計

> アイデアノート: [AIニュース要約アプリ](../ideas/AIニュース要約アプリ.md)

タグ: `#mvp` `#AIニュース` `#メール配信` `#状態:mvp設計`
最終更新: 2026-04-13

---

## 解く問題

AI関連ニュースは英語・大量・分散している。日本語圏のエンジニア・インディーハッカーが毎朝5分で要点を把握できるキュレーションメールが存在しない。

---

## ターゲットユーザー

- 日本語圏のインディーハッカー・副業エンジニア（30〜45歳）
- AIトレンドは気になるが英語を読む時間も気力もない層
- Morning Brew / TLDR などの日本語版に需要を感じている人

---

## MVP のゴール

**有料購読者 10人** が課金するところまで。機能の完成度より「価値の検証」を優先する。

---

## コア機能（作る）

| 機能 | 説明 |
|---|---|
| ニュース収集 | 主要 AI 系 RSS + 数ソースのスクレイピング。毎朝6時に自動実行 |
| LLM 要約生成 | Claude API で日本語要約 + 「インディーハッカーへの示唆」を生成 |
| メール配信 | 毎朝7時 JST に Resend で配信。HTML メール形式 |
| 登録フォーム | メール + パスワード登録。無料トライアル 14日間 |
| 課金 | Stripe Checkout。14日後に月額プランへの移行を促す |

## 除外（MVP では作らない）

- ウェブ上のアーカイブ閲覧 UI
- カテゴリフィルタ・パーソナライズ
- モバイルアプリ
- ソーシャルシェア
- 管理者ダッシュボード

---

## 画面構成（最小）

```
/                   ランディングページ
                    ヒーロー文 + メール登録CTA + 価格表

/signup             メール + パスワード登録フォーム

/dashboard          ログイン後の設定ページ（最小限）
                    - 配信状況の確認
                    - 解約ボタン

/billing            Stripe Customer Portal へのリダイレクト

/unsubscribe        ワンクリック解除（メール内リンクから）
```

---

## データモデル（概要）

```
users
  id, email, created_at, trial_ends_at, stripe_customer_id

subscriptions
  id, user_id, stripe_subscription_id, status, current_period_end

news_items
  id, title, url, source, published_at, summary_ja, implication_ja, created_at

digests
  id, sent_at, item_ids (jsonb)

digest_deliveries
  id, user_id, digest_id, delivered_at
```

RLS: `users` / `subscriptions` / `digest_deliveries` は自分のレコードのみ参照可。
詳細は [RLSパターン集](../../systems/supabase/RLSパターン集.md) を参照。

---

## 収益化

| 項目 | 内容 |
|---|---|
| モデル | 月額サブスクリプション |
| 価格 | ¥480/月（年払い ¥4,800） |
| 無料期間 | 14日間トライアル |
| MRR 目標（3ヶ月） | ¥10,000（約20人） |
| MRR 目標（6ヶ月） | ¥50,000（約100人） |

---

## 推奨スタック

```
フロントエンド:  Next.js (Lovable生成) + Tailwind CSS + shadcn/ui
バックエンド:    Supabase (DB + Auth + Cron via pg_cron)
LLM:            Claude API (claude-haiku-4-5)  ← コスト優先
メール配信:      Resend
決済:           Stripe
デプロイ:       Vercel
```

**コスト見積もり（月額、100ユーザー規模）**:
- Supabase Pro: $25/月
- Vercel Pro: $20/月
- Claude API: ~$5/月（毎日3件 × haiku）
- Resend: $0〜$20/月
- 合計: ~$50〜$70/月 → MRR ¥50,000 に対して十分な利益率

---

## 制約・リスク

| リスク | 対策 |
|---|---|
| LLM 要約品質が低い | 手動チェック期間を設ける。プロンプトチューニングを優先 |
| 配信到達率が低い | Resend + カスタムドメイン。SPF/DKIM 設定を最初に確認 |
| 大手が無料で始める | ニッチ（インディーハッカー視点）に特化して差別化 |
| チャーン率が高い | 開封率を毎週モニタリング。品質が命 |

---

## 次のアクション

- [ ] Lovable でランディングページを生成（[プロンプト設計ガイド参照](../../systems/lovable/Lovable完全プロンプト設計.md)）
- [ ] RSS 取得 + Claude 要約の Supabase Edge Function をプロトタイプ
- [ ] 手動で1週間配信して品質を確認（メール5〜10人に送る）
- [ ] Stripe 課金フローをテスト環境で通す
- [ ] 事前登録ページで50人集める

---

## 関連リンク

- [アイデアノート](../ideas/AIニュース要約アプリ.md)
- [wiki/apps/_index.md](../_index.md)
- [Lovable完全プロンプト設計](../../systems/lovable/Lovable完全プロンプト設計.md)
- [RLSパターン集](../../systems/supabase/RLSパターン集.md)

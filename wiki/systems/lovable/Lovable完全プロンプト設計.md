# Lovable 完全プロンプト設計

> **用途**: Lovable でフルスタック SaaS を高品質に生成するためのプロンプト構造ガイド

タグ: `#implementation` `#lovable` `#プロンプト設計`
最終確認: 2026-04-13

---

## 概要

Lovable はプロンプトだけでフロントエンド〜バックエンド統合まで生成できるAI開発ツール。しかし曖昧なプロンプトは曖昧なコードを生成する。このガイドは「Lovable が迷わない」プロンプトの構造を定義する。

**原則**: 決めることを全部プロンプトに書く。Lovable に判断させない。

---

## プロンプトの全体構造

```
1. プロダクトゴール
2. ターゲットユーザー
3. ページ構成
4. データスキーマ
5. 認証設計
6. 課金設計
7. Edge Functions / API
8. デザイン方向
9. 制約・除外事項
```

この順番で書くことで Lovable がコンテキストを正しく積み上げる。

---

## 1. プロダクトゴール

**悪い例**: 「ニュースアプリを作って」

**良い例**:
```
AIニュース要約サービスを作ってください。
ユーザーはメール登録し、毎朝AI関連ニュースの日本語要約を受け取ります。
無料トライアル2週間後にStripeで月額課金が始まります。
```

**ポイント**: What（何を）・Who（誰に）・How（どう届けるか）・When（いつ課金が発生するか）を含める。

---

## 2. ターゲットユーザー

```
ターゲット: 日本語圏のエンジニア・インディーハッカー（30〜45歳）
技術レベル: 中級（Stripe・Supabase の概念は理解している）
デバイス: PCメイン、スマホサブ
```

**ポイント**: Lovable はターゲットのリテラシーに合わせてUXの複雑さを調整する。

---

## 3. ページ構成

```
ページ:
- / (ランディングページ): ヒーロー・機能説明・料金表・CTA
- /signup: メール+パスワード登録
- /login: ログイン
- /dashboard: 配信設定・過去ニュース一覧
- /settings: プロフィール・メールアドレス変更
- /billing: Stripe Customer Portal へのリンク
- /unsubscribe: メール解除フォーム（トークン認証）
```

**ポイント**: 全ページをリストアップする。Lovable は書かれていないページを作らない。

---

## 4. データスキーマ

```sql
-- Supabase (PostgreSQL) を使用

users (auth.users を拡張)
  id uuid PRIMARY KEY references auth.users(id)
  email text
  display_name text
  trial_ends_at timestamptz
  stripe_customer_id text
  created_at timestamptz DEFAULT now()

subscriptions
  id uuid PRIMARY KEY
  user_id uuid references users(id)
  stripe_subscription_id text
  status text  -- active / canceled / past_due
  current_period_end timestamptz

news_digests
  id uuid PRIMARY KEY
  sent_at timestamptz
  items jsonb  -- [{title, summary, url, implication}]

digest_deliveries
  id uuid PRIMARY KEY
  user_id uuid
  digest_id uuid
  delivered_at timestamptz
  opened_at timestamptz
```

**ポイント**: スキーマを定義するとSupabase連携の精度が大幅に上がる。RLSの設計も含めると更に良い。

---

## 5. 認証設計

```
認証: Supabase Auth
方式: メール + パスワード
ソーシャルログイン: なし（MVPでは不要）
保護ルート: /dashboard, /settings, /billing

RLSポリシー:
- users: 自分のレコードのみ読み書き可
- subscriptions: 自分のレコードのみ読み取り可
- digest_deliveries: 自分のレコードのみ読み取り可
```

**ポイント**: 「ソーシャルログインなし」のような除外も明示する。

---

## 6. 課金設計

```
決済: Stripe
プラン:
  - 無料トライアル: 14日間
  - 月額プラン: ¥480/月（price_id: [後で設定]）
  - 年額プラン: ¥4,800/年（price_id: [後で設定]）

Webhookで処理するイベント:
  - checkout.session.completed → subscription レコード作成
  - customer.subscription.updated → status 更新
  - customer.subscription.deleted → status を canceled に更新

Billing ページ: Stripe Customer Portal にリダイレクト
```

**ポイント**: Webhook で処理するイベントを列挙すると Lovable が Edge Function を正しく生成する。

---

## 7. Edge Functions / API

```
Supabase Edge Functions:
  - /send-digest: 毎朝7時JST に Cron で起動。
    active/trial ユーザーに本日のダイジェストをメール配信。
    
  - /stripe-webhook: Stripe Webhook を受信して DB を更新。
  
  - /create-checkout: Stripe Checkout セッションを作成して URL を返す。

外部API:
  - Claude API (claude-haiku-4-5): ニュース要約生成
  - Resend API: メール配信
```

**ポイント**: Edge Function の名前・トリガー・役割を明確にする。

---

## 8. デザイン方向

```
デザイン:
  - カラー: ダークモード基調。アクセントカラーは青系（#3B82F6）
  - フォント: Inter（英語）/ Noto Sans JP（日本語）
  - スタイル: ミニマル・クリーン。装飾は最小限
  - UIライブラリ: shadcn/ui + Tailwind CSS
  - レスポンシブ: モバイル対応必須

ランディングページ:
  - ヒーローは大きなヘッドライン + サブコピー + CTAボタン
  - 機能説明は3カラムアイコン付き
  - 料金表はシンプルな2プラン比較
  - フッターはシンプル（リンク数は最小限）
```

**ポイント**: 抽象的な「モダンな」より具体的なカラーコードと参照UIライブラリを指定する。

---

## 9. 制約・除外事項

```
制約:
  - ルーターは Next.js App Router を使用
  - TypeScript を使用（strict モード）
  - サーバーコンポーネントを活用する
  - Supabase の型は supabase gen types で生成した型を使う

除外（MVPでは作らない）:
  - ウェブダッシュボードでのニュース閲覧UI（メールのみ）
  - カテゴリ別フィルタ機能
  - チーム・組織機能
  - 管理者ダッシュボード
```

**ポイント**: 「作らないもの」を明示することで Lovable のスコープクリープを防ぐ。

---

## プロンプト送信の順序

1. **初回**: 上記9セクションをすべて含む「設計プロンプト」を送る
2. **修正時**: 1つの変更につき1メッセージ。複数修正をまとめない
3. **行き詰まった時**: 「〇〇がうまく動かない。現在のコードを確認して原因を教えて」と聞く

---

## よくある失敗パターン

| 失敗 | 原因 | 対処 |
|---|---|---|
| Supabase 連携がズレる | スキーマを渡していない | スキーマを含めて再生成 |
| Stripe が機能しない | Webhook イベントを指定していない | Webhook セクションを追加 |
| デザインが崩れる | 具体的な指示がない | カラーコードとUIライブラリを明示 |
| 不要な機能が生成される | 除外事項を書いていない | 「作らないもの」セクションを追加 |

---

## 関連リンク

- [wiki/systems/_index.md](../_index.md)
- [wiki/apps/ideas/AIニュース要約アプリ](../../apps/ideas/AIニュース要約アプリ.md)
- [_templates/implementation-pattern.md](../../../_templates/implementation-pattern.md)
- [_templates/prompt-asset.md](../../../_templates/prompt-asset.md)

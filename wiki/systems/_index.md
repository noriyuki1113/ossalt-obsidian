# 実装ナレッジ・システム — インデックス

Lovable・Supabase・Stripe・Vercel・Next.js などの実装パターンと設計知識。

---

## コアスタック領域

### Lovable
AI駆動のフロントエンド生成ツール。プロンプト設計が成果の質を決める。

- [Lovable完全プロンプト設計](./lovable/Lovable完全プロンプト設計.md)
- 追加予定: `Lovableコンポーネントパターン.md`
- 追加予定: `LovableとSupabase連携.md`

### Supabase
PostgreSQL ベースの BaaS。Auth・Storage・Edge Functions を包括。

> `wiki/systems/supabase/` 追加予定
> - RLS パターン集
> - Auth フロー設計
> - Edge Functions ユースケース

### Stripe
決済・サブスクリプション・メータリング。

> `wiki/systems/stripe/` 追加予定
> - Checkout セッション設計
> - Webhook ハンドリングパターン
> - Supabase との統合パターン

### Vercel
デプロイ・Edge Runtime・環境変数管理。

> `wiki/systems/vercel/` 追加予定
> - Next.js デプロイ設定
> - 環境変数管理
> - Edge Middleware パターン

### Obsidian
このボルト自体の設定・プラグイン・ワークフロー。

> `wiki/systems/obsidian/` 追加予定
> - 推奨プラグイン設定
> - Git 連携ワークフロー

---

## 実装の原則

1. **最小構成から始める** — 必要になってから追加する
2. **Supabase RLS を最初から設計する** — 後から直すのは高コスト
3. **Stripe Webhook は冪等に作る** — 重複受信を前提にする
4. **Vercel 環境変数は Supabase 接続情報と分離する** — 本番/開発を明確に

---

## 関連リンク

- [wiki/index.md](../index.md)
- [wiki/hot.md](../hot.md)
- [wiki/apps/_index.md](../apps/_index.md)
- [_templates/implementation-pattern.md](../../_templates/implementation-pattern.md)
- [_templates/prompt-asset.md](../../_templates/prompt-asset.md)

---

*最終更新: 2026-04-13*

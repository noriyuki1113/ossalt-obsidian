# Supabase RLS パターン集

> Row Level Security（行レベルセキュリティ）の設計原則と再利用可能なパターン集。

タグ: `#implementation` `#supabase` `#rls` `#security`
最終更新: 2026-04-13

---

## RLS とは

Supabase（PostgreSQL）の Row Level Security は、テーブル行レベルでアクセス制御を定義する仕組み。有効にすると、明示的に許可されない限り全ての行が非表示になる。

**なぜ重要か**: Supabase の anon キーはクライアント（ブラウザ）に公開される。RLS がなければ全ユーザーが全レコードを読み書きできる。SaaS を作る場合は必須。

---

## 設計の原則

1. **テーブル作成と同時に RLS を有効化する** — 後から設定する方がリスクが高い
2. **デフォルト拒否** — `ALTER TABLE ... ENABLE ROW LEVEL SECURITY` で全拒否にした後、必要な許可だけを追加する
3. **`auth.uid()`を使う** — Supabase Auth のセッションユーザー ID と照合する標準パターン
4. **service_role は RLS を無視する** — バックエンド処理（Edge Functions）は意図的に service_role を使い、ユーザー制限を迂回する
5. **ポリシーは SELECT / INSERT / UPDATE / DELETE 別に定義する** — 1つのポリシーで複数操作をまとめることも可能だが、明示的な分割が可読性を上げる

---

## 基本パターン：自分のレコードのみ操作

### テーブル準備

```sql
-- RLS を有効化（これだけで全行が非表示になる）
ALTER TABLE public.profiles ENABLE ROW LEVEL SECURITY;
```

### SELECT — 自分のレコードのみ読める

```sql
CREATE POLICY "自分のプロフィールのみ参照可"
ON public.profiles
FOR SELECT
USING (auth.uid() = user_id);
```

### INSERT — 自分の user_id でのみ挿入可

```sql
CREATE POLICY "自分のプロフィールのみ作成可"
ON public.profiles
FOR INSERT
WITH CHECK (auth.uid() = user_id);
```

### UPDATE — 自分のレコードのみ更新可

```sql
CREATE POLICY "自分のプロフィールのみ更新可"
ON public.profiles
FOR UPDATE
USING (auth.uid() = user_id)
WITH CHECK (auth.uid() = user_id);
```

### DELETE — 自分のレコードのみ削除可

```sql
CREATE POLICY "自分のプロフィールのみ削除可"
ON public.profiles
FOR DELETE
USING (auth.uid() = user_id);
```

---

## 応用パターン

### サブスクリプション状態による読み取り制限

```sql
-- アクティブなサブスクリプションを持つユーザーのみコンテンツを読める
CREATE POLICY "有効サブスク保持者のみ閲覧可"
ON public.premium_content
FOR SELECT
USING (
  EXISTS (
    SELECT 1 FROM public.subscriptions
    WHERE user_id = auth.uid()
    AND status = 'active'
  )
);
```

### 管理者ロールによる全件アクセス

```sql
-- users テーブルに is_admin フラグがある場合
CREATE POLICY "管理者は全件参照可"
ON public.orders
FOR SELECT
USING (
  auth.uid() IN (
    SELECT id FROM public.users WHERE is_admin = true
  )
);
```

### 認証済みユーザーなら誰でも読める（公開データ）

```sql
CREATE POLICY "認証済みユーザーは全件参照可"
ON public.news_digests
FOR SELECT
TO authenticated
USING (true);
```

### 未認証ユーザーも読める（完全公開）

```sql
CREATE POLICY "全ユーザー参照可"
ON public.public_posts
FOR SELECT
TO anon, authenticated
USING (true);
```

---

## service_role の注意点

Edge Functions や Cron ジョブなど、バックエンド処理では service_role キーを使う。

```typescript
// Edge Function 内での使用例
const supabase = createClient(
  Deno.env.get('SUPABASE_URL')!,
  Deno.env.get('SUPABASE_SERVICE_ROLE_KEY')!  // RLS を無視して全件操作できる
);
```

**注意**: service_role キーは絶対にクライアントサイドに公開しない。Vercel 環境変数に設定し、Edge Function / Server Action 内でのみ使用する。

---

## よくあるミス

| ミス | 結果 | 対策 |
|---|---|---|
| RLS を有効化せずにデプロイ | 全ユーザーが全行を読み書きできる | テーブル作成直後に必ず有効化 |
| `WITH CHECK` を省略 | INSERT / UPDATE の制約がかからない | INSERT/UPDATE ポリシーは両方記述する |
| anon キーで service_role が必要な処理をしようとする | 403 または空の結果 | Edge Function で service_role を使う |
| ポリシーのデバッグが難しい | 意図しないアクセス拒否 | Supabase ダッシュボードの「SQL エディタ」で `SET ROLE authenticated; SET request.jwt.claim.sub = '...';` で確認できる |

---

## SaaS 設計での推奨パターン

AIニュース要約アプリなどの典型的な SaaS の場合:

```sql
-- 1. 全テーブルに RLS を有効化
-- 2. users: 自分のレコードのみ read/update
-- 3. subscriptions: 自分のレコードのみ read（write は service_role のみ）
-- 4. digest_deliveries: 自分のレコードのみ read（write は service_role のみ）
-- 5. news_digests: 認証済みユーザー全員が read（write は service_role のみ）
```

---

## 関連リンク

- [wiki/systems/_index.md](../_index.md)
- [AIニュース要約アプリ MVP](../../apps/mvp/AIニュース要約アプリ MVP.md)
- [_templates/implementation-pattern.md](../../../_templates/implementation-pattern.md)

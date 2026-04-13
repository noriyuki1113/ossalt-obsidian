# Umami

> **一行要約**: Google Analytics のオープンソース代替。プライバシーファーストの軽量ウェブアクセス解析ツール。

タグ: `#oss` `#アナリティクス` `#GoogleAnalytics代替`
最終確認: 2026-04-13

---

## 概要

Umami は Next.js + PostgreSQL（または MySQL）で構築された、プライバシーファーストのウェブアクセス解析ツール。Google Analytics の代替として、Cookie 不要・個人情報収集なし・GDPR 準拠の形でページビュー・訪問者・リファラー・デバイス情報などの基本指標を収集できる。

ダッシュボードはシンプルで読みやすく、GA のような過剰な複雑さがない。セルフホストまたは Umami Cloud（有料）での利用が可能。スクリプトの容量が小さくサイトのパフォーマンスへの影響が極めて小さい点が優れている。

---

## 代替する商用SaaS

| 商用SaaS | 月額コスト目安 | 主な差異 |
|---|---|---|
| Google Analytics 4 | 無料（データ収集あり） | Umami はプライバシー保護・Cookie 不要 |
| Plausible | $9〜$19/月 | Umami はセルフホストで無料 |
| Fathom | $14〜$54/月 | Umami はより軽量でシンプル |

---

## 強み

- Cookie 不要・GDPR / CCPA 準拠
- スクリプトが軽量（〜2KB）でサイトパフォーマンスへの影響小
- セルフホストで無制限サイト・無制限データ保存
- シンプルで見やすいダッシュボード
- Vercel / Railway / Supabase など主要プラットフォームへの1クリックデプロイ対応
- カスタムイベントトラッキングが可能

---

## 弱み・注意点

- GA のファネル分析・コンバージョン追跡・A/Bテストには対応しない
- eコマース向けの高度な分析は Umami では不可
- データ保持期間の管理は自己責任（セルフホストの場合）
- セルフホスト運用コスト（サーバー代・メンテナンス工数）

---

## 収益化への示唆

- **ossalt.jp コンテンツ**: GA 代替として最も需要が高いカテゴリ。GDPR・Cookie 規制の強化でニーズが増加中。日本語サイト運営者向けの導入ガイドは価値が高い。
- **マネタイズ機会**: Umami のマネージドホスティング提供（月額 ¥500〜¥1,000/サイト）は日本市場でニッチ需要あり
- **代替コスト試算**: Plausible $19/月 → Umami セルフホスト（Vercel 無料 + Supabase 無料枠）でゼロコスト可能

---

## 実装・導入メモ

- **セルフホスト難易度**: 低〜中
- **必要インフラ**: PostgreSQL DB + Node.js ホスティング（Vercel 無料可）
- **導入ステップ概要**:
  1. Vercel に Umami をデプロイ（1クリック Deploy ボタン対応）
  2. PostgreSQL を用意（Supabase / Neon / Railway など）
  3. 環境変数（DATABASE_URL・APP_SECRET）を設定
  4. 計測対象サイトの `<head>` にトラッキングスクリプトを追加
- **注意点**: Vercel の無料プランでは DB 接続数に注意。Supabase との組み合わせが安定している。

---

## 関連リンク

- [wiki/ossalt/_index.md](../_index.md)
- [AppFlowy](./AppFlowy.md)
- [Plane](./Plane.md)
- [wiki/systems/supabase/](../../systems/supabase/)
- [wiki/systems/vercel/](../../systems/vercel/)

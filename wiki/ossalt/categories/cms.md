# CMS — OSSカテゴリ概要

> コンテンツ管理システム。ヘッドレス CMS の台頭で Contentful / Sanity 代替需要が増加中。

タグ: `#category` `#cms` `#Contentful代替`
最終更新: 2026-04-13

---

## カテゴリ概要

CMS は「WordPress 型（モノリシック）」と「ヘッドレス型（API ファースト）」に大別される。近年は Next.js や Astro との組み合わせで使えるヘッドレス OSS CMS の需要が高まっている。Contentful の価格上昇が移行検討のきっかけになるケースが多い。

---

## 代表的 OSS ツール

| ツール | 種別 | 特徴 | セルフホスト難易度 |
|---|---|---|---|
| Strapi | ヘッドレス | カスタムコンテンツタイプ・REST/GraphQL API | 中 |
| Directus | ヘッドレス | 既存 DB をラップ・ノーコード管理 UI | 低〜中 |
| Ghost | ブログ特化 | ニュースレター配信・メンバーシップ機能内蔵 | 中 |
| Payload CMS | ヘッドレス | TypeScript ファースト・Next.js 統合が自然 | 中 |
| WordPress | モノリシック | 圧倒的なプラグインエコシステム | 低 |

---

## 代替する商用 SaaS

| 商用SaaS | 月額目安 | 主な差異 |
|---|---|---|
| Contentful | $0〜$300+ | Strapi / Directus がセルフホストで無料 |
| Sanity | $0〜$949 | Payload が TypeScript 環境で近い代替 |
| Webflow CMS | $23〜$39/月 | Ghost がブログ・ニュースレターで代替 |

---

## 典型的なユースケース

- Next.js サイトのブログ・記事管理バックエンドとして Strapi / Directus を使う
- ニュースレター × ブログの一体型サービスとして Ghost を使う
- 既存の PostgreSQL テーブルに Directus を被せて管理 UI を得る

---

## 収益化への示唆（ossalt.jp）

- **コンテンツ価値**: Contentful 価格改定時に移行先を探すユーザーが増える。比較記事の旬がある。
- **ビジネス機会**: Ghost のマネージドホスティング（Ghost Pro の安価版）は日本市場で空白
- **訴求ポイント**: 「API で使えるヘッドレス CMS が月額ゼロ」は開発者に刺さる

---

## 実装上の注意

- Strapi は Node.js ベースで Vercel 非対応（常駐プロセスが必要）。Railway / Render 推奨。
- Directus は既存 DB への接続が強みだが、スキーマ設計を先に決める必要がある
- Ghost の最小構成は Docker + MySQL / SQLite で動く。Caddy でリバースプロキシ推奨。

---

## 関連ノート

- [wiki/ossalt/_index.md](../_index.md)
- [analytics](./analytics.md)

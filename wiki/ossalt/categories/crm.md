# CRM — OSSカテゴリ概要

> 顧客関係管理。Salesforce / HubSpot の高額ライセンスからの脱出需要が根強い。

タグ: `#category` `#crm` `#Salesforce代替` `#HubSpot代替`
最終更新: 2026-04-13

---

## カテゴリ概要

CRM は「営業パイプライン管理」「顧客データ一元管理」「マーケティングオートメーション」の3層に分かれる。OSS 代替は HubSpot の無料 CRM からの移行より、Salesforce の高コスト問題から移行するケースが多い。スモールビジネスには機能を絞った軽量 CRM の方が刺さりやすい。

---

## 代表的 OSS ツール

| ツール | 特徴 | セルフホスト難易度 |
|---|---|---|
| Twenty | モダンな UI・Notion 風のデータモデル・GraphQL API | 低〜中 |
| SuiteCRM | SugarCRM フォーク・エンタープライズ向け高機能 | 高 |
| Erxes | マーケティング + 顧客サポート統合型 | 高 |
| Mautic | マーケティングオートメーション特化 | 中〜高 |

---

## 代替する商用 SaaS

| 商用SaaS | 月額目安/ユーザー | 主な差異 |
|---|---|---|
| HubSpot CRM | $0（無料）〜$45 | Twenty がシンプルな代替。MA 機能は Mautic |
| Salesforce | $25〜$300+ | SuiteCRM が最も機能的に近い |
| Pipedrive | $9.90〜$59.90 | Twenty がパイプライン管理で代替可能 |

---

## 典型的なユースケース

- 営業 5〜20人のスタートアップが HubSpot 有料移行前に Twenty を試す
- Salesforce を使うほどではないが顧客データを構造管理したい BtoB 企業
- メール配信と顧客セグメントを統合したいマーケター（Mautic）

---

## 収益化への示唆（ossalt.jp）

- **コンテンツ価値**: CRM は検索ボリュームが大きいが競合記事も多い。日本語市場では独自比較記事に余地あり。
- **ビジネス機会**: Twenty のセットアップ代行 + 初期データ移行サービスはスモールビジネスに需要あり
- **訴求ポイント**: 「HubSpot の無料枠が使いにくくなった」「Salesforce は高すぎる」という層に直接響く

---

## 実装上の注意

- Twenty は Docker Compose で比較的簡単に起動可能。PostgreSQL を使用。
- SuiteCRM は LAMP スタック前提で、モダンなデプロイには工夫が必要
- Mautic はメール配信機能を持つため、SPF/DKIM 設定など送信ドメイン認証が必須

---

## 関連ノート

- [wiki/ossalt/_index.md](../_index.md)
- [form-survey](./form-survey.md)

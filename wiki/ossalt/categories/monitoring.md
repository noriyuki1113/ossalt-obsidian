# モニタリング — OSSカテゴリ概要

> 稼働監視・インフラメトリクス・アラート。Datadog / New Relic 代替として OSS エコシステムが成熟している。

タグ: `#category` `#monitoring` `#Datadog代替`
最終更新: 2026-04-13

---

## カテゴリ概要

「サーバーが落ちたら通知してほしい」というシンプルな稼働監視から、「メトリクス・ログ・トレースを統合して分析したい」という高度な可観測性（Observability）まで幅広い。個人・スモールチームには軽量な稼働監視ツールで十分なことが多い。

---

## 代表的 OSS ツール

| ツール | 特徴 | セルフホスト難易度 |
|---|---|---|
| Uptime Kuma | 稼働監視特化・シンプルなダッシュボード・Docker 対応 | 低 |
| Grafana | メトリクス可視化・Prometheus / Loki と組み合わせて使う | 中〜高 |
| Prometheus | メトリクス収集・時系列 DB・Grafana と組み合わせる | 中〜高 |
| Netdata | リアルタイムシステムモニタリング・1コマンドインストール | 低 |

---

## 代替する商用 SaaS

| 商用SaaS | 月額目安 | 主な差異 |
|---|---|---|
| Datadog | $15〜/ホスト | Grafana + Prometheus がメトリクス面で代替 |
| New Relic | $0（無料枠）〜 | Netdata が軽量な代替 |
| Better Uptime / Pingdom | $7〜$50/月 | Uptime Kuma がほぼ同等の機能をゼロコストで |
| PagerDuty | $19〜/ユーザー | アラート通知はSlack/メールと組み合わせで自前実装可 |

---

## 典型的なユースケース

- セルフホストSaaSの稼働監視・ダウン時の Slack 通知（Uptime Kuma）
- VPS の CPU / メモリ / ディスク使用率の可視化（Grafana + Prometheus）
- 複数サービスのエンドポイント死活監視を一元管理する

---

## 収益化への示唆（ossalt.jp）

- **コンテンツ価値**: Uptime Kuma の導入記事は検索需要が高い。「Pingdom 代替」「Better Uptime 代替」キーワードで流入取れる。
- **ビジネス機会**: 「セルフホスト SaaS の監視セットアップ代行」は他サービスとセット提供しやすい付加価値サービス
- **訴求ポイント**: 稼働監視は「月額 ¥1,000〜¥3,000 の固定費」が「ほぼゼロ」になる = ROI が非常に分かりやすい

---

## 実装上の注意

- Uptime Kuma は `docker run` 1コマンドで起動。最初のセットアップが最も簡単な OSS の1つ。
- Grafana + Prometheus は構成要素が多く、docker compose で一括管理するのが現実的。
- アラート通知チャンネル（Slack / メール / Discord）の設定は最初に必ず確認する。

---

## 関連ノート

- [wiki/ossalt/_index.md](../_index.md)
- [analytics](./analytics.md)

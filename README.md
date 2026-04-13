# ossalt-obsidian

個人の第二の脳（Second Brain）として機能する Obsidian ボルト兼 Git リポジトリ。

OSS代替調査・SaaSアイデア・AIニュース・実装ナレッジを一元管理し、Claude との協働ワークフローを前提に設計している。

---

## セットアップ

### 1. Obsidian ボルトとして開く

Obsidian を起動し「Open folder as vault」からこのディレクトリを選択する。

### 2. Git でバージョン管理

```bash
git clone <this-repo>
cd ossalt-obsidian
```

Obsidian Git プラグインを使うか、手動でコミットする。

### 3. Claude Code で使う

```bash
cd ossalt-obsidian
claude
```

Claude は `CLAUDE.md` の指示に従って動作する。セッション開始時は自動的に `wiki/hot.md` → `wiki/index.md` の順で読む。

---

## ワークフロー

```
情報収集 → .raw/ に保存
    ↓
Claude で整理 → wiki/ に正規ノートを作成
    ↓
hot.md・各 _index.md を更新
    ↓
git commit
```

### .raw/ ディレクトリ

一次ソース（URL、スクリーンショット、ラフメモ）を入れる一時置き場。
処理済みになったら wiki/ の正規ノートに昇格させる。

### wiki/ ディレクトリ

整理・構造化済みの知識ベース。ここが本体。

### _templates/ ディレクトリ

再利用可能なノートテンプレート。新しいノートを作る前に確認する。

---

## ディレクトリ構造

```
.raw/           一次ソース（一時）
wiki/           正規ナレッジベース
  ossalt/       OSS代替ツール調査
  apps/         SaaS・マイクロSaaSアイデア
  ai-news/      AIニュース・トレンド分析
  systems/      実装パターン・スタック知識
  people-brands/ 注目人物・企業・プロダクト
_templates/     ノートテンプレート
_attachments/   画像・ファイル添付
```

---

## 関連リンク

- [ossalt.jp](https://ossalt.jp) — OSS代替ツール紹介サイト
- [CLAUDE.md](./CLAUDE.md) — Claude への行動指示
- [WIKI.md](./WIKI.md) — ナレッジベースの設計思想
- [wiki/index.md](./wiki/index.md) — ドメイン別マスターインデックス
- [wiki/hot.md](./wiki/hot.md) — 今週のホットな文脈

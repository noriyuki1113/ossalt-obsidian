# Obsidian Git 設定ガイド

> Obsidian ボルトを Git リポジトリと同期・自動コミットするためのプラグイン設定。

タグ: `#implementation` `#obsidian` `#git`
最終更新: 2026-04-13

---

## Obsidian Git とは

Obsidian のコミュニティプラグイン。ボルト内でのノート変更を自動的に Git コミット・プッシュする。Claude Code での作業と手動ノート編集の両方をバージョン管理できる。

**このボルトでの役割**: Claude が生成・更新したノートと、自分が手動で書いたノートを同じリポジトリで一元管理する。

---

## いつ使うか

- Obsidian でノートを手動編集するとき（Claude Code 以外での作業）
- スマートフォンから Obsidian Mobile でメモを取り、デスクトップと同期したいとき
- ボルトの変更履歴をビジュアルに確認したいとき（差分表示）

Claude Code から作業するときは Obsidian Git ではなく `git` コマンドを直接使う。

---

## セットアップ手順

### 1. プラグインをインストール

1. Obsidian の設定 → 「コミュニティプラグイン」を開く
2. 「コミュニティプラグインを閲覧」→ "Obsidian Git" を検索
3. インストール → 有効化

### 2. Git リポジトリの確認

このボルトは既に Git リポジトリとして初期化済み。
`git remote -v` でリモートが設定されているか確認する。

```bash
git remote -v
# origin  https://github.com/username/ossalt-obsidian.git (fetch)
# origin  https://github.com/username/ossalt-obsidian.git (push)
```

リモートが未設定の場合:

```bash
git remote add origin https://github.com/username/ossalt-obsidian.git
```

### 3. プラグイン設定（推奨値）

| 設定項目 | 推奨値 | 理由 |
|---|---|---|
| Vault backup interval (minutes) | `30` | 30分ごとに自動コミット |
| Auto pull interval (minutes) | `30` | 他デバイスの変更を取り込む |
| Commit message | `vault backup: {{date}}` | 日時入りで履歴が分かりやすい |
| Pull before push | ON | コンフリクト防止 |
| Push on backup | ON | コミットと同時にプッシュ |
| Disable push | OFF | プッシュまで自動化する |

### 4. 認証設定

GitHub を使う場合は SSH キーまたは Personal Access Token（PAT）での認証を推奨。HTTPS + PAT の場合:

```bash
git config --global credential.helper store
# 初回 push 時に PAT を入力すると保存される
```

---

## 推奨ワークフロー

```
Obsidian でノートを編集
    ↓
30分ごとに Obsidian Git が自動コミット + プッシュ
    ↓
Claude Code で作業するときは手動で git pull してから開始
    ↓
Claude Code 作業後は手動で git add / commit / push
```

**コンフリクト回避のコツ**: 同じファイルを Obsidian と Claude Code で同時に編集しない。Claude Code での作業が終わったらすぐにコミットする習慣をつける。

---

## メリット

- ノートの変更履歴が残り、誤って削除しても復元できる
- 複数デバイス（PC・スマートフォン）間でボルトを同期できる
- Claude が生成したノートと自分のノートを同じ履歴で管理できる

---

## リスク・注意点

- **コンフリクト**: 複数デバイスで同じファイルを同時編集するとマージコンフリクトが発生する。Obsidian Git は自動マージを試みるが、手動解決が必要な場合もある。
- **`.obsidian/` フォルダ**: プラグイン設定・テーマなどを含む。このボルトの `.gitignore` は `workspace.json`（ウィンドウ状態）だけを除外し、他は同期している。チームで使う場合は要調整。
- **大きなファイル**: `_attachments/` に画像・PDFを置く場合、Git LFS の導入を検討する。

---

## トラブルシューティング

| 症状 | 対処 |
|---|---|
| 自動コミットが動かない | プラグインが有効か確認。Git の設定（user.name / user.email）が完了しているか確認 |
| Push が失敗する | 認証設定を確認。`git push` をターミナルで手動実行してエラーを確認 |
| コンフリクトが発生した | Obsidian を閉じてターミナルで `git status` → 手動マージ |

---

## 関連リンク

- [wiki/systems/_index.md](../_index.md)
- [README.md](../../../README.md)

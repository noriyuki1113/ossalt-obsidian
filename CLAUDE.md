# CLAUDE.md — Instructions for Claude

This file defines how Claude should behave when working inside this vault.
Read this file first before doing anything else.

---

## Purpose of This Vault

This is a personal second-brain system for:

1. **OSS alternatives research** — sourcing and evaluating open-source alternatives to popular SaaS tools, primarily for [ossalt.jp](https://ossalt.jp)
2. **SaaS / micro-SaaS idea generation** — identifying opportunities and building toward MVPs
3. **AI news synthesis** — tracking developments and extracting actionable business implications
4. **Reusable implementation knowledge** — patterns for Lovable, Supabase, Stripe, Vercel, Next.js, and related tools

The owner is a builder and indie hacker. Think like a founder and systems designer.

---

## Reading Order

When starting a session or before doing any work, read in this order:

1. `wiki/hot.md` — what matters right now
2. `wiki/index.md` — overview of all domains and their current state
3. The nearest domain `_index.md` (e.g. `wiki/ossalt/_index.md`) — domain context
4. Only then open individual notes as needed

Do not jump directly into individual notes without first establishing context.

---

## Writing Rules

- **Write all user-facing note content in Japanese.** This includes titles, summaries, section headings, and body text inside wiki notes.
- Internal instruction files (like this one) may be in English when clarity benefits from it.
- Prefer **reusable, structured notes** over conversational summaries.
- Every note should be useful the next time it's read, not just today.
- **Always extract monetization implications** — even for technical notes, ask "how does this create or protect revenue?"
- **Always extract implementation implications** — ask "what would it take to build/integrate this?"
- Add `[[relative links]]` or markdown links to related notes whenever relevant.
- Use the templates in `_templates/` as starting points.

---

## Routing Rules

Route new knowledge to the correct domain:

| Input type | Target directory |
|---|---|
| OSS tool, GitHub repo, open-source alternative | `wiki/ossalt/tools/` |
| OSS category strategy, comparison | `wiki/ossalt/categories/` or `wiki/ossalt/alternatives/` |
| SaaS idea, product concept, market opportunity | `wiki/apps/ideas/` |
| MVP plan, feature spec | `wiki/apps/mvp/` |
| Monetization model, pricing analysis | `wiki/apps/monetization/` |
| Tech stack, tool choice | `wiki/apps/stack/` or `wiki/systems/` |
| AI model release, AI news | `wiki/ai-news/models/` or `wiki/ai-news/trends/` |
| AI repo, open-source AI tool | `wiki/ai-news/repos/` |
| AI-driven business opportunity | `wiki/ai-news/opportunities/` |
| Implementation pattern, architecture, code knowledge | `wiki/systems/<tool>/` |
| Founder, indie hacker, company, product | `wiki/people-brands/` |

When in doubt, put it in the closest domain and add a note in `wiki/hot.md`.

---

## Save Rules

- **One canonical note per topic.** Do not create duplicates. If a note exists, update it.
- After creating or updating a note, update the relevant `_index.md` to include a link.
- Update `wiki/hot.md` when the new note is relevant to this week's focus.
- Keep `wiki/index.md` current by reflecting the count of notes and current domain focus.

---

## Behavior Guidelines

- Think like a **builder** — what can I build from this?
- Think like a **founder** — what problem does this solve, and who pays for it?
- Think like a **systems designer** — how does this fit into existing architecture?
- Be concise. Don't pad notes with filler. Every sentence should earn its place.
- When analyzing OSS tools, always compare to commercial alternatives (especially Japanese market).
- When evaluating ideas, default to the simplest possible MVP.
- Flag any note that seems outdated or contradicts another note.

---

## File Naming

- Use kebab-case for English filenames: `my-tool-name.md`
- Use natural Japanese for Japanese-language filenames: `AIニュース要約アプリ.md`
- Template files start with lowercase and describe the note shape: `oss-tool.md`

---

## Quick Reference

```
wiki/hot.md          今週の文脈（毎週更新）
wiki/index.md        全ドメインのマスターインデックス
wiki/ossalt/         OSS代替ツール
wiki/apps/           SaaSアイデア
wiki/ai-news/        AIニュース
wiki/systems/        実装ナレッジ
wiki/people-brands/  人物・企業・プロダクト
_templates/          ノートテンプレート
.raw/                未処理の一次ソース
```

# SAAD 文書体系インデックス（生きた文書）

| 項目 | 内容 |
| --- | --- |
| 文書ID | SAAD-DOC-INDEX-001 |
| リポジトリ | [hoshimotoyasunori/saad-hub-mock](https://github.com/hoshimotoyasunori/saad-hub-mock) |
| 作成日 | 2026-09-25 |
| **性質** | **今後も拡張する生きた文書群**の目次。欠ける文書が出たらここに行を足してから本文を書く |

---

## 0. 使い方（必読）

1. **別の人／別のAI**はまずルートの [HANDOFF.md](../HANDOFF.md) → [STATUS.md](../STATUS.md)  
2. **システム／本番寄りの要件**は本フォルダ `docs/` から入る  
3. **モックUIの操作要件**はルートの [requirements.md](../requirements.md)  
4. 文書を増やしたら **本書（インデックス）に必ず追記**する  
5. HTMLや方針を変えたら、該当文書＋[STATUS.md](../STATUS.md)＋必要なら coverage / journey を同じ作業で更新する  

---

## 1. 文書マップ

### 1-1. 入り口・引き継ぎ（リポ直下）

| 文書 | 目的 | 状態 |
| --- | --- | --- |
| [../README.md](../README.md) | 公開URL・切替・別AI引き継ぎ手順 | ✅ 運用中 |
| [../HANDOFF.md](../HANDOFF.md) | 意図・ASIS精査・同期ルール・コピペプロンプト | ✅ 運用中 |
| [../STATUS.md](../STATUS.md) | 現状スナップショット | ✅ 運用中 |

### 1-2. システム／開発の要件・設計（本フォルダ）

| 文書 | 目的 | 状態 |
| --- | --- | --- |
| [system-requirements.md](./system-requirements.md) | **システム要件定義書（SRS）** — 目的・スコープ・機能／非機能の親 | ✅ 初版 |
| [functional-requirements.md](./functional-requirements.md) | 機能要件一覧（モック済／今後） | ✅ 初版 |
| [non-functional-requirements.md](./non-functional-requirements.md) | 非機能要件（性能・可用性・運用等） | ✅ 初版 |
| [data-model.md](./data-model.md) | データモデル要件（エンティティ・親子・整合） | ✅ 初版 |
| [integration-requirements.md](./integration-requirements.md) | 外部連携・SSO・会計・カレンダー等 | ✅ 初版 |
| [security-access.md](./security-access.md) | 認証・権限・スコープ・監査 | ✅ 初版 |
| [ui-ux-requirements.md](./ui-ux-requirements.md) | UI/UX要件（PC台帳／スマホジョブ／詳細パネル） | ✅ 初版 |
| [roadmap.md](./roadmap.md) | **今後の開発予定・フェーズ** | ✅ 初版 |
| [glossary.md](./glossary.md) | 用語集 | ✅ 初版 |
| [acceptance-criteria.md](./acceptance-criteria.md) | 受け入れ観点（モック／本番段階） | ✅ 初版 |
| [development-guide.md](./development-guide.md) | 開発・文書拡張の進め方 | ✅ 初版 |

### 1-3. 業務・ASIS・利用者視点（リポ直下・既存）

| 文書 | 目的 | 状態 |
| --- | --- | --- |
| [../asis-capability-coverage.md](../asis-capability-coverage.md) | ASIS由来の導入状況（✅🟡⬜⛔） | ✅ 運用中 |
| [../user-journey-requirements.md](../user-journey-requirements.md) | 利用者の問いと操作の流れ・§12作業 | ✅ 運用中 |
| [../requirements.md](../requirements.md) | **Hubモック専用**要件ID（E/P/M） | ✅ 運用中 |
| [../system-page-structure.md](../system-page-structure.md) | ページ構成・事業部×管理部 | ✅ 運用中 |
| [../saad-hub-manual.md](../saad-hub-manual.md) | 利用マニュアル（触り方） | ✅ 運用中 |

### 1-4. 実装（リポ直下）

| 成果物 | 目的 |
| --- | --- |
| `../index.html` | 公開入口・PC/スマホ切替 |
| `../saad-github-hub.html` | PC台帳モック |
| `../saad-mobile-hub.html` | スマホジョブモック |

### 1-5. 今後足す予定の文書（枠だけ先に置く）

| 予定文書 | 目的 | 状態 |
| --- | --- | --- |
| `api-specification.md` | REST/イベントAPI仕様 | ⬜ 本番設計時に作成 |
| `screen-transition.md` | 画面遷移図（正式版） | ⬜ |
| `migration-from-asis.md` | ASISからの移行計画 | ⬜ |
| `ops-runbook.md` | 運用手順・障害対応 | ⬜ |
| `test-plan.md` | テスト計画・ケース台帳 | ⬜ |
| `infrastructure.md` | インフラ・環境構成 | ⬜ |

---

## 2. レイヤの関係

```
意図・引き継ぎ     HANDOFF / STATUS / README
        ↓
システム要件親     docs/system-requirements.md
        ↓
機能・NF・データ・連携・権限・UI   docs/*.md
        ↓
業務精査・導入状況   asis-capability-coverage / user-journey
        ↓
モック要件ID       requirements.md（E/P/M）
        ↓
実装HTML           index / saad-*-hub.html
```

---

## 3. 改訂履歴

| 日付 | 内容 |
| --- | --- |
| 2026-09-25 | 初版。システム開発に必要な文書群を一通り新設し、拡張前提の索引とした |

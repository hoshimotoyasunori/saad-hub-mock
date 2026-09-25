# SAAD 開発・文書拡張ガイド

| 項目 | 内容 |
| --- | --- |
| 文書ID | SAAD-DEV-001 |
| 版 | 0.1 |
| 作成日 | 2026-09-25 |
| **性質** | **生きた文書**。本リポの docs/ と HTML をどう伸ばすかの手順 |

---

## 1. 認識（重要）

- `docs/` 配下およびルートの要件系Markdownは **今後も拡張する生きた文書**である  
- 「完成した仕様書セット」ではなく、**実装と一緒に育てる台帳**である  
- 欠ける論点が出たら、先に [DOC-INDEX.md](./DOC-INDEX.md) に行を足してから本文を書く  

---

## 2. 機能を足すときの手順

1. [../HANDOFF.md](../HANDOFF.md) §2 の ASIS型チェック（残す／やめる／吸収）  
2. [../user-journey-requirements.md](../user-journey-requirements.md) に問い／行があるか確認。なければ追加  
3. [functional-requirements.md](./functional-requirements.md) と [roadmap.md](./roadmap.md) の状態を更新  
4. HTML（`saad-*-hub.html`）を実装  
5. [../asis-capability-coverage.md](../asis-capability-coverage.md) の現状列を更新  
6. モック固有なら [../requirements.md](../requirements.md) にID追加  
7. [../STATUS.md](../STATUS.md) の日付と残件を更新  
8. 必要なら SRS / data / UI / security の該当節を追記  
9. `index.html` のキャッシュバストを上げて push  

---

## 3. 文書だけ増やすとき

- 新ファイルを `docs/` に置く  
- **必ず** DOC-INDEX の表に追加（予定枠なら §1-5）  
- README の文書一覧または「システム文書」節からリンク  

---

## 4. 本番設計に入るとき

DOC-INDEX §1-5 の予定文書を作成順の目安にする:

1. `api-specification.md`  
2. `infrastructure.md`  
3. `migration-from-asis.md`  
4. `test-plan.md` / `ops-runbook.md`  

---

## 5. 別AIへの最短指示

README および HANDOFF §7 のプロンプトを使う。  
システム文書から入る場合は **DOC-INDEX → SRS → roadmap** の順。

---

## 改訂履歴

| 版 | 日付 | 内容 |
| --- | --- | --- |
| 0.1 | 2026-09-25 | 初版 |

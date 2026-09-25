# SAAD Hub モック — 開発引き継ぎ（別の人／別のAI向け）

> **このファイルを最初に読んでください。**  
> GitHub 上だけで「何を作ろうとしているか」「いまどこまでできているか」「次に何を触るか」を把握できるようにした正本です。  
> **最終更新**: 2026-09-25

---

## 0. 30秒で分かる結論

| 項目 | 内容 |
| --- | --- |
| **何を作っているか** | サニックスの建物保全・メンテナンス向け **統合基幹（SAAD）の UI モック**。本番APIなしの静的HTML。合意形成・デモ用 |
| **公開URL** | https://hoshimotoyasunori.github.io/saad-hub-mock/ |
| **リポジトリ** | https://github.com/hoshimotoyasunori/saad-hub-mock |
| **正入口** | `index.html`（幅で PC / スマホを切替） |
| **PC本体** | `saad-github-hub.html`（GitHub Issues 風の台帳） |
| **スマホ本体** | `saad-mobile-hub.html`（ジョブ型。GitHub Mobile の移植はしない） |
| **導入状況の正本** | [asis-capability-coverage.md](./asis-capability-coverage.md) |
| **操作の流れの正本** | [user-journey-requirements.md](./user-journey-requirements.md) |
| **モック専用要件** | [requirements.md](./requirements.md) |
| **現状スナップショット** | [STATUS.md](./STATUS.md) |
| **システム文書目次** | [docs/DOC-INDEX.md](./docs/DOC-INDEX.md) |
| **システム要件定義（SRS）** | [docs/system-requirements.md](./docs/system-requirements.md) |
| **今後の開発予定** | [docs/roadmap.md](./docs/roadmap.md) |

---


### ローカルと Pages の見え方

- **正入口は同じ**: ローカルは `mocks/saad-hub.html?v=pc`、公開は https://hoshimotoyasunori.github.io/saad-hub-mock/?v=pc
- `saad-github-hub.html` を直開きすると切替バー無しのPC版のみ（iframe枠・自動スマホ切替が無い）
- 幅820px未満で Pages を開くとジョブ型スマホになり、PC直開きと差が出る

## 1. 作ろうとしているもの（プロダクト意図）

### 1-1. 背景

社内には旧来の業務基盤・Excel・WF（総称して **ASIS**）がある。  
依頼受付→調査→見積→決裁→購買→施工→請求…が **複数の表・メール・転記** に散らばっている。

### 1-2. ゴール（モックの範囲）

1. **データは1本**（顧客・物件・案件＝Issue行）に寄せて見せる  
2. **必要な管理（探す／承認する／手配する／締める）は残す**  
3. **無駄な管理（同じ事実の多重転記・日報Excel）はやめる**  
4. **PC＝台帳（デスク）／スマホ＝ジョブ（現場・外出）** で窓を分ける（同じデータ）  
5. 画面を触って「業務が回るか」を関係者と合意する（本番実装そのものではない）

### 1-3. ゴールではないこと

- ASIS の約500業務を全部画面化すること  
- 本番認証・API・永続化・実PDFメール  
- Figma 最終ビジュアルの確定（見た目は探索用）

### 1-4. メタファー

| 窓 | たとえ | ファイル |
| --- | --- | --- |
| PC | GitHub Issues / Projects 風の **台帳**。行＝仕事。右に詳細 | `saad-github-hub.html` |
| スマホ | 「今日やること・報告・承認」の **ジョブ**。Issue語彙は出さない | `saad-mobile-hub.html` |

---

## 2. ASISからどう精査して実装しているか

実装は「欲しい画面から」ではなく、**ASISでなぜその一覧・管理が要ったか**を型に当ててから決めている。

### 2-1. 型（A〜K）— 必ずここを通す

詳細は [asis-capability-coverage.md](./asis-capability-coverage.md) §1。

| 型 | 意味 | 刷新 |
| --- | --- | --- |
| A〜F, Hコア | 入口・探す・承認・手配・現場・締め・マスタ | **残す** |
| G, Iの転記 | 進捗Excel・日報転記・集計のためだけの表 | **やめる（⛔）／台帳へ吸収（🔀）** |
| J | 取引先専用表 | 最初から別システム化しない。属性＋後続 |
| K | 経費・勤怠など周辺 | 幹ではない。SSO／段階 |

### 2-2. 実装前チェック（毎回）

新しい機能を足す前に、次を満たすこと。

1. **ASIS根拠**: どの業務・どの「一覧／管理」由来か（型 A〜K）を1行で書ける  
2. **残す／やめる／吸収**: ⛔や🔀なら専用画面を増やさない  
3. **操作の流れ**: [user-journey-requirements.md](./user-journey-requirements.md) の作る／直す／消す／探す／通知／権限／スマホ／帳票のどれか  
4. **モックで確認できる**: クリックして状態が変わる（説明文だけは 🟡）  
5. **ドキュメント同時更新**: HTML と一緒に coverage / journey / requirements を更新（下記 §5）

### 2-3. ASIS根拠の幹（よく参照する）

| ASIS | 新での意味 |
| --- | --- |
| ES_001 調査依頼の受付 | リード1本・転記廃止 |
| ES_010 調査 | 作業・Comment・進み＝Status |
| ES_091 受注 | 金額分岐稟議・日報転記廃止 |
| ASIS対応表 48ドメイン | 網羅チェックの地図（ToDoリストではない） |

社内に詳細な業務詳細・対応表がある場合は SANIX 側（個人作業コピー）を参照。**公開リポに載っている範囲だけで引き継ぎ可能**にするのが本ファイルの目的。

### 2-4. 「精査しながら実装しているか」の現状評価（2026-09-25）

| 観点 | 状況 |
| --- | --- |
| 型A〜Fの入口・台帳・キュー | **確認しながら導入済み**（モック操作可）。coverage §2 に「ASISでなぜ要ったか」付き |
| 転記系（G/I）の廃止方針 | **文書化済み・画面化しない**（⛔）。BIは集計の置き換えとして ✅ |
| 利用者の操作の問い（C1〜等） | journey で洗い出し → 優先1〜12でモック反映。**残りは journey §12 と coverage「まだ無い」** |
| よくあったズレ | HTMLだけ先に変わり docs が遅れることがあった → **§5 の同期ルールを必須化**（2026-09-25） |
| データ整合 | Issue は `parent` 参照。一覧と詳細の子集合が矛盾しないよう正規化（requirements P-13/P-14） |

**結論**: 幹機能は ASIS型で精査したうえでモックに載せている。未着手の残りも「画面の思いつき」ではなく journey／coverage の ⬜ として追跡している。引き継ぎ時は **⬜ を勝手にスキップして新機能を足さない**こと。

---

## 3. リポジトリ内ドキュメント地図

| ファイル | 読む順 | 役割 |
| --- | --- | --- |
| **[HANDOFF.md](./HANDOFF.md)**（本ファイル） | 1 | 意図・ASIS精査・引き継ぎ手順 |
| **[STATUS.md](./STATUS.md)** | 2 | いまの完了／未完了の短いスナップショット |
| [README.md](./README.md) | 3 | 公開URL・切替・画面概要 |
| [asis-capability-coverage.md](./asis-capability-coverage.md) | 4 | **導入状況の正本**（✅🟡⬜⛔） |
| [user-journey-requirements.md](./user-journey-requirements.md) | 5 | 利用者の問いと操作の流れ。§12 が作業リスト |
| [requirements.md](./requirements.md) | 6 | 本モック専用の要件ID（E/P/M/D/N） |
| [system-page-structure.md](./system-page-structure.md) | 7 | 事業部×管理部の共有ページ構成 |
| [saad-hub-manual.md](./saad-hub-manual.md) | 8 | 触り方・約束（Open≠進み 等） |

HTML の実装の正は常にリポ内の `*.html`。社内に `SANIX/SAAD_UI/` の作業コピーがある場合は、**公開前に本リポへ cp＋docs 同期**する。

---

## 4. コードの触り方（最短）

```bash
git clone https://github.com/hoshimotoyasunori/saad-hub-mock.git
cd saad-hub-mock
python3 -m http.server 8123
# → http://localhost:8123/
```

| 変えたいこと | 主に触るファイル |
| --- | --- |
| PC台帳・詳細・管理画面・モックデータ | `saad-github-hub.html`（巨大な単一HTML＋インラインJS） |
| スマホUI | `saad-mobile-hub.html` |
| 幅切替シェル・キャッシュバスト `?_r=` | `index.html` |
| 導入状況 | `asis-capability-coverage.md` |
| 次の作業の優先 | `user-journey-requirements.md` §12 |

Issueデータは `saad-github-hub.html` 内の `issues` 配列。親子は `parent`。起動時に `normalizeIssueGraph()` で depth を揃える。

---

## 5. 変更時の必須ルール（ドキュメント同期）

HTML や挙動を変えたら、**同じコミット（または直後）で**:

1. [requirements.md](./requirements.md) — 要件ID・改訂履歴（§12）  
2. [asis-capability-coverage.md](./asis-capability-coverage.md) — §2 の現状・§3 サマリ  
3. [user-journey-requirements.md](./user-journey-requirements.md) — 該当行と §12  
4. [STATUS.md](./STATUS.md) — スナップショット日付と残件  
5. [README.md](./README.md) — 利用者に見える挙動が変わったとき  
6. `index.html` のキャッシュバスト（`_r=`）を上げる  

開閉・幅・用語・クリック挙動も「見た目だけ」扱いにせず要件に残す。

---

## 6. 次に着手してよい残件（優先の目安）

詳細は [STATUS.md](./STATUS.md) と coverage「まだ無い」。塊の例:

1. **変更の残り**: 契約変更の稟議、受注後の取引形態変更、注文書の版重ね、単価・手数料の適用日改定  
2. **取消・無効化**: 物件／外注／商品の無効化、施工後解約・クーリングオフ、請求の赤伝  
3. **一覧**: 一括CSV／ハガキ、最近見た、列の本格保存  
4. **権限・人事連動**: 例外権限、異動時引き継ぎ自動  
5. **スマホ・帳票の端**: カメラ起票、ハガキ一括、実PDF（本番寄りは後回し可）

新機能を足す前に §2-2 のチェックを通すこと。

---

## 7. 別AIへのプロンプト例（コピー用）

```
あなたは SAAD Hub モック（https://github.com/hoshimotoyasunori/saad-hub-mock）の続きを担当します。
最初に HANDOFF.md と STATUS.md を読み、システム／今後の要件は docs/DOC-INDEX.md → docs/system-requirements.md → docs/roadmap.md を読んでください。
docs/ 配下は今後も拡張する生きた文書です。欠ける論点は DOC-INDEX に行を足してから本文を書いてください。
ASIS全業務の網羅は目的ではありません。型A〜FとHコアを残し、転記系は増やさない方針です。
機能を足すときは coverage / user-journey / requirements / docs の該当文書を同じ作業で更新し、Pages の HTML と docs を整合させてください。
```

---

## 8. 改訂履歴

| 日付 | 内容 |
| --- | --- |
| 2026-09-25 | 初版。GitHub上で別AIが引き継げるよう意図・ASIS精査・現状・同期ルールを固定 |
| 2026-09-25 | docs/ にシステム要件一式を追加。DOC-INDEX・SRS・roadmap を引き継ぎ経路に含める |

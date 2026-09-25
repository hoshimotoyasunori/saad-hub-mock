# SAAD Hub モック（PC / スマホ自動切替）

1つのURLで画面幅に応じて表示が切り替わる **UIモック**（静的HTML）です。  
本番アプリではなく、**検証・デモ・合意形成用**の画面です。

> **別の人／別のAIが続きをやるとき** → 必ず **[HANDOFF.md](./HANDOFF.md)** と **[STATUS.md](./STATUS.md)** から読む。  
> コピペ用の引き継ぎプロンプトは **[HANDOFF.md の末尾 §7](./HANDOFF.md#7-別aiへのプロンプト例コピー用)** にある。

- **公開URL**: https://hoshimotoyasunori.github.io/saad-hub-mock/
- **リポジトリ**: https://github.com/hoshimotoyasunori/saad-hub-mock
- **引き継ぎ（必読）**: [HANDOFF.md](./HANDOFF.md) — 何を作るか・ASIS精査の仕方・同期ルール・**末尾にコピペ用プロンプト**
- **現状スナップショット**: [STATUS.md](./STATUS.md) — できている／できていない（日付付き）
- **要件定義**: [requirements.md](./requirements.md)
- **ASIS由来の導入状況（必読）**: [asis-capability-coverage.md](./asis-capability-coverage.md) — 何が導入済／未導入か、なぜASISで要ったか、無駄な管理をやめる方針
- **利用者目線の想定要望台帳**: [user-journey-requirements.md](./user-journey-requirements.md) — どこから起票するか・ポップアップか・下書きはどこか など操作の流れの問いと対応状況
- **システム文書一式（拡張前提）**: [docs/DOC-INDEX.md](./docs/DOC-INDEX.md) — システム要件定義・機能／非機能・データ・連携・権限・UI・ロードマップ等

---

## システム要件・開発文書（生きた文書）

現行UIモックを入力に、**本番開発にもつなぐ文書群**を `docs/` に置いています。いずれも **今後も拡張する**前提です。

| 入り口 | 内容 |
| --- | --- |
| **[docs/DOC-INDEX.md](./docs/DOC-INDEX.md)** | 文書体系の目次（必ずここから） |
| [docs/system-requirements.md](./docs/system-requirements.md) | **システム要件定義書（SRS）** |
| [docs/functional-requirements.md](./docs/functional-requirements.md) | 機能要件（✅／今後⬜） |
| [docs/roadmap.md](./docs/roadmap.md) | **今後の開発予定・フェーズ** |
| [docs/development-guide.md](./docs/development-guide.md) | 文書・機能の増やし方 |

非機能・データ・連携・セキュリティ・UI・用語・受け入れも同フォルダにあります（DOC-INDEX参照）。

---

## 別のAI／別担当への引き継ぎ

このリポジトリだけで開発を続行できます。手順は次のとおりです。

1. **最初に読む**: [HANDOFF.md](./HANDOFF.md) → [STATUS.md](./STATUS.md)（この2つで足ります）
2. **システム／本番寄りの要件**: [docs/DOC-INDEX.md](./docs/DOC-INDEX.md) → [docs/system-requirements.md](./docs/system-requirements.md) → [docs/roadmap.md](./docs/roadmap.md)
3. **必要なら続く**: [asis-capability-coverage.md](./asis-capability-coverage.md)（導入状況）／[user-journey-requirements.md](./user-journey-requirements.md) §12（残作業）／[requirements.md](./requirements.md)（モック要件ID）
4. **チャットに渡す文**: [HANDOFF.md 末尾 §7「別AIへのプロンプト例」](./HANDOFF.md#7-別aiへのプロンプト例コピー用) をそのままコピーして使う

HTMLを変えたら docs も同じ作業で更新する（[HANDOFF.md §5](./HANDOFF.md#5-変更時の必須ルールドキュメント同期)／[requirements.md §12](./requirements.md)）。

---

## ASISとの関係（要約）

全業務の網羅が目的ではない。一方で **一覧・各種管理画面（探す／承認する／締める）** は新でも置き場所が要る。刷新は「必要な管理を残し、Excel多重転記などの無駄な管理をやめる」こと。機能を何でも1画面にまとめない。

詳細な導入済・未導入の台帳は常に **[asis-capability-coverage.md](./asis-capability-coverage.md)** を正とする（Hubを変えたら同ファイルも更新）。

---

## ページ構成（ファイル）

```
saad-hub-mock/
├── index.html                   ← 公開の正入口（切替シェル）
├── saad-github-hub.html         ← PC版（GitHub型台帳）
├── saad-mobile-hub.html         ← スマホ版（ジョブ型）
├── manuals/                     ← 操作マニュアル（デモPDF）
├── HANDOFF.md                   ← 別担当／別AIの引き継ぎ正本（最初に読む）
├── STATUS.md                    ← 現状スナップショット（完了／未完了）
├── docs/                        ← システム要件・開発文書（拡張前提）
│   ├── DOC-INDEX.md             ← 文書目次
│   ├── system-requirements.md   ← システム要件定義書（SRS）
│   ├── functional-requirements.md
│   ├── roadmap.md               ← 今後の開発予定
│   └── …（非機能・データ・連携・権限・UI・用語・受入・開発ガイド）
├── requirements.md              ← 本モックの要件定義（HTML変更時は必ず更新）
├── asis-capability-coverage.md  ← ASIS由来機能の導入状況（正本コピー）
├── user-journey-requirements.md ← 利用者目線の想定要望台帳（正本コピー）
├── saad-hub-manual.md           ← Hub利用マニュアル（正本コピー）
├── system-page-structure.md     ← 全体ページ構成（正本コピー）
└── README.md                    ← 本ファイル
```

| ファイル | 役割 |
| --- | --- |
| `index.html` | **唯一の公開入口。** iframe で PC/スマホを載せ替え。下部に「自動 / PC / スマホ」切替バー |
| `saad-github-hub.html` | **PC向け本体。** 案件台帳・View・パネル・Inbox など GitHub 風の台帳UI |
| `saad-mobile-hub.html` | **スマホ向け本体。** 下部タブ＋ジョブ（今日やること／報告／承認）。Issue 語彙は出さない |
| `HANDOFF.md` | **別担当／別AIの入り口。** 何を作るか・ASIS精査・次の残件・同期ルール |
| `STATUS.md` | **現状スナップショット。** できている／できていない（日付付き） |
| `asis-capability-coverage.md` | **導入状況の常時台帳。** ASISでなぜ要ったか／残す・やめる・吸収／✅🟡⬜ |

開発比較用に各 HTML を単体で開くこともできますが、**デモの正は `index.html`（Pages のルート）**です。

---

## 表示の切替ロジック

| 条件 | 表示 |
| --- | --- |
| 幅 **820px 未満**（自動） | スマホ版（ジョブ型）→ `saad-mobile-hub.html?embed=1` |
| 幅 **820px 以上**（自動） | PC版（GitHub型）→ `saad-github-hub.html?pc=1` |

### 強制切替（デモ用クエリ）

| URL | 効果 |
| --- | --- |
| `?v=pc` | PC固定 |
| `?v=mobile` | スマホ固定 |
| `?v=auto` またはパラメータなし | 幅で自動 |

例:

- https://hoshimotoyasunori.github.io/saad-hub-mock/?v=mobile
- https://hoshimotoyasunori.github.io/saad-hub-mock/?v=pc

実機スマホ（幅520px未満かつ coarse pointer）では切替バーを隠します（`?v=` で強制可）。

---

## 画面構成の概要

### PC版（`saad-github-hub.html`）

GitHub Issues / Projects に近い **台帳メタファー**。

| 領域 | 内容 |
| --- | --- |
| グローバルナビ | ポータル／構成／案件台帳／マスタ／**台帳・登録**／業務アプリ一覧／マニュアル |
| 台帳・登録 | 案件以外の一覧・登録（定期点検・保証書・入金消込・取引先・在庫・施工予定・各種登録フォーム）。できること単位で並べた索引から開く |
| 業務アプリ一覧 | 営業・稟議・購買などアプリ単位の入口（旧称「スペース」） |
| マニュアル | 役割別操作手順の **PDFダウンロード**（デモPDFあり）＋画面上の要約 |
| 横断検索 | ヘッダの検索でEnter。進行中・Close済み・移行データ・マスタを1か所で |
| 案件台帳 | 行＝仕事。Saved views（自分・稟議・購買・施工・請求など） |
| 詳細パネル | **台帳エリア内の右オーバーレイ**（ページ全体モーダルではない）。本文｜メタ2カラム。左端ドラッグで幅変更（最小〜420px／最大エリアの2/3）。外側クリックでは閉じない（×／Escape）。Assignees列・右メタは固定幅 |
| 役割切替 | 営業／施工／拠点長などレンズを切替（見える列・View が変わる） |

### スマホ版（`saad-mobile-hub.html`）

同じデータの **ジョブ窓**。入口は「今日やること・報告・承認」。

| 下部タブ | 内容 |
| --- | --- |
| ホーム | いまやること／今日の予定／待ち状況 |
| 案件 | 担当案件カード → 案件詳細（進みステッパー＋主アクション） |
| ＋（中央） | 行動ランチャー（報告・申請など。WIP は実装予定画面） |
| 通知 | 人の言葉の通知 → 該当画面へ |
| メニュー | 稟議申請・資材申請・顧客仮登録・過去案件検索（実装済み）、ナレッジ・人事など（未実装は WIP 画面） |

ヘッダの ☰ は **ドロワーメニュー**（メニュータブと同系統の入口）。

---

## 設計の前提（要約）

- **データは1つ** — PC とスマホは別アプリではなく、同じ案件行・履歴を別の窓から見る
- **PC = GitHub型** — 一覧・View・管理・デスクワーク向け
- **スマホ = ジョブ型** — 移動中・現場・片手・数十秒の操作向け（GitHub Mobile の移植は不採用）
- **未実装機能** — 入口だけ先に固定し、「今後実装予定」画面で説明（PC と同じ方針）

詳細は [requirements.md](./requirements.md) および社内 `SAAD_UI/docs/mobile-ux-design.md` を参照。

---

## ローカル確認

```bash
# 本リポ
python3 -m http.server 8123
# → http://localhost:8123/

# または SANIX 側の作業コピー
cd SAAD_UI
python3 -m http.server 8123
# → http://localhost:8123/mocks/saad-hub.html
```

---

## 更新履歴（リポ上の主なコミット）

1. 初期公開（Hub モック）
2. PC / スマホを1URLに統合
3. モード切替・embed 全画面の調整
4. スマホをジョブ型UIへ。PC 内蔵の旧 GitHub Mobile シェルは使わない
5. 2026-09-25: 詳細＝台帳エリア内オーバーレイ＋リサイズ（〜2/3）＋外側クリックで閉じない／Assignees・右メタ固定幅（要件 P-07〜P-12）
6. 2026-09-25: Issue親子整合（P-13/14）。**HANDOFF.md / STATUS.md** を追加し、GitHub上で引き継ぎ可能に

---

## ドキュメント同期（必須）

HTMLを変えたら **同じ作業で** [requirements.md](./requirements.md) の要件ID・改訂履歴と、本READMEの画面概要を更新する。社内 `SANIX/SAAD_UI/docs/` の正本（`system-page-structure.md` 等）も揃え、Pages に載せる md は再コピーする。詳細は `requirements.md` §12。

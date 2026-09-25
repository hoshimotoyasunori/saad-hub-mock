# SAAD Hub モック（PC / スマホ自動切替）

1つのURLで画面幅に応じて表示が切り替わる **UIモック**（静的HTML）です。  
本番アプリではなく、**検証・デモ・合意形成用**の画面です。

- **公開URL**: https://hoshimotoyasunori.github.io/saad-hub-mock/
- **リポジトリ**: https://github.com/hoshimotoyasunori/saad-hub-mock
- **要件定義**: [requirements.md](./requirements.md)
- **ASIS由来の導入状況（必読）**: [asis-capability-coverage.md](./asis-capability-coverage.md) — 何が導入済／未導入か、なぜASISで要ったか、無駄な管理をやめる方針
- **利用者目線の想定要望台帳**: [user-journey-requirements.md](./user-journey-requirements.md) — どこから起票するか・ポップアップか・下書きはどこか など操作の流れの問いと対応状況

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
├── requirements.md              ← 本モックの要件定義
├── asis-capability-coverage.md  ← ASIS由来機能の導入状況（正本コピー）
├── user-journey-requirements.md ← 利用者目線の想定要望台帳（正本コピー）
└── README.md                    ← 本ファイル
```

| ファイル | 役割 |
| --- | --- |
| `index.html` | **唯一の公開入口。** iframe で PC/スマホを載せ替え。下部に「自動 / PC / スマホ」切替バー |
| `saad-github-hub.html` | **PC向け本体。** 案件台帳・View・パネル・Inbox など GitHub 風の台帳UI |
| `saad-mobile-hub.html` | **スマホ向け本体。** 下部タブ＋ジョブ（今日やること／報告／承認）。Issue 語彙は出さない |
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
| グローバルナビ | ポータル／構成／案件台帳／マスタ／**管理**／スペース／使い方 |
| 管理 | ASIS由来の一覧・台帳・登録（定期点検・保証書・入金消込・取引先・在庫・施工予定・各種登録フォーム）。できること単位で並べた索引から開く |
| 横断検索 | ヘッダの検索でEnter。進行中・Close済み・移行データ・マスタを1か所で |
| 案件台帳 | 行＝仕事。Saved views（自分・稟議・購買・施工・請求など） |
| 右パネル等 | Issue 詳細・タイムライン（Comment）・待ちバッジ |
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

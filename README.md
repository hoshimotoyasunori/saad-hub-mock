# SAAD Hub モック（PC / スマホ自動切替）

1つのURLで画面幅に応じて表示が切り替わります。

- **公開URL**: https://hoshimotoyasunori.github.io/saad-hub-mock/
- **幅 820px 未満** → スマホ版（ジョブ型）
- **幅 820px 以上** → PC版（GitHub型台帳）

## 強制切替（デモ用）

- PC固定: `?v=pc`
- スマホ固定: `?v=mobile`
- 自動に戻す: `?v=auto` またはパラメータなし

## ローカル確認

```bash
cd SAAD_UI
python3 -m http.server 8123
# → http://localhost:8123/mocks/saad-hub.html
```

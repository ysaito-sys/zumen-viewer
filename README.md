# 溶接図面ビューア（スキャナ画面）

QR コードを読み取って、対応する図面 PDF を表示する画面です。

## なぜ GitHub Pages に置いているか

Google Apps Script の Web アプリは、中身がサンドボックス化された iframe の
中で動きます。この iframe にはカメラ権限が渡されないため、とくに
iPhone / iPad ではカメラを起動できません（`NotAllowedError`）。

画面だけを iframe の外（＝通常の HTTPS サイト）に出すことで、
端末のカメラがそのまま使えるようになります。
図番の検索は、Apps Script 側に用意した API に問い合わせています。

```
[このページ] カメラ・QR デコード・PDF 表示
      ↕ fetch
[Apps Script API] 図番 → ファイル ID
      ↓
[Google ドライブ] PDF
```

## ファイル

| ファイル | 役割 |
|---|---|
| `index.html` | 画面本体。外部依存は QR 読み取りライブラリの CDN のみ |
| `robots.txt` | 検索エンジンの収録を拒否 |

## 設定

問い合わせ先は `index.html` の先頭にある `API_URL` です。
Apps Script 側を再デプロイして URL が変わった場合は、ここを書き換えます。

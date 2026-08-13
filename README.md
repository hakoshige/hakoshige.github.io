# hakoshige.github.io

**このリポジトリの中身は `.well-known/assetlinks.json` 1ファイルだけ。** サイトの本体ではない。

Android の App Links（譲渡QRのリンクを、選択ダイアログなしで MineralBox が直接開く仕組み）は、
**`assetlinks.json` を必ずドメインの根から取りに来る**:

    https://hakoshige.github.io/.well-known/assetlinks.json

⛔ `intent-filter` の `pathPrefix`（`/mineralbox-site/i`）は**取りに行く場所を変えない**。
だから `mineralbox-site` リポジトリの中に置いても検証は通らず、この user/org ページが要る。
（2026-08-13 にここで1回踏んだ。`pm get-app-links` が `1024`＝未検証のままだった）

- `.nojekyll` … これが無いと GitHub Pages（Jekyll）が `.` で始まるディレクトリを配信しない
- サイト本体は別リポジトリ `hakoshige/mineralbox-site`（`https://hakoshige.github.io/mineralbox-site/`）

## 指紋を足すとき

`sha256_cert_fingerprints` は配列で、**複数書ける**。いま入っているのは2つ:

1. 開発 PC の debug キーストア（実機テスト用）
2. `upload` 別名のリリース鍵

⛔ **Play App Signing の指紋がまだ入っていない。** ストアに出すと Google が自分の鍵で再署名するので、
**Play Console →「アプリの署名」の SHA-256 を3つ目として追記しないと、ストア版だけ検証が通らない。**

指紋を変えたら、実機で反映を確かめる:

    adb shell pm verify-app-links --re-verify com.hakoshige.mineralbox
    adb shell pm get-app-links com.hakoshige.mineralbox

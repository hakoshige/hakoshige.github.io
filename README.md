# hakoshige.github.io

**このリポジトリの出発点は `.well-known/assetlinks.json` 1ファイル。** アプリ紹介の本体は別リポジトリにある。

> **2026-08-18 追記: ルートに `index.html`（事業者 `hakoshige` の入口ページ）を置いた。**
> Play Console の組織アカウントで **「組織のウェブサイトの所有権確認」**が要るため。
> ルート `https://hakoshige.github.io/` は 2026-08-18 時点で 404 だった。
> ⚠️ Search Console の HTML ファイル方式なら**トップが 404 でも所有権確認自体は通り得る**が、
> **Play に「組織のウェブサイト」として登録する以上、トップが 404 なのは不適切**なので置いた。
>
> ⛔ **所有権の確認はルートで行うこと。** サブディレクトリ（`/mineralbox-site/`）で確認したあとに
> Play の「組織のウェブサイト」をルートへ差し替えると、確認をやり直すことになる。
> URL プレフィックスの所有権はルート配下をカバーするので、**ルートで通しておくほうが手戻りが少ない**。
> ⚠️ ただし Google が将来まったく再確認を求めない、という保証ではない。

Android の App Links（譲渡QRのリンクを、選択ダイアログなしで MineralBox が直接開く仕組み）は、
**`assetlinks.json` を必ずドメインの根から取りに来る**:

    https://hakoshige.github.io/.well-known/assetlinks.json

⛔ `intent-filter` の `pathPrefix`（`/mineralbox-site/i`）は**取りに行く場所を変えない**。
だから `mineralbox-site` リポジトリの中に置いても検証は通らず、この user/org ページが要る。
（2026-08-13 にここで1回踏んだ。`pm get-app-links` が `1024`＝未検証のままだった）

- `index.html` … 事業者 `hakoshige` の入口ページ（屋号・公開アプリ・連絡先）。⚠️ 体裁は `mineralbox-site` に合わせてある（明朝・`max-width: 34rem`）
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

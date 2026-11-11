# 業務スケジュール Android アプリ

claude.ai のアーティファクト(https://claude.ai/artifact/T92H67p3zpvHWTf744phFJ)を、Android のホーム画面から開けるアプリにしたもの。

## インストール
スマホの Chrome で [最新リリース](https://github.com/tabotabo5521/schedule-launcher/releases/latest) を開き、`schedule.apk` をダウンロードしてインストールする(「この提供元のアプリを許可」をオン)。

## 仕組み
- `android/` は Trusted Web Activity(androidbrowserhelper)のアプリ。アーティファクトの URL を Chrome で開くだけなので、claude.ai のログインと Google カレンダー等のコネクタがそのまま使える。
- アーティファクトは claude.ai の中でしかコネクタが動かないため、コードを別の場所に移さず URL を開く方式にしている。
- `.github/workflows/android.yml` が main への push でビルドし、リリースに APK を置く。
- 署名鍵はリポジトリに置かない。secrets `KEYSTORE_B64` / `KEYSTORE_PASSWORD` が無いと毎回使い捨て鍵になり、更新時は古いアプリのアンインストールが必要。
- ルートの `index.html` などは GitHub Pages 用の PWA ランチャー(端末がホーム画面追加に対応していれば使える)。

## 別のアーティファクトで使うとき
`android/app/src/main/AndroidManifest.xml` の `DEFAULT_URL`、`android/app/build.gradle` の `applicationId`、`strings.xml` のアプリ名、`mipmap-*` のアイコンを変えて push する。

# hugoで生成するサイトにGoogleAnalyticsのトラッキングIDを埋め込む
<!-- date:2019-04-21 24:32 -->

## 手順
hugoのルートディレクトリにある`config.toml`にGoogleAnalyticsのトラッキングIDの行を追加する。
```
googleAnalytics = "UA-xxxxxxxx-x"
```

上記の行を追加した後に`hugo`でサイトを生成すると`<head>`タグ内にトラッキングコードが追加される。

## トラッキングコードが追加されてませんけど？
その場合にはお使いのThemeファイルを少し修正する。

追加するファイルは恐らく
```
themes/テーマファイル名/layouts/partials/header.html
```
にあるはず。
`header.html`を開き、`<head>`タグの直下に以下の行を追加する。
```
{{ template "_internal/google_analytics.html" . }}
```

これで生成されるhtmlにトラッキングコードが追加される。はず。
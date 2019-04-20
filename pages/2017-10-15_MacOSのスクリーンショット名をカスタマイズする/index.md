# MacOSのスクリーンショット名をカスタマイズする
<!-- date:2017-10-15 09:00:00 -->

### はじめに
MacOSでスクリーンショットを撮るとファイル名に「スクリーンショット〜」と含まれるのが微妙だったり、作成されたファイルに微妙なドロップシャドウがついたりするのが気になっていたのでカスタマイズできないかググってみました。すると、
[「Will feel Tips」](http://ichitaso.com/mac/tips-for-os-x-screenshot/)さんのサイトで非常に詳しく分かりやすく説明されていたので参考にさせていただきました。

色々と試した結果、先頭の名前を「SS」にして、
```bash
defaults write com.apple.screencapture name "SS"
```

保存されるファイル名に日付や時間を含めないようにする
```bash
defaults write com.apple.screencapture include-date -bool false
```

という、上記サイトでもオススメされていた設定に落ち着きました。
さらにスクリーンショトを撮る際には`option`キーも加えることでドロップシャドウが含まれないようにしました。

便利です。
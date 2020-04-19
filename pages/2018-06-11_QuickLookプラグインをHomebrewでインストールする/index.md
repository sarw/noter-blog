# QuickLookプラグインをHomebrewでインストールする
<!-- date:2018-06-11 12:39:40 -->

## はじめに
MacOSの超便利機能である[Quick Look][1]に、これまた便利なPluginをインストールする。

```bash
brew cask install qlcolorcode qlstephen qlmarkdown quicklook-json qlprettypatch quicklook-csv betterzip qlimagesize webpquicklook suspicious-package
```

## 各プラグインの簡単な説明
* qlcolorcode : QLColorCode Quick Look plugin for source code with syntax highlighting.
* qlstephen : QLStephen is an Apple OSX QuickLook plugin that lets you view plain text files without a file extension. It is useful for reading files like:
* qlmarkdown : QLMarkdown is a simple QuickLook generator for Markdown files.
* quicklook-json : quick look json is a useful quick look plugin to preview JSON files. It will render files with a colorful view, and will allow to expand or compress nodes in the JSON tree.
* qlprettypatch : QLPrettyPatch is a QuickLook generator for patch files.
* quicklook-csv : A QuickLook plugin for CSV files
* betterzip : https://macitbetter.com/
* qlimagesize : QuickLook plugin to display the dimensions and size of an image in the title bar instead of the filename. Also preview some unsupported formats like WebP & bpg.
* webpquicklook : This is an open-source QuickLook plugin to generate thumbnails and previews for WebP images.
* suspicious-package : An Application for Inspecting macOS Installer Packages.

## webpquicklookは古い？
[webpquicklookプラグイン][2]は少なくとも４年以上更新されていない。比較的新しいプラグインとして[Quick Look Plugin for WebP Files][3]がある。しかしこのプラグインはHomeBrewではなく、自分でインストールする。（WebPなんて見られなくても問題ない？そうかも知れないね）

## hetimazipqlは後悔が停止された？
サイトにも繋がらなくなっていたため、代わりに[betterzip][4]を導入することにした

[1]: https://support.apple.com/ja-jp/guide/mac-help/mh14119/mac
[2]: https://github.com/dchest/webp-quicklook
[3]: https://github.com/emin/WebPQuickLook
[4]: https://macitbetter.com/
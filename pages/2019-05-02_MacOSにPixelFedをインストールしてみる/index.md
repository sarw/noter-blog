# MacOSにPixelFedをインストールしてみる
<!-- date:2019-05-02 04:52:30 -->

## はじめに
以前ios向けに提供されていたpathというアプリがあって、それを使うと家族限定のようなプライベートな、クローズドなSNSを楽しむ事ができた。しかし残念ながら2018年10月28日をもってサービス終了となってしまった。

その後、代替となるサービスを求めて色々と試して見たが、pathの使い心地に似たサービスを見つけることはできなかった。ほんの一時期 VERO を使っていたが、どうしても馴染めなかった。写真投稿時にグループメンバに通知してくれないことや、投稿範囲の指定などの概念が祖父母に理解させるのが難しい、など。

そんな中、[pixelFed](https://pixelfed.org/)という写真共有SNSを見つけた。自分でインストールしなくとも、[すでに構築されているインスタンス](https://fediverse.network/pixelfed)に参加する事で使用感などを試す事が出来る。試して見たところ、かなりpathの使い心地に近いものを感じた。自分でもインスタンスを立ち上げてみようと思った次第である。

## スタートからゴールまで
MacOSにてpixelFedをインストールし実行する

## 環境
- MacPro Early 2009
- MacOS High Sierra 10.13.6

## 手順
1. Homebrewでphpをインストールする。最新の7.3だとLaravel関係でエラーが出るので7.2にした。

``` bash
brew install php@7.2
echo 'export PATH="/usr/local/opt/php@7.2/bin:$PATH"' >> ~/.bash_profile
echo 'export PATH="/usr/local/opt/php@7.2/sbin:$PATH"' >> ~/.bash_profile
```

1. Composerのインストール

``` bash
brew install composer
```

1. Laravelのインストール

``` bash
composer global require laravel/installer
```

1. pathを通す

``` bash
echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> ~/.bash_profile
```

1. PixelFedのソースをダウンロードする

``` bash
cd ~/  #　もしくは任意の場所
composer create-project --prefer-dist pixelfed/pixelfed pixelfed
cd pixelfed
```

1. .envファイルの作成
設定項目の詳細については [公式のConfiguration](https://docs.pixelfed.org/master/configuration.html)を参考にする

とりあえずここまで。
続きはまた時間のある時に。。。
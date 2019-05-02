# mixhostにcomposerをインストールする
<!-- date:2019-05-02 04:27:53 -->

## はじめに
mixhostにcomposerをインストールしたさいの覚え書き。他のレンタルサーバにcomposerをインストールする記事は溢れているのが、一応自分の環境でも試した物を

## 環境
レンタルサーバのmixhost。サーバ番号はjp1からスペックアップサーバに引っ越しした版。高スペックだが、いくつか古い仕様が残っている。例えばドメイン毎にphp番号を指定する事が出来ない、とか。

## 手順
1. sshでログインし、以下のコマンドを実行する

``` bash
curl -sS https://getcomposer.org/installer | php
```

2. 下記コマンドを実行し、composerのバージョンなどが表示されて入れば正常にインストールされている。

``` bash
php composer.phar
```

## アンインストールは？
インストールディレクトリにある以下のファイルを削除する
- composer.phar
- .composer


# SSH秘密鍵を用いたログイン方法
<!-- date:2018-09-14 01:57:18 -->

## はじめに
契約しているレンタルサーバがSSH接続に対応しているなら鍵を作成すると接続が便利になる。たまにやると忘れてしまうので手順をメモしておく。

## 作業環境
Mac Pro (Early 2009)にMac OS High Sierra

## 手順
ざっくりした流れ

1. Terminal.appにて鍵のペアを作成する
2. 公開鍵をレンタルサーバへコピー＆登録＆パーミッション設定
3. 秘密鍵の名称変更と.bash_profileへaliasを追加


## 1 鍵のペア作成
Terminal.appを起動し以下のコマンドで鍵のペアを作成する

```
ssh-keygen -t rsa
```

名前はどうするか、など聞かれるがそのまま Enter で進め、パスフレーズは必要に応じて入力。すると `~/.ssh` に `id_rsa`と`id_rsa.pub` みたいな名前のファイルが出来上がる。 

## 2 公開鍵をレンタルサーバにコピーなど 
末尾に`.pub` が付いているのが公開鍵なので、このファイルをレンタルサーバの `~/.ssh`ディレクトリにコピーする。ディレクトリがない場合は作る。

レンタルサーバにsshログインし、`cd ~/.ssh`して以下のコマンドを実行し`authorized_keys`に登録する。

```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

その後パーミッションを適切に設定

```
chmod 600 ~/.ssh/authorized_keys
```

## 3 秘密鍵の名称変更と.bash_profile
ローカルの`~/.ssh/id_rsa`を`~/.ssh/severname`などと変更する。`servername`は自分が契約しているサーバ名を入れると分かり易い。

そんで`~/.bash_profile`に以下の行を追加

```
alias ssh1='ssh username@example.com -i ~/.ssh/servername'
```

上記の`ssh1`、`username`、`example.com`、`servername`は自分の環境に合わせて変更する。最後に

```
source ~/.bash_profile
```

を１度実行するか、ターミナルを立ち上げ直すと `.bash_profile`が読み込まれるので、今後は`ssh1`などと入力するだけでaliasのコマンドが実行される。

鍵を作成するときにパスフレーズを設定していない場合はそのまま接続されて便利だが、なんとなくパスフレーズは設定しておきたいところ。
# Gitのコミットに関連づけられるユーザ名とメールアドレスを設定する
<!-- date:2020-04-19 18:53:42 -->

## はじめに
Gitをインストールしただけの状態でコミットするとローカルコンピュータのホスト名が使われる。これを任意の別名に設定する方法をメモする

## ユーザー名の設定

``` bash
git config --global user.name "ユーザ名"
```

## メールアドレスの設定

``` bash
git config --global user.email "email@example.com"
```

## 正しく設定されたかの確認

``` bash
git config --global user.name
git config --global user.email
```

## 参考URI
- [Git でのユーザ名を設定する](https://help.github.com/ja/github/using-git/setting-your-username-in-git#)
- [コミットメールアドレスを設定する](https://help.github.com/ja/github/setting-up-and-managing-your-github-user-account/setting-your-commit-email-address)
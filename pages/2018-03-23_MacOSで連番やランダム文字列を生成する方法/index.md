# MacOSで連番やランダム文字列を生成する方法
<!-- date:2018-03-23 09:00:00 -->

## はじめに
MacOSにて連番やランダムな数字を生成したい時には`jot`コマンドを使う。
ランダムな文字列が欲しい時には`pwgen`とか`sf-pwgen`を使った方が良い。

```bash
NAME
     jot -- print sequential or random data

SYNOPSIS
     jot [-cnr] [-b word] [-w word] [-s string] [-p precision] [reps [begin [end [s]]]]

DESCRIPTION
     The jot utility is used to print out increasing, decreasing, random, or redundant data, usu-
     ally numbers, one per line.
```

## 1から10まで連番を作る
```bash
jot 10
```

## 100始まりの連番を10作る
```bash
#jot 生成数 開始番号
jot 10 100
```

## ランダムな文字列を10作る
```bash
#乱数を利用する場合は -r オプションを使う
jot -r 10
```

## 1から500の範囲内でランダムな数字を10作る
```bash
#jot -r 生成数 範囲始まり 範囲終わり
jot -r 10 1 500
```

## ランダムな8桁の数字フォルダを10作る
```bash
jot -r 10 10000000 99999999 | xargs mkdir
```

##### 参考にさせて頂いたサイト
・[くんすとの備忘録様](https://kunst1080.hatenablog.com/entry/2014/02/15/180842)
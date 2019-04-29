# MacOS High Sierra環境にてLogicool Trackman Marble TM-150rを使用したスクロール環境を作る
<!-- date:2019-04-25 11:43:35 -->

## はじめに
普段から愛用しているロジクールのトラックマン マーブル TM-150r。動きもスムーズで操作に全く不満がない。唯一、スクロールホイールが無いという点があるが今まではKarabinerを使用してスクロール環境を構築していたため、まさに隙のない状態だった。

しかし、MacOS SierraだかHigh Sierraの頃からKarabinerが使えなくなってしまい、さらに代替案として期待していたKarabiner Elementsでもスクロール環境を構築することができなかったため、スクロールバーを保持して上下にクリクリ動かすという辛い操作の日々であった。

[smooze](https://smooze.co/)なんていうソフトウェアも試したりしていたが、やはりボールを回転させる指の動きとスクロールの一致感には程遠く、長続きすることはなかった。

しかし、ついにHammerSpoonというソフトウェアに出会い、快適なスクロール環境を取り戻すことができたのである。

## 作業する環境
- MacPro Early 2009 + Mac Pro 2009-2010 Firmware Tool pached
- MacOS High Sierra 10.13.6

## 必要なソフトウェア
- [Hammerspoon](http://www.hammerspoon.org/)
- [Scroll Reverser](https://pilotmoon.com/scrollreverser/)
- [Logicool Control Center for Macintosh® OS X](https://support.logicool.co.jp/ja_jp/software/logitech-control-center-for-macintosh-os-x)

## ざっくりした手順
1. Logicool Control Centerにてボタンの設定をする
1. Hammerspoonをインストールする
1. Hammerspoonのメニューから 'Open Config' を開く
1. GitHubのKarabinerのissueのページにあるコードをコピペする
1. Hammerspoonのメニューから 'Reload config' を実行する
1. Scroll Reverserをインストールし、設定する

## 詳しい手順

### Logicool Control Centerにてボタンの設定をする
![設定画面]


## まとめ
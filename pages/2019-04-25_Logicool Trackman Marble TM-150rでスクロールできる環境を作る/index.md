# MacOS High Sierra環境にてLogicool Trackman Marble TM-150rを使用したスクロール環境を作る
<!-- date:2019-04-25 11:43:35 -->

## 2020.04.23 追記
- [Logicool Control Center for Macintosh® OS X](https://support.logicool.co.jp/ja_jp/software/logitech-control-center-for-macintosh-os-x) をダウンロードする際には必ず3.9.9にすること。3.9.10以降のバージョンではTM-150rを認識しなくなる（悲

追記ここまで

---

## はじめに
普段から愛用している[ロジクールのトラックマン マーブル TM-150r](https://www.logicool.co.jp/ja-jp/product/trackman?crid=7)は動きもスムーズで尚且つクリックも自然な力で行うことができ、操作に全く不満がない。スクロールホイールが無いという点だけが残念であるが、今まではKarabinerを使用してスクロール環境を構築していたた。こうなると逆にスクロールホイールなんてのは邪魔な存在となり、デザイン的にも実用的にもまさに隙のない状態だった。

しかし、MacOS SierraだかHigh Sierraの頃からKarabinerが使えなくなってしまい、さらに代替案として期待していたKarabiner Elementsでもスクロール環境を構築することができなかったため、スクロールバーを保持して上下にクリクリ動かすという辛い操作の日々であった。

時には[smooze](https://smooze.co/)なんていうソフトウェアも試したりしていたが、やはりボールを回転させる指の動きとスクロールの一致感には程遠く、長続きすることはなかった。

しかし、ついにHammerSpoonというソフトウェアに出会い、快適なスクロール環境を取り戻すことができたのである。

## 目指すゴール
トラックマンの左ミニボタンを押しながらトラックボールをグリグリ動かすことでスクロールさせる。もちろん上下左右対応で。

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
1. Hammerspoonのメニューから `Open Config` を開く
1. GitHubのKarabinerのissueのページにあるコードをコピペする
1. Hammerspoonのメニューから `Reload config` を実行する
1. システム環境設定にてHammerSpoonにコンピュータの制御を許可する
1. Scroll Reverserをインストールし、設定する

## 詳しい手順

### Logicool Control Centerにてボタンの設定をする
Mini Left Buttonの設定を下記画面と同じ状態にする。特に拘りが無ければここで割り当てるボタンナンバーを３にしておくのが無難。今まで３で失敗がないからね。

![設定画面](https://raw.githubusercontent.com/sarw/noter-blog/images/2019-04-29_logicoolControlCenterSetting.png)

### HammerSpoonのインストール
これはHomebrewで一発です。

``` bash
brew cask install hammerspoon
```

hammerspoonはbrew caskでインストールされるので、アプリケーションは`/Application`にインストールされている。いわゆる普通のアプリケーションフォルダにはいっているはず。

### Hammerspoonのメニューから設定ファイルを開く
アプリを起動すると、メニューバーにハンマーみたいなアイコンが出ているので、それをクリックして`Open Config`を選ぶ。

![メニュー画面](https://raw.githubusercontent.com/sarw/noter-blog/images/2019-04-29HammerSpoonOpenConfigMenu.png)

すると`init.lua`というテキストファイルが開くはず。

### GitHubのKarabinerのissueのページにあるコードをコピペする
`init.lua`が開かれたらば、以下のページにあるコードをコピペする。

[Githubのページ](https://github.com/tekezo/Karabiner/issues/814#issuecomment-415388742)

コピペするコードは以下

```
-- HANDLE SCROLLING WITH MOUSE BUTTON PRESSED
local scrollMouseButton = 2
local deferred = false

overrideOtherMouseDown = hs.eventtap.new({ hs.eventtap.event.types.otherMouseDown }, function(e)
    -- print("down")
    local pressedMouseButton = e:getProperty(hs.eventtap.event.properties['mouseEventButtonNumber'])
    if scrollMouseButton == pressedMouseButton 
        then 
            deferred = true
            return true
        end
end)

overrideOtherMouseUp = hs.eventtap.new({ hs.eventtap.event.types.otherMouseUp }, function(e)
     -- print("up")
    local pressedMouseButton = e:getProperty(hs.eventtap.event.properties['mouseEventButtonNumber'])
    if scrollMouseButton == pressedMouseButton 
        then 
            if (deferred) then
                overrideOtherMouseDown:stop()
                overrideOtherMouseUp:stop()
                hs.eventtap.otherClick(e:location(), 0, pressedMouseButton)
                overrideOtherMouseDown:start()
                overrideOtherMouseUp:start()
                return true
            end
            return false
        end
        return false
end)

local oldmousepos = {}
local scrollmult = -4	-- negative multiplier makes mouse work like traditional scrollwheel

dragOtherToScroll = hs.eventtap.new({ hs.eventtap.event.types.otherMouseDragged }, function(e)
    local pressedMouseButton = e:getProperty(hs.eventtap.event.properties['mouseEventButtonNumber'])
    -- print ("pressed mouse " .. pressedMouseButton)
    if scrollMouseButton == pressedMouseButton 
        then 
            -- print("scroll");
            deferred = false
            oldmousepos = hs.mouse.getAbsolutePosition()    
            local dx = e:getProperty(hs.eventtap.event.properties['mouseEventDeltaX'])
            local dy = e:getProperty(hs.eventtap.event.properties['mouseEventDeltaY'])
            local scroll = hs.eventtap.event.newScrollEvent({-dx * scrollmult, dy * scrollmult},{},'pixel')
            -- put the mouse back
            hs.mouse.setAbsolutePosition(oldmousepos)
            return true, {scroll}
        else 
            return false, {}
        end 
end)

overrideOtherMouseDown:start()
overrideOtherMouseUp:start()
dragOtherToScroll:start()

```

これをコピペしたら保存して閉じる。

### Hammerspoonにて設定ファイルを読み込ませる
次にHammerSpoonのメニューをもう一度開き、`Reload Config`を実行

![設定画面](https://raw.githubusercontent.com/sarw/noter-blog/images/2019-04-29HammerSpoonOpenConfigMenu.png)

↑これの一番上の項目ね。

### システム環境設定にてHammerSpoonにコンピュータの制御を許可する
システム環境設定 → セキュリティとプライバシー → アクセシビリティを開く。
「下のアプリケーションにコンピュータの制御を許可」の一覧にHammerSpoonがあるはずなので、チェックを入れる。文字がグレーになってチェックを入れられない時は、ウインドウ左下のカギをクリックして認証してから行う。

![設定画面](https://raw.githubusercontent.com/sarw/noter-blog/images/2019-04-29_SecurityAndPrivacySetting.png)

この時点でトラックマンの左ミニボタンを押したままトラックボールをグリグリ動かすとブラウザなどがスクロールされるはずである。もし動かない場合はHammerSpoonを終了して立ち上げなおすといいかな？
それでも動かない時はどこかが間違っていると思われるのでよく見直す。
左ミニボタンに割り当てた数字が違うか、もしくは違う番号にして試してみるか。試行錯誤です。どうしてもダメなら、お試しもできますし、[smooze](https://smooze.co/)を購入するってのも良いかも知れないね。

### Scroll Reverserをインストールし、設定する
さて、これでスクロールが出来るようにはなったけど、なんかスクロールの方向が逆だなぁとか自分のフィーリングと合わないなぁと感じた場合は[Scroll Reverser](https://pilotmoon.com/scrollreverser/)をインストールするのも手です。
読んで字のごとくマウスのスクロールを反転してくれます。
インストールはやっぱりbrewで一発。

``` bash
brew cask install scroll-reverser
```

## まとめ
そんなわけで無事にMacOS High Sierra環境でもトラックマンを安心して使い続ける事が出来るようになりました。
MacOS Mojaveでも使えるのかどうか、それは分かりませんがなんとなく使えるんじゃないでしょうかね。私のMacPro Early 2009ではMojaveのインストールは不可能なので確認しようがありません。もしMacを買い換えた際は試してみようと思います。次のMacがデスクトップなのかラップトップなのかまだ分かりませんが、必ずトラックマンは使うはずですから。

もう、トラックマン無しには生きていけないですから。
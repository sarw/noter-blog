# FlashAir_IoT_HubとIFTTTを連携し画像をクラウドへ自動転送する
<!-- date:2018-08-24 01:55:24 -->

## はじめに
FlashAirに記録された画像を逐次クラウドへアップロードする環境を整える。
以下の手順はほぼ公式サイト通りに進めたものの記録である。

参照URI : [FlashAir™ Developers - イメージのIFTTT連携](https://flashair-developers.com/ja/documents/tutorials/iot-hub/8/#ifttt_image)

## FlashAirをステーションモードにする
 - CONFIGの例

```
[Vendor]

LUA_RUN_SCRIPT=/bootscript.lua
DHCP_Enabled=NO
IP_Address=192.168.0.40
Subnet_Mask=255.255.255.0
Default_Gateway=192.168.0.1
Preferred_DNS_Server=192.168.0.1
CIPATH=/DCIM/100__TSB/FA000001.JPG
APPMODE=5
VERSION=F15DBW3BW4.00.03
CID=SDカード毎の値
PRODUCT=FlashAir
VENDOR=TOSHIBA
                                        
APPSSID=無線LANのSSID
APPNETWORKKEY=無線LANのパスワード
LOCK=1
WEBDAV=1
TIMEZONE=36
```

`DHCP_Enabled=NO`にしてIPアドレスを固定にした方が安定した。



## 手持ちのFlashAirをFlashAir IoT Hubに登録する
[FlashAir IoT Hub](https://iot-hub.flashair-developers.com/ja/) にてFlashAirの登録を行う。「アクセストークンの取得」「スクリプト」をダウンロードし、FlashAirのルートフォルダに展開する。「スクリプト」はフォルダ内の `.lua` ファイルを直接置くことに注意。
その後、`CONFIG`に`LUA_RUN_SCRIPT=/bootscript.lua`の行を追加する。この一文は`CONFIG`の一番上に記述した方が動作が安定していた。

## Webhookを作る
- IFTTTにログインし[Webhooks](https://ifttt.com/maker_webhooks)のページを開く。[CONNECT]という表示が出た場合はクリックする。その後、画面右上に「Documentation」というリンクが表示されるのでそこを開く。
- Your key is : で表示される自分のKeyをコピーする。
- [FlashAir IoT Hub](https://iot-hub.flashair-developers.com/ja)を表示し、FlashAir IoT Hubの「ファイル」の所にある「WebHookを設定」をクリック。
- 「event」には一意のイベント名を、「key」にはIFTTTで確認したkeyを入力する。このイベント名は後の工程のIFTTTでも使用するので覚えるかメモる。
- 登録ボタンを押して設定が完了する。

## IFTTTでAppletを作る
- IFTTTの[My Applets](https://ifttt.com/my_applets)を開く。
- 「this」を「Webhooks」で検索し「Receive a web request」を選択し、「Event Name」を入力する。この「Event Name」はFlashAir IoT Hubで作ったWebhookの「event」と合わせる必要がある。
- [that]に「google drive」を選択し「Upload file from URL」を選ぶ。
- 「File URL」には「Add ingredient」からValue1（画像のURL）を選択。
- 「File name」には「Add ingredient」からValue2（画像のファイル名）を選択。
- 「Google Drive folder path」には画像の保存先フォルダのパスを入力。

## CONFIGの編集
- `LUA_SD_EVENT=/upload_image.lua`を加える。
- 正常にアップロードできない場合は`LUA_RUN_SCRIPT=/bootscript.lua`を削除すると動作がより安定するらしい。
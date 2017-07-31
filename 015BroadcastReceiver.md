## BroadcastReceiver

### 目的
* BroadcastReceiverとは何か説明できる。
* ブロードキャストを受信し、任意の処理を実行できる。
* ブロードキャストを送信できる。(明示的・暗黙的ともに)

---
### BroadcastReceiverとは
* ブロードキャストしたIntentを受け取るための仕組み
* 明示的、暗黙的Intentの両方を受け取ることができる

### 設定
* 静的設定
  * AndroidManifestファイルにreceiverタグを設定
* 動的設定
  * registerReceiver()および unregisterReceiver()を呼んで設定

|設定方法|定義方法|特徴|非公開にできるか|
|:--|:--|:--|:--|
|静的|Manifestに<Receiver>を記述|・ アプリが初回起動してからアンインストールされるまでの間、Broadcast を受信できる<br>・システムから送信される一部のBroadcast（ACTION_BATTERY_CHANGED など）を受信できない制約がある|可|
|動的|プログラムでregisterReceiver(),unregisterReceiver()を記述|・静的BroadcastReceiverでは受信できないBroadcastでも受信できる<br>・Activity が前面に出ている期間だけBroadcastを受信したいなど、Broadcast の受信可能期間をプログラムで制御できる|不可|

* 非公開の場合の注意点
  * receiverのexported属性は明示的に「false」を書く
  * intent-filterは定義しない
  * 明示的Intentで発行する

---
### 確認問題
* BroadcastReceiverはどんな役割をもつコンポーネントですか?
  * ブロードキャストしたIntentを受け取るための仕組み
  * 明示的、暗黙的、両方を受け取ることができる
* BroadcastReceiverの設定にはどんな方法がありますか?
  * 静的設定：マニフェストにreceiverタグを記述
  * 動的設定：ソースにregisterReceiver(),unregisterReceiver()を記述
* BroadcastReceiverを使用する時はどんなことに気をつける必要がありますか?
  * 動的設定は非公開にすることができないため、非公開にしたい場合は静的設定にする必要がある。
  * 非公開にする場合は、マニフェストのexportedにfalseを書く
  * intent-filterは定義せず、明示的Intent

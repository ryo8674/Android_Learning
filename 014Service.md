## Service-Android Training

### 目的
* サービスが何か簡単に説明できる。
* サービスの違いについて説明できる（バインドされたサービスと通常のサービスに関して違い）
* ServiceとIntentServiceの違いに関して説明する事ができる。
* AIDLファイルとは何か簡単に説明できる。
* Serviceを使って何らかの処理を実行できる。

---
### Serviceとは
* 長時間かかる処理などを画面の状態と独立して行うための仕組み
  * バックグラウンドで処理ができる
* 複数のServiceを同時に処理できる
* ActivityやFragmentからだけでなく、別のアプリのコンポーネントからでも実行できる
* 起動方法(重複可)
  * Intent(startService()で起動)
    * ライフサイクル
      * onCreate
      * onStartCommand
      * -実行中-
      * onStopService/onStopSelf
      * onDestory
    * 一つの処理が完了しても特に返り値は返さない
    * 必要に応じて、処理が終わり次第、Serviceのプロセスを終了させる必要がある

  * Bind
    * ライフサイクル
      * onCreate
      * onBind
      * -実行中-
      * unbindService
      * onUnbind
      * onDestory
    * クラサバのインタフェースを持ち、バインドされたコンポーネントとプロセス間通信を行うことができる。
    * バインドされたコンポーネントが生き続けるかぎりServiceも生き続ける
    * 1つもなくなるとServiceは終了する
* AIDL
  * メソッドの戻り値
    * intやbooleanなどのプリミティブ型
    * Stringクラス、List、Map、CharSequence
    * Parcelableインターフェースを実装したクラス
  * Javaが自動生成される(暗黙的)
    * インターフェースなので記述されているメソッドは定義しないといけない

---
### 確認問題
* Serviceはどのような場面で利用するためのコンポーネントですか?
  * 長時間かかる処理などを画面の状態と独立して行う
* Serviceはデフォルトではどのスレッドで動作しますか？またスレッドを変えたい場合はどのような処理をする必要がありますか?
  * 通常、メインスレッド
  * HandlerThreadを利用して別スレッドを立て、Handlerを利用してServiceの停止処理をメインスレッドになげる。
* Serviceの起動方法には何がありますか？
  * startService
  * Bind
* それぞれの起動方法でServiceを停止させるためにはどうしますか？
  * startService
    * stopSelf()
  * Bind
    * unbindService

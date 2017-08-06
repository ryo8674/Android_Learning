### androidmanifest

#### 目的
*

#### ゴール
*

---
#### androidmanifestとは
* アプリに関する重要な情報をandroidシステムに提供する
  * アプリのJavaのパッケージ名を指定
  * アプリのコンポーネントを記述する
    * アプリを構成するアクティビティ、サービス、ブロードキャストレシーバ、コンテンツプロバイダなど
  * アプリのコンポーネントをホストするプロセスを指定する
  * アプリに必要なandroid APIの最小限のレベルを宣言
  * アプリにリンクする必要があるライブラリ

* 必須項目
  * Manifestタグ
    * ルート要素
      * xlmns:androidとpackage属性を特定する必要がある
        * xlmns:android
          * androidネームスペースを定義
        * package
          * androidアプリを識別するために必要な情報
  * Applicationタグ
    * androidmanifest.xmlファイルで定義するアプリの構成要素
      * アプリの設定に関するサブ要素を含んでいて、アプリに関する様々な指定ができる
        * label, activity, service, etc...

* versionCode, versionName
  * versionCode
  * 内部バージョン番号として使用する整数
    * アプリケーションのバージョンを示す整数値
    * アプリをバージョンアップするごとにインクリメントする必要がある
    * android marketにアプリがアップデートする際に、この値が登録値よりも大きい値になっているかチェックされる
  * versionName
    * ユーザに表示するバージョンとして使用される文字列(e.g. 1.0.0)
    * android marketでアプリのバージョンとしてユーザに伝えられる

* minSdkVersion, tagetSdkVersion
  * minSdkVersion
    * アプリを実行するために必要な最小のAPIレベルを指定する。
    * この値よりも低い場合、アプリのインストールを防ぐ。
    * この属性は必須
  * tagetSdkVersion
    * アプリのターゲットとなるAPIレベルを指定する整数。既定値：minSdkVersionで指定した値
    * 正確に動作することを確認してあることを保証する。

* Permission
  * コードの一部や端末上のデータへのアクセスを制限する機能を提供する。
  * カメラやネットワークなど一部機能を使用するには、Permissionを記載して、使用することを明示的に宣言しないと使えない。
  * ユーザはそのアプリがどのような機能を使用しているかを把握できる
  * android6.0以前
    * すべてインストール前に確認する
    * 許可しないとインストールできない
    * 問題点
      * インストール前にアプリがどのPermissionをどのように使うのか把握しづらく、Permissionに何が宣言されていようとそれが妥当か判断できない
      * 一度許可したアプリは永続的に許可され続けるのでユーザによるPermissionチェックが適切に働きづらい
      * Permissionを変更されるとユーザの手動アップデートが必要となるため、Permissionを追加したバージョンアップでアップデートが行ってもらえなくなったり、予め片っ端からPermissionを宣言しておくなどということが発生していた。

  * android6.0以降
    * Runtime Permission：リスクの高いPermissionについて、アプリ実行時に、アプリ内で許可を求める
    * メリット
      * Permissionを必要になったタイミングで求めることができる
      * ユーザがなぜそのPermissionが必要になったか理解しやすくなり、あとからアプリがどのような機能を使っているかを見ることができ、Permissionをすることもできる
      * Permissionを追加しても、自動的にアップデートが行われ、古いアプリを使い続けることが減る

```java
android.permission.*
```

* *はパーミッション名(下記：Runtime Permission一覧)

|name|内容|
|:--|:--|
|READ_CALENDAR |カレンダーの読み込み|
|WRITE_CALENDAR |カレンダーの書き込み|
|CAMERA |カメラ機能|
|READ_CONTACTS |連絡先の読み込み|
|WRITE_CONTACTS |連絡先の書き込み|
|GET_ACCOUNTS |ユーザーが使用しているアカウントの取得|
|ACCESS_FINE_LOCATION |詳細な位置|
|ACCESS_COARSE_LOCATION |大まかな位置|
|RECORD_AUDIO |オーディオの録音（マイク）|
|READ_PHONE_STATE |電話の状態を取得する|
|CALL_PHONE |電話をかける（直接発信するのではなく通話アプリをIntentで呼び出す場合は不要）|
|READ_CALL_LOG |通話履歴を取得する|
|WRITE_CALL_LOG |通話履歴を書き込む|
|ADD_VOICEMAIL |ボイスメールを追加する|
|USE_SIP |SIP( Session Initiation Protocol)を使用する|
|PROCESS_OUTGOING_CALLS |通話発信時のIntentを補足する|
|BODY_SENSORS |心拍数などの身体センサーを使用する|
|SEND_SMS |SMSを送信する|
|RECEIVE_SMS |SMSを受信する|
|READ_SMS |SMSを読む|
|RECEIVE_WAP_PUSH |WAP(Wireless Application Protocol）PUSHを受信する|
|RECEIVE_MMS |MMSを受信する|
|READ_EXTERNAL_STORAGE |外部ストレージから読み込む|
|WRITE_EXTERNAL_STORAGE |外部ストレージに書き出す|

その他Permissionは下記を参考<br>
http://pentan.info/android/app/permission_list.html

* 

---
### 確認問題
*

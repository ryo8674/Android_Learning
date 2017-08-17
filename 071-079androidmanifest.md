### androidmanifest

#### 目的
* AndroidManifestがもつ役割を理解する
* AndroidManifestになにを設定するのか理解する
* Permissionの役割を理解する
* Permissionの設定方法を理解する
* application属性になにを定義するのかを理解する
* AndroidManifestファイルのactivity要素に定義するものを理解する
* AndroidManifestでのBroadcastReceiverの設定方法を理解する
* AndroidManifestファイルのprovider要素の定義を行えるようになる
* AndroidManifestファイルのservice要素の定義を行えるようになる
* 定義される項目が何かを理解する

#### ゴール
* AndroidManifestの役割を説明できること
* uses-permission要素にあるname属性が何か理解し、適切な属性値を設定できるようになる
* application属性に設定する属性とその意味を説明できる
* activity要素に定義するものとその役割を説明できる
* AndroidManifestファイルのreceiver要素の定義をできるようになる
* AndroidManifestファイルのprovider要素の定義をできるようになる
* サービスの簡単な定義をすることができる

---
#### androidmanifestとは
* Androidアプリケーションにおいて必ず作成されるファイル
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

* 注意点
  * uses-permissionを設定すると暗黙的にuses-featureが定義されてしまう
    * uses-feature:
      * アプリが動作するのに必要不可欠な機能を指定
      * 要求する機能を持たないユーザはインストールできない

* **application**
  * マニフェストに記載されている事項のメイン要素で、子要素としてactivityやserviceなどがある

|属性|属性値|説明|
|:--|:--|:--|
|android:allowClearUserData|trueかfalse|	ユーザがこのアプリケーションで使うユーザデータを 削除できるかどうかを指定。デフォルトは "true" 。
|android:allowTaskReparenting	|trueかfalse|	このアプリケーション内の Activity が Task の親（Affinity）を変更可能かどうかを指定する。 デフォルトは "false" 。これは Activity 単位でも定義できる。
|android:debuggable| trueかfalse|	このアプリケーションがデバッグ可能かどうかを指定する。デフォルトは "false"
|android:description|	文字列|	このアプリケーションの説明文を記述する。
|android:enabled	|trueかfalse|	アプリケーション内のコンポーネントを初期化することが可能かどうかを指定する。 デフォルトは "true" 。これはコンポーネント単位でも定義可能。
|android:hasCode	|trueかfalse|	アプリケーションが自身のコードを持っているかどうかを指定する。 デフォルトは "true" 。これは、AliasActivity などの特殊な場面でのみ使われる属性。
|android:icon	|drawableリソースに対する参照|	アプリケーションのデフォルトアイコンを指定する。これはコンポーネント単位でも定義できる。
|android:label	|stringリソースに対する参照|	アプリケーションのラベル名称を指定する。
|android:manageSpaceActivity	|アクティビティのFull Qualified Name|	デバイス上のアプリケーションに使用されるメモリを管理する Activity 名を Full Qualified Name で指定する。この Activity は 要素で定義されている必要がある。
|android:name|	Application を継承したクラス名の Full Qualified Name|	Application を継承したクラス名を Full Qualified Name で指定。 この指定は通常必要なし。 この場合、Android は基本 Application クラスを使用する。
|android:permission	|文字列|	クライアントがアプリケーションを使うために必要な Permission 名を指定。 これは、アプリケーション全体で Permission を指定する簡単な方法。 各コンポーネントで個別に Permission を指定することもできる。
|android:persistent	|trueかfalse|	アプリケーションが常時稼動するべきかどうかを指定する。デフォルトは "false"
|android:process	|プロセス名|	このアプリケーションを実行するプロセス名を指定する。各コンポーネントで個別に指定することも可能。 デフォルトでは、Android は最初にコンポーネントを作成するときにプロセスを作り、 全てのコンポーネントはそのプロセス上で実行される。 デフォルトのプロセス名は、 要素で定義されたパッケージ名。
|android:taskAffinity	|文字列|	このアプリケーションのデフォルト Affinity を指定する。 デフォルトの Affinity は、要素で定義されたパッケージ名。
|android:theme	|文字列|	アプリケーションで採用するテーマ名を指定。

* **activity**
  * applicationにある属性以外の属性

|属性|属性値|説明|
|:--|:--|:--|
|android:stateNotNeeded	|trueかfalse|	Activityが状態を保存しなくても再起動できるかどうかを指定する。 true：onSavedInstanceStateが呼び出されず、onCreateにnullが渡される。 false：デフォルト
|android:screenOrientation|	別表|	Activityの方位を指定する。
|android:launchMode|	別表|	Activityの起動モードを指定する。
|android:alwaysRetainTaskState	|trueかfalse|	Task の状態を保持するかどうかを指定する。 デフォルトはfalse。 trueの場合：Taskの状態は常に保持 falseの場合：長時間放置するとRootActivity以外|のActivityが全てクリア この属性はRootActivityでのみ有効
|android:clearTaskOnLaunch|	trueかfalse|	Taskを直ちにクリアするかを指定する。 true：ユーザーが一瞬でもこのActivityを含むTaskを 離れると直ちにRootActivity も含めて全てのActivity をクリアする。 false：デフォルト。 この属性はRootActivityでのみ有効。
|android:multiprocess	|trueかfalse|	true：Activityのインスタンスが呼び出し元プロセスで動作する。 false：Activityのインスタンスは常に定義されたプロセスと同一プロセスで動作する。
|android:finishOnTaskLaunch	|trueかfalse|	true：一瞬でもユーザーがTaskを離れるとこのActivityがシャットダウンされる。 false：デフォルト
|android:excludeFromRecents	|trueかfalse|	true：最近起動したActivityのリストに自分が載らなくなる fale：デフォルト
|android:configChanges	|別表|	ここに指定した設定が変更されたとき、この Activity がそれをハンドリングできるようにする。
|android:allowTaskReparenting	|trueかfalse|	この Activity が、Taskの親を変更可能かどうかを指定する。この属性はandroid:launchMode が "standard" または "singleTop" の Activity でのみ有効
|android:exported	|trueかfalse|	この Activity が外部から呼び出されるかどうかを指定する。 true：IntetnFilterが一つでも定義されている場合はtrue false：同一アプリ内にあるコンポーネントから明示的インテントのみで呼ばれる。
|android:windowSoftInputMode	|別表|	ソフトウェアキーボードに関する設定を記述する。

  * screenOrientation

|値|意味|
|:--|:--|
|unspecified|	デフォルト。方位は特定しない。
|landscape|	横長の画面。
|portrait|	縦長の画面。
|user|	ユーザが現在設定している方位を使う。
|sensor|	端末のセンサーによって方位を決定。
|nosensor|	unspecified" と同じ。

  * launchMode

|値|意味|
|:--|:--|
|standard|	デフォルト。新しい Intent に応答するとき、新しいインスタンスが生成される。 Activityは複数のインスタンスを持つ。
|singleTop|	新しい Intent に応答するとき、もし自身の Activity が「現在のスタックにあり、しかも最上位である」場合に限り、 そのインスタンスが再利用される。Activityがスタックの最上位にない場合は新しいインスタンスが生成される。 Activityは複数のインスタンスを持つ。
|singleTask|	Activity は起動するときに新しいTaskを作り、そこに自身を配置する。その後、自身が別の Activity を起動しようとした場合、それを同じ Task 内に配置することができる。新しい Intent に応答するとき、もしこの Activity がその Task の最上位にあればこれを再利用し、その Intent に応答する。もしこの Activity の上に別の Activity が積まれていると、その Intent に応答することができず、Intent はドロップされる。
|singleInstance|	常に新しいタスクを生成し、自身のみを配置する。Activityは複数のインスタンスを持たない。

  * configChanges

|値|意味|
|:--|:--|
|mcc|	端末の地域コードの変更をキャッチ
|mnc|	端末のネットワークコードの変更をキャッチ
|locale|	ロケールの変更をキャッチ
|touchscreen|	タッチスクリーンの変更をキャッチ。（通常こんなことは起きません）
|keyboard|	キーボードの種類の変更をキャッチ。例えばユーザが外部キーボードを接続した場合など。
|keyboardHidden|	キーボードの Accessibility の変更をキャッチ。例えばユーザが端末をスライドさせてキーボードをしまった時など
|navigation|	ナビゲーションの種類の変更をキャッチ。（通常こんなことは起きません）
|orientation|	端末の縦横を反転させたことをキャッチ。
|fontScale|	フォントサイズの変更をキャッチ。

  * windowSoftInputMode

|値|意味|
|:--|:--|
|stateUnspecified|	キーボードの状態について、特に指定はしない。デフォルト。
|stateUnchanged|	キーボードの状態を、前回から変化させない。
|stateHidden|	Activity がアクティブ化されたとき、キーボードを隠す。
|stateAlwaysHidden|	この Activity にフォーカスがある間中、キーボードを表示しない。
|stateVisible|	Activity がアクティブ化されたとき、キーボードを表示する
|stateAlwaysVisible|	この Activity にフォーカスがある間中、キーボードを表示したままにする。
|adjustUnspecified|	キーボードのサイズについて、特に指定しない。
|adjustResize|	キーボードを表示させるために、Activity をリサイズする。

* **BoradcastReceiver**
  * 設定できる属性

|属性|属性値|説明|
|:--|:--|:--|
|android:enabled|t/f|システムによりブロードキャストレシーバをインスタンス化できるかどうかの指定。<br>true(default):可<br>false:不可<br>アプリケーションタグのenabled属性もtrueでないとインスタンス化できない|
|android:exported|t/f|コンテンツプロバイダが他のアプリケーションのコンポーネントにより使用可能かの指定。<br>true(default):可<br>false:不可<br>同じアプリケーションのコンポーネントから送信されたメッセージまたは同じユーザ ID のアプリケーションから送信されたメッセージのみ受信可能です。デフォルト値はブロードキャストレシーバが、インテントフィルタを含むかどうかに依存します。ブロードキャストレシーバを外部に公開することを制限する方法としてはこの属性の設定以外にもあります。レシーバにメッセージを送信可能な外部エンティティを制限するために許可を使用することもできます ( permission 属性参照) 。|
|android:icon|イメージ定義を含めた drawable リソースに対する参照|ブロードキャストレシーバを表現するアイコンです。設定されていない場合は、アプリケーション全体に設定されたアイコンを代わりに使用します。|
|android:label|文字列リソースへの参照|ユーザが読める提供されたブロードキャストレシーバのラベルです。この属性が設定されていない場合は、アプリケーション全体に設定されたラベルを代わりに使用します|
|android:name|ブロードキャストレシーバのFull Qualified Name(default:none)|BroadcastReceiver のサブクラスである、ブロードキャストレシーバ実装のクラスの名前です。|
|android:permission|文字列|ブロードキャスト送信者がブロードキャストレシーバにメッセージを送信するために保持する必要のある許可の名前です。この属性が設定されていない場合、application要素の permission 属性で設定された許可がブロードキャストレシーバに適用されます。どちらの属性も設定されていない場合は、このレシーバは許可により保護されません。|
|android:process|プロセス名|ブロードキャストレシーバが実行されているべきプロセスの名前です。通常は、アプリケーションのすべてのコンポーネントは、アプリケーションに対するデフォルトのプロセスで実行されます。application要素の process 属性により、すべてのコンポーネントに対し、異なるデフォルト値を設定することができます。しかし、各コンポーネントは自身にある process 属性でデフォルトを上書きすることができ、マルチプロセスの間で、アプリケーションとの分離をはかることができるようになります。|

* **ContentProvider**
  * http://yuki312.blogspot.jp/2012/06/android.html
  * provider要素の属性

|属性|属性値|説明|
|:--|:--|:--|
|android:authorities	|リスト|	１個以上のコンテンツプロバイダの有効範囲内にあるデータを識別する情報源のリストを指定する。情報源の名前は重複を避けるためにcom.example.provider.firstproviderのように表記される。 通常はコンテンツプロバイダのサブクラス名。デフォルトはなく、少なくても一つ以上の情報源が特定されなければならない。
|android:enabled	|true,false|	システムによりコンテンツプロバイダがインスタンス化できるかの指定。 デフォルトはtrue。application要素にもenabled属性があり、これはアプリケーション内のすべてのコンポーネントに適用される。 applicationとproviderの属性は、どちらもtrueにする必要がある。どちらかがfalseの場合、プロバイダは無効になる
|android:exported	|true,false|	他のアプリケーションからコンテンツプロバイダが使用可能かを指定する。API17以降ではデフォルトはfalse。以前ではtrue。基本的にfalse。permissionでより細かく制限をかける。
|android:grantUriPermissions	|true,false|	コンテンツプロバイダに対してアクセス許可を持たないものに対して一時的にアクセスを許可することができる。readPermission,writePermission,permissionで制限を強制的に乗り越えさせる。デフォルトはfalse。trueですべてのコンポーネントに対し、許可を与え、falseにしていてもgrant-uri-permissionで列挙されていればデータのサブセットに対して許可を与えられる。
|android:icon|drawableのリソース|	コンテンツプロバイダを表現するアイコンを指定する。これが設定されていない場合は、アプリケーション全体に設定されたアイコンを代わりに使用使用する。 ( application 要素の icon 属性) 。
|android:initOrder	|integer|	コンテンツプロバイダが、同じプロセスにより提供されるコンテンツプロバイダと関連して、インスタンス化されるべき順序の指定。コンテンツプロバイダの間に依存関係がある場合は、この属性をそれらに設定することにより、依存関係による必須の順序に従った作成を保証する。この値は、単純な数値で、大きい数値ほど先に初期化される。
|android:label	|stringリソース|	ユーザが読める提供されたコンテントのラベル。この属性が設定されていない場合は、アプリケーション全体に設定されたラベルを代わりに使用(application要素の label 属性参照 ) 。
|android:multiprocess	|true,false|	コンテンツプロバイダのインスタンスがクライアントプロセスごとに作成可能かどうかの指定。"true" はマルチプロセスで実行可能、"false" は不可。デフォルト値は "false" 。
|android:name	|string|	ContentProvider のサブクラスである、コンテンツプロバイダ実装のクラスの名前。これは完全修飾のクラス名 ( "com.example.project.TransportationProvider" のような) 。しかしながら、名前の最初の 1 文字をピリオドにすることにより、 manifest要素で特定したパッケージ名に付加され、簡略化することがでる。デフォルトはなし。この名前は特定されなければならない。
|android:permission	|string|	コンテンツプロバイダのデータを読み書きするためにクライアントが必要とする許可の名前。 この属性は読み込みと書き込みの両方を1回で設定する便利な方法。しかし、readPermission と writePermission 属性がこれよりも優先される。readPermission 属性も設定されている場合は、コンテンツプロバイダの問い合わせに対するアクセスを制御する。writePermission 属性が設定されている場合は、プロバイダのデータの変更に対するアクセスを制御する。
|android:process	|string|	コンテンツプロバイダが実行されているべきプロセスの名前。
|android:readPermission	|string|	コンテンツプロバイダを問い合わせするためにクライアントが必要とする許可。
|android:syncable	|true,false|	コンテンツプロバイダ配下のデータをサーバ上のデータを同期するかどうかの指定。"true" は同期させ、"false" は同期させない。
|android:writePermission	|string|	コンテンツプロバイダにより制御されているデータを変更するためにクライアントが必要とする許可

* **Service**

|属性|属性値|説明|
|:--|:--|:--|
|android:description	|string resource|	このサービスがどんな役割をするサービスかを記載する
|android:directBootAware	|true,false|	サービスを直接起動できるかを表す。デフォルトはfalse
|android:exported	|true,false|	異なるアプリ(IDの異なるアプリ)から呼び出せるかどうかを設定する。デフォルトはtrue
|android:enabled	|true,false|	シスタムがサービスをインスタンス化できるかどうかを設定する。デフォルトはtrue
|android:icon	|drawable resource|	サービスを表すアイコンをセットする。
|android:isolatedProcess	|true,false|	サービスを隔離されたプロセスで起動する。動作制限がある。
|android:label	|string resource|	ユーザーに見せることができるサービスの名前。
|android:name	|string|	アプリ内のサービス名を記載する。例："com.example.project.RoomService"
|android:permission	|string|	サービスを呼び出す為に必要なパーミッション
|android:process	|string|	サービスが動作するプロセス。通常はシステムが起動したプロセスで動作する。

---
### 確認問題
* AndroidManifestはアプリに対していくつ設定しますか？
  * 1つ
* Activityを新たに追加した場合、どのタグ内にどのタグを設定する必要がありますか？
  * applicationタグ内にactivityタグを設定
* SDKのバージョンを指定する場合の注意点は何ですか？
  * buildツールの設定で上書きされてしまう
* インターネットを利用したい場合、どこにパーミッションを指定しますか?
  * アプリケーションタグ
* パーミッションを指定する場合に何に気をつける必要がありますか?
  *
* applicationタグ内に設定する代表的なアプリのコンポーネントは何ですか?
  * activity
* 端末のホーム画面に表示されるアイコンはどこで設定しますか?
  * activityタグ内のアイコン
* 新たにActivityを作成した場合、AndroidManifest内のどこにActivityを記載する必要がありますか?
  * アプリケーションタグ内
* 画面の向きを固定した場合に設定する属性は何ですか？
  * screenOrientation

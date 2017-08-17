### Handler

#### 目的
* Handlerの利用方法を理解する
* Handlerを使ったpostの実施方法を理解する

#### ゴール
* post を用いて UI スレッドに処理を渡し、UIスレッドでその処理を行わせることができる。
* 「Handler、メッセージキュー、メッセージ、UIスレッド」のキーワードを元に Handler について説明ができる。
* sendMessage を用いて UI スレッドにメッセージを送信し、メッセージ内容によって適切な処理を行わせることができる。

---
#### Handlerとは
* ワーカースレッドからUIスレッドに処理を依頼する方法に、LooperとHandlerを利用するものがある

##### Looper
* 無限にループしながら自分が属したスレッドのMessage Queueに入ってきたMessageやRunnableオブジェクトを
順に取り出して、これを処理するHandlerに伝える役割
*　LooperはMessage Queueを持っています。Message Queueは他スレッド、または自スレッドから受け取ったMessageを管理する仕組みで、Messageを先入れ先出し法で管理
*　LooperはMessage Queueを使ってスレッドから受け取ったMessageやRunnableオブジェクトを取り出し、Handlerにそれらを実行させる
* Handlerはインスタンスを生成したスレッドで処理を実行

##### Handler
* LooperのMessage QueueからMessageやRunnableオブジェクトを受け取り、指定された処理を実行する
* HandlerはHandlerインスタンスを生成したスレッドのMessage Queueにバインドされる

|メソッド|説明|
|:--|:--|
|**void** handleMessage (Message msg)|	LooperがMessage Queueで取り出したMessageやRunnableオブジェクトを処理する
|**boolean** post (Runnable r)|	Message QueueにRunnableを渡す
|**boolean** sendMessage (Message msg)|	Message QueueにMessageを渡す
|**boolean** postAtFrontOfQueue (Runnable r)|	Message Queueの先頭にMessageを渡す
|**boolean** postDelayed (Runnable r, long delayMillis)|	delayMillisミリ秒後 に処理されるようにRunnableをMessage Queueに渡す
|**boolean** sendMessageDelayed (Message msg, long delayMillis)|	delayMillisミリ秒後 に処理されるようにMessageをMessage Queueに渡す

##### Message
* Messageとは、Handlerに送ることができるスレッド間通信する内容を格納するオブジェクト
* Messageが必要なときに常に新しいMessageオブジェクトを生成するとパフォーマンスが悪いため、Androidがシステムに作っておいたMessage Pool内のオブジェクトを再利用する

#### スレッドの作成方法
* Runnableインタフェースを実装
  * 処理を実行するRunnableとThreadの生成が分離されるので、役割の分担とクラス間の独立性を高めることができる
  * 注意点:RunnableはMessageと同様にHandlerで実行される処理のことであり、単体でスレッドを作成するものではないということ
* Threadクラスを継承

---
### 確認問題
* Handlerとはどんな役割をするクラスですか?
  * LooperのMessage QueueからMessageを受け取り、指定された処理を実行できる。
* Handlerを使ってスレッドへ処理を投げる場合、どんなことに注意する必要がありますか？
  * Looperから渡されたか、そのスレッドでHandlerを生成したのかを意識する必要がある

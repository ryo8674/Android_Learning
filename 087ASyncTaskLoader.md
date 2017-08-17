### ASyncTaskLoader

#### 目的
* AsyncTaskLoaderの役割を理解

#### ゴール
* AsyncTaskLoaderを利用することができる

---
#### Loaderとは
* Android3.0から導入された、非同期でのデータロードを行うためのクラス
* 利用することでActivityやFragmentのライフサイクルと分離して非同期処理を行うことができる
* 拡張することは可能だが、直接Loaderクラスを継承することは推奨されていない(Loaderは扱いにくい)
* 代わりに継承したAsyncTaskLoaderやCursorLoaderを利用する
* 参考<br>
http://yuki312.blogspot.jp/2012/02/loader.html

#### 利用時に必要なこと
* Loaderを継承したサブクラス
* LoaderManager.LoaderCallbacksを実装したクラス
* LoaderMangerを呼び出すためのActivityやFragment
  * LoaderはLoaderManagerを通じて操作することが前提となっている

#### 主なメソッド群
* startLoading
  * Loaderを開始するメソッド
  * Loaderを呼び出したActivityやFragmentのonStartのタイミングで自動的に呼ばれる。
  * 結果のロードが完了し、通知の準備ができればメインスレッドのコールバックが呼び出される。
    * 前回のロードが完了済みかつ有効である場合は即コールバックが呼び出される
  * コールバック通知はstopLoadingで一時停止することができる
  * データソースに対するForceLoadContentObserverを内包しており、データセットソースの変更検知もloaderが行なってくれる
  * startLoadingを呼び出すとLoaderの内部状態が更新される
    * 開始状態：true/リセット状態：false/abandon状態/false
    * それぞれはメソッドで取得可能
    * startLoadingは状態の更新後、サブクラスレスポンスのためにonStartLoadingを呼び出す
  * startLoadingメソッドの注意点
    * 直接呼び出すとLoaderの管理に影響が出るため、避けるべき
    * 常にメインスレッドから実行する必要がある

* onStartLoading
  * サブクラスはLoader開始時の実装をここで行う
  * startLoading()経由で呼び出されることが前提
  * 直接呼び出すことは非推奨
  * このメソッドもメインスレッドから実行する必要がある

* stopLoading
  * Loaderを停止し、startLoadingが呼ばれるまでデータの更新通知も停止する。
  * LoaderManager経由でLoaderを管理している場合、関連するctivityやFragmentが停止される時、このメソッドはLoaderManagerによって自動的に呼び出される
  * ここでデータセットを無効にすべきではなく、クライアントはLoaderが最後に通知したデータ結果を自由に使用できるようにすべき
  * Loaderが停止している間はデータセットが更新されてもそれがクライアントに通知されることはない。
    * Loaderの再開時、正しい値(takeContentChangedの返り値)を保証するためにデータセットの監視は続けられる
  * stopLoadingメソッドを呼び出すことでLoaderの内部状態は更新される
    * 開始状態：false
    * stopLoadingは状態更新後、サブクラスレスポンスのためにonStopLoadingを呼び出す
  * 注意点
    * 直接呼び出すとLoaderの管理に影響が出るため、避けるべき
    * 常にメインスレッドから実行する必要がある

* onStopLoading
  * サブクラスはLoader開始時の実装をここで行う
  * stopLoading()経由で呼び出されることが前提
  * 直接呼び出すことは非推奨
  * このメソッドもメインスレッドから実行する必要がある

* abandon
  * LoaderManager経由でLoaderを再起動した際にLoaderManagerから自動的に呼び出されるメソッド
  * reset()前に呼び出される
    * Loaderはabandon状態になっても現在のデータを保持し続けるが、更新されてもユーザに通知しない
  * abandonを呼び出すことでLoaderの内部状態が更新
    * abandon:true
    * abandonは状態の更新後、サブクラスレスポンスのためにonAbandonを呼び出す
  * 注意点
    * 直接呼び出すことは非推奨

* onAbandon
  * サブクラスはLoaderが不要となったときの実装をここで行う
  * abandon状態はLoaderが不要になったことを指す
    * リセットされるときはonResetが呼ばれるため、onAbandonが呼び出された時のLoaderはstart→resetの中間的な状態であると言える
  * abandon状態であるLoaderにクライアントは興味を持たない
    * Abandonなユーザに通知を送ってはいけない
    * Loader.onResetが処理されるまではLoaderは通知したデータを有効な状態に保持し続ける必要がある
  * abandon()経由で呼び出されることが前提
  * 直接呼び出すことは非推奨

* reset
  * Loaderを破棄する場合にLoaderManagerから自動的に呼ばれるメソッド
    * resetによりLoaderは破棄される
  * 再度呼び出されることはない
    * Loaderはその時点で解放できるすべてのリソースを解放する必要がある
    * resetのあとでstartLoadingが呼ばれることもあるため、再実行可能である必要がある
  * resetを呼び出すことでLoaderの内部状態が更新される
    * 開始状態：false/リセット状態：true/abandon状態：false/データソース変更状態：false
  * Loaderの状態更新前にサブクラスレスポンスのためにonResetを呼び出す
  * 注意点
    * 直接呼び出すことはLoaderの管理に影響がでるため避けるべき
    * 常にメインスレッドから実行する必要がある

* onReset
  * サブクラスはLoaderのリセット要求時の実装をここで行う
  * reset経由で呼び出されることが前提
  * 直接呼び出すことは非推奨
  * このメソッドもメインスレッドから実行する必要がある

* forceLoad
  * Loaderによるロードを強制する
  * startLoadingとはことなあり、以前にロードしたデータは全てキャンセルされ、新しいものに置換される
  * サブクラスレスポンスのためにonForceLoadを呼び出す
    * 通常、Loaderが開始状態の場合にこれを呼び出すべき
  * 常にメインスレッドから実行する必要がある

* onForceLoad
  * サブクラスは強制ロード要求時の実装をここで行う
  * このメソッドもメインスレッドから実行する必要がある

* onContentChanged
  * ForceLoadContentObserverがデータセットソースの変更を検知したときにコールされるメソッド
  * default:Loaderが開始済みの場合にforceLoadを呼び出し、違う場合は、takeContentChangedがtrueを返すようにフラグを設定
  * 常にメインスレッドから実行する必要がある

* takeContentChanged
  * Loaderの停止中にデータセットに変更があったかどうかを取得
    * 変更時：true、フラグはリセットされる

* deliverResult
  * クライアントへロード結果を送信
  * サブクラスから呼び出されることを想定しており、メインスレッドで実行する必要がある

* isStarted
  * Loaderが開始状態かを返却
    * True:startLoadinが呼び出され、stoploadingまたはresetが呼び出されていない状態

* isAbandoned
  * Loaderが不要となったかどうかを返却
  * abandon状態のLoaderは現在のデータを保持するが、それが更新されてもユーザに通知しない

* isReset
  * Loaderがリセット状態かを返却
    * True:Loaderがまだ１度も開始されていない状態、またはresetがすでに呼び出されている状態

#### Loaderの状態変化
|メソッド|isStarted|isReset|isAbandon|
|:--|:--|:--|:--|
|startLoading|T|F|F|
|stopLoading|F|F|F|
|abandon|F|F|T|
|reset|F|T|F|

#### LoaderManager
* Loaderを管理するためのクラス
* 各ActivityやFragmentごとに1つ割り当てられ、何度LoaderMana

##### LoaderManagerのメソッド
* getLoaderManager
  * 正確にはActivity,Fragmentのメソッド
    * 呼び出したActivity,Fragmentに紐づくLoaderを取得
  * LoaderManagerはgetLoaderManagerを初めて呼び出したタイミングで生成され、Activity・Fragmentによってライフサイクルが管理
  * onStart時に開始されるため、Activity・Fragmentでは必ずonStartが呼ばれる前にLoaderManagerを**初期化**しておく必要があり
* initLoader
  * LoaderManagerを使って複数のLoaderを管理したい場合は、LoaderごとにIDを割振る必要があり、initLoaderメソッドで指定したIDによってLoaderを初期化・生成する
    * Loaderが生成されると、Loader.onCreateLoaderがコールバックされる
  * 指定したIDに紐づくLoaderがすでに存在している場合、Loaderは初期化されませんが、Loaderへのコールバックが、指定されたインスタンスで上書き
    * 引数のargsは無視されるため、Bundleで渡された値を利用することができない
  * initLoaderはActivity・FragmentのonCreateまたはonCreateActivityで利用するべきメソッドですが、コンフィギュレーションが変わってもLoaderは破棄・再生成されず再利用される
    * すでにLoaderManagerがLoaderを持っている場合、コンフィギュレーションの変化でonCreateが再度コールされても、Loaderを生成するonCreateLoaderが再び呼ばれることはない
    * Loaderが再利用される際も引数のargsは無視される
* restartLoader
  * 引数のIDに指定されているLoaderを再生成
  * 既存のLoaderは必要に応じてキャンセル、停止、破棄される
  * 生成されるLoaderは引数argsを持つ新たなLoaderとなるが、同じIDに紐づくLoaderが複数作成されていて、それらが実行中の場合は再生成しても既存のLoaderの処理が完了するまで新しいLoaderを起動できない
  * 新規でLoaderが作成されると、古いLoaderは無効となり、コールバックは通知されなくなる
* destroyLoader
  * 引数のIDに紐付いたLoaderを停止・破棄します。
  * 対象のLoaderがデータをユーザーへ通知していた場合は、onLoadFinished→onLoaderResetがコール


---
#### ASyncTaskLoaderとは
* AsyncTaskLoaderはWorkerとしてのAsyncTask(ロードタスク)を内部にもつLoader
* AsyncTaskで行なっていた処理を、メインスレッドで行うべき処理と、バックグラウンドで行うべき処理に分離して行うことができるクラス
* イメージ図<> ![](http://public-blog-dev.s3.amazonaws.com/wp-content/uploads/2012/06/AsyncTaskLoader.png)

##### メソッド
* onLoadInBackground, loadInBackground
  * Loaderタスクのワーカースレッドから呼び出される
  * onLoadInBackgroundはロード処理の結果を返す必要がありますが、基本的にワーカースレッド間で結果を返すだけで、メインスレッドへ結果を返す場合はdeliverResult(メインスレッド)メソッドを利用
  * loadInBackgroundメソッドはonLoadInBackgroundメソッドからコールされる
* cancelLoad
  * 現在のLoaderのタスクをキャンセルする
  * メインスレッドから呼び出す必要がありますが、処理自体はワーカースレッドで動作しているため、即時キャンセルできない
* onCanceled
  * Loaderタスクが完了前にキャンセルされた場合にコールされる
  * キャンセルされたタスクに関係するデータをここでクリア

#### AsyncTaskの問題点
* ネットワーク通信などのインフラに近い処理と、結果を受けてUIを更新するなどの表示処理が同じクラスに混在してしまい、アクティビティやFragmentに依存しやすい

#### メリット
* 処理結果をキャッシュとして持っているため、次回からは再処理することなく結果を取得できる
* コンフィグを変化させても、Loaderを再設定すれば再処理することなく最終結果を取得できる
* Loaderはデータソースを監視してるため、内容が変更された際に新しい結果を取得できる
* 非同期の処理がLoaderManagerで管理されるため、ActivityやFragmentと分けて処理を実行できる
* UIスレッドを必ずしも必要としない

#### デメリット
* 画面の状態をただしく理解した上で実装しないと、エラーハンドリングができない
* 自由にカスタマイズできる分、非同期処理の知識が必要
* 進捗を常に表示するようなUIスレッドとの密接な処理ができない

#### よくある間違いと回避方法
* 意味のないLoader IDを作成する
  * Loaderの再利用の妨げとなり、混乱にしかならないので、Loaderの種類ごとに、単一一意のIDを使用する
* アプリ内のすべてのローダーに対してのIDを定数で作成する
  * 各LoaderManagerは 独立しているので、Activity や Fragment内でローダーの種類ごとに privateな定数を作成する
* FragmentManager Exceptions を回避する
  * LoaderCallbacks で直接 FragmentTransaction を作成することはできない(DialogFragmentと利用する場合など)
    * FragmentTransaction をディスパッチするハンドラを作成

##### 参考
https://wiki.toridge.com/index.php?android-AsyncTaskLoader

---
### 確認問題
* AsyncTaskLoaderはどんなことを実現するためのクラスですか？
  * AsyncTaskで行なっていた処理をメインスレッドで行うべき処理と、バックグラウンドで行うべき処理に分離して行うことができるクラス
* AsyncTaskLoaderを使って非同期処理を行う場合、何クラスを利用してLoaderの管理を行いますか？
  * LoaderManagerクラス

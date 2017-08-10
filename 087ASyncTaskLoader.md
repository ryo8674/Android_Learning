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
* LoaderManager


---
#### ASyncTaskLoaderとは
* AsyncTaskLoaderはWorkerとしてのAsyncTask(ロードタスク)を内部にもつLoader
* メインスレッドで行うべき処理と、バックグラウンドで行うべき処理を分離したもの
* イメージ図<> ![](http://public-blog-dev.s3.amazonaws.com/wp-content/uploads/2012/06/AsyncTaskLoader.png)


#### AsyncTaskの問題点
* ネットワーク通信などのインフラに近い処理と、結果を受けてUIを更新するなどの表示処理が同じクラスに混在してしまい、アクティビティやFragmentに依存しやすい

#### メリット
* 処理結果をキャッシュとして持っているため、次回からは再処理することなく結果を取得できる
* コンフィグを変化させても、Loaderを再設定すれば再処理することなく最終結果を取得できる
* Loaderはデータソースを監視してるため、内容が変更された際に新しい結果を取得できる

#### メソッド
* onLoadInBackground
  * ローダタスクのワーカースレッド上から呼び出されます。
  * ワーカースレッド上で実行されるonLoadInBackgroundから直接、結果データをクライアントへ返却すべきではありません。
  * 結果の返却はメインスレッド上で呼び出されるdeliverResult()内で行います。
  * メインスレッドに結果を返却したい場合はdeliverResultをオーバーライドすることでそれが可能になります。
  * onLoadInBackgroundはロード処理の結果を返す必要があります。
  * onLoadInBackgroundは、サブクラスレスポンスのためにloadInBackgroundをコールします
* loadInBackground
* cancelLoad
  * 現在のロードタスクをキャンセルしようとします。
  * ロードタスクはバックグラウンドで動作しているため、キャンセル操作は即時反映されません。
  * 実行中のロードタスクの場合、この要求によってロードがキャンセルされます。もし、ロード中に他のロード要求があったとしてもロードが完了するまで保持されます。
  * ローダタスクの処理が完了すると、タスクの状態はクリアされます。
  * ロードをキャンセルできなかった場合はfalseを返します。
  * ロードが既に完了していた、あるいは、まだstartLoadingがコールされていない場合でもfalseを返します。
  * このメソッドは常に**メインスレッド**から実行する必要があります。

* onCanceled
  * ローダタスクがそのタスクを完了する前にキャンセルされた場合にコールされます。
  * ここでキャンセルされたタスクに関係するデータを破棄することができます。
* setUpdateThrottle
  * Throttleはクエリ発行頻度を調整する為の弁の役割を持ちます。
  * 引数delayMSは発行頻度を決めるミリ秒単位の調整値です。
  * タスクの完了(onLoadInBackground)から次のローダタスクが開始されるまでの最小の待ち時間を指定できます。


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
*

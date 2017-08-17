### ASyncTask

#### 目的
* AsyncTaskの利用方法を理解

#### ゴール
* AsyncTaskの各メソッドの役割・利用方法を説明できる

---
#### ASyncTask
* ThreadやRunnableを意識することなく、メインスレッドとは別のスレッドで処理を行うことができるようになるクラス
* バックグラウンド処理とUIスレッドに対してHandlerを使用することなく処理結果を返すことができる
* このクラスはASyncTaskを継承したクラスを作成して利用する必要がある

#### メソッド
1. onPreExecute()
  * doInBackgroundメソッド実行前にメインスレッド（UIスレッド）で実行される
  * 非同期処理前に何か処理を行いたい時に使用します。
  * UIスレッドで非同期処理を行う前に呼ばれる
2. doInBackground()
  * メインスレッドとは別のスレッド（ワーカースレッド）で実行される
  * 非同期で処理したい内容（時間のかかる処理）を記述
  * このメソッドだけは必ず実装する必要がある
  * 処理が終了したら、このメソッドから処理結果をUIスレッドに返す
  * onPreExecute()終了後にすぐに呼び出される
  * 長時間かかる処理をここで行い結果をUIスレッドに返す。 実行はワーカースレッドで行われる
3. onProgressUpdate()
  * メインスレッドで実行される
  * 非同期処理の進行状況をプログレスバーで表示したい時などに使用
  * publishProgress(Progress...)がdoInBackgroundで呼ばれた場合にのみ呼びだされ、実行
  * doInBackground()で、publishProgress()が呼ばれた場合にUIスレッドで呼び出し
4. onPostExecute()
  * doInBackground()メソッド実行後にメインスレッドで実行
  * doInBackground()メソッドの戻り値をこのメソッドの引数として受け取り、その結果を画面に反映させることができる
  * doInBackground()の処理が終わったあとにUIスレッドで呼び出し
  * doInBackground()の結果をこのメソッドで受け取る
5. onCanceled
  * cancel(boolean)がUIスレッドで呼ばれ、isCanceled()がtrueになった場合、doInBackground()での処理が終了し、結果が返ってきた後に、onPostExecuteの代わりに呼ばれる

#### スレッドのルール
* AsyncTaskクラスはUIスレッドで読み込まれなければならない。
* このクラスのタスクインスタンスはUIスレッドで作られなければならない。
* このクラスのメソッドを手動で呼び出してはならない。
* タスクは一度だけ実行される。（２つ目のタスクが実行されると例外が発生する。）

##### バージョンの違い
* AsyncTaskには２つの実行モードがありAPIレベルにより実行モードが異なる
* APIレベル12以下
  * THREAD_POOL_EXECUTORのみ
* APIレベル13以上
  * THREAD_POOL_EXECUTOR, SERIAL_EXECUTOR(デフォルト)
<br>
* THREAD_POOL_EXECTOR
  * 複数のバックグラウンド処理を並行して行われる
* SERIAL_EXECUTOR
  * 複数のバックグラウンド処理を1つずつ順に行われる

#### 注意点
* ActivityやFragmenrのライフサイクルに対応していない
  * Activityが破棄されたあともonPostが呼ばれる
  * コンフィグが変わったときにバグが発生しやすい

#### AsyncTaskの中のリスナー、コールバック
* AsyncTaskの各コールバックメソッドは役割を考えるとリスナーとコールバックに分けられる
* onProgressUpdate()はdoInBackground()でpublishProgress()が呼ばれるたびに呼び出される
  * リスナー
* そのほかのメソッドはタスク生成時に1度だけ呼ばれる
  * コールバック

---
### 確認問題
* AsyncTaskとは何ですか?
  * メインスレッドとは別のスレッドで処理を行うことができるようになるクラス
* AsyncTaskの中でUIスレッド、ワーカースレッドで実行されるメソッドをそれぞれ答えてください。
  * ワーカースレッド
    * doInBackground
  * UIスレッド
    * それ以外
* どのような順番でAsyncTaskのメソッドは呼ばれますか?
  * onPreExecute
  * doInBackground
  * onProgressUpdate
  * onPostExecute

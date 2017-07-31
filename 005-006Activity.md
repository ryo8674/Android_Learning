## Activity
1. Activityがユーザに見えるようになる直前に呼ばれるメソッド
  * onResume()：
2. 下記の挙動を行った場合、コールバックメソッドがどのような順番で呼ばれるか答えてください。


*  A を起動

|順番|メソッド|
|--:|--:|
|1.|onCreate()|
|2.|onStart()|
|3.|onResume()|

  - AからBを起動

|順番|メソッド|
|--:|--:|
|1.|onCreate()|
|2.|onStart()|
|3.|onResume()|
|4.|onPause()|
|5.|onCreate()|


- Aからスリープ

|順番|メソッド|
|--:|--:|
|1.|onCreate()|
|2.|onStart()|
|3.|onResume()|
|4.|onPause()|
|5.|onStop()|

- Aからホーム

|順番|メソッド|
|--:|--:|
|1.|onCreate()|
|2.|onStart()|
|3.|onResume()|
|4.|onPause()|
|5.|onStop()|

- Aから電源ボタン

|順番|メソッド|
|--:|--:|
|1.|onCreate()|
|2.|onStart()|
|3.|onResume()|
|4.|onPause()|
|5.|onStop()|


- BをバックキーでAに戻る

|順番|メソッド|
|--:|--:|
|1.|onCreate()|
|2.|onStart()|
|3.|onResume()|
|4.|onPause()|
|5.|onCreate()|
|6.|onStop()|
|7.|onRestart()|
|8.|onStart()|
|9.|onResume()|

3. Activityの破棄は？
  * OSのガベージコレクション
    * finish()
    * onDestroy,onStop()が呼ばれた状態で放置

## Instance State
* onSaveInstanceState
  * OS 判断でActivityが強制的に終了・停止させられる場合に、一時的にデータを保存するために使用されるメソッド
  * onPauseメソッドの前に呼び出される
  * 必ず呼び出されるわけではない
    * 呼ばれないとき：finish()、バックキーとか？
  * 確実に保存するにはonPause()を用いる
* onRestoreInstanceState
  * onSaveInstanceStateで保存したデータを取り出すメソッド
    * onCreateの引数からでも取り出し可
  * onResumeの前に呼び出される
  * 必ず呼び出されるわけではない
    * 長時間バックグラウンドで置いていた場合？
  * 確実に永続的に呼び出すにはonResume()を用いる
*  Parcelabelインタフェース
  * プロセス間通信などの一時的なデータの受け渡しで用いる？
  * マシン間通信や永続的なデータの受け渡しでは用いない
  *

* 質問
  * メモリの使い方とは？
---
### 確認問題
1. onSaveInstanceStateはいつ呼ばれるか
  *  OS判断でActivityが強制的に終了・停止させられる場合に、一時的にデータを保存する際に呼び出される。
  * onPauseメソッドの直前
2. onRestoreInstanceStateはいつ呼ばれるか
  * onResumeメソッドの直前
3. 確実にデータを保存したい場合は、どのメソッドで保存すべきか
  * onPause()

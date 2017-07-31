## Fragment

### 目的
* Fragmentとはなにか
* Fragmentの役割、ライフサイクルについて理解する

---
### Fragmentとは
* Activityと同様にUI(Buttonなどのウィジェット)を持ち、Activityの中に組み込むことが出来るコンポーネント
* Fragmentのデザインは、モジュール単位で再利用できるように作成しなければならないとされており、これにより、別のActivityでもFragmentを利用すれば同じデザインや機能を再利用することができるようになります。
* 1つのActivityに複数のFragmentを設置できる
* デバイスの違いに対応しながら画面を使いまわすことができる

##### 背景
* タブレットなど、画面が大きいものに対し、UIの表現の幅を広げるため
* Android3.0,APIレベル11以降

#### ライフサイクル
|no|メソッド|内容|
|:--|:--|:--|
|1|onAttach|FragmentがActivityにひも付けられる時<br>Android6.0マシュマロ APIレベル23から引数がActivity->Contextに変わった|
|2|onCreate|Fragmentの生成時|
|3|onCreateView|Fragmentが自身のレイアウトを描画する時|
|4|onActivityCreated|親となるActivityの「onCreate」が終了した後|
|5|onStart|ActivityのonStartに基づき開始|
|6|onResume|ActivityのonResumeに基づき開始|
|7|onPause|・ActivityがonPauseになった時<br>・Fragmentが変更更新され、操作を受け付けなくなった場合<br>Fragmentが破棄されても保持しておきたい情報はこのメソッドで保存|
|8|onStop|Fragment自身またはActivityがフォアグラウンド(前面で表示)で無くなった場合|
|9|onDestroyView|・onCreateViewで生成されたViewが破棄されるとき<br>Fragmentの内部のViewリソースの整理を行う<br>ここでViewが破棄されるため、あらたにFragmentが呼び出された場合は、onCreateViewでViewを再生成する必要があります。|
|10|onDestroy|Fragmentが破棄されるとき|
|11|onDetach|Activityの関連付けから外された時|

* 1~6がFragmentを含むActivityの起動時に呼び出し

#### 注意点
* Activityが存在しない（破棄された）状態ではFragmentを生成・操作することはできない

---
### 確認問題
* Fragmentとは何ですか?
  * Activity同様にUIを持ち、Activityに組み込むことができるコンポーネント
* Fragmentを使う際は何に気をつける必要がありますか?
  * Activityが存在する必要がある
  * 存在しない場合、Fragmentを生成・操作を行うことができない
* Fragmentを使用するメリットは何ですか?
  * 再利用できる
  * 1つのActivityに複数のFragmentを設置できる
  * デバイスの違いに対応しながら画面を使いまわすことができる

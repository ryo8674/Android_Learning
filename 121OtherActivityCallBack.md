### 他のActivityコールバック

#### 目的
* 主要コールバックについて理解する。

#### ゴール
* □主要コールバック(onActivityResult, onKeyDown, onTouchEvent, onWindowFocusChanged)がどのような状況で呼ばれるか説明でき、それがコールされるサンプルコードが書ける。

---
#### 主要コールバックメソッド
* onActivityResult
  * 遷移先のActivityの処理が完了したときに呼び出される。
* onKeyDown
  * キーを押したとき又は押し続けたときに呼び出される。
* onTouchEvent
  * アクティビティ上に配置したビューのタッチイベントに対応して呼びだされる。
* onWindowFocusChanged
  * Activityの現在のウィンドウがフォーカスを得た、またはフォーカスを失った場合に呼び出される。

## ImageView

### 目的
* ImageViewの使い方を理解

---
#### ImageViewとは
* 画像を表示するためのViewです。
* drawableフォルダに配置した画像を表示することができる。

java.lang.Object
<br>   ↳    android.view.View
<br>       ↳    android.widget.ImageView

#### 実装方法
* xmlに直書き(画像はdrawableフォルダ)
* 動的に画像を配置
  * Viewの参照とリソースIDを取得して設定

|属性|振る舞い|
|:--|:--|
|src|drawableリソースを設定する。ここに表示したい画像をおく|
|scaleType|画像をImageViewの大きさにフィットさせる|
|adjustViewBounds|trueの場合、アスペクト比を保ったまま画像をスケールする|

---
### 確認問題
* ImageViewは何をするためのViewですか？
  * 画像を表示するためのView
* 画像をアスペクト比を保ったまま表示したい場合、何属性を設定しますか？
  * adjustViewBounds

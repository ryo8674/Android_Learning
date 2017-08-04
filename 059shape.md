### shape

#### 目的
* shapeの利用方法を理解する。

#### ゴール
* shapeを使って丸角・枠線・グラデーションを作成し、ButtonやTextViewに表示できる

---

#### shapeとは
* TextViewやButtonなどのViewを装飾することができるxmlファイル
* drawableフォルダ下に作成する。

* shapeタグ

|属性|振る舞い|
|:--|:--|
|rectangle|矩形|
|oval|楕円形|
|line|水平直線|
|ring|円形|

	* 簡単な図形であれば画像を入れるよりもメモリ消費が少ないのでshapeで表現

* gradient:グラデーションを表現

|属性|振る舞い|
|:--|:--|
|startColor|グラデーションの開始色|
|endColor|終了色|
|angle|グラデーションの角度。45度ずつで指定|

* stroke:枠線

|属性|振る舞い|
|:--|:--|
|width|太さ。dpで指定|
|color|色|
|dashGap|破線の線と線の間をdpで指定。dashWidthが設定されている場合のみ有効|
|dashWidth|破線の各線の長さをdpで指定。dashGapが設定されている場合のみ有効|

* corners:角の丸み

|属性|振る舞い|
|:--|:--|
|radius|すべての角の半径をdpで指定。|
|topLeftRadius|左上角の半径をdpで指定|
|topRightRadius|右上角の半径をdpで指定|
|bottomLeftRadius|左下角の半径をdpで指定|
|bottomRightRadius|右下角の半径をdpで指定|


---
### 確認問題
* shapeで図形を描画する利点は何ですか？
	* 簡単な図形であれば、画像を挿入するよりもメモリ消費を抑えることができる
* 丸を描きたい場合、shapeで何属性を指定しますか？
	* ring属性
* 枠線を描きたい場合、何属性を指定しますか？
	* stroke属性
* 図形を塗りつぶしたい場合、何属性を指定しますか？
	* solid属性

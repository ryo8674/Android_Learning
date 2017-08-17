### 9-patch

#### 目的
*

#### ゴール
* 9-patchとは何か説明できる
* ボタン画像を9-patchで作成し、ボタンのサイズによらず模様が荒くなることなく表示できる。(画像は枠と中央に文字があるものなど)

---
#### 9-patchとは
* Androidで利用できる一部分のみ拡縮可能になった画像のこと
* 適切に利用することで枠線や画像の状態を保ったまま、拡大縮小ができる

##### Stretchable Patches
* 9-patch画像をより大きな領域に描画する際、拡大して描画される領域
* 通常の画像と異なり、9-patch画像ではStretchable Patches以外の部分が拡大されないため、角丸や影を崩さずにボタン画像などを描画することができる。
* Stretchable Patchesは最低2x2以上で定義することとなっている。

![sketchable_patches](https://qiita-image-store.s3.amazonaws.com/0/48019/fc9c8823-a734-15b2-d757-363f8bef5e2b.png)

##### Contents Area
* 描画する際にコンテンツ(テキストなど)を表示する領域
* Contents Areaがある9patch画像をViewの背景として指定した場合、Contents Area以外の領域がViewのpaddingに設定され、コンテンツはContents Areaに収まるように描画される

![Content_area](https://qiita-image-store.s3.amazonaws.com/0/48019/fc1972e6-5a06-ffbf-003c-fed58c30d492.png)

##### Optical Bounds
* Optical BoundsはAPI レベル18で追加されたOptical bounds layoutに対応した要素
* 利用することで影や余白などの要素をViewのレイアウト領域から除外することができる

|Android5.1.0|Android4.1.1|
|:--|:--|
|![optical_bound_5.1.0](https://qiita-image-store.s3.amazonaws.com/0/48019/c53f1be8-1d15-53e9-a5ca-e8cc49bc4452.png)|![optical_bound_4.1.1](https://qiita-image-store.s3.amazonaws.com/0/48019/98108cc2-843d-aff5-bd01-ea70cd6fb89e.png)|

#### 9-patchアンチパターン
* 大きすぎる画像
  * 9-patch画像は基本的に縮小が下手。
  * 描画領域よりも大きい9-patchを背景に指定した場合、Stretchable Areaしか縮小されないため思った通り表示されない場合がある。
* Stretchable Patchesが小さい
  * 端末の画面密度向けリソースに同名の9-patch画像が提供されていない場合には、9-patch画像も描画前に画素密度に応じてリサイズされる。
  * Stretchable Patchesが小さすぎる場合、複数のStretchable Patchesのサイズ比に不整合が生じたり、Stretchable Patchesが消失してしまったりする。
  * Stretchable Patchesは最低2x2以上で定義することとなっている。
* 特定のdpi向けにしか9-patch画像を提供していない
  * 特定のdpi向けにしか9-patch画像を提供していない。
  * ズレを防ぐためには、Stretchable Patchesを大きくする以上に複数のdpi向けに9-patchを用意することが有効
  * nodpiの9-patchであればこちらも検討
* paddingを上書きしている
  * Contents Areaを持った9-patchを背景に指定したViewにpaddingを設定すると、9patchに設定されているContents Area情報が上書きされてしまう。
  * Optical Boundsはmarginに設定されるわけではないため、marginを設定しても上書きされることはありません。
* すべての領域をStretchable Patchesに指定している
  * 画像が単純に縦横に引き伸ばされるだけになってしまう
  * Contents Areaを設定した場合はpadding設定の効果は残っていますが、paddingはViewサイズを考慮していない9-patch画像内のdpで指定されるため、大抵の場合はズレる
* グラデーション
  * 画像の一部を引き延ばすという仕組み上、グラデーション表現は9-patchに向いていない。
  * できる限り、xmlで表現した方がよい
* ストライプやドットなどの繰り返しパターン
  * グラデーション同様

* **画像のファイル名が同じだと.9じゃないほうと競合する**
---
### 確認問題
*

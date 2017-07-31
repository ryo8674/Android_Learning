## RecyclerView,CardView

### 目的
* RycyclerViewの使い方を理解する。
* CardViewの使い方を理解する。

---
#### RecyclerViewとは
* 動的にViewを繰り返し表示するためのView
* サポートライブラリv7で利用できる
* ViewGroupクラスのサブクラス
* RecyclerViewは最低限3つのメソッドをオーバーライドする必要がある
  * getItemCount
  * onCreateViewHolder
  * onBindViewHolder
* クリックされたアイテムのイベントを拾うためのリスナーも自分で実装する必要あり
  * ArrayAdapterのOnItemClickListenerなど

##### 特徴(ListViewとの違い)
* メリット
  * ViewHolderが標準で実装されている
  * 横スクロールやグリッド表示など複雑な表示が簡単にできる
* デメリット
  * ListViewより多くのメソッドをオーバーライド、実装しなくてはならない(カセットのクリックイベントなど)
  * ヘッダーとフッターが無い
* 用途
  * RecyclerViewはListViewでは解決出来ない or より自由にカスタマイズしたい場合に使う

#### CardViewとは
* サポートライブラリv7に追加された、カード状のウィジェット
* FrameLayoutを継承しているので、LinearLayoutなどViewGroupと同じ扱い
* 資料では同じページにあるだけでlistviewでも使えるよー

---
### 確認問題
* RecyclerViewとはどんなViewですか？
  * 動的にViewを繰り返し表示するためのView
* CardViewとはどんなViewですか?
  * support library v7に追加されたカード状のウィジェット
* RecyclerViewのAdapterには標準で何が実装されていますか？
  * ViewHolder
* RecyclerViewで最低限オーバーライドするメソッドは何ですか？
  * getItemCount
  * onCreateViewHolder
  * onBindViewHolder

## ListView

### 目的
* ListViewの使い方を理解する
* ListViewを使ってリストの表示方法

---
### ListViewとは
* データをリストにして表示することができるView
* AdapterViewクラスのサブクラス

#### Adapterクラス
* BaseAdapter
  * Simple,Arrayの親クラス
  * 自由に拡張したリストを作成可
  * 必要な処理を独自Adapterで全て実装する必要があり、実装量が多くなる
* SimpleAdapter
  * 渡すデータはList-Map型
  * XMLファイルで定義された複数のビューを表示する場合に利用されることが多い
  * 継承して独自Adapterを作成しなくても利用することができる
  * 独自Adapter作成可能
* ArrayAdapter
  * 渡すデータはList型
  * 配列やListを1行に1つのビューを表示する場合に多く利用
  * 最も使用頻度が高い


---
### 確認問題
* ListViewとはどんなViewを表示するためのウィジェットですか?
  * データをリストにして表示することができる
* ListViewとデータをバインドさせるために使用するクラスはなんですか?
  * Adapterクラス
* List<>でデータを渡したい場合、どのAdapterを使用するのが良いですか?
  * ArrayAdapter

## DynamicFragment

### 目的
* 動的Fragmentの生成方法を理解する
* Fragmentのコンストラクタに引数を渡してはいけない理由を理解する
* Fragmentへのデータの渡し方がわかる
---
#### 静的Fragmentとの違い
* Activity側でJavaからFragmentを生成する。
* ActivityのレイアウトファイルにはFragmentではなく、Fragmentを入れるためのコンテナのみ用意

#### コンストラクタ
* コンストラクタは、別のクラスから対象のクラスを呼び出すときにインスタンスを取得するために呼び出されます。
* Fragmentは必ず空のコンストラクタを使って呼び出されます。

  ##### コンストラクタに引数を渡してはいけない理由
  * メモリ不足時に、システム側により自動的に破棄される
  * 破棄されたFragmentを再生成するのに引数がないコンストラクタを用いる
    * 引数があるコンストラクタでFragmentの生成処理を行うと、空のコンストラクタが使用されず、アプリが落ちる

---
### 確認問題
* 動的Fragmentを追加するためにはActivityになにを設定しますか?
  * Fragmentを入れるためのコンテナのみ
* 動的Fragmentに設定するコンストラクタにはどんな条件がありますか?
  * 引数を持たないコンストラクタである
* Fragmentに値を渡すためにはなにを利用しますか?
  * データを渡すためのBundle
  * setArgment()でFragmentにbundleをセット

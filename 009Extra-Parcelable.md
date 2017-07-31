## ExtraとParcelableを用いたデータ受け渡し

### Extra - Intentの補足情報(他のオブジェクトと受け渡しする情報)
  * ActivityやServiceにデータを渡すときに使用
  * 受け渡したい情報をキーとセットにしてIntentに付与する

  * メソッド
    * putExtra()で情報を追加
    * getExtra()で情報を取得

#### ・遷移Activityからのデータ受け取り
  * startActivityForResult
    * 必ず遷移元のActivityに戻る必要がある
    * Activity間の双方向のデータのやりとりができる

  * Parameter
    * REQUEST_CODE:どこのActivityから結果が返ってきたかを識別する値
    *

### Parcelable
  * Parcelクラスを利用してインスタンスとバイナリを相互変換する
    * Parcel:Android特化のSerialize

  * メリット
    * 独自PJまるごとプロセス間をまたいだデータのやりとりができる
      * 独自オブジェクトを運ぶ
        * Parcelableを継承したクラスは、Bundleに乗せることができる
        * 継承クラスに型を書けばいい？
        * クラスごとBundleにのせる→Intentを使って別のActivityに

    * 別アプリ間のプロセスもまたいだデータのやりとりができる
      * アプリ間をまたいだデータのやりとりができる
        * アプリ間でオブジェクトのやりとりをしたいとき
  * メソッド
    * writeToParcel(Parcel out, int flags)
      * 受け渡したい値をoutに格納
    * MyParcel(Parcel in)
      * Parcelからデータを読み出す
    * 書き込む順番と読み込む順番は同順にする必要がある


---
## 確認問題
* Extraとはなにか
  * Intentの補足情報(データの受け渡しに使用)
  * 受け渡したい情報をキーとセットにしてIntentに付与する

* 遷移先のActivityからデータを受け取りたい場合、何メソッドでActivityを呼び出しますか？
  * startActivityForResult()

* Parcelableのメリット
  * 独自プロジェクトごとプロセス間をまたいだデータのやりとりができる
  * 同アプリ内だけでなく、別アプリ間のプロセスをまたいだデータのやり取りができる

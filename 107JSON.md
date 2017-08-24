### JSON

#### 目的
* APIからJSON形式で結果を受け取ることができる
* 受け取った結果をパースし、値を取り出すことができる


#### ゴール
* JSONとは何か説明できる
* org.jsonパッケージを利用したJSONパースができる。(例えば、Google Geocoding の結果をデータとして)

---
#### JSONとは
* JSON(JavaScript Object Notation)は、XMLなどと同様のテキストベースのデータフォーマット
* XMLと比べると簡潔に構造化されたデータを記述することができるため、記述が容易で人間が理解しやすいデータフォーマットになっている

##### 使用するパッケージ・クラス
* パッケージ
  * org.json:JSONファイルを解析するためのクラスを提供するパッケージ
* クラス
  * JSONArray
    * JSONファイルの「配列」を取得するためのメソッドを提供するクラス。JSONファイルの[]の部分に対する処理を行う。
  * JSONObject
    * JSON Data Format での「オブジェクト」に該当する部分に対する処理を行うメソッドを提供するクラス。nameとvalueがマッピングされており、nameを指定することで、値を取得できる。JSONの{}の部分を抜き出すためのクラス。

##### 実装方法
* 大まかな流れ
  1. JSONデータをネットから非同期またはファイルから取得する
  2. 取得したJSONをStringのデータに変換する
  3. JSONObjectを生成する
  4. 生成したJSONObjectから、キーを指定して配列または配列配下の値を取り出す


---
### 確認問題
*
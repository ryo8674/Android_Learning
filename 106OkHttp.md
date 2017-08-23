### OkHttp

#### 目的
* OkHttpの使い方を理解する。

#### ゴール
* OkHttpとは何か説明ができる
* OkHttpを使用し、GETメソッドで、ネットワーク上のファイル(TML/XML/JSON)をダウンロードできる。
* POST で同様のことができる。

---
#### OkHttpとは
* OkHttpはSquare製のネットワークライブラリです。ライセンスはApache License 2.0です。
* Android 2.3, Java 7以降で使用できます。 http://square.github.io/okhttp/

##### 特徴
* HTTP/2をサポート
  * http2について -> http://blog.redbox.ne.jp/http2-cdn.html
* HTTP/2が利用できない場合、要求の待ち時間を減少させる接続プーリング
* ダウンロードサイズの縮小
* 繰り返し要求の応答キャッシュによるネットワーク接続の回避

#### 実装方法

##### 使用例(GET)
* 大まかな流れ
  1. OkHttpClientクラスのオブジェクト生成
  2. RequestオブジェクトをBuilderクラスでURLなどを設定しながら生成
  3. OkHttpClientクラスのcallメソッドでリクエストの送信準備
  4. OkHttpClientクラスのexecuteメソッドでリクエストの送信及び、レスポンス（Responseオブジェクト）の取得
  5. ResponseオブジェクトからHTMLなどが取得可能

##### 使用例(POST)
* 大まかな流れ
  1. OkHttpClientクラスのオブジェクト生成
  2. MediaTypeクラスのparseメソッドでMIMEタイプなどを事前に用意する
  3. RequestBodyクラスで送信データの準備
  4. RequestオブジェクトでURLと送信データなどを設定しながら生成(RequestBodyオブジェクトはpostメソッドの引数に渡す)
  5. レスポンスの取得などはGETと同じ



---
### 確認問題
*

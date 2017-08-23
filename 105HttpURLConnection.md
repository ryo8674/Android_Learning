### HttpURLConnection

#### 目的
* HttpURLConnectionの使い方が分かる。

#### ゴール
* HttpURLConnection を利用しGETメソッドで、ネットワーク上のファイル(JSON)をダウンロードできる。
POST で同様のことができる。

---
#### URLConnectionとは
* ほとんどのアプリケーションに適応する汎用的で軽量なHTTPClient
* Android5.0以降ではApacheHTTPClientに対するサポートが外され、さらに6.0以降では使用自体が不可となっているため、URLConnectionを使用することが推奨されている
* APIがシンプルでサイズが小さいのでリソースに限りがある Android に適しているクライアント

##### 使用するクラス
* URLクラス
  * URLオブジェクトを生成する
  * URLConnectionクラスをURLオブジェクトから呼び出すことで、URLに紐付いた接続を開始することができる
* URLConnectionクラス
  * URLConnectionクラスは、アプリとURLが示すリモート環境への接続をするためのクラス
  * HttpURLConnection、HttpsURLConnection(HttpURLConnectionのサブクラス)の2つのサブクラスが提供
* HttpURLConnection/HttpsURLConnectionクラス
  * HttpURLConnectionとHttpsURLConnectionクラスは、HttpまたはHttpsでURLが示すリモート環境へ接続するためのコネクションを提供するクラス

---
### 確認問題
* Androidで通信を行う場合には何クラスを利用しますか？
  * URL, URLConnection, そのサブクラス
* ネットワーク通信を行う場合は、どんなパーミッション設定が必要ですか？
  * android.permission.INTERNET
* ネットワーク通信を行う時に気をつけることはなんですか？
  * ネットワークへの通信処理は、非同期で実施しないといけない
  * そのため、ネットワーク通信は必ず、別スレッドを立て、非同期で実施することが必須

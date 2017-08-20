### Preference

#### 目的
* Preferenceの使い方を理解する

#### ゴール
* デフォルトプリファレンスとデフォルトでは無いプリファレンスの違いを説明できる。
* プリファレンスへの読み書きが行える。
* プリファレンスのデータ構造がわかる

---
#### データ保存方法
* 共有プリファレンス
  * Map型(K,V)でプライベートなプリミティブデータを保存
* 内部保存域
  * デバイスのストレージにプライベートなデータを保存
* 外部保存域
  * 共有の外部保存域にパブリックなデータを保存
* SQLiteDB
  * プライベートDBに構造化データを保存
* ネットワーク接続
  * ネットワークサーバを使用したWeb上にデータを保存

#### Preferenceとは
* アプリケーションが利用する設定をMapのようにキーと値の組として取り扱う仕組み
* プリファレンスを利用することで設定項目と値を組にし、複数の組を1つの設定ファイル（xmlプリファレンスファイル）にまとめて永続化することができる
* アプリケーションの表示形式や通信に関わる設定など、さまざまな設定を保存することができる

##### Preferenceのモード

|MODE|Accessibility|
|:--|:--|
|MODE_PROVATE|他アプリからアクセス不可|
|MODE_WORLD_READABLE|他アプリから読み込み可能|
|MODE_WORLD_WRITABLE|他アプリから書き込み可能|

* default:mode_private

##### Preference作成方法
* Context#getSharedPreferences(String name, int mode)
  * 新たにPreference名をつけて作成する方法
* Activity#getPreferences(int mode)
  * 自分のアクティビティのクラス名をプリファレンス名として作成する方法
* PreferenceManager.getDefaultSharedPreferences(Context context)
  * デフォルトで作成されるPreferenceを利用する方法
  * 共有モードは常にMODE_PRIVATE
  * Preference名の指定は不要

##### Preference名
* デフォルトプリファレンス　＝　プロジェクト作成時のパッケージ名_preference.xml
* Activityクラスのプリファレンス　＝　Activityのクラス名.xml
* ContextWrapperクラスのプリファレンス　＝　引数nameで指定した値.xml


---
### 確認問題
* Preferenceとはどのようにデータを保存するデータ形式ですか？
* Preferenceにはどのような種類がありますか？

## Context

### 目的
* Contextが何か理解する
* Contextが果たす役割を理解する
* ApplicationContextとActivityContextの違いを理解する
* Contextの扱いによるメモリリークの仕組みを理解できる

### Contextとは
* アプリのグローバル情報を持つインタフェース
  * ### グローバル情報
    * パーミッション：アプリがユーザにどのような許可を要求していて、ユーザが許可しているかどうか
    * アプリリソース情報：アプリに含まれるリソース情報
    * アプリ内情報：コンポーネント名、プロセス名などアプリの構成やふるまいの情報
    * ファイルリソース：永続化したDBや内部データの情報

* アクティビティの起動やブロードキャスト、インテントの受取などのような、アプリケーションレベルでの操作の呼び出しや、アプリケーションの特定のリソースやクラスにアクセスするのに利用されます。

### ActivityContextとApplicationContext

* アプリに依存するかActivityに依存するかの違いがある

||ActivityContext|ApplicationContext|
|--:|:--|:--|
|違い|Activityに対して1つ<br>Activityが再生成されるたびに新しく作成される。|アプリのプロセスに対して1つ|
|使用目的|Activity内で完結する、Activity独自の設定を行いたい場合|アプリ全体の情報や設定を使用する場合|

* 注意点
  * メモリリーク
    * private static変数でActivityを保持していると、このActivityを持つライフサイクルが終了しても、参照は破棄されず、残る
    * Activityへの参照が生成され続けるとメモリリークが発生する。

---

### 確認問題
* Contextとは
* ActivityContextとApplicationContextの違い
* コンテキストの使用時には何に注意する必要があるか
  * メモリリーク
  * private staticな変数でActivityを保持していると、このActivityのライフサイクルが終了しても参照は破棄されない。
    * 参照が生成され続け、次第にメモリリークが発生する。

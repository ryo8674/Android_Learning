## StaticFragment

### 目的
* Fragmentの静的生成方法を理解する
* FragmentからActivityへコールバックする仕組みを理解する

---
### 確認問題
* 静的Fragmentを生成する場合、Fragmentはどこに設定しますか?
  * Activityのレイアウトファイル
* Fragmentのイベントをコールバックするにはなにを作成しますか?
  * コールバックインターフェース
* Fragmentのコールバックを受け取るために、Activityは何を継承する必要がありますか?
  * インターフェースのコールバックメソッド
* ActivityがFragmentのコールバックを受け取るためのリスナーを継承しているのかの確認はFragmentのどこで行いますか?
  * onAttach()

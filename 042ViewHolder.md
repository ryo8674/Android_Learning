## ViewHolder

### 目的
* ViewHolderとはなにか、使い方を理解する
* ViewHolderを利用する目的を理解する

---
### ViewHolderとは
* ListView高速化の技法
* ListViewのアイテムレイアウトの参照を保持しておくためのクラス

* findViewByIdはコストが高く、頻繁に使用していると動作が重くなるというデメリット
* ViewHolderを利用し参照を保持しておくことでこのコストを省き、View描画の挙動を軽くする事ができ
---
### 確認問題
* ViewHolderを利用する目的は？
  * View描画の挙動を軽くする事ができる

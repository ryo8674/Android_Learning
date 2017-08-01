## Actionbar,Toolbar,menu

### 目的
* ActionBarとToolbarの違いを理解する
Toolbarを利用方法を理解する
Menuの表示方法を理解する

### ゴール
* ActionBarとは何か説明できる。
* Toolbarとは何か説明できる。
* ActionBarの代わりにToolbarを使用することができる。
* menuとは何か説明できる。
* menuを作成しアプリに適用できる。
* OptionMenuに自分でメニューを追加できる。

---
#### Actionbarとは
* ActionBarはAndroid3.0(APIレベル11)以降で導入された、<br>画面タイトルやメニューを表示することができるコンポーネントです。

#### Toolbarとは
* Android5.0以降で導入された、ActionBarにかわって画面タイトルやメニューを表示できるViewです。
* SupportLibrary v7に入っているため、Android5系未満でも利用できます。
* 現在のアプリではActionBarではなくToolbarを使用します。

#### メリット
* ボタン、タブを配置できる
  * ->機能追加ができる

#### 両者の違い
* ActionBar:Viewでない
* ToolbarはView
  * Viewであることにより、よりカスタマイズしやすくなっています。

#### Toolbarの実装
* ActionBarのように利用する
  1. レイアウトに配置
  2. ActionbarとしてToolbarをセット
  3. アプリのthemeを変更
* 独立したViewとして利用する

---
### 確認問題
* ActionBarとToolbarとは何ですか?
  * 画面タイトルやメニューを表示することができるコンポーネント
* ActionBarとToolbarの違いは何ですか?
  * ToolbarはViewで、ActionbarはViewでない
* Toolbarにmenuを設定する場合は何ファイルを作成する必要がありますか？
  * menuファイル
* ToolbarをActionBarとして利用する場合にMenuを表示する方法を調べてください。
  1. onCreateOptionsMenuメソッドをオーバーライド
  * menuのレイアウトをインフレートする

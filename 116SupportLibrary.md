### SupportLibrary

#### 目的
* Support Libraryが何か説明できるようになる
* Support Libraryをプロジェクトに導入し、使用できる

#### ゴール
*　Support Library がどんなライブラリか簡単に説明できる。
*　Support Library には「v4」「v7」のようにバージョンが異なるものがあるが、これが何を意味しているか説明できる。
*　Support Library の入手と、Android プロジェクトへの導入ができる。

---
#### SupportLibraryとは
* Support Libraryとは、Androidの新しいAPIレベルで追加された機能を、古いAPIレベルでも使用できるようにしたり、新たな便利機能を提供するためのライブラリパッケージ
* AndroidSDKから提供
* Support Libraryの中でも、v4とv7は広範囲のAndroidバージョンをサポートし、便利なインターフェースを提供しているため、かならず導入することが推奨されている

##### v4
* Android 1.6 (API level 4) 以降を対象としたライブラリ
* 古いAPIレベルをサポートする場合ほぼ必須のライブラリとなっている
* Fragment,Loader, ViewPagerなど

##### v7
* Android 2.1 (API level 7) 以降を対象としたライブラリ
* ActionBarの実装を提供するため、古いAPIレベルの端末もサポートする場合はほぼ必須
* ActionBar,RecyclerViewなど

##### v13
* Android 3.2（API level 13）以降を対象としたライブラリです。Fragmentに対する追加機能を提供
* v4でバックポートされたFragmentを使わないためにある
  * http://quesera2.hatenablog.jp/entry/2015/01/04/001328

##### SupportDesignLibrary
* Android 2.1 (API level 7) 以降を対象とした、マテリアルデザインをサポートするためのライブラリ
* Android5.0以前の端末でもマテリアルデザイン対応ができる

---
### 確認問題
* Support Library がどんなライブラリか簡単に説明できる。
  * 新しいAPIレベルで追加された機能を古いAPIレベルでも使用できるようにしたり、新しい機能を提供するためのパッケージ
* Support Library には「v4」「v7」のようにバージョンが異なるものがあるが、これが何を意味しているか説明できる。
  * Support Libraryを使用できるAPIレベル
* Support Library の入手と、Android プロジェクトへの導入ができる。
  * したこと：ViewPager+TabLayoutを用いたリストの表示

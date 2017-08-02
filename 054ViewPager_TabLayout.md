### ViewPager/TabLayout

#### 目的
* ViewPager,TabLayoutの利用方法を理解する。

#### ゴール
* ViewPagerとは何かを説明できる
* ViewPagerを使い複数ページを切り替えることができる
* TabLayoutを用いてタブUIを作成できる
* ViewPagerと組み合わせてページに紐づくタブを生成できる

---

#### ViewPagerとは
* ViewPagerとは、Fragmentなどをスワイプ動作で切り替えができるView
* ListViewなどと同様にAdapterを使って切り替える
* e.g.ViewPagerを使ってFragmentを切り替える
* ページが変わったことを検知するリスナー：OnPageChangeListner

#### TabLayoutとは
* TabLayoutとは、ViewPagerと併用することを前提として作られたView
* 画面のタイトルやアイコンをViewPagerの各ページにつけることができる

##### GravityとMode
* Gravity:Tabの中心に置くか画面の幅を使用するか
	* setTabGravity(TabLayout.□□□)
	* GRAVITY_CENTER: Tabを中心に置く
	* GRAVITY_FILL: Tabを画面の幅いっぱい使用して表示する

* Mode:Tabを固定にするかScrollできるようにするか
	* setTabMode(TabLayout.□□□)
	* MODE_FIXED:全てのTabを画面内に表示。Tab数が多いと潰れて表示される
	* MODE_SCROLLABLE:Tabの横スクロールが可能。Tabが長くなったり数が多い場合に有効

#### PageAdapter
* FragmentPagerAdapter
	* Fragmentをメモリ上に保持する
	* ページが多くなるとメモリリークを起こす可能性がある。
	* 継承すると、getItem()とgetCount()をオーバーライドする必要がある。
		* getItem:ViewPagerの各ページに表示するFragmentを返す
		* getCount:ViewPagerのページ数を返す
		* getPageTitle:各ページのタイトルを返す。TabLayoutと紐づけるとここで返した文字列が表示される。

* FragmentStatePagerAdapter
	* ページを切り替えたときに非表示になったページを破棄する。
	* 再生成が頻繁に行われるので、初期化処理を適切に行う必要がある。

---
### 確認問題
* ViewPagerとはどんなViewか？
	* スワイプで切り替えることのできるView
* ViewPagerが変わったことを検知するためのリスナーは？
	* OnPageChangeListner
* TabLayoutのgravityにはどんな種類があるか？
	*  GRAVITY_CENTER: Tabを中心に置く
	* GRAVITY_FILL: Tabを画面の幅いっぱい使用して表示する

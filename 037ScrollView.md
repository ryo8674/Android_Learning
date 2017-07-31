## ScrollView

### 目的
* ScrollViewの使い方を理解

---
### ScrollView
* ScrollViewは画面を縦にスクロールすることを可能にするView
* 横にスクロールする場合はHorizontalScrollView

↳    android.view.View
<br>       ↳    android.view.ViewGroup
<br>           ↳    android.widget.FrameLayout
<br>               ↳    android.widget.ScrollView

#### 実装の手順
* レイアウトファイルにScrollViewを書く
* OnCheckedChangeListenerインターフェースを実装
* ScrollViewの最初の子ViewにViewGroupを配置
  * ScrollViewは1つしか子Viewをもつことができないため

---
### 確認問題
* ScrollViewとはどんなViewですか？
  * 表示がページ内に入りきらない場合に画面を縦にスクロールすることを可能にするView
* 水平方向のスクロールをするためにはどのような方法がありますか？
  * HorizontalScrollView

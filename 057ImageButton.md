### ImageButton

#### 目的
* ImageButtonの利用方法を理解する。

#### ゴール
* ImageButtonとButtonの違いを説明できる。

---

#### ImageButtonとは
* Button同様、クリック操作をできるView
* 画像をボタンとすることを前提としているボタン
* Buttonと継承関係が異なる
* ボタンに文字列を載せることはできない

#### Buttonとの違い
* Buttonは背景に画像を設定している。
* ImageButtonは画像自体をボタンにしている。

* Buttonには文字列を設定できる。
* ImageButtonには設定できない。
* ##### これといった明確なメリットはない。

---
### 確認問題
* ImageButtonとはどのようなViewですか？
	* クリック操作をできるView
	* 画像をボタンとすることを前提にしている
* ButtonとImageButtonはそれぞれどんなViewを継承していますか?
	* Button -> TextView
	* ImageButton -> ImageView
* 画像の上に文字列が配置されたボタンを作成したい場合、ButtonとImageButtonのどちらを利用しますか？
	* Button

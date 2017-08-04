### selector

#### 目的
* selectorを使ったViewの表示状態の切り替え方法を理解する

#### ゴール
* ボタンの通常/押下/無効時の画像をセレクタで設定できる

---

#### selectorとは
* Viewの表示状態をxmlを利用して切り替えられるようにするためのもの
* drawbaleフォルダにselectorタグをいれたxmlファイルを定義

#### 注意点
* itemタグのcolor
	* textColor
		* itemタグ内に書く
	* background
		* itemタグ内のcolorタグ内に書く

---
### 確認問題
* selectorは何を指定できるxmlファイルですか？
	* Viewの表示状態
* 押下状態を表す場合に指定する属性は何ですか？
	* state_pressed属性
* バックグランドの色を変える場合、itemタグのどこにcolor属性を定義しますか？
	* colorタグに記述する。

### customview

#### 目的
* CustomViewをは何かを説明できる
* 自分でCustomViewを作成することができる

#### ゴール
* LinearLayoutを継承した、簡単なカスタムビューの生成ができる。※ボタンが3つあり、押すとトーストが表示される
* カスタムビューにカスタム属性を定義し、XMLで利用できる。

---
#### customviewとは
* viewを継承して作成する独自view
* 処理を移譲することで、ActivityやFragmentがViewの処理を気にする必要が減る
* あくまでもViewはActivityやFragmentのライフサイクルに紐づいているので、
自動的に破棄されたり、再生成されることを考慮しないといけない

---
### 確認問題
* CustomViewとはどのようなViewですか？
  * Viewを継承して作成する独自View
* CustomViewを利用するメリットは何ですか？
  * 処理を移譲することで、ActivityやFragmentがViewの処理を気にする必要が減る

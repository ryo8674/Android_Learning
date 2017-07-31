## EditText

### 目的
* EditTextの使い方を理解

---
#### EditViewとは
EditTextとは、ユーザーから入力させる為のViewです。
値を制限せずに入力できるものや、パスワード、メールアドレスなど、
特定の文字列に制限をつけることもできます。

java.lang.Object
<br>   ↳    android.view.View
<br>       ↳    android.widget.TextView
<br>           ↳    android.widget.EditText




---
### 確認問題
* EditTextとはどんなことができるViewですか?
  * ユーザが入力できるView
* 入力値を数字のみにしたい場合は、なに属性になにを設定しますか?
  * inputType = "number";
* EditTextから文字列を取得するにはどんなメソッドを利用しますか?
  * getText()
  * toString()

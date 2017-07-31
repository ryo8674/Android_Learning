## TextView

### 目的
* TextViewの使い方を理解

---
#### TextViewとは
java.lang.Object
<br>→ android.view.view
<br> → android.widget.textview

##### セット方法
* setText
* xmlで直書き

##### フォーマット指示子
* Cみたいに文字列の一部をプログラムで扱える
* 多言語の文法に対応できる
* 文字列リソースファイルに記載する

##### htmlを用いた表示
* 多様な表現ができる
* 自由度はstyleの方が高いが、HTMLのほうが簡単で、実際の形をイメージしやすい
* android.text.Htmlクラス：htmlでの表現をサポートするクラス

---
### 確認問題
* TextViewはなにを実現するためのViewか
  * 文字列を表示するためのView

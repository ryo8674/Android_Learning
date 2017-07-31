## ToggleButton

### 目的
* toggleButtonの使い方を理解

---
### ToggleButton
* クリックすることで、ON/OFFを切り替えられるボタンのことです。
* ボタンを見れば、状態をすぐに把握することができます。

↳    android.widget.Button
<br>↳    android.widget.CompoundButton
<br>↳    android.widget.ToggleButton

#### 実装の手順
* レイアウトファイルにtogglebuttonを書く
* OnCheckedChangeListenerインターフェースを実装
* onCheckedChangeに処理を実装
* OnCheckedChangeListenerを登録

### SwitchView
* APILevel14でON/OFFをわかりやすく切り替えるために新たに設定されたViewです。
* switchはSupportLibraryに含まれていないため、APIレベル14未満ではswitchは使用できません。


---
### 確認問題
* ToggleButtonをはどんな特徴をもつViewですか？
  * クリックすることで0/1を切り替えることができるボタン
* ToggleButtonのON/OFFを検知するリスナーは何ですか？
  * onCheckedChangeListener
* ToggleButtonと同じようにON/OFF状態を表せるViewは何ですか？
  * switchView

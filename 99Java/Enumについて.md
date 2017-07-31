## 3. Enumとは
#### 目的
Enumを使うメリットについて理解する事

#### ゴール
Enumを使うメリットについて口頭で説明できる事

### Enumとは
- http://javatechnology.net/java/enum/

### Enumを使いたい時とは
- if文やswitch文の分岐判定に定数を使いたい
 - 分岐条件が何かをメソッドの呼び出し側でもわかりやすくする
- フラグを定数化することで可読性をあげる

```java
private static String check(CheckEnum checkEnum) {
        swich(checkEnum) {
          case CheckEnum.OK:
               return "OKです。";
          case CheckEnum.Success:
               return "成功です。";
          default:
               return null;
        }
}
```

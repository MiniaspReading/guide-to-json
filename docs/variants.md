# Variants 變種

Components may have variants. Elements may have variants, too.<br>
元件可以有多樣的變化，元素當然也有，我們這邊稱為變種。

![](images/component-modifiers.png)

<br>

## Naming variants （變種的命名）
Classnames for variants will be prefixed by a dash (`-`).<br>
變化的名稱前須加上分號(-)作為前綴詞。

  ```scss
  .like-button {
    &.-wide { /* ... */ }
    &.-short { /* ... */ }
    &.-disabled { /* ... */ }
  }
  ```

## Element variants 元素變種
Elements may also have variants.<br>
元素也會有變種。

  ```scss
  .shopping-card {
    > .title { /* ... */ }
    > .title.-small { /* ... */ }
  }
  ```

## Dash prefixes 分號做為前綴
Dashes are the preferred prefix for variants.<br>
對於變種，分號是較好的前綴用法。

  * It prevents ambiguity with elements. 
  * 可防止雙關語的元素。
  * A CSS class can only start with a letter, `_` or `-`. 
  * 一個 CSS 的 class 只能以 底線 "_" 或分號 "-" 作為開頭。
  * Dashes are easier to type than underscores. 
  * 分號比底線更容易輸入。
  * It kind of resembles switches in UNIX commands (`gcc -O2 -Wall -emit-last`).
  * 它有一點類似在 UNIX 命令切換 （`gcc -O2 -Wall -emit-last`)。

How do you deal with complex elements? Nest them.<br>
遇到複雜的元素該如何處理呢? 將它們巢狀化吧！
[Continue →](nested-components.md)
<!-- {p:.pull-box} -->

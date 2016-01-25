# Helpers 

For general-purpose classes meant to override values, put them in a separate file and name them beginning with an underscore. They are typically things that are tagged with *!important*. Use them *very* sparingly. <br>
對於一般用途的類別(class)通常都是去做覆蓋的動作，將它們放在另一個檔案中並且以底線作為開頭來命名。由於他們通常會在後面標記 *!important* ，因此使用時要 *非常* 謹慎。

```css
._unmargin { margin: 0 !important; }
._center { text-align: center !important; }
._pull-left { float: left !important; }
._pull-right { float: right !important; }
```

## Helpers 的命名
Prefix classnames with an underscore. This will make it easy to differentiate them from modifiers defined in the component. Underscores also look a bit ugly which is an intentional side effect: using too many helpers should be discouraged.
以底線做為類別名稱的前綴。這將使定義的元件修飾中較容易區分。底線看起來也許是有那麼一點難看，這是刻意的副作用：讓你知道不應該使用太多的 helper。

  ```html
  <div class='order-graphs -slim _unmargin'>
  </div>
  ```

## 整理 helpers
Place all helpers in one file called `helpers`. While you can separate them into multiple files, it's very preferrable to keep your number of helpers to a minimum.
將所有 helper 放在一個名為 `helpers` 的檔案中。 雖然你可以把它們分開成多個檔案，但最好讓你的 helper 數量降到最低。
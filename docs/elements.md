# 元素(Elements)

Elements are things inside your component. <br>
元素就是在你的元件中的物件

![](images/component-elements.png)

## Naming elements 元素的命名
Each component may have elements. They should have classes that are only **one word**. <br>
每個元件或許有數個元素。它們的 class 應該只能用 **一個單字** 來命名。
```scss
.search-form {
  > .field { /* ... */ }
  > .action { /* ... */ }
}
```

## Element selectors 元素選擇器
Prefer to use the `>` child selector whenever possible. This prevents bleeding through nested components, and performs better than descendant selectors. <br>
盡可能使用 `>` 來指定子選擇器。 這可以防止在巢狀元件中發生滲漏的情況，且效能比後代選擇器要來得好。

```scss
.article-card {
  .title     { /* okay */ }
  > .author  { /* ✓ better */ }
}
```

## On multiple words 在多個單字上
For those that need two or more words, concatenate them without dashes or underscores. <br>
對於那些需要兩個或更多的單字，將它們連接起來並不要加上破折號或底線。

```scss
.profile-box {
  > .firstname { /* ... */ }
  > .lastname { /* ... */ }
  > .avatar { /* ... */ }
}
```

## Avoid tag selectors 避開標籤 (tag) 選擇器
Use classnames whenever possible. Tag selectors are fine, but they may come at a small performance penalty and may not be as descriptive. <br>
盡可能使用 class 名稱。 標籤選擇器雖然可以，但他們可能會造成一些效能上的損失及不具有可描述性。

```scss
.article-card {
  > h3    { /* ✗ avoid */ }
  > .name { /* ✓ better */ }
}
```

Not all elements should always look the same. Variants can help. <br>
並非所有元素總是看起來要是一樣的。變數可以提供幫助。
[Continue 繼續 →](variants.md)
<!-- {p:.pull-box} -->

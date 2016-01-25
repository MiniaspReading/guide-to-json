# CSS 架構

## One component per file 一個元件一個檔案
For each component, place them in their own file.
對每個元件，請將它們放在屬於自己的檔案中。

  ```scss
  /* css/components/search-form.scss */
  .search-form {
    > .button { /* ... */ }
    > .field { /* ... */ }
    > .label { /* ... */ }

    // variants
    &.-small { /* ... */ }
    &.-wide { /* ... */ }
  }
  ```

## Use glob matching 使用全域配對
In sass-rails and stylus, this makes including all of them easy:<br>
在 sass-rails 及 stylus 中，要將所有元件引入是很容易的。

  ```scss
  @import 'components/*';
  ```

## Avoid over-nesting 避免過度的巢狀架構
Use no more than 1 level of nesting. It's easy to get lost with too much nesting.
不要使用超過一層的巢狀架構。過度的巢狀結構容易使你迷失。

  ```scss
  /* ✗ 要避免使用: 兩層的巢狀架構 */
  .image-frame {
    > .description {
      /* ... */

      > .icon {
        /* ... */
      }
    }
  }

  /* ✓ 較好的方式: 兩層剛剛好 */
  .image-frame {
    > .description { /* ... */ }
    > .description > .icon { /* ... */ }
  }
  ```

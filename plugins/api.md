# 情境與 APIs

GitBooks 對外掛提供了不同的 APIs 與使用情境，這些 APIs 往往都依賴 GitBook 的特定版本，因此你的外掛應該要在 `package.json` 中指定 `engines.gitbook`。

#### 內容區塊與篩選器的使用情境

內容區塊（Blocks）與篩選器（filters）對相同的情境內容具有存取權，這個情境被綁定在模板引擎執行期間：

```js
{
    // Current templating syntax
    "ctx": {
        // For example, after a {% set message = "hello" %}
        "message": "hello"
    },
    
    // Book instance
    "book" <Book>,
    
    // Current generator
    "generator": "website"
}
```

#### 掛勾的使用情境

掛勾（Hooks）只能存取這個 `<Book>` 實例（instance）。

#### 書籍實例

The `Book` class is the central point of GitBook, it centralize all access methods. This class is defined in [book.js](https://github.com/GitbookIO/gitbook/blob/master/lib/book.js).

```js
// Access to book's configuration (book.json)
var title = book.config.get('title');
var websiteStylesheet = book.config.get('styles.website', 'default_value.css');

```

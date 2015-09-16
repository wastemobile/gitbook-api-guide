# 使用內容區塊 Blocks

在模板中使用內容區塊（以特殊的標籤語法添加），是向作者提供額外功能的最佳方式。

最常見的用途，就是在轉製書籍時，透過某些標籤的指引處理內容。有點像是強化後的 [filters](./filters.md)，因為你可以使用多種表達式來完成目的。

> 內容區塊（block）其實像是管理視圖（Views）的一個小幫手（helper），它如何處理內容，是由另一個控制器（Controller）、也就是一段 JavaScript 程式來控制。

### 定義一個新的內容區塊

內容區塊（blocks）是由外掛定義的，它有特定的名稱，並與一個 **block descriptor** 關聯在一起。一個 block descriptor 至少需要包含一個處理（process）方法。

```js
module.exports = {
    blocks: {
        tag1: {
            process: function(block) {
                return "Hello "+block.body+", How are you?";
            }
        }
    }
};
```

內容區塊的處理程序，必須回傳要拿來替代區塊標籤的 HTML 內容。請參照 [情境與 APIs](./api.md) 一章的內容，學習 `this` 與 GitBook API 的使用方法。

### 處理內容區塊參數

模板語法可以將參數送進內容區塊中：

```
{% tag1 "argument 1", "argument 2", name="Test" %}
This is the body of the block.
{% endtag1 %}
```

內容區塊的**處理程序**就可以使用這些參數：

```js
module.exports = {
    blocks: {
        tag1: {
            process: function(block) {
                // block.args equals ["argument 1", "argument 2"]
                // block.kwargs equals { "name": "Test" }
            }
        }
    }
};
```

### 處理次級內容區塊（sub-blocks）

內容區塊可以被拆解成多個次級區塊，像是下面的範例：

```
{% myTag %}
    Main body
    {% subblock1 %}
    Body of sub-block 1
    {% subblock 2 %}
    Body of sub-block 1
{% endmyTag %}
```

# 使用篩選器 Filters

篩選器（Filters）是能被套用到變數上的基礎功能，使用一個管道符號（`|`）呼叫，還能加上一些參數。

```
{{ foo | title }}
{{ foo | join(",") }}
{{ foo | replace("foo", "bar") | capitalize }}
```

### 定義一個新的篩選器

外掛可以從程式起點的 `filters` 領域，定義一些自訂函數，藉以擴張它的功能。

一個篩選功能會拿篩選的內容當第一個參數，應該回傳處理後的新內容。請參照 [情境與 APIs](./api.md) 一章的內容，學習 `this` 與 GitBook API 的使用方法。

```js
module.exports = {
    filters: {
        hello: function(name) {
            return 'Hello '+name;
        }
    }
};
```

經由上面的定義，就可以在書中使用 `hello` 篩選器了：

```
{{ "Aaron"|hello }}, how are you?
```

### 處理內容區塊參數

內容區塊的參數可以送給篩選器處理：

```
Hello {{ "Samy"|fullName("Pesse", man=true}} }}
```

參數被送進自訂函數中處理，篩選器自帶的命名參數要以最後一個物件送進去。

```js
module.exports = {
    filters: {
        fullName: function(firstName, lastName, kwargs) {
            var name = firstName + ' ' + lastName;
            
            if (kwargs.man) name = "Mr" + name;
            else name = "Mrs" + name;
            
            return name;
        }
    }
};
```
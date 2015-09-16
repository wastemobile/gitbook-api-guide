# 使用掛勾 Hooks

掛勾（Hooks）是添加功能，或改變處理程序行為的一種方法，使用自訂的回呼。

### 掛勾列表

### 相對於全域流程

> 頁面解析相關的額外功能，建議使用 [blocks](./blocks.md) 。

| Name | Description | Arguments |
| ---- | ----------- | --------- |
| `init` | 在解析完書籍內容後呼叫，在實際轉製網頁與書籍之前執行。 | None |
| `finish:before` | 在轉製頁面完成後呼叫，尚未複製素材、封面等... | None |
| `finish` | 所有轉製程序完成後呼叫。 | None |

### 相對於頁面流程

| Name | Description | Arguments |
| ---- | ----------- | --------- |
| `page:before` | 在對頁面套用模板引擎之前呼叫 | Page Object |
| `page` | 在輸出與建立頁面索引前呼叫 | Page Object |

##### 頁面物件

```js
{
    // Parser named
    "type": "markdown",
    
    // File Path relative to book root
    "path": "page.md",
    
    // Absolute file path
    "rawpath": "/usr/...",
    
    // Progress of the page in summary
    "progress": {
        ...
    },
    
    // Page Content (available in "page:before")
    "content": "# Hello",
    
    // Page Content splited in sections (available in "page")
    "sections": [
        {
            "content": "<h1>Hello</h1>",
            "type": "normal"
        }
    ]
}
```

##### 添加標題的範例

```js
{
    "page:before": function(page) {
        page.content = "# Title\n" +page.content;
        return page;
    }
}
```

##### 替換某些 html 內容的範例

```js
{
    "page": function(page) {
        page.sections[0].content = page.sections[0].content.replace("<b>", "<strong>")
            .replace("</b>", "</strong>");
        return page;
    }
}
```


### 非同步操作

Hooks callbacks can be asynchronous and return a promise.

Example:

```js
{
    "init": function() {
        return writeSomeFile()
        .then(function() {
            return writeAnotherFile();
        });
    }
}
```
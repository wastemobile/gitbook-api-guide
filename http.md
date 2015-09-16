# HTTP API

這裏是存取 GitBook API 的基礎事項，有任何問題請聯絡 [支援頻道](https://www.gitbook.com/contact)。

#### Schema

所有 API 均使用 HTTPS，經由這個 `https://api.gitbook.com/` 正式網址。所有資料進出格式都是 **JSON**。

```raw
$ curl -i https://api.gitbook.com/author/gitbookio

HTTP/1.1 200 OK
Server: Cowboy
Connection: keep-alive
Content-Type: application/json; charset=utf-8
Content-Length: 275
Etag: W/"113-25d22777"
Date: Thu, 11 Jun 2015 14:49:26 GMT
Via: 1.1 vegur

{ ... }
```


#### Authentication

目前只有一種認證模式： **Basic Auth** 。

嘗試存取需要認證的資源，某些地方會收到 `404 Not Found` 訊息，而不是 `403 Forbidden`。這是為了避免讓未獲授權的讀者接觸到私密書籍資源。

```
$ curl -u "username:token" https://api.gitbook.com/books/
```

#### Error Format

錯誤訊息也以 JSON 格式回覆： 

```js
{
    "error": "Not found",
    "code": 404
}
```

#### Pagination

如果回覆是個許多項目的列表，預設會以每 30 個項目進行分頁。

你可以使用 `?skip` 參數索取特定的頁數。對某些資源，也可以使用 `?limit` 參數限制上線數量為 100。

分頁結果會以下面的格式提供使用情境：

```js
{
    list: [],
    skip: 0,
    limit: 100,
    total: 0
}
```
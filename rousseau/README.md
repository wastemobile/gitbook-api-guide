# 校對

校對 API 使用的是開源工具： [Rousseau](https://github.com/GitbookIO/rousseau)，因此原文目錄中直接以 Rousseau（盧梭）命名。（至於為什麼叫做「盧梭」，我也不知道...）

Rousseau 提供了簡易的 API 進行校對與拼字檢查，目前只支援英文。

拼字檢查使用 Hunspell 字典。

GitBook 提供的 API 資源位於 `https://rousseau.gitbook.com`。


### 校對文字（英文）

```
POST https://rousseau.gitbook.com/document

{ "document": "Hello World" }
```

### 檢查拼字（英文）

```
POST https://rousseau.gitbook.com/words

{ "words": ["Hello", "World"] }
```

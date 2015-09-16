# 建立與發佈外掛

GitBook 外掛是根據 NPM 規格所發佈的一個 Node 套件。

## 架構

#### package.json

根目錄下的 `package.json` 包含各種套件的一般資訊（建立者名稱、版本、描述...）：

```
{
    "name": "gitbook-plugin-mytest",
    "version": "0.0.1",
    "description": "This is my first GitBook plugin",
    "engines": {
        "gitbook": ">1.x.x"
    }
}
```

請直接參照 [NPM 說明文件](https://docs.npmjs.com/files/package.json) 中關於 `package.json` 的說明。

**注意：** 套件的名稱必須以 `gitbook-plugin-` 起始，**package engines** 也應該包含 `gitbook`。

#### index.js

外掛套件是以 `index.js` 為主要程式起點：

```js
module.exports = {
    // Map of hooks
    hooks: {},
    
    // Map of new blocks
    blocks: {},
    
    // Map of new filters
    filters: {}
};
```

## 發佈你的外掛

GitBook 外掛的發布與安裝都透過 [NPM](https://www.npmjs.com)。

在發佈之前，你必須擁有 npmjs.com](https://www.npmjs.com) 的帳號，設置完成後使用終端機指令就能發佈：

```
$ npm publish
```

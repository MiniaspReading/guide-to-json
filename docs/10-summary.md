# 第十章 結論
JSON 作為資料容器的運輸工具，他並不鎖定單一功能，在 NoSQL 的 JSON 中看到這樣的角色。JSON 在專案中的應用越來越常見，且發展成很實用的工具。
JSON 另外一個所扮演的角色：設定檔案的容器。

## 以 JSON 作為設定檔

組態或設定檔通常用於軟體以讓他可以改變而無須重新編譯，通常設定檔的格式大都為 INI、XML。

### INI 格式的設定檔範例
```sh
[general]
playInfo = false
mouseSensitivity = 0.54

[display]
complexTextures = true
mode = wondowed
widgetsPerFrame = 222

[sount]
volume =1
effects = 0.68
```
 ### XML 格式的設定檔範例
 
 ```sh
<?xml version="1.0" encoding="UTF-8"?>
<settings>
   <general>
     <playInfo>false</playInfo>
     <mouseSensitivity>false</mouseSensitivity>
   </general>
   <display>
     <complexTextures>false</complexTextures>
     <mode>wondowed</mode>
     <widgetsPerFrame>222</widgetsPerFrame>
   </display>
   <sount>
     <volume>1</volume>
     <effects>0.68</effects>
   </sount>
</settings>
   ```
### JSON 格式的設定檔範例
 
 ```sh
{
  "settings": {
    "general": {
      "playInfo": "false",
      "mouseSensitivity": "false"
    },
    "display": {
      "complexTextures": "false",
      "mode": "wondowed",
      "widgetsPerFrame": "222"
    },
    "sount": {
      "volume": "1",
      "effects": "0.68"
    }
  }
}
 
 ```
INI 檔案讓人很容易閱讀，快速找到要修改的設定區域，但不適合更為複雜的資料。XML 格式適合更複雜的資料，但沒有 JSON 的資料型別。
此三種格式人眼都可讀，所以很適合做為設定檔。

Node .js 預設的 Javascript 套件管理員：npm 是以 JSON 作為套件的設定檔。package.json 檔案保存了每一個套件的特定資訊，
，像是名稱、版本、貢獻者、相以性、說明、授權等。

```sh
{
  "name": "guide-to-json",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "directories": {
    "doc": "docs"
  },
  "scripts": {
    "test": "true",
    "build": "docpress b",
    "deploy": "git-update-ghpages -e --keep MiniaspReading/guide-to-json _docpress"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/MiniaspReading/guide-to-json.git"
  },
  "author": "MiniaspReading <jeff@miniasp.com.tw>",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/MiniaspReading/guide-to-json/issues"
  },
  "homepage": "https://github.com/MiniaspReading/guide-to-json#readme",
  "devDependencies": {
    "docpress": "^0.6.10",
    "git-update-ghpages": "1.3.0",
    "markdown-it-decorate": "1.0.0",
    "resolve": "^1.1.6"
  }
}
```  
雖然 JSON 是作為設定檔容器使用，他還是扮演著資料交換格式的角色

### 大局

* 在伺服器端，物件可以序列化成 JSON 文字格式並反序列化回物件。JSON 也可從伺服器端程式請求。

* 此外 JSON 也可作為文件儲存體類型資料庫的文件，第八章我們使用 CouchDB API 介面的資料操作。

* JavaScript 的 XmlHttpRequest 可以從一個 URL 請求 JSON 資源。為於 JavaScript 程式中使用 JSON 
我們必須將 JSON 反序列化成 JavaScript 物件，透過內建的 JSON.press() 函式達成。

* 在網際網路瀏覽器等系統中，JavaScript 支援物件導向程式設計，JSON 很適合交換資料，可透過 API 溝通及以建構 AJAX 互動。

* 在伺服器端物件導向的架構中，JSON 很適合交換資料，JSON 進出系統時以物件實字維護資料的結構。



 
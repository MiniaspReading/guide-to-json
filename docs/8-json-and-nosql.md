# 第八章 JSON 與 NoSQL

一般 Web 應用程式通常都是使用關聯性資料庫做為資料儲存體，就可以很容易的透過 SQL 語法做新增、修改、刪除與查詢對資料進行操作，
甚至可以結合兩個表格的查詢。

```sh
SELECT Account.firstName,Account.lastName,Address.street,Address.zip From Account JOIN Address
ON Account.accoundId = Address.accountId;
```
透過SQL JOIN 語句，就可以取得 Account 與 Address 這兩個資料表的關聯資料：firstName，lastName，street與zip。

<b> NoSQL 不是關聯式資料庫，無法使用 SQL 語句查詢資料已取得關聯表格。</b> NoSQL是一個【鍵-值儲存體】有些是XML文件或JSON文件，
我們討論一種使用JSON文件來儲存資料的文件儲存體資料庫 <b>[CouchDB](http://couchdb.apache.org/) </b>。
## CouchDB 資料庫 ##

[CouchDB](http://couchdb.apache.org/) 是一種 NoSQL 資料庫，以非關聯式方式儲存 JSON 文件資料。

CouchDB 網站位置：<a href="http://couchdb.apache.org/" target="_blank">http://couchdb.apache.org/</a>

<font color="red" ><i>以【NoSQL】冠名的資料庫，就是告訴我們他不是關聯式資料庫，我們不能使用SQL語句來查詢資料。</i></font>

當我們要查詢帳戶與地址這總關聯式資料庫時，使用 [CouchDB](http://couchdb.apache.org/) 時，資料的關係不會要求使用資料表分開的方式儲存
並於讀取時組合，關係是由資料表達。
####　範例【表示帳戶的JSON物件】###
```sh
{
  "firstName": "Bob",
  "lastName" : "Barker",
  "age" : 91,
  "address" : [
	{
	"street" : "123 fake st",
	"city" : "Somewhere",
	"state" : "OR",
	"zip" : "97520"
	},
	{
	"street" : "456 fake st",
	"city" : "Some Place",
	"state" : "CA",
	"zip" : "9600"
	}
	]
}
```
當我們向 [CouchDB](http://couchdb.apache.org/)  資料庫查詢帳戶資料時，會取得一份結構化的文件，無須重組關聯性，這種方式既方便又快。
但是當需要多層的關聯，這種文件模式很快就會遇到麻煩。例如地址與城市要與不同的表作關聯，或者是城市
與郵遞區號產生關聯，單一結構文件就會很難表達複雜的關係。

[CouchDB](http://couchdb.apache.org/)  另一個擅長的事情就是處裡演進資料。<i>我覺得用【處裡演進資料】來敘述有點抽象，我把它稱為
【加欄位】這樣比較有感覺，每當客戶要改資料欄位時，就真的很想....幫他改XDD。</i> 當我的資料表越複雜時，
也許就會再開一個資料表來協助儲存關聯資訊。

使用 [CouchDB](http://couchdb.apache.org/)  時，當資料<b>演進</b>時可以不需要修改結構描述，可以在JSON中以物件陣列代表電話號碼，這樣每個帳號
可以有無限的相關電話號碼相關紀錄。
####　範例【物件陣列代表電話號碼】###
```sh
{
  "phoneNumbers" : [
    {
	   "description" : "home phone",
	   "number" : "02-753-3967"
	},
	{
	   "description" : "cell phone",
	   "number" : "0935-999-999"
	},
	{
	   "description" : "fax",
	   "number" : "02-899-9888"
	}
  ]
}
```
如果再度演進，買了第二支手機有新的號碼，我們就可以直接將他加入陣列中。
####　範例【物件陣中加入新的號碼】###
```sh
{
  "phoneNumbers" : [
    {
	   "description" : "home phone",
	   "number" : "02-753-3967"
	},
	{
	   "description" : "cell phone",
	   "number" : "0935-999-999"
	},
	{
	   "description" : "fax",
	   "number" : "02-899-9888"
	},
	{
	   "description" : "cell phone2",
	   "number" : "0988-888-888"
	}
  ]
}
```
另外，若要在帳戶中加入新的欄位，我們可以直接加入新的紀錄中，無須修改資料結構描述。加入"galaxy"。
####　範例【帳戶加入新的欄位】###
```sh
{
  "firstName": "Bob",
  "lastName" : "Barker",
  "age" : 91,
  "address" : [
				{
				"street" : "123 fake st",
				"city" : "Somewhere",
				"state" : "OR",
				"zip" : "97520"
				},
				{
				"street" : "456 fake st",
				"city" : "Some Place",
				"state" : "CA",
				"zip" : "9600"
				}
  			  ],
    "galaxy" : "Milky Way"				
}
```
<i> PS：看了這些介紹好像感覺不出來有多強大阿。</i>
問題是使用 [CouchDB](http://couchdb.apache.org/)  到底要如何寫入資料與讀取資料呢?到底是有多強呢?讓我們繼續看下去.....。

## 安裝CouchDB ##
使用Ubuntu安裝方式很簡單，照著官網提供的方式順序安裝即可完成。

* 安裝 ppa-finding 工具 for 12.04 release

``` sudo apt-get install python-software-properties -y ``` 

```sudo apt-get install software-properties-common -y ```

* 添加 PPA 。PPA 說明參考網址：[PPA](http://askubuntu.com/questions/4983/what-are-ppas-and-how-do-i-use-them)

``` sudo add-apt-repository ppa:couchdb/stable -y ```

* 更新套件

``` sudo apt-get update -y ```

* 移除全部的二進位安裝方式的 Couchdb 檔案

```
sudo apt-get remove couchdb couchdb-bin couchdb-common -yf 
```

* 開始安裝 Couchd，加入-V 參數，可以觀看安裝訊息

``` 
sudo apt-get install -V couchdb 
``` 
  >Reading package lists...   
  Done Building dependency tree   
  Reading state information...   
  Done   
  The following extra packages will be installed:  
  couchdb-bin (x.y.z0-0ubuntu2)   
  couchdb-common (x.y.z-   0ubuntu2)   
  couchdb (x.y.z-0ubuntu2)   

* 停止 Couchdb 

```sudo stop couchdb  ```  
 >couchdb stop/waiting
   
#### 若有需求可修改 /etc/couchdb/local.ini 設定檔的 'bind_address=0.0.0.0' 修改連線IP  

* 啟動 CouchDB 指令

```sudo start couchdb  ``` 
>couchdb start/running, process 3541


馬上透過網址連線 CouchDB，[http://127.0.0.1:5984/](http://127.0.0.1:5984/)
若已正常啟動，就以透過網址方式看到網頁顯示的內容，代表您的 CouchDB 已安裝成功。
```sh
{
    "couchdb": "Welcome",
    "uuid": "ca53fa82a896fde3fe1f35d53162bedb",
    "version": "1.6.1",
    "vendor": {
        "name": "Ubuntu",
        "version": "14.04"
    }
}

```

####　相關連結 
[其他安裝方式](http://docs.couchdb.org/en/1.6.1/install/index.html)

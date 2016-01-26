# 第八章 JSON 與 NoSQL

一般 Web 應用程式通常都是使用關聯性資料庫做為資料儲存體，就可以很容易的透過 SQL 語法做新增、修改、刪除與查詢對資料進行操作，
甚至可以結合兩個表格的查詢。

```sh
SELECT Account.firstName,Account.lastName,Address.street,Address.zip From Account JOIN Address
ON Account.accoundId = Address.accountId;
```
透過SQL JOIN 語句，就可以取得 Account 與 Address 這兩個資料表的關聯資料：firstName，lastName，street與zip。

* NoSQL 不是關聯式資料庫，無法使用 SQL 語句查詢資料已取得關聯表格。* NoSQL是一個【鍵-值儲存體】*有些是XML文件或JSON文件，
我們討論一種使用JSON文件來儲存資料的文件儲存體資料庫 * CouchDB。
## CouchDB 資料庫 ##

[CouchDB](http://couchdb.apache.org/) 是一總NoSQL資料庫，已非關聯式方式儲存JSON文件資料。
```sh
已【NoSQL】冠名的資料庫，就是告訴我們他不是關聯式資料庫，我們不能使用SQL語句來查詢資料。
```

當我們要查詢帳戶與地址這總關聯式資料庫時，使用CouchDB時，資料的關係不會要求使用資料表分開的方式儲存
並於讀取時組合，關係是由資料表達。
###　範例【表示帳戶的JSON物件】###
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
當我們像CouchDB資料庫查詢帳戶資料時，會取得一份結構化的文件，無須重組關聯性，這種方式既方便又快。
但是當需要多層的關聯，這種文件模式很快就會遇到麻煩。例如地址與城市要與不同的表作關聯，或者是城市
與郵遞區號產生關聯，單一結構文件就會很難表達複雜的關係。(所以SQL資料庫存在是有意義的!XD)。

CouchDB另一個擅長的事情就是處裡演進資料。 *我覺得用【處裡演進資料】來敘述有點抽象，我把它稱為
【加欄位】這樣比較有感覺，每當客戶要改資料欄位時，就真的很想....幫他改XDD。*  當我的資料表越複雜時，
也許就會再開一個資料表來協助儲存關聯資訊。

使用CouchDB時，當資料演進時可以不需要修改結構描述，可以在JSON中以物件陣列代表電話號碼，這樣每個帳號
可以有無限的相關電話號碼相關紀錄。
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
如果再度演進，買了兩支手機有新的號碼，我們就可以直接將他加入陣列中。
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
* PS：看了這些介紹好像感覺不出來有多強大阿。

問題是使用CouchDB到底要如何寫入資料與讀取資料呢?到底是有多強呢?讓我們繼續看下去.....。

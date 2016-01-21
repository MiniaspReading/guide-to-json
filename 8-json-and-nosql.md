#第八章 JSON 與 NoSQL

一般 Web 應用程式通常都是使用關聯性資料庫做為資料儲存體，就可以很容易的透過 SQL 語法做新增、修改、刪除與查詢對資料進行操作，
甚至可以結合兩個表格的查詢。

```sh
SELECT Account.firstName,Account.lastName,Address.street,Address.zip From Account JOIN Address
ON Account.accoundId = Address.accountId;
```
透過SQL JOIN 語句，就可以取得 Account 與 Address 這兩個資料表的關聯資料：firstName，lastName，street與zip。

*NoSQL*不是關聯式資料庫，無法使用 SQL 語句查詢資料已取得關聯表格。*NoSQL*是一個*【鍵-值儲存體】*有些是XML文件或JSON文件，
我們討論一種使用JSON文件來儲存資料的文件儲存體資料庫*CouchDB*。
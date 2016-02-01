# 第九章 伺服器端的 JSON
在第八章我們使用 *HTTP* 來發送 *JSON* 文件給 *CouchDB* 的 API，伺服器端程式就必須解析結構，
做出相對的動作應並回傳結果。
分類伺服器端與用戶端技術分類：
*   用戶端：HTML、CSS、Javascript...等。
*   伺服器端：PHP、ASP .NET、Node.js...等。

## 9-1 序列化、反序列化與請求JSON 
網路上的資料交換格式需要用戶端與伺服器的支援，如果只有用戶端支援沒有伺服器端支援，JSON 會消逝。幸好JSON格式
受大部分伺服器端網路架構與程式語言的支援。若沒有內建 JSON 序列化或反序列化支援，其函式庫或擴充套件也會支援。
    
    序列化：將物件轉化成文字的動作 
    反序列化：將文字轉化成物件的動作
    
### 9-1-1 ASP .NET

為解析 JSON ，我們必須使用第三方的 ASP .NET 函式庫，我們使用的函式庫為 Json .Net ，他來至
[Newtonsoft](http://www.newtonsoft.com/json) 的開源 JSON 架構。

### 9-1-2 JSON 序列化

專案透過 [Nuget](https://www.nuget.org/packages/Newtonsoft.Json/) 安裝 JSON .NET。

``` PM> Install-Package Newtonsoft.Json ```

ASP .NET C# 中定義 Accousts 型別
    
```sh
public class Account
{
    public string firstName {get; set;}
    public string lastName {get; set;}
    public int age {get; set;}
    public Address[] address {get; set;}    
}

    public class Address
{
    public string street {get; set;}
    public string city {get; set;}
    public string state {get; set;}
    public int zip {get; set;}    
}
```
程式中建立新的物件並給定值。
```sh
 Account myaccount = new Account();
 myaccount.firstName = "Bob";
 myaccount.lastName = "Barker";
 myaccount.age = 91;
 
 Address[] addrsses;
 addrsses = new Address[2];
 
 Address myaddress1= new Address();
 myaddress1.street="123 fake st";
 myaddress1.city="Somewhere";
 myaddress1.state="OR";
 myaddress1.zip=1234;
 
 addrsses[0] = myaddress1;
 
 Address myaddress2= new Address();
 myaddress2.street="456 fake st";
 myaddress2.city="Some Place";
 myaddress2.state="CA";
 myaddress2.zip=9600;
 
 addrsses[1] = myaddress2;
 
 myaccount.Address = addrsses;
 
```
最後使用 JSON .NET 函式庫將此物件序列化成 JSON 。

```sh
 string json = JsonConvert.SerializeObject(myaccount);
```
物件序列化成 JSON 的結果。
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
### 9-1-3 JSON 反序列化

將前一例的 JSON 字串反序列化，將會被反序列化成 Accousts 型別。
```sh
Account account = JsonConvert.DeserializeObject<Account>(json);
```
重點是我們的物件屬性名稱與 JSON 文件中的名稱-值對的名稱要相符，不然會反序列化失敗。

### 9-1-4 請求 JSON
在ASP .NET 環境中，通常需要輸出 JSON 格式給前端運用，都會使用 WebAPI 的方式開發，因為預設回應的格式自然就是 JSON 了。

參考網站 [http://blog.sanc.idv.tw/2012/04/aspnet-mvc-4-web-apihello-web-api.html](http://blog.sanc.idv.tw/2012/04/aspnet-mvc-4-web-apihello-web-api.html)

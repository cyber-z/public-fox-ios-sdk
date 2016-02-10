#Force Operation X 
iOS向け
F.O.Xエンゲージメント配信
Criteo連携仕様書
v2.16g

株式会社CyberZ 2016/2/2

## 1. 概要
本ドキュメントでは、Force Operation X SDK(以下F.O.X)におけるF.O.Xエンゲージメント配信およびCriteoとの連携を行う際に必要となる実装を説明します。対応しているF.O.X SDKのバージョンは **v2.16g** 以上となります。F.O.Xエンゲージメント配信連携を行う場合は同一の箇所にLTVとアクセス解析のそれぞれの計測処理を実装する必要があります。

### 1.1.	SDK仕様
F.O.X SDKアクセス解析機能を利用することにより媒体を横断したイベント計測連携を行います。計測は内容に応じて各種メソッドを実行することで行います。

引数それぞれのパラメータの仕様は以下の通りです。

| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
eventName       |        String |     計測を行うイベント種別に応じて、指定されたイベント名を設定します。
<span style="color:#b8b8b8">action     |        <span style="color:#b8b8b8">String |     <span style="color:#b8b8b8">使用しません。 
label	|String|	アクションに属するラベル名を設定します。ラベル名は⾃由に設定可能です。
orderId	|String|	注⽂番号等を指定します。
sku	|String|商品コード等を指定します。
 <span style="color:#b8b8b8">itemName| <span style="color:#b8b8b8">String| <span style="color:#b8b8b8">使用しません。
 <span style="color:#b8b8b8">value	| <span style="color:#b8b8b8">int|<span style="color:#b8b8b8">使用しません。
price|	double|	売上金額を指定します。
quantity|	int|	数量を指定します。price * quantityが売上金額として計上されます。
currency	|String|	通貨コードを指定します。nullの場合は”JPY”が指定されます。
eventInfo|	JSONObject|	任意のイベント情報をまとめて送信する際に指定します。

### 1.2. eventInfo仕様
eventInfo内にアクションに付随する情報をJson形式で設定することで、ダイナミックな配信連携が可能になります。
Jsonの仕様は以下の通りです。 

| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
|product[].id	|String	|閲覧した、カートに入れた等の商品IDを設定します。|
|product[].price	|double	|閲覧した、カートに入れた等の商品単価を設定します。|
|product[].quantity	|int	|閲覧した、カートに入れた等の商品数量を設定します。|
|product[].category	|String|	閲覧した、カートに入れた等の商品カテゴリを指定します。<br>複数ある場合はカンマ「,」区切り、階層がある場合は「>」で分割します。<br>例）映画、ビデオ>DVD>スポーツ、レジャー|
|din	|String	|開始日の指定がある場合に設定します。|
|dout	|String	|終了日の指定がある場合に指定します。|
|criteo_partner_id	|String	|CriteoアカウントIDが同一アプリで異なる場合に設定します。|
|fox_cvpoint	|Long	|F.O.Xの成果地点IDを入力します。|
 
### 1.3. リアルタイムデータフィード更新仕様
eventInfo内にデータフィードの更新情報をJson形式で設定することで、F.O.Xエンゲージメント配信連携により、リアルタイムにデータフィードを更新することができます。

データフィードの状態が更新されるアクションの場合、下記を実装してください。

| 引数 |必須|型 | 概要 |
|:----------:|:-------:|:----:|:------------|
datafeed.version|必須|String|データフィードのバージョンを指定します。
datafeed.product|必須|Array<Object>|商品マスタデータフィードの設定領域です。
datafeed.product[].id|必須	|String|データフィードの商品を一意に識別するIDです。
datafeed.product[].action	|必須|String|データフィードをどのように変更するかを入力します。<br>U:追加もしくは編集　D:削除
datafeed.product[].name|必須|String|商品名です。<br>削除の際はnullで構いません。
datafeed.product[].expire|任意|String|商品の有効期限です。<br>「yyyy-MM-dd HH:mm:ss」もしくは「yyyy-MM-dd」の書式で日付を入力してください。
datafeed.product[].effective|任意|String|商品の公開日時です。<br>これが設定された場合、公開日時になるまで商品は表示されません。「yyyy-MM-dd HH:mm:ss」もしくは「yyyy-MM-dd」の書式で日付を入力してください。
datafeed.product[].img|任意|String|商品画像のURLです。
datafeed.product[].category1|任意|String|第一階層のカテゴリを指定します。
datafeed.product[].category2|任意|String|第二階層のカテゴリを指定します。
datafeed.product[].category3|任意|String|第三階層のカテゴリを指定します。
datafeed.product[].price|任意|Double|商品の価格を指定します。
datafeed.product[].currency|任意|String|商品の通貨コードを指定します。nullの場合JPYが適用されます。
datafeed.product[].(任意)|任意|String|その他の配信や分析に使用する項目を指定します。データフィードの項目を設定してください。

### 1.4. イベント情報の送信方法

ヘッダファイル AnalyticsManager.hをインポートします。
```objective-c
 #import "AnalyticsManager.h"
```

次のsendEventメソッドを利用し、イベント情報を送信します。
```objective-c
+ (void)sendEvent:(NSString*)eventName
           action:(NSString*)action
            label:(NSString*)label
          orderID:(NSString*)orderID
              sku:(NSString*)sku
         itemName:(NSString*)itemName
            price:(double)price
         quantity:(NSUInteger)quantity
         currency:(NSString*)currency;
         eventInfo:(NSDictionary*)eventInfo;
```
    
　　
　　
　　
　　　　
## 2.イベント計測の実装
F.O.X SDKで対応しているF.O.XエンゲージメントおよびCriteoのイベント計測は以下の５つとなっています。

- View Home イベント
- View Listing イベント
- View Product イベント
- View Basket イベント
- Track Transaction イベント

### 2.1	View Home(アプリトップ訪問イベント)実装方法
View Home（ホーム画面）イベントが発生する箇所に、下記に従ってアクセス解析のイベント計測機能を実装ください。

```objective-c
[ForceAnalyticsManager sendEvent:@"_view_toppage" 
action:nil 
label:nil 
value:0　
eventInfo:@{
@"din":@"2016-01-02",
@"dout":@"2016-01-05",
@"criteo_partner_id":@"XXXXX",
@"fox_cvpoint":@"12345"
}];
```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
eventName|NSString|“\_view\_toppage”を指定してください。
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">value|<span style="color:#b8b8b8">NSInteger|<span style="color:#b8b8b8">使用しません。
eventInfo(din/dout)|NSDictionary|日付の指定がある場合は入力（任意）
eventInfo(criteo_partner_id)|NSDistionary|CriteoアカウントIDが同一アプリで異なる場合は入力(任意)
eventInfo(fox_cvpoint)|NSDirectory|F.O.Xの成果地点IDを設定します。(任意)

　　
　　　　
### 2.2	View Listing（複数商品閲覧イベント）実装方法
View Listing（検索結果・一覧画面）イベントが発生する箇所に、下記に従ってアクセス解析のイベント計測機能を実装ください。上位３つの商品が計測されます。

```objective-c
[ForceAnalyticsManager 
		sendEvent:@"_view_listing"
		action: nil
		label: nil
		value: 0
		eventInfo:@{
@"fox_cvpoint":12345,
@"product":@[
{@"id": "111", @"category":@"映画、ビデオ>DVD>スポーツ、レジャー"},
{@"id": "112", @"category":@"映画、ビデオ>DVD>スポーツ、レジャー"},
{@"id": "113", @"category":@"映画、ビデオ>DVD>スポーツ、レジャー"}
], 
@"din":@"2016-01-02",
@"dout":@"2016-01-05",
@"criteo_partner_id":@"XXXXX"
}];

```


#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
eventName|NSString|"\_view\_listing"を指定してください。
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">value|<span style="color:#b8b8b8">NSInteger|<span style="color:#b8b8b8">使用しません。
eventInfo(product)|NSDictionary|Productをキーとして商品ID を配列で⼊⼒してください。
eventInfo(product[].id)|NSDictionary|商品IDを設定します。<br>データフィードと同じ商品IDを使⽤してください。
eventInfo(product[].category)|NSDictionary|商品カテゴリ.データフィードと同じ商品カテゴリを使用してください。<br>１商品に対して複数カテゴリある場合はカンマ「,」区切り、階層がある場合は「>」で分割します。<br>例）映画、ビデオ>DVD>スポーツ、レジャーnullでも構いません。
eventInfo(din/dout)|NSDictionary|⽇付の指定がある場合は⼊⼒してください。（任意）
eventInfo(criteo_partner_id)|NSDictionary|Criteo アカウントID が同⼀アプリで異なる場合は⼊⼒(任意)
eventInfo(fox_cvpoint)|NSDirectory|F.O.Xの成果地点IDを設定します。

　　
　　　　
### 2.3	View Product（商品閲覧イベント）実装方法
View Product（単一商品閲覧）イベントが発生する箇所に、下記に従ってアクセス解析のイベント計測機能を実装ください。

```objective-c
JSONObject json = new JSONObject("{
'fox_cvpoint':12345,
'product':[{'id': '111'}],
'din':'2016-01-02',
'dout':'2016-01-05',
'criteo_partner_id':'XXXXX'
}");
AnalyticsManager.sendEvent(this, "_view_content", null, null, 0, json);
```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
eventName|NSString|"\_view\_content" を指定してください。
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">value|<span style="color:#b8b8b8">NSInteger|<span style="color:#b8b8b8">使用しません。
eventInfo(fox_cvpoint)|NSDictionary|F.O.Xの成果地点IDを設定します。
eventInfo(product[].id)|NSDictionary|閲覧した商品IDを設定します。
eventInfo(din/dout)|NSDictionary|⽇付の指定がある場合は⼊⼒してください。（任意）
eventInfo(criteo_partner_id)|NSDictionary|Criteo アカウントID が同⼀アプリで異なる場合は⼊⼒(任意)

　　
　　　　
### 2.4	View Basket（買い物かご）実装方法
View Basket（商品購入予定一覧）イベントが発生する箇所に、下記に従ってアクセス解析のイベント計測機能を実装ください。

```objective-c
[ForceAnalyticsManager sendEvent:@"_add_to_cart" 
action: nil 
label: nil 
value: 0 
eventInfo:@{
@"din":@"2016-01-02", 
@"dout":@"2016-01-05",
@"currency":@"JPY",
@"criteo_partner_id":@"XXXXX",
@"fox_cvpoint":12346,
@"product":@[
{@"id ":@"1234",@"price":@100,@"quantity":@1},
	{@"id ":@"1235",@"price":@200,@"quantity":@2},
	{@"id ":@"1236",@"price":@300,@"quantity":@3}
]
}];


```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
eventName|NSString|"\_add\_to\_cart" を指定してください。
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">value|<span style="color:#b8b8b8">NSInteger|<span style="color:#b8b8b8">使用しません。
eventInfo(fox_cvpoint)|NSDictionary|F.O.Xの成果地点IDを設定します。
eventInfo(product[].id)|NSDirectory|商品ID<br>データフィードと同じ商品IDを使用してください。
eventInfo(product[].price)|NSDirectory| 該当商品の価格を設定します。
eventInfo(product[].quantity)|NSDirectory|該当商品を買った個数を設定します。
eventInfo(currency)|NSDictionary|通貨<br>Nil/Nullの場合、デフォルト “JPY”
eventInfo(din/dout)|NSDictionary|⽇付の指定がある場合は⼊⼒してください。（任意）
eventInfo(criteo_partner_id)|NSDictionary|Criteo アカウントID が同⼀アプリで異なる場合は⼊⼒(任意)

　　
　　　　
### 2.5	Track Transaction（商品購入イベント）実装方法
Track Transaction（商品購入）イベントが発生する箇所に、下記に従ってアクセス解析のイベント計測機能を実装ください。

```objective-c
[ForceAnalyticsManager 
		sendEvent:@"_purchase"
		action:nil
		label:nil
		orderID:nil
		sku:nil
		itemName:nil
		price:1400
		quantity:6
		currency: "JPY"
		eventInfo: @{
@"fox_cvpoint":12348, 
@"transaction_id":@"ABC",
@"product":@[
{@"id ":@"1234",@"price":@100,@"quantity":@1},
{@"id ":@"1235",@"price":@200,@"quantity":@2},
{@"id ":@"1236",@"price":@300,@"quantity":@3}
],
@"din":@"2016-01-02",
@"dout":@"2016-01-05",
@"criteo_partner_id":@"XXXXX"
}]; 


```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
eventName|NSString|任意の名前を指定してください。<br>特に指定がない場合は、"_purchase" を指定してください。
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
orderID|NSString|（任意）購入時のオーダーIDを指定します。
sku|NSString|（任意）商品のSKUを指定します。
<span style="color:#b8b8b8">itemName|<span style="color:#b8b8b8">NSString|<span style="color:#b8b8b8">使用しません。
price|double|商品総額<br><span style="color:red">※必ず price * quantity の値が商品総額となるよう指定ください
quantity|NSUInteger|1を指定してください。
currency|NSInteger|通貨コード。<br>Nil/Nullの場合、デフォルト”JPY”となります。
eventInfo(fox_cvpoint)|NSDirectory|F.O.Xの成果地点IDを設定します。
eventInfo(transaction.id)|NSDictionary|注文番号、問い合わせ番号などのトランザクションID
eventInfo(product[].id)|NSDirectory|商品IDを設定します。<br>データフィードと同じ商品IDを使用してください。
eventInfo(product[].price)|NSDirectory|該当商品の価格を設定します。eventInfo(product[].quantity)|NSDirectory|該当商品を買った個数を設定します。
eventInfo(din/dout)|NSDictionary|⽇付の指定がある場合は⼊⼒してください。（任意）
eventInfo(criteo_partner_id)|NSDictionary|Criteo アカウントID が同⼀アプリで異なる場合は⼊⼒(任意)<br>以下、このアクションによってデータフィードが変動する場合に設定します。
eventInfo(datafeed.product)|NSDirectory|変動するデータフィードを設定します。
eventInfo(datafeed.product[].id)|NSDirectory|データフィードのアイテムを一意に識別するIDです。
eventInfo(datafeed.product[].action)|NSDirectory|データフィードをどのように変更するかを入力します。<br>U:追加もしくは編集　D:削除
eventInfo(datafeed.product[].name)|NSDirectory|アイテム名です。以下全て、削除の際はnullで構いません。
eventInfo(datafeed.product[].expire)|NSDirectory|アイテムの有効期限です。<br>「yyyy-MM-dd HH:mm:ss」もしくは「yyyy-MM-dd」の書式で日付を入力してください。nullでも構いません。
eventInfo(datafeed.product[].effective)|NSDirectory|アイテムの公開日時です。<br>これが設定された場合、公開日時になるまで商品はでません表示されません。「yyyy-MM-dd HH:mm:ss」もしくは「yyyy-MM-dd」の書式で日付を入力してください。nullでも構いません。
eventInfo(datafeed.product[].img)|NSDirectory|アイテムの画像URLです。nullでも構いません。
eventInfo(datafeed.product[].category1)|NSDirectory|第一階層のカテゴリを指定します。nullでも構いません。
eventInfo(datafeed.product[].category2)|NSDirectory|第二階層のカテゴリを指定します。nullでも構いません。
eventInfo(datafeed.product[].category3)|NSDirectory|第三階層のカテゴリを指定します。nullでも構いません。
eventInfo(datafeed.product[].price)|NSDirectory|アイテムの価格を指定します。nullでも構いません。
eventInfo(datafeed.product[].currency)|NSDirectory|アイテムの通貨コードを指定します。nullの場合JPYが適用されます。
eventInfo(datafeed.product[].{任意})|NSDirectory|その他配信、分析に使用する項目を指定します。



<span style="color:red">※必ず price * quantity の値が商品総額となるよう指定ください※商品購⼊イベントの price に⼊⼒する⾦額は必ず、Json データに指定した商品の総額 (price * quantity)となるよう指定してください。指定されていない場合、集計が正しく⾏われません。



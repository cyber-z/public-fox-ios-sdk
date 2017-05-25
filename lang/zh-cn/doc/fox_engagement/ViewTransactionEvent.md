# Track Transaction（商品购入事件）実装方法

在Track Transaction（商品购入）事件发生的地点、请按照下面的例子来安装流量分析的事件计测功能。

### 安装实例

```objective-c
[ForceAnalyticsManager sendEvent:@"_purchase"
		                      action:nil
		                       label:nil
		                     orderID:nil
		                         sku:nil
		                    itemName:nil
		                       price:2750
		                    quantity:6
		                    currency: "JPY"
		                   eventInfo: @{
                              @"fox_cvpoint":12348,
                           @"transaction_id":@"ABC",
                                  @"product":@[
                                          {@"id ":@"1234",@"price":550,@"quantity":@1},
                                          {@"id ":@"1235",@"price":550,@"quantity":@2},
                                          {@"id ":@"1236",@"price":550,@"quantity":@2}
                                  ],
                                      @"din":@"2016-01-02",
                                     @"dout":@"2016-01-05",
                        @"criteo_partner_id":@"XXXXX",
                        @"datafeed":@{
                                @"version":@"v1.0"
                                @"product":@[
                                          {
                                                   @"id":12345,
                                               @"action":@"U",
                                                 @"name":@"icecreame",
                                               @"expire":@"2016-10-31",
                                            @"effective":@"2016-04-01",
                                                  @"img":@"http://pngimg.com/upload/ice_cream_PNG5099.png",
                                            @"category1":@"food",
                                                @"price":@"2750",
                                             @"currency":@"JPY"
                                          }
                                ]
                        }
                       }
];
```

### 参数详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventName|NSString|请指定为任意名称。如果没有特別指定，请指定为"_purchase"。|
|<span style="color:grey">action|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">label|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|orderID|NSString|（任意）指定订单号。|
|sku|NSString|（任意）指定商品代号sku。|
|<span style="color:grey">itemName|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|price|double|指定商品总额。<br><span style="color:red">※请务必把price * quantity的结果作为商品总额来指定|
|quantity|NSUInteger|请指定为1。|
|currency|NSUInteger|指定货币代码。<br>nil的场合默认指定为"JPY"。|
|eventInfo|NSDictionary|事件资讯详细 (参考下面)|

#### 事件资讯详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventInfo (fox_cvpoint)|NSDictionary|设定F.O.X的成果地点ID。|
|eventInfo (transaction_id)|NSDictionary|订单号，咨询号等处理事务ID|
|eventInfo (product)|JSONArray|把Product作为KEY，用数组形式设定商品ID。|
|  eventInfo (product[].id)|NSDictionary|商品ID<br>请使用和数据字段相同的商品ID。|
|  eventInfo (product[].price)|NSDictionary|设定该商品的价格。|
|  eventInfo (product[].quantity)|NSDictionary|设定购入该商品的个数。|
|eventInfo (din/dout)|NSDictionary|如果希望指定日期请输入。（任意）|
|eventInfo (criteo_partner_id)|NSDictionary|Criteo帐号ID在同一个APP里不一样的时候请设定。(任意)<br>在下方，根据这个Action的不同，在数据字段变动时做设定|
|eventInfo (datafeed)|NSDictionary|实时数据字段 (参考下方)|

#### 数据字段详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|datafeed (version)|NSDictionary|指定数据字段的版本。|
|datafeed (product)|JSONArray|指定变动的数据字段。|
|  datafeed (product[].id)|NSDictionary|能够专门识別数据字段的商品的ID。|
|  datafeed (product[].action)|NSDictionary|输入对数据字段的操作。<br>U:添加或编辑　D:删除|
|  datafeed (product[].name)|NSDictionary|商品名。<br>下面的项目同样，删除时可以设定为nil。|
|  datafeed (product[].expire)|NSDictionary|商品的有效期限。<br>请按照「yyyy-MM-dd HH:mm:ss」或者「yyyy-MM-dd」的格式来输入日期。可以为nil。|
|  datafeed (product[].effective)|NSDictionary|商品的公开日期和时间。<br>如果此项被设定，到公开日期和时间为止，商品不会被显示出来。<br>请按照「yyyy-MM-dd HH:mm:ss」或「yyyy-MM-dd」的格式来输入日期。可以为nil。|
|  datafeed (product[].img)|NSDictionary|商品的图像URL。<br>可以为nil。|
|  datafeed (product[].category1)|NSDictionary|指定第一层次的种別。<br>可以为nil。|
|  datafeed (product[].category2)|NSDictionary|指定第二层次的种別。<br>可以为nil。|
|  datafeed (product[].category3)|NSDictionary|指定第三层次的种別。<br>可以为nil。|
|  datafeed (product[].price)|NSDictionary|指定商品价格<br>可以为nil。|
|  datafeed (product[].currency)|NSDictionary|指定商品的货币代码。<br>nil的场合默认指定为"JPY"。|
|  datafeed (product[].{任意})|NSDictionary|指定其他投放或分析使用的项目。|

> ※ 商品购入事件的price里输入的金额，请一定按照Json数据里指定的商品总额(price * quantity)来指定。没有指定的话，无法正常统计。

---
[返回](/lang/zh-tw/doc/fox_engagement/README.md)<br>
[TOP](/lang/zh-tw/README.md)

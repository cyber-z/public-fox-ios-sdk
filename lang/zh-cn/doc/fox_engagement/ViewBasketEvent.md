# View Basket（购物筐）実装方法

　在View Basket（商品购入预定一览）事件发生的地点、请按照下面的例子来安装流量分析的事件计测功能。

### 安装例

```objective-c
[ForceAnalyticsManager sendEvent:@"_add_to_cart"
                          action: nil
                           label: nil
                           value: 0
                       eventInfo:@{
                           @"currency":@"JPY",
                        @"fox_cvpoint":12346,
                            @"product":@[
                                    {@"id ":@"1234",@"price":@100,@"quantity":@1},
	                                  {@"id ":@"1235",@"price":@200,@"quantity":@2},
	                                  {@"id ":@"1236",@"price":@300,@"quantity":@3}
                            ],
                                @"din":@"2016-01-02",
                               @"dout":@"2016-01-05",
                  @"criteo_partner_id":@"XXXXX"             
                       }
];
```

### 参数详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventName|NSString|请指定"\_add\_to\_cart"|
|<span style="color:grey">action|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">label|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">value|<span style="color:grey">NSUInteger|<span style="color:grey">不使用。|
|eventInfo|NSDictionary|事件资讯详细 (参考下面)|


#### 事件资讯详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventInfo (currency)|NSDictionary|货币<br>如果设定为Nil/Nil、默认为“JPY”|
|eventInfo (fox_cvpoint)|NSDictionary|设定F.O.X的成果地点ID。|
|eventInfo (product)|JSONArray|把Product作为KEY，用数组形式设定商品ID。|
|  eventInfo (product[].id)|NSDictionary|商品ID<br>请使用和数据字段相同的商品ID。|
|  eventInfo (product[].price)|NSDictionary|设定该商品的价格。|
|  eventInfo (product[].quantity)|NSDictionary|设定购入该商品的个数。|
|eventInfo (din/dout)|NSDictionary|如果希望指定日期请输入。（任意）|
|eventInfo (criteo_partner_id)|NSDictionary|Criteo帐号ID在同一个APP里不一样的时候请设定。(任意)|


---
[返回](/lang/zh-tw/doc/fox_engagement/README.md)<br>
[TOP](/lang/zh-tw/README.md)

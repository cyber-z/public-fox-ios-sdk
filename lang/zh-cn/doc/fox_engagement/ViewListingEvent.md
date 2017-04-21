#	View Listing（多个商品阅览事件）安装方法

　在View Listing（检索结果・一览画面）事件发生的地点、请按照下面的例子来安装流量分析的事件计测功能。先头的3个商品被计测。

### 安装实例

```objective-c
[ForceAnalyticsManager sendEvent:@"_view_listing"
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
                       }
];
```

### 参数详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventName|NSString|请指定"\_view\_listing"|
|<span style="color:grey">action|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">label|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">value|<span style="color:grey">NSUInteger|<span style="color:grey">不使用。|
|eventInfo|NSDictionary|事件资讯详细 (参考下面)|

#### 事件资讯详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventInfo (product)|NSDictionary|把Product作为KEY，用数组形式设定商品ID。|
|  eventInfo (product[].id)|NSDictionary|商品ID<br>请使用和数据字段相同的商品ID。|
|  eventInfo (product[].category)|NSDictionary|设定商品种別。<br>请使用和数据字段相同的商品种別。<br>如果一个商品有多个种別请用「,」区分、分层次请用「>」来分割。<br>例）电影，录像>DVD>体育，休闲，可以设定成nil。|
|eventInfo (din/dout)|NSDictionary|如果希望指定日期请输入（任意）|
|eventInfo (criteo_partner_id)|NSDictionary|Criteo帐号ID在同一个APP里不一样的时候请设定。(任意)|
|eventInfo (fox_cvpoint)|NSDictionary|设定F.O.X的成果地点ID。|

---
[返回](/lang/zh-tw/doc/fox_engagement/README.md)<br>
[TOP](/lang/zh-tw/README.md)

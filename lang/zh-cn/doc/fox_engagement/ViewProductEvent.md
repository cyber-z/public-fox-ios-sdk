#	View Product（商品阅览事件）安装方法

　在View Product（单个商品阅览）事件发生的地点、请按照下面的例子来安装流量分析的事件计测功能。

### 安装实例

```java
[ForceAnalyticsManager sendEvent:@"_view_content"
                          action: nil
                           label: nil
                           value: 0
                       eventInfo:@{
                              @"fox_cvpoint":12345,
                                  @"product":@[{@"id": "111"}],
                                      @"din":@"2016-01-02",
                                     @"dout":@"2016-01-05",
                        @"criteo_partner_id":@"XXXXX"
                       }
];
```

### 参数详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventName|NSString|请指定"\_view\_content"|
|<span style="color:grey">action|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">label|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">value|<span style="color:grey">NSUInteger|<span style="color:grey">不使用。|
|eventInfo|NSDictionary|事件资讯详细 (参考下面)|

#### 事件资讯详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventInfo (fox_cvpoint)|NSDictionary|设定F.O.X的成果地点ID。|
|eventInfo (product)|NSDictionary|把Product作为KEY，用数组形式设定商品ID。|
|  eventInfo (product[].id)|NSDictionary|设定阅览的商品ID。|
|eventInfo (din/dout)|NSDictionary|如果希望指定日期请输入（任意）|
|eventInfo (criteo_partner_id)|NSDictionary|Criteo帐号ID在同一个APP里不一样的时候请设定。(任意)|
　　

---
[返回](/lang/zh-tw/doc/fox_engagement/README.md)<br>
[TOP](/lang/zh-tw/README.md)

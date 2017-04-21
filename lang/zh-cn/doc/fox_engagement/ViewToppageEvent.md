#	View Home(APP TOP访问事件)安装方法
　在View Home（HOME画面）事件发生的地点、请按照下面的例子来安装流量分析的事件计测功能。

### 安装实例

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
                                  }
];
```

### 参数详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventName|NSString|请指定“\_view\_toppage”|
|<span style="color:grey">action|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">label|<span style="color:grey">NSString|<span style="color:grey">不使用。|
|<span style="color:grey">value|<span style="color:grey">NSUInteger|<span style="color:grey">不使用。|
|eventInfo|NSDictionary|事件资讯详细 (参考下面)|


#### 事件资讯详细

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventInfo (din/dout)|NSDictionary|如果希望指定日期请输入（任意）|
|eventInfo (criteo_partner_id)|NSDictionary|Criteo帐号ID在同一个APP里不一样的时候请设定。(任意)|
|eventInfo (fox_cvpoint)|NSDictionary|设定F.O.X的成果地点ID。|

---
[返回](/lang/zh-tw/doc/fox_engagement/README.md)<br>
[TOP](/lang/zh-tw/README.md)

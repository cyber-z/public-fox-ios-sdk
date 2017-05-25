## 依靠流量分析进行付费计测

利用流量分析机能，能够计测不同广告流入和自然流入的用户付费状况。如果希望在LTV计测地点也做付费计测，请在同一个地点安装LTV和流量分析的各自的计测处理代码。

为了依靠流量分析进行付费计测，请安装下面的sendEvent方法。

```objective-c
+ (void)sendEvent:(NSString*)eventName action:(NSString*)action label:(NSString*)label orderID:(NSString*)orderID sku:(NSString*)sku itemName:(NSString*)itemName price:(double)price quantity:(NSUInteger)quantity currency:(NSString*)currency;
```

sendEvent方法的参数说明如下。

|参数|型|最大长度|概要|
|:------|:------:|:------:|:------|
|eventName|NSString*|255|设定能够识別监测Event的任意名称。可以自由设定。|
|action|NSString*|255|设定属于Event的Action名。可以自由设定。不做特別指定的场合可以为nil。|
|label|NSString*|255|属于Action的Label名。可以自由设定。不做特別指定的场合可以为nil。|
|orderId|NSString|255|指定订单号。不做特別指定的场合可以为nil。|
|sku|String|255|指定商品代号sku。不做特別指定的场合可以为nil。|
|itemName|String|255|指定商品名。不指定的场合请设定空文字串@""|
|price|double||指定商品单价。|
|quantity|NSUInteger||指定数量。按price * quantity的销售金额来计算在内。|
|currency|String||指定货币代码。nil的场合默认指定为"JPY"。|

> currency请用[ISO 4217](http://ja.wikipedia.org/wiki/ISO_4217)定义的货币代码来指定。

下面是一个按日币300日圆付费的安装实例。

```objective-c
#import "Ltv.h"

// LTV计测形式的付费计测
AppAdForceLtv *ltv = [[[AppAdForceLtv alloc] init] autorelease];
[ltv addParameter:LTV_PARAM_PRICE:@"300"];
[ltv addParameter:LTV_PARAM_CURRENCY:@"JPY"];
[ltv sendLtv:成果地点ID];

// 流量分析形式的付费计测
[ForceAnalyticsManager sendEvent:@"purchase" action:nil label:nil orderID:nil sku:nil itemName:@"Item A" price:300 quantity:1 currency:@"JPY"];
```

---
[TOP](/lang/zh-tw/README.md)

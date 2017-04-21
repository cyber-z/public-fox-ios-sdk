## 依靠流量分析进行Event计测

能够计测按不同广告流入和自然流入的用户在APP里面引发的Event。请在想要做Event计测的全部地点追加代码。

为了进行依据流量分析的Event计测，请安装下面的sendEvent方法。

```objective-c
+ (void)sendEvent:(NSString*)eventName action:(NSString*)action label:(NSString*)label value:(NSUInteger)value;
```

sendEvent方法的参数说明如下。

|参数|型|最大长度|概要|
|:------|:------:|:------:|:------|
|eventName|NSString*|255|设定能够识別计测Event的任意名称。|
|action|NSString*|255|设定属于Event的Action名。可以自由设定。可以为nil。|
|label|NSString*|255|设定属于Event的Label名。可以自由设定。可以为nil。|
|value|NSUInteger|255|指定Event次数。可以为1。|



```objective-c
#import "AnalyticsManager.h"

//- (void) didTutorial {
    // Event的发送
    [ForceAnalyticsManager sendEvent:@“教程突破" action:nil label:nil value:1];
//}
```

---
[TOPへ](/lang/zh-tw/README.md)

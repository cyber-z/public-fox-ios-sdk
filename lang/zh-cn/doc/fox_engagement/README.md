# F.O.X Engagement广告投放

## 1. 概要
本章对基於Force Operation X SDK(下面略称F.O.X)的F.O.X Engagement广告投放以及和Criteo协作时的必要安装做说明。
在进行F.O.X Engagement广告投放时，需要在相同地点安装LTV和流量分析各自的计测处理。

* **对应F.O.X iOS SDK版本** : `v2.16g`及以上

### 1.1.	SDK式样

透过利用F.O.X SDK流量分析机能，进行横跨媒体的协作事件计测。计测可以根据不同内容来执行各种方法。

#### 事件资讯的送信

引入头文件AnalyticsManager.h。
```objective-c
 #import "AnalyticsManager.h"
```

利用下面的sendEvent方法，发送事件资讯。
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

### sendEvent方法参数

各参数的式样如下。

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|eventName|String|针对做计测的事件种別来设定指定的Event名称。|
|<span style="color:grey">action|<span style="color:grey">String|<span style="color:grey">不使用。|
|<span style="color:grey">label	|<span style="color:grey">String|<span style="color:grey">不使用。|
|orderId|String|(任意)指定订单号。|
|sku	|String|(任意)指定商品代号sku。|
|<span style="color:grey">itemName|<span style="color:grey">String|<span style="color:grey">不使用。|
|<span style="color:grey">value	|<span style="color:grey">int|<span style="color:grey">不使用。|
|price|double|	指定商品单价。|
|quantity|int|	指定数量。<br>按price * quantity来计算销售额。|
|currency|String|指定货币代码。null的场合默认指定为"JPY"。|
|eventInfo|JSONObject|按下面式样的说明来指定Json。|

### 1.2. eventInfo式样
在eventInfo里，通过Json形式设定Action附带的资讯这种方式，能够进行动态广告协作投放。Json式样如下。

| 参数 | 型 | 概要 |
|:----------|:-----------:|:------------|
|product|Array|阅览过的放入购物车的商品的设定领域。|
|  product[].id|String|指定阅览过的放入购物车的商品ID。|
|  product[].price|double|指定阅览过的放入购物车的商品单价。|
|  product[].quantity|int|指定阅览过的放入购物车的商品数量。|
|  product[].category|String|指定阅览过的放入购物车的商品种別。<br>若想设定多个请用「,」来区分、分层次请用「>」来分割。<br>例）电影，录像>DVD>体育，休闲|
|din|String|若想指定开始日请设定。|
|dout|String|若想指定结束日请设定。|
|criteo_partner_id|String|Criteo帐号ID在同一个APP里不一样的时候请设定。|
|fox_cvpoint|Long|输入F.O.X的成果地点ID。|
|datafeed|JSONObject|实时数据字段(参考下方)|

### 1.3. 实时数据字段更新式样
在eventInfo里，通过Json形式设定数据字段的更新情报的方式，根据F.O.X Engagement广告投放协作能够实时更新数据字段。

#### JSON 布局详细

对于更新数据字段状态的Action，请按下面Json式样来安装。

| 参数 |必须|型 | 概要 |
|:----------|:-------:|:----:|:------------|
|version|必须|String|指定数据字段的版本。|
|product|必须|Array|商品主表的数据字段的设定领域。|
|  product[].id|必须|String|能够专门识別数据字段的商品的ID。|
|  product[].action|必须|String|输入对数据字段的操作。<br>U:添加或编辑　D:删除|
|  product[].name|必须|String|商品名。<br>删除时可以设定为null。|
|  product[].expire|任意|String|商品的有效期限。<br>请按照「yyyy-MM-dd HH:mm:ss」或者「yyyy-MM-dd」的格式来输入日期。|
|  product[].effective|任意|String|商品的公开日期和时间。<br>如果此项被设定，到公开日期和时间为止，商品不会被显示出来。<br>请按照「yyyy-MM-dd HH:mm:ss」或「yyyy-MM-dd」的格式来输入日期。|
|  product[].img|任意|String|商品的图像URL。|
|  product[].category1|任意|String|指定第一层次的种別。|
|  product[].category2|任意|String|指定第二层次的种別。|
|  product[].category3|任意|String|指定第三层次的种別。|
|  product[].price|任意|Double|指定商品价格。|
|  product[].currency|任意|String|指定商品的货币代码。<br>null的场合默认指定为"JPY"。|
|  product[].(任意)|任意|String|指定其他投放或分析使用的项目。<br>请指定数据字段的项目。|

　　　
## 2.事件计测的安装
　F.O.X SDK对应的F.O.X Engagement的事件计测和Criteo的事件计测分为以下5种。<br>安装的详细请确认下面的详细页面。

* [> View Toppage事件](./ViewToppageEvent.md)
* [> View Listing事件](./ViewListingEvent.md)
* [> View Product事件](./ViewProductEvent.md)
* [> View Basket事件](./ViewBasketEvent.md)
* [> Track Transaction事件](./ViewTransactionEvent.md)


---
[TOP](/lang/zh-tw/README.md)

## sendLtv的详细

通过在会员登录，新手教程突破，付费等任意的成果地点安装LTV计测处理，能够测定不同广告流入的LTV成果。

请按照如下格式安装LTV计测的代码。

```objc
#import "Ltv.h"
// ...
AppAdForceLtv *ltv = [[[AppAdForceLtv alloc] init]];
[ltv sendLtv:{成果地点ID}];
```

> **成果地点ID**(必须) : 请输入Force Operation X管理员告知的值。

#### 指定广告主终端ID(buid)

在APP内部的成果里可以包含广告主终端ID（USER ID等），能够进行以此为基準的成果计测。
请按如下代码来给LTV成果设置广告主终端ID。

```objc
#import "Ltv.h"
// ...
AppAdForceLtv *ltv = [[[AppAdForceLtv alloc] init]];
[ltv sendLtv:{成果地点ID}:{广告主终端ID}];
```

> **広告主端末ID**(任意) : 是指贵公司管理的唯一识別ID(USER ID等)。可以指定64文字以内的半角英文数字。

---
[Top](/lang/zh-tw/README.md)

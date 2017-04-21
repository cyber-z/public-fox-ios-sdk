## (任意)Opt-Out的安装

有些广告公司会允许用户选择不接受瞄準投放的广告。在APP启动时，用户若在显示隐私条例和使用规范的视窗中选择不参加的选项，接收到效果测量通知的同时，F.O.X会把此用户选择不参加的资讯，发送给广告公司。

若要对应Opt-Out，请在如同以下「Install计测安装」导入sendConversionWithStartPage之前设定。

```objective-c
if(user.optout) {
	[[AppAdForceManager sharedManager] setOptout:YES];
}

[[AppAdForceManager sharedManager] sendConversionWithStartPage:@"default"];
```
---
[TOP](/lang/zh-tw/README.md)

## Reengagement计测时的疏通测试

在上架申请以前，请在导入SDK后的状态做充分的测试，以确保APP的动作没有问题。

因为在启动后只发生一次Install计测的通信，如果想要再次进行Install计测的话，请卸载APP再次安装

**测试步骤**

1. 如果测试用的设备已安装APP，请先卸载掉APP<br />
1. 清除测试移动终端默认浏览器Safari的Cookie，请按「设定」→「Safari」→「Cookie和数据消除」删除Cookie<br />
1. 复制鄙司发行的【安装用测试URL】，粘贴到默认浏览器（标準浏览器）的URL栏里进行访问。<br />
＊请在管理画面（SDK导入→平台的选择→SDK导入文档→测试URL→安装用测试URL）里取得【安装用测试URL】。<br />
＊请一定在OS设定的默认浏览器里粘贴测试URL来发出请求。邮件APP或QR码读取APP等这些APP内部会用WebView发生的画面跳转是无法计测的。<br />
1. 画面移转到Market<br />
＊使用测试URL，可能会因为没有设定跳转目的地（没有在APP详细里设定「商城URL」）而弹出错误对话框，这个不影响测试。<br />
1. 在测试终端上安装测试APP<br />
1. 启动APP（F.O.X设定和不同测试终端会影响APP启动后的举动，请参考下面的说明）<br />
＊如果没有勾选cookie计测手法，Safari浏览器将不会弹跳出来。<br />
＊如果勾选了cookie计测手法，并且使用iOS9以下的测试终端，浏览器将自动弹跳出来<br />
＊如果勾选了cookie计测手法，并且使用iOS9及以上的测试终端，会启动SFSafariViewController。但是如果设定了`setStartPageVisible:NO`的话，SFSafariViewController和Safari都不会启动。<br />
＊如果没有出现上述的举动，说明没有正常设定。请重新设定，若仍无法发现问题，请与弊司联系。<br />
1. 把画面移转到LTV计测地点<br />
＊如果登录了LTV地点执行此步骤<br />
1. 结束并从后台关闭APP<br />
1. 删除默认浏览器的Cookie、点击【Reengage用测试URL】。请确认APP是否启动。<br />
＊请在管理画面（SDK导入→平台的选择→SDK导入文档→测试URL→安装用测试URL）里取得【Reengage用测试URL】。<br />
＊如果APP没有启动，请确认是否设定了定制的URL Scheme。请重新设定，若仍无法发现问题，请与弊司联系。<br />
1. 把画面移转到LTV地点（至少1个）<br />
1. 不显示APP、让其运行在后台。<br />
1. 再次删除默认浏览器的Cookie、点击【Reengage用测试URL】。请确认APP是否启动。<br />
＊如果APP没有启动，请确认是否设定了定制的URL Scheme。请重新设定，若仍无法发现问题，请与弊司联系。<br />
1. 把画面移转到LTV地点（至少1个）<br />
1. 结束并从后台关闭APP<br />
1. 再次启动APP<br />

请告诉鄙司3，6，7，9，10，12，13的时间。在鄙司这边会确认是否正常被计测。确认没有问题的话，测试算正式完成。


> 请注意在步骤3使用的测试URL和步骤9、12使用的Reengagement计测测试用URL是不一样的。

---
[TOP](/lang/zh-tw/README.md)

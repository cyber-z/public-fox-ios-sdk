# 有关利用Tag的LTV计测

在WEB页面上进行会员登录或商品购入的场合，可以利用img Tag进行LTV计测。

F.O.X的LTV计测适用于外部浏览器和APP内WebView。外部浏览器利用ltvOpenBrowser:而APP内WebView利用setLtvCookie来把LTV计测需要的信息记录到浏览器的Cookie里。

## 使用外部浏览器的LTV计测

从APP启动外部浏览器，使用外部浏览器表示WEB页面进行Tag计测的场合，请利用ltvOpenBrowser:方法来启动外部浏览器。用字符串形式设定外部浏览器使用的URL给参数。

```objective-c
#import "Ltv.h"
// ...
AppAdForceLtv *ltv = [[[AppAdForceLtv alloc] init] autorelease];
[ltv ltvOpenBrowser:@"http://yourhost.com/"];
```

## 使用APP内WebView的LTV计测

如果画面迁移在APP内WebView里进行，可以利用setLtvCookie。请在生成WebView的地方安装下面的代码。多次生成和废弃WebView的场合，请在生成之际执行setLtvCookie。在内部利用NSHTTPCookieStorage来设定Cookie。

```objective-c
#import "Ltv.h"
// ...
AppAdForceLtv *ltv = [[[AppAdForceLtv alloc] init] autorelease];
[ltv setLtvCookie];
```

## Tag的安装

请在LTV成果地点页面里安装F.O.X管理员提供的计测Tag。

Tag的参数式样如下。

<table>
<tr>
  <th>参数名</th>
  <th>必须?</th>
  <th>备考</th>
</tr>
<tr>
  <td>_buyer</td>
  <td>必须</td>
  <td>识別广告主的ID。<br />请输入管理员提供的值。</td>
</tr>
<tr>
  <td>_cvpoint</td>
  <td>必须</td>
  <td>识別成果地点的ID。<br />请输入管理员提供的值。</td>
</tr>
<tr>
  <td>_price</td>
  <td>任意</td>
  <td>付费额。付费计测时请设定。<br /></td>
</tr>
<tr>
  <td>_currency</td>
  <td>任意</td>
  <td>半角字母数字3位长度的货币代码。<br />付费计测时请设定。<br />如果未设定、_price默认设定为JPY(日圆)。</td>
</tr>
<tr>
  <td>_buid</td>
  <td>任意</td>
  <td>半角字母数字最大64位长度。<br />像会员ID这样为每个用户保持唯一值的时候请使用。</td>
</tr>
</table>

在_currency里用[ISO 4217](http://ja.wikipedia.org/wiki/ISO_4217)定义的货币代码来指定。

---
[TOP](/lang/zh-tw/README.md)

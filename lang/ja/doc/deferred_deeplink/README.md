## ディファードディープリンクの実装

ディファードディープリンクを実装することで、広告をクリックした際に紐付いているディープリンクにリダイレクトしアプリ内の対象のページに遷移することが可能となります。また、アプリが未インストールの場合でも、インストール後に広告のリダイレクト先となるディープリンクに遷移させることが可能となります。

> サポートバージョン：3.5.0以上

### API詳細
ディファードディープリンクの実装は、初回起動時のsendConversionWithStartPage実行する前に以下のメソッドを使用します。

|メソッド名|説明|
|:---|:---|
|setDefaultDeferredDeeplinkHandler|ラストクリックの有効期間が1日、ディープリンクを受け取った際にディープリンク先に自動遷移します。|
|setDeferredDeeplinkValidDuration:(NSTimeInterval)durationSinceClick<br/>andHandler:^(NSString url)handler|`durationSinceClick` : ラストクリックの有効期間を秒数で指定します。<br/>`handler` : DeeplinkをNSStringとして処理するコールバックに渡します。Deferred Deeplinkを取得に失敗する時urlはnilです。

### 実装例
**1. デフォルト処理**

ディープリンクを取得し、ディープリンク先への遷移をSDKが行う例となっています。
```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // ...
    [[AppAdForceManager sharedManager] setDefaultDeferredDeeplinkHandler];
    [[AppAdForceManager sharedManager] sendConversionWithStartPage:@"default"];
    // ...
}

-(BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {
    [[AppAdForceManager sharedManager]setUrlScheme:url];
    return YES;
}
```

> ※ 遷移するタイミングはディープリンク取得直後となっており、コントロールすることはできません。<br>
また、ディープリンクを取得出来なかった場合や、遷移が不可能な無効なディープリンクの場合には反応しません。

> ※ ディープリンクに記号や特殊な文字を含む場合には、画面遷移の処理を本SDKに委譲せず`setDeferredDeeplinkValidDuration:andHandler:`を用いて実装されることを推奨します。

**2. カスタマイズ処理**

1日以内のラストクリックを有効とし、ディープリンクを取得する例となっています。
```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // ...
    [[AppAdForceManager sharedManager] setDeferredDeeplinkValidDuration:60*60*24 andHandler:^(NSString* url) {
        NSLog(@"received deep link %@", url);
        if (url) {
            [[UIApplication sharedApplication] openURL:[NSURL URLWithString:url]];
        }
    }];
    [[AppAdForceManager sharedManager] sendConversionWithStartPage:@"default"];
    // ...
}

-(BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {
    [[AppAdForceManager sharedManager]setUrlScheme:url];
    return YES;
}
```

---
[トップ](/lang/ja/README.md)

# CallKi简介

CallKit 是iOS10 推出的新框架。Callkit 包含两个方面的功能

* 来电识别，号码黑名单。

* 与原生页面的整合


Callkit 可以通过 call Directory Extension 实现对来电的识别与过滤。
Callkit 可以将你的Voip 通话级别上升到系统通话级别，可以实现后台接听，通讯录呼叫。
            配合 VoipPush 应用可以做到与原声电话一样的通话体验。

## 使用原生页面

### 呈现来电页面

创建Provider

```ruby
    - (void)initialProvider {

    CXProviderConfiguration *config = [self initialConfigration];

    self.provider = [[CXProvider alloc] initWithConfiguration:config];

    [self.provider setDelegate:self queue:dispatch_get_main_queue()];

    }

    - (CXProviderConfiguration *)initialConfigration {

    CXProviderConfiguration *config = [[CXProviderConfiguration alloc]    initWithLocalizedName:self.appName];

    config.supportsVideo = YES;

    config.maximumCallsPerCallGroup = 1;

    config.supportedHandleTypes = [[NSSet alloc] initWithObjects:@(CXHandleTypePhoneNumber), nil];

    return config;

}

```

创建 update

```
CXCallUpdate \*callupdtae = \[\[CXCallUpdate alloc\] init\];

callupdtae.remoteHandle = \[\[CXHandle alloc\] initWithType:CXHandleTypeGeneric value:self.handId\];

callupdtae.hasVideo = YES;

callupdtae.localizedCallerName = @"显示的名字";
```

调用这个方法呈现来电的页面

    [self.provider reportNewIncomingCallWithUUID:[NSUUID UUID] update:callupdtae completion:^(NSError * _Nullable error) {`

     }];

做完这些后 用户在原生界面的操作都将在provider 的回调中 由系统回调到我们的应用。根据回调进行相关的逻辑操作。

### 主动呼叫

```
    [self.provider reportOutgoingCallWithUUID:[NSUUID UUID] connectedAtDate:[NSDate dateWithTimeIntervalSinceNow:0.2]] 
```

主动呼叫是没有界面出现的，只是通知系统你进行了呼叫

通知体统你开始了呼叫

     CXStartCallAction *startaction = [[CXStartCallAction alloc] initWithCallUUID:self.currentCall.UUID handle:[[CXHandle alloc] initWithType:CXHandleTypeGeneric value:showName]];`

     CXTransaction *transaction = [[CXTransaction alloc] init];`

     [transaction addAction:startaction];`

     CXCallController *controller = [[CXCallController alloc]init];`

     [controller requestTransaction:transaction completion:^(NSError * _Nullable error) {`

     }];

在开始的回调中，或则合适的时机，向系统传递远端的信息

        CXCallUpdate *callupdtae = [[CXCallUpdate alloc] init];`

        callupdtae.remoteHandle = [[CXHandle alloc] initWithType:CXHandleTypeGeneric value:self.handId];`

        callupdtae.hasVideo = YES;`

        callupdtae.localizedCallerName = @"显示的名字";`

         [provider reportCallWithUUID:self.currentCall.UUID updated:callUpdate];`

### 挂断

        CXEndCallAction *action = [[CXEndCallAction alloc] initWithCallUUID:self.currentCall.UUID];`

         CXTransaction *transAction = [[CXTransaction alloc] init];`

         [transAction addAction:action];`

         [self.callController requestTransaction:transAction completion:^(NSError * _Nullable error) {`

     }];

### 通讯录点击事件

    - (BOOL)application:(UIApplication *)application continueUserActivity:(nonnull NSUserActivity *)userActivity restorationHandler:(nonnull void (^)(NSArray * _Nullable))restorationHandler {`

     dealUserActivity(userActivity);`

     return YES;`

    } static void dealUserActivity(NSUserActivity *userActivity ){ `

     if (!userActivity) {`

     return;`

     }



     NSInteger activityType = 0;

     if ([userActivity.activityType isEqualToString:@"INStartAudioCallIntent"] ) {
     activityType = 1;

     }else if ([userActivity.activityType isEqualToString:@"INStartVideoCallIntent"]) {

     activityType = 2;

     }

     if (activityType !=0) {

      }

    }

## 总结：

CallKit 所完成的内容其实是两个app 之间的通讯与交互。


```
CXProvider 

```



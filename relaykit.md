ReplayKit 使用

简介

ReplayKit 是用于应用直播的一个库，与callkit 一样是一个进程间通讯的库。他提供两个功能：

1.录制屏幕-将屏幕录制。录制成功后提供一个预览controller

2.广播屏幕-将屏幕流投射到一个支持 boradCast 的extension。 可以选择流。或者mp4 文件的方式。

录屏

开始录制

`[[RPScreenRecorder sharedRecorder] startRecordingWithHandler:^(NSError * _Nullable error) {`

`}];`

停止录制

`[[RPScreenRecorder sharedRecorder] stopRecordingWithHandler:^(RPPreviewViewController * _Nullable previewViewController, NSError * _Nullable error) {`

`[self presentViewController:previewViewController animated:YES completion:^{`

`}];`

`previewViewController.previewControllerDelegate = self;`

`}];`

这里的 `RPPreviewViewController 是结束后产生的预览视图。需要对这个预览视图的事件进行处理。`

广播

弹出广播选择视图

`[RPBroadcastActivityViewController loadBroadcastActivityViewControllerWithHandler:^(RPBroadcastActivityViewController * _Nullable broadcastActivityViewController, NSError * _Nullable error) {`

`broadcastActivityViewController.delegate = self;`

`[self presentViewController:broadcastActivityViewController animated:YES completion:nil];`

`}];`

![](/assets/IMG_0912.PNG)



选择了了这个extention 后biiardcastUI 的controller 会被初始化。并在回调中返回。boardcastUI 在这个controller 里面进行用户授权等工作。等确认授权后 可以调用  \[self userDidFinishSetup\];  完成操作。返回回调到应用中。

`didFinishWithBroadcastController:(RPBroadcastController *)broadcastController error:(NSError *)error {`

` broadcastController.delegate = self;`

` [broadcastActivityViewController dismissViewControllerAnimated:YES completion:nil];`

` [broadcastController startBroadcastWithHandler:^(NSError * _Nullable error) {`

` }];`

`}`



这时候就可以 开始广播。不需要调用  \[`[RPScreenRecorder sharedRecorder] startRecordingWithHandler`\]; 



这时 boardCast 就会收到屏幕的数据了


























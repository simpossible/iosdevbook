ReplayKit 使用



简介

ReplayKit 是用于应用直播的一个库，与callkit 一样是一个进程间通讯的库。他提供两个功能：

1.录制屏幕-将屏幕录制。录制成功后提供一个预览controller

2.广播屏幕-将屏幕流投射到一个支持 boradCast 的extension。 可以选择流。或者mp4 文件的方式。



录屏

开始录制

` [[RPScreenRecorder sharedRecorder] startRecordingWithHandler:^(NSError * _Nullable error) {`

` }];`



停止录制

` [[RPScreenRecorder sharedRecorder] stopRecordingWithHandler:^(RPPreviewViewController * _Nullable previewViewController, NSError * _Nullable error) {`

` [self presentViewController:previewViewController animated:YES completion:^{`

` }];`

` previewViewController.previewControllerDelegate = self;`

` }];`



这里的 `RPPreviewViewController 是结束后产生的预览视图。需要对这个预览视图的事件进行处理。`


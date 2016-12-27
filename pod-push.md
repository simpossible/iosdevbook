# CocoaPods 升级为 1.0 问题

## 1.repo push

repo push 在xcode 8不能使用。xcode8 不支持 iphone 4s模拟器，在将 xcode -&gt; window -&gt; devices 中的 iphone 5s 改名为

iphone 4s 后 会出现新问题 （ Unable to create a source with URL http:\/\/git.sdp.nd\/cocoapods\/spec.git ）

故切换为

`sudo xcode-select -switch /Applications/Xcode7.app/`

然后push 的时候遇到新问题

`Terminating app due to uncaught exception 'NSInternalInconsistencyException', reason: 'The loaded com.apple.CoreSimulator.CoreSimulatorService job does not match our expectations: versionOfLoadedJob: 303.8, our version: 209.19'`

根据说明发觉是工作路径不对

所以 切换工作路径

`export DEVELOPER_DIR=/Applications/Xcode7.app/Contents/Developer`

然后push 成功

pod push 指令

`pod repo push sdp_repo ECISDK.podspec --use-libraries --allow-warnings --no-private --verbose`


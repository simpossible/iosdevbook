# 编译错误

## 1.swift 使用OC的 库会造成问题

`include of non-modular header inside framework module`

问题原因:  
swift 的调用需要moudle 定义。将 buildsetting 里的 DEFINES\_MODULE 设置为YES。就会额外编译一个  
module.modulemap 的文件。有了这个文件swift 才能正常编译。  
这个文件的内容可以看到如下:

```
framework module ProtocolBuffers {
  umbrella header "ProtocolBuffers.h"

  export *
  module * { export * }
}
```

这里我的库为 ProtocolBuffers.h 所以 你需要在framework 的目录下新建一个 module.modulemap 的文件。并更改framework 的目录为以下样子:

![](/assets/framwork_moudle_map.png)




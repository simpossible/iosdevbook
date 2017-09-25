# Universal-Link

## 简介

Universal-link 是应用唤起的一种方式，统一了http请求，与应用请求。

## 应用唤起方式整理

* ### Url-types

![](/assets/import.png)

app 注册一个urltype 用于在web唤醒自己app。

限制: 不能识别是否已经安装了app，但是已经了很多的解决方案，这里有一种从网上找到的方案

![](/assets/web-app.png)

* ### Banner

  safari 提供了一种方式，方便前端在网页顶端嵌入一个bannner 可以识别是否安装app，并自动管理app 的打开或者下载。  
  官网链接：  
  [https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html)

* ### universal-link

  为了解决url-type 带来的一些弊端，将http 请求与唤起app 请求进行了统一。  
  官网链接： [https://developer.apple.com/library/content/documentation/General/Conceptual/AppSearch/UniversalLinks.html\#//apple\_ref/doc/uid/TP40016308-CH12-SW2](https://developer.apple.com/library/content/documentation/General/Conceptual/AppSearch/UniversalLinks.html#//apple_ref/doc/uid/TP40016308-CH12-SW2)

* ### 通讯录跳转

  call-kit的特性，允许app 使用系统的通讯并在通讯录中留下记录。点击这些记录将会唤醒app

## 配置

* 已有域名：mydomain.com

* 配置 Xcode

![](/assets/universallink-xcode-config.png)

* 制作 json 文件

```
/**没有文件后缀*/
touch touch apple-app-site-association
```

* 拷贝 json

  ```
  /**appid 为 TeamId(可以在membercenter 中看到).bundleId*/
  {
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "9JA89QQLNQ.com.apple.wwdc",
                "paths": [ "/wwdc/news/", "/videos/wwdc/2015/*"]
            },
            {
                "appID": "ABCD1234.com.apple.wwdc",
                "paths": [ "*" ]
            }
        ]
    }
  }
  ```

* 上传到服务端根目录 或者 .well-known 目录下

## 特性

* 跨域问题
  9.2 版本后就只能跨域才能触发universallink。
* 测试跨域问题我做了以下的测试得出以下结论。

![](/assets/universallink-cross-domain.png)

## 适配性（应用跳转解决方案设计者需注意）

Universal-Link 是可以进行通用跳转，目前测试 QQ，微信， safari，chrome 可以进行跳转。  
需要注意的事项：

* universal link 不能使用 JS 进行唤起。  
  最好使用a标签，或者其他静态方式  
  `<a src="https:mydomain/?pa=xxx">link</a>`

* qq，微信中 universal-link 的连接参数如果是使用js 进行拼接的话。这个链接是无效的。  
  safari 中可以。

* 部分第三方浏览器是无效的，目前测试的有 UC，QQ浏览器 无效。chrome 有效（表现与qq内置一致）

* 针对浏览器是否支持跳转应用做了以下统计

  ```
     ![](/assets/webbrosersupport.png)  
  ```

* 以下是一些总结性的博客:

[http://www.gexiao.me/2016/03/10/iOS9-universal-links/](http://www.gexiao.me/2016/03/10/iOS9-universal-links/)

[http://www.gexiao.me/2016/03/10/iOS9-universal-links/](http://www.gexiao.me/2016/03/10/iOS9-universal-links/)

[http://www.bijishequ.com/detail/521297?p=](http://www.bijishequ.com/detail/521297?p=)


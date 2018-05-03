# KeyChain 简介

keychain 可以用来存储 app间共享的一些密码，或者key值，证书，或文本。

keychain 的本质是一个关系数据库。每一个item 都是一个元组。

keychain 的元组有5种类型：

* kSecClassGenericPassword  通用密码的存储这是最常用的一种

* kSecClassInternetPassword

* kSecClassCertificate

* kSecClassKey

* kSecClassIdentity

每一种类型支持的字段是不一样的。需要作出分别。

## KeyChian 共享方式

我们这里不讨论macOS，在 iOS 中只有一个KeyChain。KeyChain 会通过两种方式来控制访问权限：

* ACL\(访问控制列表\),一个App 访问的时候如果在这个元组的访问控制列表中那么拥有这个的元组的权限。

* AccessGroup,Xcode 在开启Keychain Share 的时候又一个 access group。很多开始用的人会因为对这个组的理解不正确

  导致一些无法共享的情况，每个元组有一个所属的AccessGroup，当一个应用在读取这个元组的时候，KeyChian 会将这个

  AccessGroup 与当前应用的所有 AccessGroup 比较。如果当前的 group 列表中包含了它所属的AccessGroup 那么就拥有

  访问权限。每个元组的所属AccessGroup 是当前应用的group列表的第一个值。当存储成功后能获取到。

## 通用密码存储

通用密码的存储方法如下

accessgroup\(自动生成\) + account + service\(可为空\) ---&gt; valueData

在这中模式下还拥有其他的key值

* CreationDate

* ModifyDate

* DesCription

* Commont

* Creator

* Type

* Label

* Invisible

* IsNegative

* Account

* Generic

* Synchoronizable

这些值在创建后不能修改。只有valuedata 能通过 secUpdate 的函数进行修改。

用 IBLKeyChain 的库，使用方式为：

```
IBLKeyChainGPItem *gpItem = [[IBLKeyChainGPItem alloc] init];

gpItem.itemAccount = @“user”;
gpItem.itemValueData = [@"password" dataUsingEncoding:NSUTF8StringEncoding];
gpItem.itemService = @"ftp";
gpItem.itemLabel = @"hehe";
gpItem.itemGeneric = @"generic"
gpItem.itemType = @"type";
gpItem.itemComment = @"comm";
gpItem.itemDescription = @"des";

OSStatus a = [[IBLKeyChainAccessor defaultAccessor] storeItem:gpItem];
```




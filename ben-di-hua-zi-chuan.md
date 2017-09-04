# 本地化字串

* 创建

  创建比较简单，只需要在xcode中像增加普通文件一样增加.string 类型的文件。
  在xcode 的右边栏中会有一个 localize file 的按钮。点击即可创建不同的语言
* 增加key-value
  
  只需要在文件中增加如下的字段 
  
  `"test"="测试字段";`
  
  或者
  ```
  /**这个是带有注释的情况*/
  "test"="测试字段";
  ```
  注意要添加分号结束;
  
* 使用

  我们可以给不同bundle 不同的额字串文件都定义一个宏可以方便使用
  ```
  /**key为string 文件中的每一个key*/
  #define IBLLocalizedString(key) \
  [[NSBundle mainBundle] localizedStringForKey:(key) value:@"" table:nil]
  
  /**这里的tbl 就是字串文件的名字。EXP：test.string tbl=test*/
  #define IBLTLocalizedString(key,tbl)\
   [[NSBundle mainBundle] localizedStringForKey:(key) value:@"" table:(tbl)]
   
   NSString *word = IBLTLocalizedString(@"test");
   //在 my.strings 中查找文件
   NSString *myWord = IBLTLocalizedString(@"test",@"my");
  ```
 




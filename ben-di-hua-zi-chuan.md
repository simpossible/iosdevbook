# 本地化字串

* 创建
* 使用

  我们可以给不同bundle 不同的额字串文件都定义一个宏可以方便使用
  ```
  #define IBLLocalizedString(key) [[NSBundle mainBundle] localizedStringForKey:(key) value:@"" table:nil]
  /**这里的tbl 就是字串文件的名字。EXP：test.string tbl=test*/
  #define IBLTLocalizedString(key,tbl) [[NSBundle mainBundle] localizedStringForKey:(key) value:@"" table:(tbl)]
  ```
 




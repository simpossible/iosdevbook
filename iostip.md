# Tips\(开发中的一些小代码\)

## 手势禁用

`if ([self.navigationController respondsToSelector:@selector(interactivePopGestureRecognizer)]) {`

`self.navigationController.interactivePopGestureRecognizer.enabled = NO;`

`}`


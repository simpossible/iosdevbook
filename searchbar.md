# UISearchBar - UISearchController

简介

遇到问题合集

searchcontroller 中的searchbar 点击后 bar的位置盖住了statuar。

本来y应该是20。高度为56。现在的高度变为了 50。y变为了0

![](/assets/IMG_1691.PNG)

可以发现这是由于view的布局直接布局到了屏幕的顶端的问题

解决方案  
`self.edgesForExtendedLayout = UIRectEdgeNone;`

添加 这个后bar的高度以及位置都正常了

![](/assets/IMG_1692.PNG)








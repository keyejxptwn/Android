# MVC MVP MVVM简介

----------

#1.MVC
 1. 视图（View）：用户界面。
 2. 控制器（Controller）：业务逻辑
 3. 模型（Model）：数据保存
 ![此处输入图片的描述][1]


View 传送指令到 Controller
Controller 完成业务逻辑后，要求 Model 改变状态
Model 将新的数据发送到 View，用户得到反馈
***所有通信都是单向的。***

----------
#2.MVP
1. 各部分之间的通信，都是双向的。
2. View 与 Model 不发生联系，都通过 Presenter 传递。
3. View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而 Presenter非常厚，所有逻辑都部署在那里。

![此处输入图片的描述][2]

----------
#3.MVVM
MVVM 模式将 Presenter 改名为 ViewModel，基本上与 MVP 模式完全一致。

![此处输入图片的描述][3]

唯一的区别是，它采用*双向绑定（data-binding）*：View的变动，自动反映在 ViewModel，反之亦然。Angular 和 Ember 都采用这种模式。

  [1]: http://image.beekka.com/blog/2015/bg2015020105.png
  [2]: http://image.beekka.com/blog/2015/bg2015020109.png
  [3]: http://image.beekka.com/blog/2015/bg2015020110.png

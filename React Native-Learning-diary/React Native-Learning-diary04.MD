# react-native第四天     
### 导航 && navigators ###    

|Navigation|ability|
| --- | --- |
|StackNavigator|一次至渲染一个页面，并提供页面之间跳转方法。当打开一个新页面时，它被放置在堆栈顶部|
|TabNavigator|渲染一个选项卡，让用户可以在几个页面之间切换|
|DrawerNavigator|提供一个从屏幕左侧划入的抽屉|

### 概念 ###  
1. 导航渲染的仅仅是 React 组件对应的页面    

|||
|-|-|
|Screen navigation prop| 允许调用导航操作，列入打开另一个页面|
|Screen navigationOptions|定制导航器显示如何显示(标题栏标题，选项卡标签)|
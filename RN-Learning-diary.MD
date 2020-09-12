### react-native第一天
1. 第一个demo首先搭配环境
   1. 环境搭配的时候走了很多弯路，相信网上的教程，网上教程多少有些久远，导致一直搭建不成功
   2. 最后公司负责人告诉我相信官网，我也没办法了，跟着官网一步一步的，结果很容易就成功了
ps: 此处为我总结
2. window 官网明确有node python2(此处必须2.几的) JDK Android-Studio
   1. 官网说不能用cnpm但是我在家的时候用的就是cnpm也是没有问题的
   2. python2 的安装直接傻瓜式就行了，注意在 Customize Python这个页面的时候吧最后一项勾选为第一个will be installed on local hard drive这个，也就是第一项，这个意思就是给电脑自动配置环境。
   3. JDK安装，首先要根据操作系统下载对应的JDK，JDK下载版本不能太低，
   4. 傻瓜式安装，建议C盘，记下路径，安装完之后，去计算机->属性->高级系统设置->环境变量，新建系统变量"N": JAVA_HOME "V":刚才的路径，以我为例 C:\Program Files\Java\jdk1.8.0_181，在java中有多个文件夹，选择jdk路径，编辑系统变量Path，双击Path即可，新建变量值 %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin（电脑win10），新建系统变量"N": CLASSPATH "V": %JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar 之后在cmd窗口输入java 弹出内容为java相关的一大堆即安装成功。
   5. 安装Android Studio PS:http://www.android-studio.org/
   6. 安装Android Studio的时候每要记住勾选Android-SDK,Android-SDK-Platform, Performance (Intel  HAXM), Android-Virtual-Device,如果安装的时候有些是黑的不能勾选可以先跳过，
安装Android-SDK 这个需要注意官网了，因为RN版本与Android系统版本需要支持才行，有些Android版本RN并不支持。这个推荐看官网PS: https://reactnative.cn/docs/getting-started.html
#### 没错这个环境其实我搭配了三天，每天都熬夜整，PS: 总结官网更新很及时，官网没有的百度出来的需要仔细看看时间，以及博客主的知名度

### react-native 第二天
1. 根据初始化的项目新作个页面，再做个跳转
	都是js结尾的后缀，那就创建个js后缀，复制其他的页面代码，啥都不改
之后去路由 routes文件中 找到index.js，看import导入了什么，下面哪里用到了，复制代码进行路径修改，看看是否能跑起来，之后再回到复制的这个页面，进行一些最简单的修改，之后看跳转页面是那个触发的，找到这个页面看怎么实现的，这边要学习一个新的api (onPress = {this.函数名})
经过学习了解到这个是相当于点击事件，{ }这个括号的意思查文档得知，RN把一切都当作对象。
之后基于已经继承好的REDUX写一个循环渲染，复制的代码只是修改了arr, 开始查阅文档，学习到react的JSX语法，return 后面返回的目前理解是视图dom ,<Text>标签是RN框架封装的标签,如果用到需要额外导入
 1. 在redux文件中 state这个对象里写一个数组
 2. 做这个的时候需要额外引入<Text> react-redux 
```js
    // 循环渲染
    {arr.map(item=>{
	    return (
		    <Text>{ item }</Text>
	    )
    })}
``` 
 3. 使用connect 这个方法
```js
    // 需要额外引入俩个文件
    import { connect } from 'react-redux'
    import { Text } from '@react-native'
class ShopingCart extends Component {
    state = { }
    render() {
        const { arr } = this.props
        return (
            <SafeAreaView> 
                {arr.map(item=>{
	                return (
		            <Text>{ item }</Text>
	                )
                })}
            </SafeAreaView>
        )
    }
}
    export default connect(
            ({ users }) => ({
            listdata: users.listdata,
        }),
            ({ users }) => ({
            listdata: users.listdata，
        }),
    )(ShopingCart);
    // ShopingCart是自己起的组建名 需要与class名字对应 users是redux里面的文件名字 <SafeAreaView>目前理解是一个跟组建，还没实际用到，不做了解
```
 4. 这个API的用法是 接受俩个函数，第一个函数是流入，第二个是流出，RN会检测数据变化自动触发这个方法进行实时更新
#### github提交代码
1. 首先在github创建仓库 傻瓜式填空下一步
2. 下载git，傻瓜式安装 生成SSH key 本人win电脑 在Git Bush Here输入ssh 看看有没有一大堆东西，
没有就输入 ssh-keygen -t rsa 这个就会自动生成，生成的文件位置在本人为例/c/Documents and Settings/username/.ssh 有可能是隐藏文件，自己让他显示很容易不做总结了。 需要做的就是吧id_rsa.pub内容复制到GitHub上 也就是GitHub的 SSH 开头的侧栏中，点进去 会看到一个New SSH key按钮 复制粘贴就行了
3. 在这个项目文件中用Git Bash Here打开，也可以cd进去。不过仍要用Git Bash Here打开
4. 输入命令 git init -> git add . -> git commit -m "comment"(第一次让你登陆) -> git commit -m ""comment"(登陆成功后在输入一次) -> git remote add origin https://自己的仓库地址 -> git push -u origin master 
5. 第二次上传我的操作是: git add . -> git commit -m "comment" -> git remote add origin https://自己的仓库地址 -> git push origin master
#### 第二天学到的东西仍然很少，但他真真的用掉我这么一整天晚上还熬夜搞

### react-native 第三天
 1. 学习了mocker 这个是一个虚拟数据的，类似mock.js
 2. 复制上面已有的接口代码，完成接口配置请求数据，这花费了我俩天的时间才正确的拿到数据，
   server文件
   ```js
    export async function shopinglist(params) {
        return fetch('/api/shop', {
    body: params,
    });
   ```
   mocker文件
   ```js
    'POST /api/shop':(req,res) => {
        return res.status(200).json({
            arr:[
                //...
            ]
        })
    }
   ```
   redux文件 -> users文件
    ```js
        state: {
            arr:[]
        },
        reducers: {
            updata: (state, payload) => ({ ...state, ...payload})
        }
        effects: dispatch => ({
            async getlist(_, { users, global }) {
                const l = await shopinglist(users.listdata);
                await this.update({ listdata: l.listdata });
            }
        })
    ```
    需要渲染的组件文件
      添加一个点击事件 onPress 使用redux的 connect这个API 使用循环渲染将这组合
      思路在组建页面添加一个点击事件等于 users的事件 利用connectAPI特性触发这个方法，让这个方法去请求接口拿到数据并给定redux中需要流入的变量，这里使用到了updata()这个方法。本页面的话用this就可以调用他，参数就是后面的覆盖前面的。这样便可以存到redux里面，connect是自动检测数据变化的，列表自然就渲染了，这个循环渲染DOM的方法，当数组没有元素的时候不会报错因为用的是map，这个东西我是在第四天弄出来的
### 这一周时间学习的东西很少，但是耗费了很久才勉强会用还不知道原理
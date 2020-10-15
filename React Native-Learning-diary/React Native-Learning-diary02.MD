# react-native 第二天   

1. 根据初始化的项目新作个页面，再做个跳转   

   1. 都是js结尾的后缀，那就创建个js后缀，
   2. 复制其他的页面代码，啥都不改，
   3. 之后去路由 routes文件中 找到index.js，看import导入了什么，下面哪里用到了，
   4. 复制代码进行路径修改，看看是否能跑起来，
   5. 之后再回到复制的这个页面，进行一些最简单的修改，
   6. 之后看跳转页面是那个触发的，找到这个页面看怎么实现的，这边要学习一个新的api (onPress = {this.函数名})   
   7. 经过学习了解到这个是相当于点击事件，{ }这个括号的意思查文档得知，RN把一切都当作对象。   
   8. 之后基于已经继承好的REDUX写一个循环渲染，复制的代码只是修改了arr, 开始查阅文档，学习到react的JSX语法，return 后面返回的目前理解是视图dom ,
   9. <Text>标签是RN框架封装的标签,需要额外引入<Text>
   10. 如果用到需要额外导入在redux文件中 state这个对象里写一个数组    

## 代码实现   

1. 做这个的时候需要额外引入<Text> react-redux   

```js
    // 循环渲染
{arr.map(item=>{
    return (
        <Text>{ item }</Text>
    )
})}
```    

2. 使用connect 这个方法        

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

3. 这个API的用法是 接受俩个函数，第一个函数是流入，第二个是流出，RN会检测数据变化自动触发这个方法进行实时更新       
     
## github提交代码     

1. 首先在github创建仓库 傻瓜式填空下一步
2. 下载git，傻瓜式安装 生成SSH key 本人win电脑 在Git Bush Here输入ssh 看看有没有一大堆东西，
没有就输入 ssh-keygen -t rsa 这个就会自动生成，生成的文件位置在本人为例/c/Documents and Settings/username/.ssh 有可能是隐藏文件，自己让他显示很容易不做总结了。 需要做的就是吧id_rsa.pub内容复制到GitHub上 也就是GitHub的 SSH 开头的侧栏中，点进去 会看到一个New SSH key按钮 复制粘贴就行了
3. 在这个项目文件中用Git Bash Here打开，也可以cd进去。不过仍要用Git Bash Here打开
4. 输入命令 git init -> git add . -> git commit -m "comment"(第一次让你登陆) -> git commit -m ""comment"(登陆成功后在输入一次) -> git remote add origin https://自己的仓库地址 -> git push -u origin master 
5. 第二次上传我的操作是: git add . -> git commit -m "comment" -> git remote add origin https://自己的仓库地址 -> git push origin master       

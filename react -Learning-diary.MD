## react 
### &emsp;jsx语法
    在js中写html 是 jsx 。。。
    react里认为首字母应是大写，否者会被认为是html标签
    最终都会被转换为浏览器认识的js
    react使用jsx是为了让结构更加清晰，( UI + M = V )
    jsx中添加js表达式加上大括号保住就可以，如果加上引号会被认为是字符串，且react认为大括号与引号只使用一个
    react认为jsx语法更接近js而不是HTML所以采用小驼峰
    <div className = { expression }></div> && <App className = "box" />
    jsx防注入(XSS)攻击，因为它会默认转译 PS: 大概就是转译这样又或者说是创建了一个这样的对象
```js
    {
        type: 'div'
        props: {
            className: 'expression',
            children: 'innerHTML' && [
                type: 'p'
                props:{
                       ...
                }
            ]
        }
    }
```
    react 赃检查 不会，会根据需要跟新的视图跟新部分视图，也就是如果一个DOM元素中间的文字需要改变，react的处理是只替换中间的文本，DOM元素本身不会发生进行删除重建，react还认为DOM是唯一的，不能进行修改，它代表UI的某个特定时刻，更新UI的方式只有创建全新的DOM,而它的赃检查只是使用了上一个DOM。
    props是组建传值的属性，所有的传值都通过props，react也规定任何组建不能修改props只能用纯函数，即相同的函数相同的参数，不管调用多少次都是相同的结果，所以组建都要保护props，
    每一个组建都有自己的state 这个是只属于组建本身的，要修改state也只能通过setState({Kye: newValue}),
```js
    class Parent extends React.Component {
        constructor(){
            super() //这个是必须的 所有的 react 组建都继承与 react 封装好的 react - class
            this.state = {
                num: 1
            }
        }
        render() {
            let num = this.state.num
            return (
                <Sun sendNum = { num }/>
            )
        }
    }
    function Sun(props) {
        let num = props.sendNum //props.num 中的 sendNum 需要与父组件的<Sun sendNum = { num }> 中的 sendNum 对应
        return (
            <div>{ num }</div>
        )
    }
```
### &emsp;生命周期
| react                     | vue            | describe |
|---------------------------|-----           |----------|
| constructor               | beforeCreate   | 初始化数据 &&vue：可以在这里做Ajax请求       |
| componentWillMount        | created        | 代表组建经历过初始化数据，但是还未渲染      |
| componentDidMount         | beforeMout     | react：DOM节点已经生成，组建第一次渲染，这里react调用AJAX请求，数据返回state会从新渲染&&vue: 挂载完成         |
| componentWillUnmount      | monted         | react：组建完成卸载和数据销毁&& vue挂载完成         |
| componentWillReceiveProps | beforeUpdate   | react：接受父组件props会重新渲染&&vue：监听数据变化并做出下一步修改视图的准备         |
| getDerivedStateFromProps  | updated        | react：newUp&&vue：根据视图更新数据或者数据跟新视图      |  new
| shouldComponentUpdate     | beforeDestroy  | react：可以控制组建渲染，当state发生变化时，react会更新视图，但是在这个过程中如果在这里 return false则不会更新渲染&&vue：组建销毁前，用于清空一些定时器什么的         |
| componentWillUpdate       | destroyed      | react：当组建更新被移除前会先调用这个方法&&vue：组建被销毁        |
| getSnapshotBeforeUpdate   | activate       | react：newUp&&vue：keep-alive创建时调用        |
| componentDidUpdate        | dectivated     | react：组建更新完成，每次更新完成都会进入这里，第一次渲染也是&&vue：keep-alive销毁         |
| render                    |     | react：会在这里将jsx生成VNode，更新时会用react的diff算法进行对比，进行赃检查         |

### &emsp;事件处理
    在react中点击事件需要加上大括号而不是引号，且在react中组织默认事件不能通过return false，只能通过e.preventDefault();这个e是react封装好的，不必担心兼容，如果用es6的class来定义组建，组要绑定this
```js
    class Demo extends React.Component{
        constructor(props){
            super(props);
            this.state = {flag: false}
            //绑定this
            this.handle = this.handle.bind(this)
        }
        handle(){
            //阻止默认事件
            e.preventDefault();
            this.setState(state=>({
                flag: !flag
            }))
        }
        // 使用public class fields 方法也可以不用绑定this
        han=()=>{

        }
        rendur() {
            return (
                <div>
                    <button onClick={handle}></button>
                    <button onClick={_=>this.handle()}></button>
                </div>
                // 如果觉得这样麻烦可以使用回掉函数使用箭头函数就不用绑定this
                //不过这样如果传入props有可能导致重新渲染
            )
        }
    }
```
### &emsp;事件传参
```js
    var gz = "箭头函数没有this指向，默认是继承外部上下的this，所以箭头函数中的this指向的就是组件(也是这个类),事件对象必须显式的进行传递"
    <button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
    var jt = "bind() 方法可以把组件的this代替函数的this,事件对象以及更多的参数将会被隐式的进行传递。第一个this当前组建，第二个this防止处理在deleteRow函数内部的this失真 所以用了bind"
    <button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```
### &emsp;条件渲染 
    1. if语句, 条件运算符, 去创建元素来表现当前状态, react 会根据他们来渲染 UI
    --if语句
```js
    function LogIn() {
        return <button>logIn</button>
    }
    function SigInOut() {
        return <button>SigInOut<button>
    }
    function AccountSigInout() {
        render ()
        const flag = false;
        if(flag){
            <LogIn />
        }else {
            <SigInOut />
        }
    }
```
    --&&逻辑运算符
```js
    function AccountSigInout() {
        consot str = 'sssss'
        return (
            <div>
                {str.lenght > 1000 && 
                    <h1>哈哈哈</h1>
                }
            </div>
        )
    }
```
    --三目运算符
```js
    function AccountSigInout() {
        const flag = false
        return (
            <div>
                { flag ? <LogIn /> : <SigInOut /> }
            </div>
        )
    }
```
### &emsp;循环渲染 || 列表 & key
    1. 需要一个数组，使用数组 map() 方法。此方法不会修改数组本身,会返回一个新的数组
        ---react {} 可以放一切表达式, 此处只需要在打括号内即可在 render() 中直接使用
        ---key是唯一的且是必须的(ps: 不同的 map 渲染可以使用相同的 key 并不冲突),如果不加 key, react 会默认加上 index, index 并不是一个好的选择因为 diff 算法。ps: 总结的 diff 算法
```js
    {
        arr.map(item => {
            <div key = { item.id }></div>
        })
    }
```
        ---嵌套循环,不要在 map 中嵌套太多层级 可利用 props 传值
```js
    // 父组件
    class Parent extends React.Component {
        constructor(){
            super()
            this.state = {
                arr[
                    {
                        first:[
                        {id: '1',
                        name: Value},
                        ...
                        ],
                        id: '1'
                    },{
                        first:[...]
                        id: '2'
                    }
                ]
            }
        }
        render() {
            let arr = this.state.arr;
            return (
                <>
                    {
                        arr.map( item => {
                            <sun sendArr = {item.first} key = { item.id } />
                        })
                    }
                </>
            )
        }
    }
    // 子组件
    function sun(props) {
        let arr = props.sendArr;
        return(
            {
                arr.map(item => {
                    return(
                        arr.map( item => {
                            <div key = { item.id }>{ item.name }</div>
                        })
                    )
                })
            }
        )
    }
```
### &emsp;表单
    
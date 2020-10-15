# React 第三天    

## 条件渲染     

1. if语句, 条件运算符, 去创建元素来表现当前状态,逻辑运算符， react 会根据他们来渲染 UI     

1.1 if语句     

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

1.2 &&逻辑运算符      

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

1.3 三目运算符     

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

## 循环渲染 || 列表 & key      

1. 需要一个数组，使用数组 map() 方法。此方法不会修改数组本身,会返回一个新的数组
   react {} 可以放一切表达式,  render() 中添加大括号可以直接使用
   key是唯一的且是必须的(ps: 不同的 map 渲染可以使用相同的 key 并不冲突),如果不加 key, react 会默认加上 index, index 并不是一个好的选择因为 diff 算法。ps: 总结的 diff 算法     
```js
{
arr.map(item => {
    <div key = { item.id }></div>
})
}
```     

2. 嵌套循环,不要在 map 中嵌套太多层级 可利用 props 传值     

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

## 表单     

1. 概念: 受控组件与非受控组件  
   可以被 react 状态控制的组件就是受控组件, Input textarea 是非受控组件但是可以用onChange 事件转换为受控组件
   双向数据绑定就是受控组件
   若指定 value,不要将 value 值设置为 undefined && null  

```js
class App extends React.Component {
    constructor() {
        super()
        this.state = {
            value: '请输入内容' //若指向了它，不要设置为 undefined && null
            name: 'name'
        }
        // this 绑定
        this.handleInputChange = this.handleInputChange.bind(this);
    }
    handleInputChange(e) {
        e = // 事件 
        e.target = // DOM 元素
        e.target.value = // 值
        e.target.name = // DOM 元素的 name,多个 input 可以使用这个方法区分 input 
        e.target.checked = // 单选框复选框的 checked = false && true 
    }
    render() {
        return (
            <>
                <input type="text" value={ this.state.value } name={ this.state.name }>
            </>
        )
    }
}
```     
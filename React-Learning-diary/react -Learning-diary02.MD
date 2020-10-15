# React 第二天

## props     

1. props是组件传值的属性，所有的传值都通过props。
2. react也规定任何组件不能修改props只能用纯函数，即相同的函数相同的参数，不管调用多少次都是相同的结果。
3. 所有组件都要保护props。
4. 每一个组件都有自己的state 这个是只属于组件本身的，要修改state也只能通过     

```js
setState({Kye: newValue}),
// 策略函数，就是当传入不同的参数走不同的代码，
setState((state,props) => ({ state.key,props.key }))
```       

```js
class Parent extends React.Component {
    constructor(){
        super() //这个是必须的 所有的 react 组件都继承与 react 封装好的 react - class
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

## 生命周期         

|react|describe |vue           |describe|
|---|---| ------------- | ----------------------------------------------------------------------------------- |
|componentWillMount |渲染前调用| beforeCreate  | 可以在这里做Ajax请求|
||| created       | 代表组件经历过初始化数据，但是还未渲染|
||| beforeMount   | 初始化模板完成|
|componentDidMount|在第一次渲染后调用，之后组件已经生成了对应的DOM结构，发送AJAX| mounted       | 挂载完成|
|componentWillReceiveProps |在组件接收到一个新的 prop (更新后)时被调用。这个方法在初始化render时不会被调用| beforeUpdate  | 监听数据变化并做出下一步修改视图的准备|
|shouldComponentUpdate |返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。可以在你确认不需要更新组件时使用|||
|componentWillUpdate|在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。|||
|componentDidUpdate|  在组件完成更新后立即调用。在初始化时不会被调用。|updated|根据视图更新数据或者数据跟新视图|
||| beforeDestroy | 组件销毁前，用于清空一些定时器什么的 |
|componentWillUnmount|在组件从 DOM 中移除之前立刻被调用。| destroyed     | 组件被销毁|
||| activate      | keep-alive创建时调用|
||| deactivated   | keep-alive销毁|

### react分为三个阶段
1. 挂载
2. 渲染&&更新
3. 卸载   
     
### 挂载 ###
| react              | describe |
| ------------------ | ----------------------------------------------------------------------- |
| render             | 这个比较特殊，它是生成虚拟DOM的函数，也是在更新时用来做新旧对比的函数，挂载会执行它，(ps: 挂载会执行俩次因为我在做demo的时候打印了俩次render()里的console.log(),目前还没找到合适的答案)更新也会执行不过要用,组件更新要用setState()才会调用render |
| constructor        | constructor()中完成了React数据的初始化，它接受两个参数：props和context，当想在函数内部使用这两个参数时，需使用super()传入这两个参数。|
| componentWillMount | 在服务端渲染时使用。它代表的过程是组件已经经历了constructor()初始化数据后，但是还未渲染DOM时。|
| componentDidMount  | 组件第一次渲染完成，此时dom节点已经生成，可以在这里调用ajax请求，返回数据setState后组件会重新渲染|

### 渲染&&更新 ###


| react                                      | describe|
| ------------------------------------------ | --------------------------------- |
| componentWillReceiveProps (nextProps)      | 需要接收一个参数，在接受父组件改变后的props需要重新渲染组件时用到，通过对比nextProps和this.props，将nextProps的state为当前组件的state，从而重新渲染组件|
| shouldComponentUpdate(nextProps,nextState) | 主要用于性能优化(部分更新)，唯一用于控制组件重新渲染的生命周期，由于在react中，setState以后，state发生变化，组件会进入重新渲染的流程，在这里return false可以阻止组件的更新，因为react父组件的重新渲染会导致其所有子组件的重新渲染，这个时候其实我们是不需要所有子组件都跟着重新渲染的，因此需要在子组件的该生命周期中做判断 |
| componentWillUpdate (nextProps,nextState)  | shouldComponentUpdate返回true以后，组件进入重新渲染的流程，进入componentWillUpdate,这里同样可以拿到nextProps和nextState。|
| componentDidUpdate(prevProps,prevState)    | 组件更新完毕后，react只会在第一次初始化成功会进入componentDidmount,之后每次重新渲染后都会进入这个生命周期，这里可以拿到prevProps和prevState，即更新前的props和state。|

#### 新增生命周期   



##### getDerivedStateFromProps(nextProps, prevState)

1. 代替componentWillReceiveProps()。老版本中的componentWillReceiveProps()方法判断前后两个 props 是否相同，如果不同再将新的 props 更新到相应的 state 上去。这样做一来会破坏 state 数据的单一数据源，导致组件状态变得不可预测，另一方面也会增加组件的重绘次数。   
2. 在 componentWillReceiveProps 中，我们一般会做以下两件事，一是根据 props 来更新 state，二是触发一些回调，如动画或页面跳转等。   
3. 在老版本的 React 中，这两件事我们都需要在 componentWillReceiveProps 中去做。   
4. 而在新版本中，官方将更新 state 与触发回调重新分配到了 getDerivedStateFromProps 与 componentDidUpdate 中，使得组件整体的更新逻辑更为清晰。而且在 getDerivedStateFromProps 中还禁止了组件去访问 this.props，强制让开发者去比较 nextProps 与 prevState 中的值，以确保当开发者用到 getDerivedStateFromProps 这个生命周期函数时，就是在根据当前的 props 来更新组件的 state，而不是去做其他一些让组件自身状态变得更加不可预测的事情。   

##### getSnapshotBeforeUpdate(prevProps, prevState)   

1. 代替componentWillUpdate。   
2. 常见的 componentWillUpdate 的用例是在组件更新前，读取当前某个 DOM 元素的状态，并在 componentDidUpdate 中进行相应的处理。   
3. 在 React 开启异步渲染模式后，在 render 阶段读取到的 DOM 元素状态并不总是和 commit 阶段相同，这就导致在componentDidUpdate 中使用 componentWillUpdate 中读取到的 DOM 元素状态是不安全的，因为这时的值很有可能已经失效了。   
4. getSnapshotBeforeUpdate 会在最终的 render 之前被调用，也就是说在 getSnapshotBeforeUpdate 中读取到的 DOM 元素状态是可以保证与 componentDidUpdate 中一致的。此生命周期返回的任何值都将作为参数传递给componentDidUpdate()。       

### 卸载 ###   
| react                | describe|
| -------------------- | --------------------------------------------------------------------------------- |
| componentWillUnmount | 在此处完成组件的卸载和数据的销毁。clear你在组建中所有的setTimeout,setInterval。移除所有组建中的监听 removeEventListener。 |




         
## 事件处理     

1. 在react中点击事件需要加上大括号而不是引号
2. 且在react中组织默认事件不能通过return false，只能通过e.preventDefault();这个e是react封装好的，不必担心兼容
3. 如果用es6的class来定义组件，组要绑定this     

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

## 事件传参     

1. 箭头函数没有this指向，默认是继承外部上下的this，所以箭头函数中的this指向的就是组件(也是这个类),事件对象必须显式的进行传递
2. bind() 方法可以把组件的this代替函数的this,事件对象以及更多的参数将会被隐式的进行传递。第一个this当前组件，第二个this防止处理在deleteRow函数内部的this失真 所以用了bind      

```js
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```     
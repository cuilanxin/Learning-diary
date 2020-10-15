# React 第四天

## 状态提升     

1. 这里面遇到的坑,当要实现 input 与子组件内容同步更新时     

```js
class sun extends React.Component {
    // 这个 props 只会在第一次调用的时候执行一次，后面就不会调用了
    constructor(props) {
        super()
        // 这个 state 只会在 constructor 执行的时候才会执行一次赋值
        this.state= {
            k: props.v
        }
    }
    // 若需要同步更新，直接使用 this.props 即可
    render() {
        return (
            <>{ this.props.v}</>
        )
    }
}
```     

## 组合&&继承     

1. 组合 && 嵌套 ps: Vue v-slot(插槽) 会发现与这样差不多,但是 react 并没有槽(solt)概念, 因为它的所有东西都可以用 props 进行传递,也可以写任意东西只需要在子组件中写上 { this.props.children }     

```js
class Sun extends React.Component {
    constructor(props) {
        super()
    }
    render() {
        return(
            <>
                { this.props.children }
            </>
        )
    }
}
class Parent extends React.Component {
    constructor() {
        super()
    }
    render() {
        return(
            <>
                <Sun>
                    { ... 任意标签 && 内容 }
                </Sun>
            </>
        )
    }
}
```     

2. 若需要在指定位置插入内容,或者内容对应显示,需要在子组件上留下印记,也就是 "名字" react 把这个叫做 "洞"它们会对应这个自己的名字显示在位置上，而不是依次显示     

```js
class Sun extends React.Component {
    constructor(props) {
        super()
    }
    render() {
        return(
            <>
                { this.props.left }
                { this.props.right }
            </>
        )
    }
}
class Parent extends React.Component {
    constructor() {
        super()
    }
    // 显然跟上面的是相反的顺序, 渲染的时候他会按照上面这个顺序去插入,会先找到 left 渲染, 再找到 right 渲染。
    // 也就是子组件写的什么顺序, 就是什么顺序
    render() {
        return(
            <>
                <Sun right={
                    <>1 rigth </>
                }
                left={
                    <>2 left</>
                } />
            </>
        )
    }
    // PS: 如果没传则不显示
}
// 扩展: 通过状态传递不同的 props, 达成条件渲染
```

## state 与 props 区别
1. props是父组件向子组件传递数据的属性，state是每个组件都有的属性   
2. props数据流是单向的，任何组件都不能修改props
3. state是组件私有的，可以通过 setState() 进行修改，且只通过这个修改render()才会更新
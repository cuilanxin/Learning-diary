## react-native 第三、四天   

1. 学习了mocker 这个是一个虚拟数据的，类似mock.js
2. 复制上面已有的接口代码，完成接口配置请求数据，这花费了我俩天的时间才正确的拿到数据，
3. server文件    

```js
export async function shopinglist(params) {
    return fetch('/api/shop', {
body: params,
});
```  

4. mocker文件   

```js
'POST /api/shop':(req,res) => {
    return res.status(200).json({
        arr:[
            //...
        ]
    })
}
```    

5. redux文件 -> users文件    

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

6. 需要渲染的组件文件,添加一个点击事件 onPress 使用redux的 connect这个API, 使用循环渲染将这组合思路在组建页面添加一个点击事件等于 users 的事件. 利用connectAPI特性触发这个方法，让这个方法去请求接口拿到数据并给定redux中需要流入的变量，这里使用到了updata()这个方法。本页面的话用this就可以调用他，参数就是后面的覆盖前面的。这样便可以存到redux里面，connect是自动检测数据变化的，列表自然就渲染了，这个循环渲染DOM的方法，当数组没有元素的时候不会报错因为用的是map，这个东西我是在第四天弄出来的   

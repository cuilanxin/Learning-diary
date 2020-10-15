# React 第一天    

## jsx语法     

1. 在js中写 html 是 jsx  
2. react里认为首字母应是大写，否者会被认为是html标签  
3. 最终都会被转换为浏览器认识的js
4. react使用jsx是为了让结构更加清晰，( UI + M = V )
5. jsx中添加js表达式加上大括号保住就可以，如果加上引号会被认为是字符串，且react认为大括号与引号只使用一个
6. react认为jsx语法更接近js而不是HTML所以采用小驼峰     

```js
<div className = { expression }></div> && <App className = "box" />
```  

7. jsx防注入(XSS)攻击，因为它会默认转译 PS: 大概就是转译这样又或者说是创建了一个这样的对象       

```js
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
```     

## react 赃检查     

1. 会根据需要更新的视图更新部分视图，也就是如果一个DOM元素中间的文字需要改变，react的处理是只替换中间的文本，DOM元素本身不会发生进行删除重建
2. react还认为DOM是唯一的，不能进行修改，它代表UI的某个特定时刻，更新UI的方式只有创建全新的DOM,而它的赃检查只是使用了上一个DOM。     

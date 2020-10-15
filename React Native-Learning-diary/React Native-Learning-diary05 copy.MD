# react-native第五天     
### 样式 && 笔记 ###

#### 默认布局   

1. 默认采用 flex 布局   
2. 默认主轴 column (ps: 即PC端交叉这轴)   

#### 与 CSS 异同

1. View 会默认占 100%
2. rn元素的绝对定位和相对定位不需要父元素设置position，且没有zIndex配置
3. 包裹在View元素中的Text表现为block => 可以设置margin和padding的各种属性
4. 包裹在Text元素中的Text表现为inline元素 =>  不能设置其marginTop和marginBottom
5. Text元素里面的Text元素存在继承
7. 在 React-Native 中，并不支持百分比单位 

```js
//可以这样
let MainHeight = Dimensions.get('window').height;
let MainWidth = Dimensions.get('window').width;
// 屏幕宽度的30%
const styles = StyleSheet.create({
    box: {
        width: MainWidth*0.3
    }
})
```

## 根据像素密度指定边框厚度 ##

```js
var styles = StyleSheet.create({
    box: {
        borderWidth: 1 / PixelRatio.get(),
        borderStyle: solid
    }
});
```

```js
<View></View> = <div></div>
<Text></Text> = <text></text>
```
#### 记忆 
1. solid, dotted, dashed
2. 实心、虚线、虚线
3. Radius 
4. align-self允许有单个项目与其他排列方式不一样,覆盖(alignItems)
5. resizeMode 参考background—size 取值(cover, contain, stretch)
6. overlayColor 当图像有圆角时，将角落都充满一种颜色
7. tintColor iOS 图像上特殊的色彩，改变不透明像素的颜色 取值(color)
8. transparent 全透明黑色(black)的速记bai法，即一个类du似rgba(0,0,0,0)这样的值 参考：https://zhidao.baidu.com/question/393408778864605725.html

|Text|值|属性|
|--|--|--|
| includeFontPadding|bool| Android在默认情况下会为文字额外保留一些padding，以便留出空间摆放上标或是下标的文字。对于某些字体来说，这些额外的padding可能会导致文字难以垂直居中。如果你把textAlignVertical设置为center之后，文字看起来依然不在正中间，那么可以尝试将本属性设置为false|
| textAlignVertical|auto, top, bottom, center|对应 CSS vertical-align 属性，增加了 auto 取值，center 取代了 middle，并阉割了 baseline, sub 等值|
|css: vertical-align|--| 该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。这会使元素降低而不是升高。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。|
|fontVariant| small-caps, oldstyle-nums, lining-nums, tabular-nums, proportional-nums|对应 CSS font-variant 属性，但取值更丰富|
|css: font-variant|-|font-variant 属性设置小型大写字母的字体显示文本，这意味着所有的小写字母均会被转换为大写，但是所有使用小型大写字体的字母与其余文本相比，其字体尺寸更小。|
|letterSpacing|number|增加或减少字符间的空白|
|textDecorationLine|none, underline, line-through, underline line-through|下划线在哪显示|
|textDecorationColor|color|定义文本下划线颜色| 
|textDecorationLine|none, underline, line-through, underline line-through|下划线|
|textDecorationStyle|solid, double, dotted, dashed|定义下划线样式|
|writingDirection|auto, ltr, rtl|文本方向|

|Margin&&padding|描述|
|---|---|
|(margin&&padding)Horizontal|相当于同时设置 Right 和 Left|
|(margin&&padding)Vertical|相当于同时设置 Top 和 Bottom|

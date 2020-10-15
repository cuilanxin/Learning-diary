# JS中diff算法是O(n3),这样及其浪费性能, 优化后是O(n)   

1. 是采用只对同级比较,不夸级比较;
2. tag和key只要有一个不同就直接删除重建,这样虽然多了操作,但是对比之前算法的性能使用,是更加节约性能的;
3. tag和key相同,就认为是相同节点,不在深度比较,而是比较他们的子元素;   

#  优化的diff算法 简述:
## VNode是JS语法生成的js对象; ##
1. 在优化中的diff算法,有一个h函数,h函数最多接收三个参数,"h(sel(标签),data(数据),children(子元素))",h函数返回一个vNode()函数;vNode函数接收五个参数,"vNode(sel(元素),data(数据),children(),text(文本),undefined)",需注意的是一般情况下children和text只会存在一个;vNode()函数又会返回一个对象,"{sel,data,children,text,elm,key}",也就是vNode=h(return=>vNode(return=>{sel,data,children,text,elm,key}));
2. patch函数接收俩个参数,但是分三种情况:"patch(container(DOM元素),vNode)","patch(vNode,newVNode)","patch(newVNode,null)";
3. patch会执行一个"pre hook"声明周期;if第一个参数是不是一个vNode,那他就是一个DOM元素,则会声明一个空的vNode,关联到这个DOM元素,return出去一个vNode,这个vNode会与这个DOM元素绑定;if判断使用"sameVNode(oldVNode,vNode)这个函数"判断新的vNode与老的是不是相同,也就是对比新老vNode的sel(或者tag)与key是不是相同,没有key,则就是未定义,返回true,情况有二:   
   1. 不相同就删了重建,第一次如果参数是DOM元素也会走到重建这里,因为声明的vNode是不会与老vNode相同的   
   2. 相同就会调用patchVNode(oldVNode,vNode,一个操作DOM元素添加删除的方法),这个函数会执行一个生命周期钩子prepatch hook,然后设置新的vNode.elm,也就是将oldNode.elm赋值给它,因为新的vNode可能没有elm(它需要知道更新什么,相反现在是新的执行之后就会变成旧的);
      1. if判断新的text是不是有,如果新的有(text)老的也有(text)还不相同就直接把老的remove,在设置新的值,
      2. 如果新的(text)没旧的有(text),直接把旧的掉;
      3. 在if判断新旧的children,如果新的有(children)旧的没(children),先将旧的text判断是不是有值,如果有值便设置为空,再把新的children添加进去;
      4. 如果新的有children旧的没有就直接添加进去;
      5. 如果新的没有(children)旧的有(children),就直接remove旧的(children);
      6. 如果新的旧的都有children便执行"updataChlidren(elm(元素),oldChildren,newChildren,删除增加DOM元素的方法)";这个函数中会使用"sameVNode()这个函数"来判断是不是相同的children,对比方式是将新旧children的首和尾都进行对比,也就是首是递增,尾是递减,当值为一样的时候就停止对比,这样节省性能,如果这样没有相同的,则将新的首挨个对比老的每个children,同时用新的尾也开始对比老的每个children,这个时候就是用key的时候了,如果key是使用的下标很容易造成有相同的children但是位置不一样导致key不相同,如果都没中则会重建,如果有相同的则会调用"patchVNode()"进行再次对比
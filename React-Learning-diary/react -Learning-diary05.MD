# React 第五天

## 路由

https://reacttraining.com/react-router/   

### react-router-dom

1. -S下载到生产环境的依赖中。
2. 在组件中通过对象的解构方式去获取到react-router-dom内置组件，在组件中，按需引入内置组件，在页面中进行使用
3. HashRouter表示一个路由的根容器，将来所有的路由相关的东西，都要包裹在HashRouter里面，而且一个网站中，只需要使用一次HashRouter就好了
4. Route表示一个路由规则，在Route上，有两个比较重要的属性，path(路径)，component(组件)
5. Link则表示一个路由的链接

### 创建路由

```js
// Baokuo
import {BrowserRouter, HashRouter, Router, link} from 'react-rounter-dom'
import {Button, DatePicker, Icon} from 'antd'

class Baokuo extends React.Component {
    render() {
        return (
            // 跟容器
            <HashRouter>
                <div>
                    <h1>跟目录</h1>
                    {/*链接*/}
                    <nav>
                        <Link to="/home">首页</Link>
                    </nav>
                    {/* 路由规则，Route是配置路由的规则，同时也是一个占位符 */}
                    <Switch>
                        <Router path="/home" component={Home} />
                            <Component />
                        </Router>
                    </Switch>
                </div>
            </HashRouter>
        )
    }
}
```

```js
import React from 'react'
import ReactDOM from 'react-dom'
import Baokuo from '/Baokuo'

ReactDOM.render(<Baokuo />,document.getElementById('root'))
```

### 步骤 ###

1. 配置路由容器 Router
2. 配置路由链接 Link
3. 配置路由填充的位置以及路径和组件的映射关系
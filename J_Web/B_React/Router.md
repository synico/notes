## React Router
基于React的路由库，用于快速向应用中添加视图和数据流，同时保持页面与URL间的同步。

### routers
#### `<BrowserRouter>`
使用HTML5的pushState history API保持页面与URL同步。

#### `<HashRouter>`
使用URL中的hash (window.location.hash) 部分保持页面与URL同步。

***

### route matchers
#### `<Route>`
React Router中最重要的组件，当定义的path匹配目前URL时渲染UI。

#### `<Switch>`

***

### navigation
#### `<Link>`

#### `<NavLink>`

#### `<Redirect>`

***

### `<Route>`
Route目前推荐的渲染方式为将欲渲染的部分定义为`<Route>`的子元素，除此之外还有几种为兼容引入hooks之前版本的渲染方法。优先级childeren > component > render，所以不要在同一个`<Route>`中同时使用三个属性。
#### route props
* match
* location
* history

#### `<Route component>`
* 当路由的路径匹配时React组件才会被渲染，同时组件能读取route props。
* 每次都会调用React.createElement创建新的React元素，如果将inline内联函数赋予component属性，则每次渲染时都会创建新的组件，而不是更新现有的组件。

#### `<Route render>`
* render: func
* 通过传入一个函数给render属性，每次当路由的路径匹配时都会更新现有组件。
* render属性会接受所有由route传入的参数。

#### `<Route children>`
* children: func
* 无论路由的路径时候匹配，组件都会被渲染，路由不匹配时，route props的match属性为null。

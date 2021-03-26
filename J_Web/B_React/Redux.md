## Redux
Action描述发生了什么，Reducer根据Action更新state，而Store是将它们联系到一起的对象。

### Action
* Action的本质是普通Javascript对象。
* Action是把数据从应用传到store的载体，并是store数据的唯一来源。
* Action只是描述了有动作发生，但并未描述应用如何更新state。

***

### Reducer
* Reducer是纯函数，没有副作用。
* Reducers指定了应用状态的变化如何响应Action并将Action发送到Store。
* 接收旧的state和要执行的Action，返回新的state `(previousState, action) => newState`。

#### Reducer合成
开发一个函数做为主Reducer，它调用多个子Reducer分别处理state中的一部分数据，然后再把这些数据合成一个大的单一对象。

***

### Store
`let store = createStore(combinedReducers)`
* 维持应用的state。
* 提供getState()方法获取state。
* 提供setState()方法更新state。
* 通过subscribe(listener)注册监听器。

***

### 应用中数据的生命周期
*  调用store.dispatch(action)。
* Redux store调用传入的Reducer函数。
* 根Reducer把多个子Reducer输出合并成一个单一的state树。
* Redux store保存根Reducer返回的完整state树。

***

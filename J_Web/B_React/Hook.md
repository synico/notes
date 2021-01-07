## React Hook
Hook就是Javascript函数，但使用它们有两个额外的规则
* 只能在函数最外层调用Hook，不要在循环，条件判断或子函数中调用。
* 只能在React的函数组件中调用Hook，不能在class组件中使用。不要在其他Javascript函数中调用。

### useState()
状态钩子，用于为函数组件引入状态 (state) 。useState()函数接受状态的初始值作为参数，该函数返回一个数组。数组的第一个成员是一个变量，指向状态的当前值。第二个成员是一个函数，用来更新状态，约定是set前缀加上状态的变量名。
```
const [state, setState] = useState(initialState);
```

***

### useEffect()
副作用钩子，用于在函数组件中执行副作用操作。useEffect()函数接受两个参数。第一个参数是一个函数，用于执行异步操作；第二个参数是一个数组，用于给出Effect的依赖项，只要依赖项的值发生变化，useEffect就会执行，如果传入空数组，则Effect仅运行一次，如果省略该参数，则每次渲染时 (包括挂载和更新) 都会运行Effect。
* 如与React的class组件类比，可把useEffect Hook看作componentDidMount，componentDidUpdate和componenetWillUnmount这三个函数的组合。
* useEffect如有副作用需要清除，则需返回一个函数。

```
useEffect(() => {
  // Async action
}, [dependencies]);

useEffect(() => {
  function handleStatusChange(status) {
    setIsOnline(status.setIsOnline);
  }
  ChatAPI.subscribeToStatus(id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromStatus(id, handleStatusChange);
  };
});
```

***

### useContext()
共享状态钩子，用于在组件之间共享状态，引入Context对象，可从Context对象中获取相应属性。
```
const value = useContext(MyContext);
```

***

### useReducer()
action钩子，用来引入Reducer功能。useReducer()函数接受Reducer函数和状态的初始值作为参数，返回一个数组。数组的第一个成员是状态的当前值，第二个成员是发送action的dispatch函数。

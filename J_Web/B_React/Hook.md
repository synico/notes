## React Hook
Hook就是Javascript函数，但使用它们有两个额外的规则
* 只能在函数最外层调用Hook，不要在循环，条件判断或子函数中调用。
* 只能在React的函数组件中调用Hook，不能在class组件中使用。不要在其他Javascript函数中调用。

### useState
状态钩子，用于为函数组件引入状态 (state) 。useState()函数接受状态的初始值作为参数，该函数返回一个数组。数组的第一个成员是一个变量，指向状态的当前值。第二个成员是一个函数，用来更新状态，约定是set前缀加上状态的变量名。
```
const [state, setState] = useState(initialState);
```

***

### useEffect
副作用钩子，用于在函数组件中执行副作用操作。useEffect()函数接受两个参数。
* 第一个参数是一个函数，用于执行异步操作。该函数会在组件渲染到屏幕之后执行，即在每轮渲染结束后执行。
* 第二个参数是一个数组，用于给出Effect的依赖项，只要依赖项的值发生变化，useEffect就会执行，如果传入空数组，则Effect仅运行一次，如果省略该参数，则每次渲染时 (包括挂载和更新) 都会运行Effect。
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

### useContext
共享状态钩子，用于在组件之间共享状态，引入Context对象，可从Context对象中获取相应属性。调用了useContext的组件总会在context值变化时重新渲染。

```
const context = useContext(MyContext);
```

***

### useReducer
action钩子，用来引入Reducer功能。useState的替代方案，接收一个形如 `(state, action) => newState`的reducer。useReducer()函数接受Reducer函数和状态的初始值作为参数，返回一个数组。数组的第一个成员是状态的当前值，第二个成员是发送action的dispatch函数。

```
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

***

### useCallback
返回一个memoized回调函数。
* 第一个参数为回调函数。
* 第二个参数为依赖项数组。如果省略该参数，则回调函数每次都执行，如果传入空数组，则回调函数仅执行一次。
* `useCallback(fn, deps)` 相当于`useMemo(() => fn, deps)`。

```
const memoizedCallback = useCallback(fn, deps);
```

***

### useMemo
返回一个momoized值。定义一段函数逻辑是否重复执行。
* 仅用来做性能优化。
* 第一个参数为需要执行的函数，会在渲染期间执行。不要在这个函数内部执行与渲染无关的操作。
* 第二个参数为依赖项数组。如果省略该参数，则函数每次都执行，如果传入空数组，则函数仅执行一次。

```
const memoizedValue = useMemo(() => fn, deps)
```

***

### useMemo与useEffect
* useMemo与useEffect的语法是一样的，第一个参数是要执行的逻辑函数，第二个参数是这个逻辑函数依赖的变量组成的数组。
* useMemo与useEffect的执行时机是不一致的，useEffect执行的是副作用，所以一定是在渲染之后执行的，useMemo是需要有返回值的，而返回值可以直接参与渲染，所以useMemo是在渲染期间完成。

***

### useCallback与useMemo
useCallback返回的是函数，只要用来缓存函数，因为函数式组件中的state的变化都会导致整个组件被重现刷新，此时用useCallback将函数进行缓存，减少渲染时性能损耗。而useMemo返回的是计算的结果值，用于缓存计算后的状态。

***

### memo与useMemo
memo用来优化函数组件的重复渲染行为，当传入属性值都不变的情况下不会触发组件的重新渲染，否则会触发组件的重新渲染。memo针对的是一个组件的渲染是否重复执行，而useMemo则定义了一段函数逻辑是否重复执行。严格来说，不使用memo和useMemo不会导致业务逻辑发生变化，memo和useMemo只是用来做性能优化。

***

### useRef

***

### useImperativeHandle

***

### useLayoutEffect

***

### useDebugValue

***

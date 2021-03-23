## Javascript Array对象

### map()
map()方法按照原始数组元素顺序依次处理元素，返回一个新数组，新数组中的元素为原始数组元素调用函数处理后的值。

```
array.map(function(currentValue, index, arr), thisValue)
```

参数说明

参数|描述
:--|:--
function(currentValue, index, arr)|必须。函数，数组中的每个元素都会执行这个函数
currentValue|必须，当前元素的值
index|可选，当前元素的索引值
arr|可选，当前元素属于的数组对象
thisValue|可选，对象作为该执行回调时使用，传递给函数，用作this的值，如果省略，则回调函数的this为全局对象

```
let strArray: Array<string> = ['1', '2', '3', 'a', 'b', 'c'];
let newArray: Array<string> = strArray.map((currentValue: string, index: number, arr: Array<string>) => {
    console.log(currentValue, index, arr)
  });

```

***

### filter()
filter()方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

```
array.filter(function(currentValue, index, arr), thisValue)
```

参数说明

参数|描述
:--|:--
function(currentValue, index, arr)|必须。函数，数组中的每个元素都会执行这个函数
currentValue|必须，当前元素的值
index|可选，当前元素的索引值
arr|可选，当前元素属于的数组对象
thisValue|可选，对象作为该执行回调时使用，传递给函数，用作this的值，如果省略，则回调函数的this为全局对象

```
let ages: Array<number> = [32, 22, 12, 40];
let list: Array<number> = ages.filter(age => age > 30);
```

***

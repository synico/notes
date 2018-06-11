## Programming Scala

### 字面量
#### 元组字面量
Scala库中包含TupleN类，用于组建N元素组，它以小括号加上逗号分隔的元素序列的形式来创建元素组。以下为创建元组方式:
* 通过TupleN，如```Tuple2(1, "one")```。
* 通过逗号和小括号，如```(1, "one")```。
* 通过箭头操作符创建仅包含两个元素的元组，如```1 -> "one"```。
#### 函数字面量
* Scala的函数是头等函数，可以把函数定义为匿名的字面量，并将其作为值传递。
```
val funcLiteral = (x: Int) => x + 1

funcLiteral(1)
```
* 当函数字面量很长时，可用{...}代替(...)。
```
val funcLiteral = (x: Int) => {
  println(s"value of param: $x")
  x + 1
}

funcLiteral(1)
```
* 调用无参方法时可以省略点号，括号。如无参方法在定义时省略了括号，则调用时必须省略括号 (一般定义无副作用的方法时省略括号，定义有副作用的方法时则添加括号) 。

### for推导式
一个for推导式并未使用yield，而是执行具有副作用的操作，那么将其称为for循环。
* for推导式的第一句表达式必须使用箭头符执行抽取，迭代操作。
* 当for推导式仅包含单一表达式时使用圆括号，当其包含多个表达式时使用大括号。
* 通过yield关键字能在for推导式中生成新的集合。
***

### 模式匹配
#### 简单匹配
```
val bools = Seq(true, false)
for (bool <- bools) {
  bool match {
    case true => println("Got heads")
    case false => println("Got tails")
  }
}
```
#### match中的值和变量
```
for {
  x <- Seq(1, 2, 2.7)
} {
  val str = x match {
    case 1  => "int i"
    case i: Int => "other int: " + i
    case unexpected => "unexpected value: " + unexpected
  }
  println(str)
}
```
#### 序列的匹配
```
def seqToString[T](seq: Seq[T]): String = seq match {
  case head +: tail => s"$head +: " + seqToString(tail)
  case Nil => "Nil"
}
```
***

### 隐式参数
方法声明中包含implicit关键字标记的方法参数，如果未输入隐式参数且代码所处作用域存在类型兼容的值时，类型兼容值会从作用域中调出并使用，反之，将抛出编译错误。
***

### 函数式编程
* 作为某个对象成员的函数被称为方法，即与实例绑定的函数称为方法。
* ```=>```指明这个函数把左边的东西转变成右边的东西。
* 返回Unit的函数只能执行带副作用的操作。
* 一个函数采用其他函数作为变量或返回值时，它被称为高阶函数。

### 闭包
* 自由变量，当前作用域中某个值得引用。
* 一个函数，可能匿名或具有名称，在定义中包含了自由变量，函数中包含了环境信息，以绑定其引用的自由变量。

### Lambda函数
在Scala中，称Lambda函数为匿名函数或函数字面量。

### 作为函数的方法
在需要函数的地方用了方法，就称该方法被提升为了函数。

### 尾递归
当一个调用了自身的方法，有可能被子类型中的同名方法覆写时，尾递归是无效的。所以，尾递归的方法必须用private或final关键字声明，或者将它嵌套在另一个方法中。

### 偏函数 (PartialFunction)
此类型函数不处理所有可能的输入，而只处理那些能与至少一个case语句匹配的输入。
* 偏函数中只能使用case语句。
* 整个函数必须用花括号包围 (普通函数字面量可以用花括号，也可以使用圆括号包围)。
* 偏函数可以通过orElse连接。

### 偏应用函数 (partially applied function)
偏应用函数是一个表达式，带部分而非全部参数列表的函数。返回值是一个新函数，新函数负责携带剩下的参数列表。
* 对于拥有多个参数列表的函数，如果希望忽略其中一个或多个参数列表，可以通过定义一个新函数来实现。
* 偏应用函数是一个表达式，带部分而非全部参数列表的函数。
* 返回值是一个新函数，新函数负责携带剩下的参数列表。

### case类
* 为方便且简单的域类型提供了模式匹配和实例分解。
* 让编译器自动生成许多方法，其中包括类似于Java语言中toString，equals和hashCode方法。
* 编译器同时生成一个伴生对象 (companion object) ，伴生对象是一个与case类同名的单例对象。

### 伴生对象
对象名和类名相同且定义在同一个文件中，这个对象就称为伴生对象。

### Curry化
* Curry将一个带有多参数的函数转换为一系列函数，每个函数都只有一个参数。
* 在Scala中，Curry化的函数带有多个参数列表，处理后，每个函数都只有一个参数列表。
***

### 6.8 遍历，映射，过滤，折叠与归约
#### 遍历 (foreach)
Scala容器标准的遍历方法是foreach (scala.collection.IterableLike)，IterableLike的部分子类可能会重新定义该方法。
#### 映射 (map)
map方法返回一个与原集合类型大小相同的新集合，其中每个元素均由原集合的对应元素转换得到。
#### 扁平映射 (flatMap)
* flatMap中，对原始集合中的每个元素，都分别产生零或多个元素。调用flatMap时传入一个函数，该函数对每个输入返回一个集合。然后flatMap把生成的多个集合合并 ("压扁") 为一个集合。
* flatMap不能处理超过一层的集合。如果处理的是深层嵌套集合，那么集合只能被压扁一层。
#### 过滤 (filter)
遍历集合并抽取满足特定条件的元素组成一个新的集合。
* def drop (n : Int) : TraversableLike.Repr
* def dropWhile (p : (A) => Boolean) : TraversableLike.Repr
* def exists (p : (A) => Boolean) : Boolean
* def filter (p : (A) => Boolean) : TraversableLike.Repr
* def filterNot (p : (A) => Boolean) : TraversableLike.Repr
* def find (p : (A) => Boolean) : Option[A]
* def forall (p : (A) => Boolean) : Boolean
* def partition (p : (A) => Boolean) : (TraversableLike.Repr, TraversableLike.Repr)
* def take (n : Int) : TraversableLike.Repr
* def takeWhile (p : (A) => Boolean) : TraversableLike.Repr
#### 折叠 (fold) 与规约 (reduce)
两者很相似，它们都是将一个集合"缩小"成一个更小的集合或一个值的操作。
***

### 价值类
继承自AnyVal的自定义类。

### 通用特征
***

### 构造器
* 主构造器是整个类体，构造器所需参数都罗列在类名称后面。
* 辅助构造器被命名为this，辅助构造器第一个表达式必须调用主构造器或其他辅助构造器。
* 编译器要求被调用的构造器在代码中先于当前构造器出现。
***

# 第一行代码读书笔记——Kotlin

## 变量

### 定义

```kotlin
val a = 10 // 不可变
var b = 10L // 可变
var c : Int = 10 // 指定类型
```

> 永远优先使用val来声明一个变量

### 类型

| 数据类型 | 说明         |
| -------- | ------------ |
| Int      | 整型         |
| Long     | 长整型       |
| Short    | 短整型       |
| Float    | 单精度浮点型 |
| Double   | 双精度浮点型 |
| Boolean  | 布尔型       |
| Char     | 字符型       |
| Byte     | 字节型       |

## 函数

### 定义

```kotlin
fun methodNme(param1: Int, param2: Int): Int{
    return 0
}
```

> 经常使用代码补全功能

### 语法糖

```kotlin
fun largerNumber(num1: Int, num2: Int): Int = max(num1, num2)
```

## 逻辑控制

### if条件语句

#### 基本写法

```kotlin
if (condition) {
    // doSomething
} else {
    // doSomething
}
```

#### 返回值

if语句使用每个条件的**最后一行**代码作为返回值

```kotlin
val value = if (num1 > num2) {
    num1
} else {
    num2
}
```

### when条件语句

#### 格式

```kotlin
when (variable) {
    value1 -> {doSomething}
    value2 -> {doSomething}
}
```

> 当执行逻辑只有一行代码时，{ }可以省略

when语句和if语句一样，都**有返回值**。

#### 类型匹配

```kotlin
when (num) {
    is Int -> println("Int")
    is Double -> println("Double")
    else -> println("Unkonwn")
}
```

#### 不带参数

```kotlin
when {
    name.startsWith("Tom") -> 86
    name == "Jim" -> 77
    else -> 0
}
```

### 循环语句

#### 区间

```kotlin
0..10 // [0,10]
0 until 10 // [0,10)
10 downTo 1 // [10,1]
```

#### for-in循环

```kotlin
for (i in 0..20) {}
for (i in 0 until 10 step 2) {} // 相当于i += 2
```

## 面向对象

### 类与对象

#### 类定义

```kotlin
class Person {
	var name = ""
	var age = 0
	
	fun eat() {
		println("...")
	}
}
```

#### 实例化

```kotlin
val p = Person()
p.name = "Jack"
p.eat()
```

### 继承与构造函数

#### 开放继承

```kotlin
open class Person{
    // doSomething
}
```

#### 继承

```kotlin
class Student : Person() {
    // doSomething
}
```

#### 主构造函数

```kotlin
class Student(val sno: String, val grade: Int) : Person() {} // 默认，无函数体
class Student(val sno: String, val grade: Int) : Person() {
    init { // init结构体，主构造函数执行逻辑
        println("sno is ${sno}")
    }
}
```

> 在绝大多数情况下，我们是不需要编写init结构体的

子类的构造函数必须**调用父类的构造函数**，在继承时通过**括号**指定。

```kotlin
class Student(val sno: String, val grade: Int) : Person(name, age) {}
// 传入父类构造函数参数的参数未带val/var关键字，作用域限定在构造函数中
```

#### 次构造函数

```kotlin
class Student(val sno: String, val grade: Int) : Person(name, age) {
    constructor(name: String, age: Int) : this("", 0, name, age) {   
    }
    constructor() : this("", 0){ // 调用上一个次构造，进而间接调用主构造
    }
}
```

任何一个类只能有一个主构造函数，但**可以有多个次构造**函数。（异同：用于类的实例化，次构造函数有函数体）

当一个类既有主构造函数又有次构造函数时，所有的次构造函数都必须**调用主构造函数**（包括间接调用）。

#### 特例——只有次构造函数

```kotlin
class Student : Person { // 无主构造函数，此处无法调用父类构造函数，不加括号
    constructor(name: String, age: Int) : super(name, age) {}
    // 通过super调用父类构造函数
}
```

### 接口

#### 定义

```kotlin
interface Study {
    fun read()
    fun homeWork()
}
```

#### 实现

```kotlin
class Student(name: String, age: Int) : Person(name, age), Study{
// 接口后不加括号，因为没有可以调用的构造函数
    override fun read() {
        // doSomething
    }
    
    override fun homeWork() {
        // doSomething
    }
}
```

任何一个类最多只能继承一个父类，但是却**可以实现任意多个接口**。

#### 多态特性

```kotlin
doStudy(Student("Jack", 19))

fun doStudy(study: Study){ // 实现Study接口，可以传入该实例
    study.read()
}
```

#### 默认实现

```kotlin
interface Study {
    fun read()
    fun homeWork() {
        println("do some homework")
    }
}
```

有默认实现时，不会强制要求实现，**无实现时使用默认实现**；无默认实现强制实现。

#### 函数可见性修饰符

| 修饰符    | 说明               |
| --------- | ------------------ |
| public    | 默认，所有类可见   |
| private   | 当前类可见         |
| protected | 对当前类和子类可见 |
| internal  | 同一模块的类可见   |

### 数据类

```kotlin
data class Cellphone(val brand: String, val price: Double)
```

数据类将根据主构造函数中的参数自动生成equals(),hashCode(),toString()等固定且无逻辑意义的方法。

### 单例类

```kotlin
object Singleton {
    fun singletonTest() {
        // doSomething
    }
}
```

## 数据结构

### ArrayList

#### 定义

```kotlin
val list = ArrayList<String>()
```

#### 添加元素

```kotlin
list.add("...")
```

#### 初始化

```kotlin
val list = listOf(item1, item2, item3) // 不可变集合
val list = mutableListOf(item1, item2, item3) // 可变集合
```

#### 遍历

```kotlin
for (fruit in list)
	println(fruit)
```

### Set

#### 初始化

```kotlin
val set = setOf(item1, item2, item3) // 不可变集合
val set = mutableSetOf(item1, item2, item3) // 可变集合
```

Set中**不可以存放重复元素。**

### HashMap

#### 定义

```kotlin
val map = HashMap<String, Int>()
```

#### 添加元素

```kotlin
map.put(key, value) // 不建议
map[key] = value
```

#### 读取元素

```kotlin
val value = map[key]
```

#### 初始化

```kotlin
val map = mapOf(key1 to value1, key2 to value2)
val map = mutableMapOf(key1 to value1, key2 to value2)
```

#### 遍历

```kotlin
for ((key, value) in map) {
    // doSomething
}
```

#### 函数式API

```kotlin
val maxLengthFruit = list.maxBy { it.length } // maxBy: 
```

## Lambda编程

### Lambda表达式

```kotlin
{param1: Type, param2: Type -> body}
```

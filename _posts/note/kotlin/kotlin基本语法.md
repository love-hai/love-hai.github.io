### 变量
1. 变量关键字
    - var 可变变量:可以重新赋值
    - val 不可变变量:第一次赋值后不能再次赋值
2. 变量声明
    (var|val) 变量名: 类型 = 值
### 基本数据类型
1. 基本数据类型
|类别|基本类型|示例|
|  ----  | ----  | ----  |
|整数|Byte, Short, Int, Long|val a: Int = 100|
|无符号整数|UByte, UShort, UInt, ULong|val b: UInt = 100u|
|浮点数|Float, Double|val c: Double = 100.0 ; val d: Float = 100.0f|
|字符|Char|val e: Char = 'A'|
|布尔|Boolean|val f: Boolean = true|
|字符串|String|val g: String = "Hello"|

### 集合
1. list : 有序可重复
    - listOf() : 创建不可变集合
    - mutableListOf() : 创建可变集合
2. set : 无序不重复
    - setOf() : 创建不可变集合
    - mutableSetOf() : 创建可变集合
3. map : 键值对
    - mapOf() : 创建不可变集合
    - mutableMapOf() : 创建可变集合
    查询集合元素
    - 集合名[索引]
    - 集合名.get(索引)

### 控制流
1. if..else
    - if (条件) {代码块} else {代码块}
2. when
    - when (条件) {条件1 -> 代码块1; 条件2 -> 代码块2; else -> 代码块3}
    和java 21的switch类似
3. ranges
    - in : 判断是否在范围内
    - downTo : 递减
    - step : 步长
    - until : 不包含结束值
    - .. : 创建范围 如果不包含结束值使用 ..<

### 方法
1. 方法声明
    fun methodName([参数名: 参数类型]*): 返回值类型 {
        // 方法体
    }
    例：
    ``` kotlin
    fun sum(a: Int, b: Int): Int {
        return a + b
    }
    ```
2. 返回类型可以不写
    // 返回类型可以不写
     ``` kotlin
    fun sum(a: Int, b: Int) = a + b
    ```
3. 参数可以有默认值
   ``` kotlin
    fun sum(a: Int, b: Int = 0) = a + b
    fun main() {
        println(sum(1))
    }
    ```
4. 参数可以不按照顺序传递
    ``` kotlin
    fun main() {
        println(sum(b = 1, a = 2))
    }
    ```
5. 可以没有返回值
    ``` kotlin
    fun printSum(a: Int, b: Int): Unit {
        println("sum of $a and $b is ${a + b}")
    }
    fun printSum(a: Int, b: Int) {
        println("sum of $a and $b is ${a + b}")
    }
    ```
6. lambda表达式
    + lambda表达式的声明
    ``` kotlin
    val sum: (Int, Int) -> Int = { x, y -> x + y }
    println(sum(1, 2))
    ```
    + lambda表达式的类型可以省略
    ``` kotlin
    val sum = { x: Int, y: Int -> x + y }
    println(sum(1, 2))
    ```
    + lambda表达式作为方法参数
    ``` kotlin
    fun printSum(a: Int, b: Int, sum: (Int, Int) -> Int) {
        println("sum of $a and $b is ${sum(a, b)}")
    }
    fun main() {
        printSum(1, 2, { x, y -> x + y })
    }
    ```
    + lambda表达式作为参数时，且是最后一个参数，可以将lambda表达式移到括号外
    ``` kotlin
    fun main() {
        printSum(1, 2) { x, y -> x + y }
    }
    ```
### 类和数据类
1. 类的声明
    + 类的声明
    ``` kotlin
    class Person(val name: String, var age: Int)
    // 人的名字不变，年龄可变
    ```
    + 和方法一样，类的参数可以是默认值,也可以不按照顺序传递
2. 数据类
    + 数据类是一种只保存数据的类
    + 数据类的声明
    ``` kotlin
    data class Person(val name: String, var age: Int)
    ```
    + 数据类的实例化
    ``` kotlin
    val person = Person("Tom", 20)
    ```
    + 数据类的属性
    ``` kotlin
    println(person.name)
    println(person.age)
    ```
    + 数据类的copy方法
    ``` kotlin
    val person2 = person.copy(name = "Jerry")
    println(person2)
    ```
    + 数据类的toString方法
    ``` kotlin
    println(person.toString())
    ```
    + 数据类的componentN方法
    ``` kotlin
    val (name, age) = person
    println(name)
    println(age)
    ```
### 空指针 安全 
1. lotkin 会在编译的时候就检查空指针
2. 通过?来标记一个变量可以为空
    ``` kotlin
    var a: String? = null
    ```
3. ?: 运算符
    ``` kotlin
    val b = a ?: "default"
    ```
4. !! 运算符
    ``` kotlin
    val l = a!!.length
    ```


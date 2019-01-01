参考教程： [Go 语言教程](http://www.runoob.com/go/go-tutorial.html)，70%的代码来自于这个教程，仅当笔录。
## 一、语言结构初探
以 **.go** 文件的形式存在，一个简单的文件结构如下：
```
// 引入的包名
package main
// 具体的包
import "fmt"

// 先于 main 函数调用
func init() {
fmt.Println("INIT")
}

// 主函数
func main() {
// 简单的变量定义
var a int
a = 78
var b int
b = 20
// 定义并做加法运算
var c int = a + b
// 简单的打印
fmt.Println("Hello,  CoderHG!  c = ", c)
/** 打印结果：
Hello,  CoderHG!  c =  98
*/
}
```

如果文件名为 **hello.go**， 则在终端执行：
> go run hello.go


其实以上简简单单的代码，已经透露了很多的技术点了，比如函数的定义，变量的定义，注释的使用，等等。但是这些在接下来还会详细的介绍。

## 二、变量
套路：
> var identifier type

套路只有一个，表现形式却很有很多，分成两个小模块：
### 2.1 简单使用
```
// 变量的使用
func varUse() {
// 方式一
var name string 
name = "CoderHG"

// 方式二
var sex = "handsome"

/** 方式三
var age
age = 18
*/// 这种方式是不对的

// 方式四 这种方式有点厉害了....
girlFriend := false

// 打印结果: CoderHG handsome false
fmt.Println(name, sex, /**age*/ girlFriend)
}
```

尤其注意 **第四种方式**。

### 2.2 多变量声明
```
//  多变量的使用
func varMUse() {
// 方式一
var name, sex string = "CoderHG", "handsome"
// 方式二
var (
x int = 10
y int = 10
address string = "TJ"
)

// 打印结果: CoderHG handsome 10 10 TJ
fmt.Println(name, sex, x, y, address)
}
```
多多少少有点 **Swift** 中元组的味道。

**注意事项**
```
// 没有使用已经声明的变量, 编译直接报错
func unUseVar() {
var a string = "abc"
}
```

## 三、常量
套路：
```
const identifier [type] = value
```
由此看出，关键字是 **const**。
```
func constUse() {
const LENGTH int = 10
const WIDTH int = 5   
var area int
const a, b, c = 1, false, "str" //多重赋值

area = LENGTH * WIDTH
// 打印结果: 面积为 : 50
fmt.Printf("面积为 : %d", area)
println()
// 打印结果: 1 false str
println(a, b, c)   
}
```


## 四、运算符

**确认过的眼神：可以不用看，因为与其它语言没有区别。**

## 五、函数
套路：
```
func function_name( [parameter list] ) [return_types] {
函数体
}
```

注意可以这么使用即可：
```
// 函数定义
func funcUse(a int, b int, c string) (int, int, string) {
return a*10, b*5, c
}

// 这样来调用
// 函数调用
a, b, c := funcUse(10, 8, "99")
// 打印结果: 100 40 99
fmt.Println(a, b, c)
```

## 六、作用域
Go 语言中变量可以在三个地方声明：
1. 函数内定义的变量称为局部变量
2. 函数外定义的变量称为全局变量
3. 函数定义中的变量称为形式参数

## 七、数组
套路：
> var variable_name [SIZE] variable_type

简单的使用：
```
// 数组
func arrayUse() {
var balance = [...]float32{1000.0, 2.0, 3.4, 7.0, 50.0}
balance[4] = 50.0

var j = 0
/* 输出每个数组元素的值 */
for j = 0; j < 5; j++ {
fmt.Println("balance[", j, "] = ", balance[j])
}

/** 打印结果
balance[ 0 ] =  1000
balance[ 1 ] =  2
balance[ 2 ] =  3.4
balance[ 3 ] =  7
balance[ 4 ] =  50
*/
}
```

## 八、指针
这里的指针与 C 语音的指针没哟多大的差别，只是在定义的时候那个小星星的位置需要注意一下就可以：

简单的使用：
```
// 指针
func pointerUse() {
var a = 3
var pointer *int 

if (pointer != nil) {
fmt.Println("pointer 有值")
} else {
fmt.Println("空指针")
} // 打印结果: 空指针

pointer = &a
if (pointer == nil) {
fmt.Println("空指针")
} else {
fmt.Println("pointer 有值")
} // 打印结果: pointer 有值

// 修改 a 的值
a = 10

// 打印结果: 10
fmt.Println(*pointer)
}
```

## 九、结构体
套路：
```
type struct_variable_type struct {
member definition;
member definition;
...
member definition;
}
```

简单使用：
```
// 定义一个结构体
type Books struct {
title string
author string
subject string
book_id int
}

// 结构体
func structUse() {
// 创建一个新的结构体
fmt.Println(Books{"Go 语言", "www.runoob.com", "Go 语言教程", 6495407})

// 也可以使用 key => value 格式
fmt.Println(Books{title: "Go 语言", author: "www.runoob.com", subject: "Go 语言教程", book_id: 6495407})

// 忽略的字段为 0 或 空
fmt.Println(Books{title: "Go 语言", author: "www.runoob.com"})
}

/** 打印结果:
{Go 语言 www.runoob.com Go 语言教程 6495407}
{Go 语言 www.runoob.com Go 语言教程 6495407}
{Go 语言 www.runoob.com  0}
*/
```

结构体作为函数的参数：
```
func printBook( book *Books ) {
fmt.Printf( "Book title : %s\n", book.title);
fmt.Printf( "Book author : %s\n", book.author);
fmt.Printf( "Book subject : %s\n", book.subject);
fmt.Printf( "Book book_id : %d\n", book.book_id);
}
```

以上是指针传参，也可以之传参，两种方式看上去是没有区别的，但是指针传参能修改具体的值。

## 十、切片(Slice)
这个功能就厉害了，有点像 iOS 中的可变数组，更向散列数据表。
套路：
```
var identifier []type
```

如：**s :=[] int {1,2,3 }**

直接初始化切片，[]表示是切片类型，{1,2,3}初始化值依次是1,2,3.其cap=len=3
简单使用：
```
// 打印切片
func printSlice(x []int){
fmt.Printf("len=%d cap=%d slice=%v\n",len(x),cap(x),x)
}

// 切片
func sampleSlipeUse() {
// 创建切片
// var numbers = make([]int,3,5)
numbers := []int{0,1,2,3,4,5,6,7,8}
// 打印切片
printSlice(numbers)
// 打印结果: len=9 cap=9 slice=[0 1 2 3 4 5 6 7 8]

// 剪切切片
number1 := numbers[2:]
number2 := numbers[2:5]

// 打印结果: len=7 cap=7 slice=[2 3 4 5 6 7 8]
printSlice(number1)
// 打印结果: len=3 cap=7 slice=[2 3 4]
printSlice(number2)

// 同时添加多个元素
number2 = append(number2, 21,31,41)
// 打印结果: len=6 cap=7 slice=[2 3 4 21 31 41]
printSlice(number2)
}
```

注意打印切片使用的是 **%v**。

## 十一、范围(Range)
这个 **range** 不是一种数据类型，而是一种标准。
> Go 语言中 range 关键字用于 for 循环中迭代数组(array)、切片(slice)、通道(channel)或集合(map)的元素。在数组和切片中它返回元素的索引和索引对应的值，在集合中返回 key-value 对的 key 值。

简单使用：
```
func rangeUse() {
// 这是我们使用range去求一个slice的和。使用数组跟这个很类似
nums := []int{2, 3, 4}
sum := 0
for _, num := range nums {
sum += num
}
fmt.Println("sum:", sum)
// 在数组上使用range将传入index和值两个变量。上面那个例子我们不需要使用该元素的序号，所以我们使用空白符"_"省略了。有时侯我们确实需要知道它的索引。
for i, num := range nums {
if num == 3 {
fmt.Println("index:", i)
}
}
// range也可以用在map的键值对上。
kvs := map[string]string{"a": "apple", "b": "banana"}
for k, v := range kvs {
fmt.Printf("%s -> %s\n", k, v)
}
// range也可以用来枚举Unicode字符串。第一个参数是字符的索引，第二个是字符（Unicode的值）本身。
for i, c := range "go" {
fmt.Println(i, c)
}
}

/** 打印结果
sum: 9
index: 1
a -> apple
b -> banana
0 103
1 111
*/
```
莫名的感觉很像 Swift 中的元组的用法。

## 十二、Map(集合)
就是 iOS 中的字典。
套路：
```
/* 声明变量，默认 map 是 nil */
var map_variable map[key_data_type]value_data_type

/* 使用 make 函数 */
map_variable := make(map[key_data_type]value_data_type)
```

简单使用：
```
// map
func mapUse() {
// 定义一个集合
var countryCapitalMap map[string]string 
// 创建集合实例
countryCapitalMap = make(map[string]string)

// map插入key - value对,各个国家对应的首都 
countryCapitalMap [ "France" ] = "Paris"
countryCapitalMap [ "Italy" ] = "罗马"

// 使用键输出地图值 
for country := range countryCapitalMap {
fmt.Println(country, "首都是", countryCapitalMap [country])
}

/*查看元素在集合中是否存在 */
captial, ok := countryCapitalMap [ "美国" ] /*如果确定是真实的,则存在,否则不存在 */
/*fmt.Println(captial) */
/*fmt.Println(ok) */
if (ok) {
fmt.Println("美国的首都是", captial)
} else {
fmt.Println("美国的首都不存在")
}

fmt.Println("=====删除元素======")

// 删除 : delete() 函数用于删除集合的元素, 参数为 map 和其对应的 key。
/*删除元素*/ 
delete(countryCapitalMap, "France")


for country := range countryCapitalMap {
fmt.Println(country, "首都是", countryCapitalMap [country])
} // 发现已经没有 France 的数据

}

/** 打印结果:
France 首都是 Paris
Italy 首都是 罗马
美国的首都不存在
=====删除元素======
Italy 首都是 罗马
*/
```

## 十三、递归函数
递归函数是一种特有的函数，不局限于某种语言。
套路：
```
func recursion() {
recursion() /* 函数调用自身 */
}
```

简单使用：
```
// 阶乘
func Factorial(n uint64) (uint64) {
if n > 0 {
return n * Factorial(n-1);
}
return 1
}

// 斐波那契数列
func fibonacci(n int) int {
if (n < 2) {
return n
}

return fibonacci(n-2) + fibonacci(n-1)
}

// recursion
func recursionUse() {
// 阶乘
var i int = 15
fmt.Printf("%d 的阶乘是 %d\n", i, Factorial(uint64(i)))
// 打印结果: 15 的阶乘是 1307674368000

// 斐波那契数列
for i = 0; i < 10; i++ {
fmt.Printf("%d\t", fibonacci(i))
} // 打印结果: 0    1    1    2    3    5    8    13    21    34
}
```

## 十四、类型转换
套路：
> type_name(expression)

简单使用：
```
// 类型转换
func typeChangedUse() {
var sum int = 17
var count int = 5
var mean float32

mean = float32(sum)/float32(count)
// 打印结果: mean 的值为: 3.400000
fmt.Printf("mean 的值为: %f\n",mean)
}
```

## 十五、语言接口
> Go 语言提供了另外一种数据类型即接口，它把所有的具有共性的方法定义在一起，任何其他类型只要实现了这些方法就是实现了这个接口。


套路：
```
/* 定义接口 */
type interface_name interface {
method_name1 [return_type]
method_name2 [return_type]
method_name3 [return_type]
...
method_namen [return_type]
}

/* 定义结构体 */
type struct_name struct {
/* variables */
}

/* 实现接口方法 */
func (struct_name_variable struct_name) method_name1() [return_type] {
/* 方法实现 */
}
...
func (struct_name_variable struct_name) method_namen() [return_type] {
/* 方法实现*/
}
```

**接口**：很像 iOS 中的协议与其它语言中的抽象类，只定义（声明）不实现。

```
// 定义接口
type Phone interface {
call()
}

// 结构体定义 诺基亚
type NokiaPhone struct {

}

// 函数实现
func (nokiaPhone NokiaPhone) call() {
fmt.Println("I am Nokia, I can call you!")
}

// 结构体定义 苹果
type IPhone struct {

}

// 函数实现
func (iPhone IPhone) call() {
fmt.Println("I am iPhone, I can call you!")
}

// 接口
func interfaceUse() {
var phone Phone

phone = new(NokiaPhone)
// 打印结果: I am Nokia, I can call you!
phone.call()

phone = new(IPhone)
// 打印结果: I am iPhone, I can call you!
phone.call()
}
```

## 十六、错误处理
> Go 语言通过内置的错误接口提供了非常简单的错误处理机制。

error类型是一个接口类型，这是它的定义：
```
type error interface {
Error() string
}
```

一个简单的例子，被除数不能为 0， 如果为 0， 则抛出异常。
```
// 定义一个 DivideError 结构
type DivideError struct {
dividee int
divider int
}

// 实现 `error` 接口
func (de *DivideError) Error() string {
strFormat := `
Cannot proceed, the divider is zero.
dividee: %d
divider: 0`

return fmt.Sprintf(strFormat, de.dividee)
}

// 定义 `int` 类型除法运算的函数
func Divide(varDividee int, varDivider int) (result int, errorMsg string) {
if varDivider == 0 {
dData := DivideError{
dividee: varDividee,
divider: varDivider,
}
errorMsg = dData.Error()
return
} else {
return varDividee / varDivider, ""
}
}

func errorUse() {
// 正常情况
if result, errorMsg := Divide(100, 10); errorMsg == "" {
fmt.Println("100/10 = ", result)
}
// 当被除数为零的时候会返回错误信息
if _, errorMsg := Divide(100, 0); errorMsg != "" {
fmt.Println("errorMsg is: ", errorMsg)
}
}

/** 打印结果:
100/10 =  10
errorMsg is:  
Cannot proceed, the divider is zero.
dividee: 100
divider: 0
*/

```

## 十七，总结
学习 [Go 语言教程](http://www.runoob.com/go/go-tutorial.html)。整个流程花了3个半小时，这个速度算是中等吧。对 Go 语言有了一个初步的认识。


# 1 数据

## 1.1 go 特性：

静态语言：强类型语言

go,java,c++,c#

动态语言：弱类型语言

JavaScript,php,python



数据声明不使用就会报错

GoLand快捷键 ：ctrl+alt+l  格式化

## 1.2 变量声明

go语言中非全局变量申明后必须使用，不然会编译报错

**1.声明赋值**

```go
var num1 int
num1 = 15
```

```go
var num2 int =15
```

**2.类型推断**

```go
var name ="xtt"
```

**3.简短声明**

只能在函数内使用

```go
num：= 1
```

**4.批量申明**

一般是全局变量

```go
var(
   name string // ""
   age int    // 0
   isOk bool  //false
)
```

## 1.3 常量

```go
const a = 1
fmt.Printf("%d",a);
```

批量声明，如果某一行声明后没有复制，默认就和上一行一致

```
const (
   n1 = 200
   n2 = 404
)
```

### iota

是go语言中的常量计数器，只能在常量的表达式中使用

在const出现的时候，就会置0。每增加一行常量声明就会增加1

```go
const (
   a1 = iota	//0
   a2			//1
   a3			//3
)
```

```go
const (
   b1 = iota  	 //0
   b2 = iota 	 //1
   _       		 //2
   b3       	 //3
)
```

```go
//插队
const (
   c1 = iota  //0
   c2 = 100	  //100
   c3 = iota  //2
)
```

```go
const (
   d1,d2 = iota+1,iota+2	// 1, 2
   d3,d4 = iota+1,iota+2	// 2, 3
)
```

# 2 基本数据类型

## 2.1 变量初始化

-  整型和浮点型变量的默认值为 0 和 0.0。

-  字符串变量的默认值为空字符串。

-  布尔型变量默认为 bool。

-  切片、函数、指针变量的默认为 nil。

  1. 变量初始化的标准格式

     **var 变量名 类型 = 表达式**

     2.编译器推导类型的格式

     ​	var hp =100 

     3.短变量申明并初始化

     ​	hp :=100

### 整型

​	Go语言同时提供了有符号和无符号的整数类型，其中包括 **int8、int16、int32 和 int64 ** 四种大小截然不同的有符号整数类型，分别对应 8、16、32、64 bit（二进制位）大小的有符号整数，与此对应的是 **uint8、uint16、uint32 和 uint64**四种无符号整数类型。

### 浮点

常量 math.MaxFloat32 表示 float32 能取到的最大数值，大约是 3.4e38；

常量 math.MaxFloat64 表示 float64 能取到的最大数值，大约是 1.8e308；

float32 和 float64 能表示的最小值分别为 1.4e-45 和 4.9e-324。

float32类型不能直接赋值给float64类型

```
f:= float32(1.23)
f:= 1.23
```

### 布尔值

```
var b2 bool
b1:=true
```

### 字符串

双引号包裹“ ”

单引号包裹是字符''

单独的字母,汉字,符号表示一个字符

**字符串拼接符“+”**

字符串是基于UTF-8字符访问

这种双引号字面量不能跨行，如果想要在源码中嵌入一个多行字符串时，就必须使用``反引号，代码如下： 

```go
	const str = `第一行
第二行
第三行\r\n`
	fmt.Println(str)
```

```go
var s1 string
s1 = "王"
fmt.Println(s1)
s2 := `helloworld`
fmt.Println(s2)
```

```go
v1 := 'A'
v2 := "A"
v3 := '中'
fmt.Printf("%T,%d\n",v1,v1)
fmt.Printf("%T,%s\n",v2,v2)
fmt.Printf("%T,%c\n",v3,v3)
//int32,65
//string,A
//int32,中
```

### 字符

 Go语言的字符有以下两种：

-  一种是 uint8 类型，或者叫 byte 型，代表了 ASCII 码的一个字符。

-  另一种是 rune 类型，代表一个 UTF-8 字符，当需要处理中文、日文或者其他复合字符时，则需要用到 rune 类型。rune 类型等价于 int32 类型。

  ```
  var ch1 byte = 65 //
  var ch2 byte = '\x41'      //（\x 总是紧跟着长度为 2 的 16 进制数）
  var ch3 byte ='A'
  fmt.Printf("%c\n",ch1)
  fmt.Printf("%c\n",ch2)
  fmt.Printf("%c\n",ch3)
  //输出结果为
  //A
  //A
  //A
  ```

在书写 Unicode 字符时，需要在 16 进制数之前加上前缀`\u`或者`\U`。因为 Unicode 至少占用 2 个字节，所以我们使用 int16 或者 int 类型来表示。如果需要使用到 4 字节，则使用`\u`前缀，如果需要使用到 8 个字节，则使用\U前缀。

```GO
var ch int = '\u0041'
var ch2 int = '\u03B2'
var ch3 int = '\U00101234'
fmt.Printf("%d - %d - %d\n", ch, ch2, ch3) // integer
fmt.Printf("%c - %c - %c\n", ch, ch2, ch3) // character
fmt.Printf("%X - %X - %X\n", ch, ch2, ch3) // UTF-8 bytes
fmt.Printf("%U - %U - %U", ch, ch2, ch3)   // UTF-8 code point
//65 - 946 - 1053236
//A - β - 􁈴
//41 - 3B2 - 101234
//U+0041 - U+03B2 - U+101234
```

 Unicode 包中内置了一些用于测试字符的函数，这些函数的返回值都是一个布尔值，如下所示（其中 ch 代表字符）：

-  判断是否为字母：unicode.IsLetter(ch)
-  判断是否为数字：unicode.IsDigit(ch)
-  判断是否为空白符号：unicode.IsSpace(ch)

  ## 2.1 匿名变量

__匿名变量的特点是一个下画线'_'，__本身就是一个特殊的标识符，被称为空白标识符。它可以像其他标识符那样用于变量的声明或赋值（任何类型都可以赋值给它），但任何赋给这个标识符的值都将被抛弃，因此这些值不能在后续的代码中使用，也不可以使用这个标识符作为变量对其它变量进行赋值或运算。使用匿名变量时，只需要在变量声明的地方使用下画线替换即可

## 2.2 变量的作用域

Go语言程序中全局变量与局部变量名称可以相同，但是函数体内的局部变量会被优先考虑。   

## 2.3 数据类型转换

**bool类型无法转化成其他数据类型**

```go
a := 5.0  
b := int(a)
```

```go
var a int8
a = 10

var b int16
b = int16(a)
fmt.Println(a, b)

f1 :=4.13
var c int
c = int(f1)
fmt.Println(f1,c)
```

# 3 输入输出

## 3.1 输出

```go
Print()  //打印
Printf()	//格式化打印
Println()	//格式化之后换行
```

格式化打印占位符号

```shell
%v  原样输出

%T 打印类型

%t bool类型

%s 字符串

%f 浮点

%d 10进制整数

%b   二进制的整数

%o	八进制

%x   %X  10进制

	%x：0-9  a-f

	%X:  0-9  A-F

%c  打印字符

%p  打印地址
```

## 3.2 输入

Scanln：阻塞式

```go
var x int
var y float64
fmt.Println("请输入一个整数，一个浮点类型")
fmt.Scanln(&x,&y)
fmt.Println(x,y)
```

bufio包

```go
package main

import "fmt"

func main() {
   var x int
   var y float64
   fmt.Println("请输入一个整数，一个浮点类型")

   fmt.Scanf("%d,%f", &x, &y)
   fmt.Printf("x:%d,y%f",x,y)
}
```


# 4 流程控制

## if else

```go
age:=10
if age >20{
   fmt.Printf("1111")
}else {
   fmt.Printf("2222")
}
```

```go
age:=12
if age >20{
   fmt.Printf("大于20")
}else if age >10 {
   fmt.Printf("大于10")
}else {
   fmt.Printf("小于10")
}
```

```go
if num := 4; num > 0 {
   fmt.Println("111")
} else {
   fmt.Println("222")
}
```

## for循环

```go
//基本格式
for i := 0; i < 10; i++ {
   fmt.Printf("%d ",i)
}
```

```go
i := 0
for ; i < 10; i++ {
   fmt.Printf("%d ",i)
}
```

```go
i := 5
for i < 10{
   fmt.Printf("%d ",i)
   i++
}
```

```go
//死循环
for {
   fmt.Printf("111")
}
```

```go
//for range遍历
s:="hello"
for i,v:=range s {
   fmt.Printf("%d,%c\n",i,v)
}
```

```go
//跳出死循环
for i :=0;i <10;i++{
   if i== 5{
      break
   }
   fmt.Println(i)
}
fmt.Println("over")
```

```go
for i :=0;i <10;i++{
   if i== 5{
      continue//继续下一次循环
   }
   fmt.Println(i)
}
fmt.Println("over")
```

break 和continue

```go
i := 0
for ;i < 10;i++{
   if i == 5{
      continue  // break
   }
}
fmt.Println(i)
//break  	直接跳出循环  输出打印5
//continue	结束当前循环	输出打印10
```

## switch

Go语言改进了 switch 的语法设计，case 与 case 之间是独立的代码块，不需要通过 break 语句跳出当前 case 代码块以避免执行到下一行，示例代码如下： 

fallthrough 会直接进行下一个case,只能在case的最后一行

```
var n =5
switch n {
case 1: fmt.Printf("1") 
case 2: fmt.Printf("2") 
case 3: fmt.Printf("3")
default:fmt.Printf("err")
}
```

# 5 随机数

时间

```
t ：=time.Now()
```

包math/rand

伪随机数，根据一定的算法公式算出来的

设置种子数

```go
rand.Seed(time.Now().UnixNano())
for i:=0;i<9;i++{
   num := rand.Intn(10)
   fmt.Println(num)
}
```

```go
num1 := rand.Int()%10+1
fmt.Println(num1)
```

```go
num := rand.Intn(10) //生成随机数是0～n-1之间
```



# 6 数组

申明  

var 数组名 [长度] 数据类型

var 数组名 = [长度]  数据类型 { 元素1 ,元素2...}

数组名 := [...]数据类型{元素1,元素2}

```go
var a1[3] bool
var a2[3] bool
var a3[3] int
for i:=0;i<3;i++{
   fmt.Printf("%T ",a1[i])
   fmt.Printf("%T ",a2[i])
}
//
//	var a1[3] bool
//	var a2[3] bool
//	for i:=0;i<3;i++{
//		fmt.Println(a1[i],a2[i])
//	}
```

## 6.1 初始化

```go
a1 = [3]bool{true, true, true}
```

```go
a1 := [10]int{0, 10, 2, 3}
```

根据初始化自动推断数组长度

```go
a1 := [...]int{0, 10, 2, 3}
```

根据索引

```go
a1 := [5]int{0: 1, 4: 2}
```

容量cap() 实际存储的长度len()

```go
var nums [12] int
rand.Seed(time.Now().UnixNano())
for i:=0;i<9;i++{
   num := rand.Intn(10)
   nums[i]  = num
}
fmt.Print("数组的长度",len(nums))
fmt.Print("数组的容量",cap(nums))
//因为数组定长，长度和容量相同
```

## 6.1 遍历

根据索引遍历

```go
a1 := [...]string{"北京", "上海", "南极"}
for i := 0; i < len(a1); i++ {
   fmt.Println(a1[i])
}
```

for range遍历

```go
a1 := [...]string{"北京", "上海", "南极"}
for i, v := range a1 {
   fmt.Println(i, v)
}
```

```go
//数组练习 对数组求和
a1 := [...]int{1, 3, 4, 5, 6}
sum := 0
for _,v :=range a1{
   sum = sum + v
}
fmt.Println(sum)
```

```go
//返回两元素和为8的索引
a1 := [...]int{1, 3, 5, 7, 8}
for i := 0; i < len(a1)/2; i++ {
   for j := 0; j < len(a1); j++ {
      if a1[i]+a1[j] == 8 {
         fmt.Printf("%d,%d\n", i, j)
      }
   }
}
```

```go
//数组排序
var a = [...]int{3, 1, 5, 6, 2, 7}
sort.Ints(a[:])
fmt.Println(a)
```

## 多维数组

```go
var a [3][2]int
a = [3][2]int{
   [2]int{1, 2},
   [2]int{3, 4},
   [2]int{5, 6},
}
for i, v := range a {
   fmt.Println(i, v)
}
```

```go
var a [3][2]int
a = [3][2]int{
   [2]int{1, 2},
   [2]int{3, 4},
   [2]int{5, 6},
}
for _, v1 := range a {
   for _,v2 := range v1{
      fmt.Printf("%d",v2);
   }
}
```

# 7 切片(Slice)

## 7.1 切片定义

拥有相同元素可变长度的序列

```go
var a [] int //存放int类型元素的切片
a = []int{1, 2, 3}
fmt.Printf("%d", a)
```

由数据得到切片

```go
a := []int{1, 2, 3, 4, 5, 6, 7, 8, 9}
b := a[0:4]
fmt.Printf("%d\n", a)
fmt.Printf("%d", b)
```

```go
//第0切到6
a := []int{1, 2, 3, 4, 5, 6, 7, 8, 9}
b := a[:6]
```

```go
//第三切到最后一个
a := []int{1, 2, 3, 4, 5, 6, 7, 8, 9}
b := a[3:]
```

```go
a := []int{1, 2, 3, 4, 5, 6, 7, 8, 9}
b := a[:]
```

```go
//切片再切片,，切片的容量是指底层数组的容量
	a := []int{1, 2, 3, 4, 5, 6, 7, 8, 9}
	b := a[:3]
	c := b[:2]
	fmt.Printf("%d,%d,%d\n", a, cap(a), len(a))
	fmt.Printf("%d,%d,%d\n", b, cap(b), len(b))
	fmt.Printf("%d,%d,%d\n", c, cap(c), len(c))
//运行结果
//[1 2 3 4 5 6 7 8 9],9,9
//[1 2 3],9,3
//[1 2],9,2
```
切片指向一个底层数组

切片的长度就是它元素的个数

切片的容量是指底层数组从切片的第一个元素到最后一个元素的数量

切片是引用类型，都指向了底层的一个数组



## 7.2切片扩容

append：调用append必须用原来的切片变量接收返回值，二倍速扩容

```
a = append(a,0)
```

```go
//添加切片
a = append(a,b...)
```

```go
copy(a2,a1)
```

```go
//将索引为1的删除
a1 = append(a1[:1],a1[2:]...)
```

```go
var a = make([]int, 0, 10)  //创建切片，长度为5，容量为10
for i := 0; i < 10; i++{
   a = append(a,i)
}
fmt.Println(a)
//输出 0~9
```

```go
var a = make([]int, 5, 10)  //创建切片，长度为0，容量为10
for i := 0; i < 10; i++{
   a = append(a,i)
}
fmt.Println(a)
//先输出5个0，再输出0~9
```
## 7.3 切片使用
make创建
```go
s3 := make([]int, 3,8) //3是长度,8是容量
```
不能直接通过下标索引访问超出长度的数据
append
```go
s:=append(s,1,2)//将数据1，2添加到切片后
s = append(s,s...)//将s的数据复制到s后
```
# 运算符号

Go语句自增自减只能当当单独的语句，不能赋值操作

not：取反

# 指针

Go语言中不存在指针操作，只需要记住两个符号

1.&：取地址

2.*:根据地址取值

```go
n := 18
p := &n
m := *p
fmt.Println(p)
fmt.Printf("%T\n",p)
fmt.Println(m)
fmt.Printf("%T\n",m)
//输出结果
//0xc0000a4010
//*int
//18
//int
```
```go
var a1 *int //nil pointer
var a2 = new(int)
*a2 = 10
fmt.Println(a1)
fmt.Println(*a2)
//输出结果
//<nil>
//10
```

# make和new的区别

1.make和new都是用来申请内存

2.new很少用,一般都是用来给基本数据类型申请内存，string\int,返回对应类型的指针

3.make是用来给slice\map\chan申请内存的,make函数返回的是对饮类型的引用

# map

map是一种无序的基于key-value的数据结构，Go语言中的map是引用类型，必须初始化才能使用。

```go
var m1 map[string]int
fmt.Println(m1 == nil)        //还没有初始化(没有在内存中开辟空间)
m1 = make(map[string]int, 10) //要估算好该map容量,避免在程序运行期间动态扩容
m1["理想"] = 18
m1["啊"] = 35
fmt.Println(m1)
fmt.Println(m1["理想"])
```

```go
//事例
var m1 map[string]int
fmt.Println(m1 == nil)        //还没有初始化(没有在内存中开辟空间)
m1 = make(map[string]int, 10) //要估算好该map容量,避免在程序运行期间动态扩容
m1["理想"] = 18
m1["啊"] = 35
fmt.Println(m1)
fmt.Println(m1["理想"])
value,ok := m1["娜扎"]
if !ok{
   fmt.Println("查无此key")
}else {
   fmt.Println(value)
}
```
# 指针

```
package main

import "fmt"

// 交换函数
func swap(a, b *int) {
   // 取a指针的值, 赋给临时变量t
   t := *a
   // 取b指针的值, 赋给a指针指向的变量
   *a = *b
   // 将a指针的值赋给b指针指向的变量
   *b = t
}

func main() {
   a := 5
   b := 6
   swap(&a,&b)
   fmt.Println(a)
   fmt.Println(b)
}
```

 Go语言还提供了另外一种方法来创建指针变量

new(类型)

```
	str := new(string)
	*str = "Go语言教程"

	fmt.Println(*str)
```


# 算法

## 排序

### 冒泡排序

```go
var nums[10] int
for i:=0;i<9;i++{
    nums[i]= rand.Intn(10)
}
fmt.Println(nums)
for i :=0; i< len(nums);i++{
    for j :=i;j < len(nums) ;j++  {
        if nums[i] > nums[j]{
            nums[i],nums[j] = nums[j],nums[i]
        }
    }
}
fmt.Println(nums)
```
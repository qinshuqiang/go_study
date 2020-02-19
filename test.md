# 数据类型

**数据类型的作用：**告诉编译器这个变量应该以多大的内存存储

#### 命名规范

- 字母、下划线、数字组成
- 开头不能以数字开头
- 名字不能是关键字
- 区分大小写

#### 声明变量的注意事项

- 导入包必须要使用
- 函数内的变量声明了必须要使用
- 同一个{}内不能重复声明变量
- 声明的变量默认值为0
- 变量需要声明后才能使用

#### 变量的声明方式

```go

	var a int      //声明变量
	var b int = 10 //声明并初始化变量
	e := 10        //自动推导类型，通过初始化的值确定类型
	var (
		c int
		d float64
	)// 全局声明多个变量
	f, g := 10, 20 ///多重声明变量并且赋值
	_ := 10        //匿名变量
	
```

#### 常量

```go

	const a int = 20   //常量不可修改，不可重复声明
	const a  = 20.1   //类似变量的声明a:=10，不过声明的是常量
	const (
		c int
		d float64
	)// 全局声明多个常量
```

#### iota 枚举

1、iota 是常量自动生成器，每隔一行，自动累加1

2、iota给常量赋值使用

3、iota遇到const重置为0



## 数据类型分类

Go语言内置一下这些基础类型：

|   名称   | 类型         | 长度 | 零值  | 说明                                  |
| :------: | ------------ | ---- | ----- | ------------------------------------- |
| 布尔类型 | bool         | 1    | false | 其值不为true则为false，不可以数字表示 |
|  字节型  | byte         | 1    | 0     | uint8的别名                           |
| 字符类型 | rune         | 4    | 0     | 专用于存储Unicode编码，等价于uint32   |
|   整型   | int,uint     | 4或8 | 0     | 32位或64位                            |
|          | int8,uint8   | 1    | 0     | -128~127,0~255                        |
|          | int16,uint16 | 2    | 0     | -32768~32767,0~65535                  |
|          | int32,uint32 | 4    | 0     | -21亿～21亿，0~42亿                   |
|          | int64,uint64 | 8    | 0     |                                       |
|  浮点型  | float32      | 4    | 0.0   | 小数位精确到7位                       |
|          | float64      | 8    | 0.0   | 小数精确到十五位                      |
| 复数类型 | complex64    | 8    |       |                                       |
|          | complex128   | 16   |       |                                       |
|   整数   | uintptr      | 4或8 |       | 足以存储指针的uint32或uint64整数      |
|  字符串  | string       |      | ""    | utf-8字符串                           |

 

#### 类型转换

**不兼容类型**

布尔类型不能转换为整型，整型也不能转换位布尔类型

- 字符型本质上就是整型，可以转换

#### 类型别名

```go
	type bigint int64 //声明一个类型别名
	var a bigint      //声明一个bigint别名的变量，等价于int64
	fmt.Println(a)    //输出默认值0
	type (  //批量声明类型别名
		long int64
		char byte 
	) 
```

# 流程控制

## 选择结构

### if语句

```go
	
	if name:="小明";name=="小明" {
		fmt.Println("小明")
	}else if name=="小花" {
		fmt.Println("小花")
	}else {
		fmt.Println("不是小明也不是小花")
	}
```

#### switch语句

```go

	
	num := 1
	switch num { //switch 后面写的是变量本身
	case 1:
		fmt.Println(1)
		//break  //go语言默认就有
		//fallthrough  //加如有这个关键字，不跳出此switch语句，后面的无条件执行
	case 2:
		fmt.Println(2)
	default:
		fmt.Println("不是1或者2")
	}
	switch {
	case num > 1:
		fmt.Println("可以不写条件")
	}

```

## 循环语句

#### for循环

```go

	for i:=0;i<10 ;i++  {
		fmt.Println(i)
	}
```

#### range迭代

```go

	str := "abc"
	for index, data := range str {
		fmt.Println(index)
		fmt.Println(data)
	}
	for index := range str {  //默认放弃第二个返回值
		fmt.Println(index)

	}
	for _, data :=range str{  //第一个不需要使用的返回值用匿名变量接收
		fmt.Println(data)
	}
```

## 跳转语句

#### break和continue

```go

	i:=0
	for{//for不写任何条件，则是死循环
		i++
		if i==3 {
			break  //如果i=3就终止循环循环
			//continue  //  如果i=3跳过本次循环，进行下一次循环
		}
		fmt.Println(i)
	}
```

#### goto

```go

	//goto 可以用在任何地方，但是不能跨函数使用
	fmt.Println(1111111111111111111)
	goto End  //goto是关键字 ,End 是自定义的名字
	fmt.Println(2222222222)
	End:  //直接调到此处执行，不执行上一行
		fmt.Println(33333333333)
```

# 函数

#### 无参数无返回值的函数：

```go
func f1()  {
	fmt.Println("这个是没有参数和返回值的函数")
}
```

#### 有参数无返回值的函数

```go
func f1(i int)  {
	fmt.Println(i)
}
```

#### 无参数有一个返回值的函数

```go
func f1 ()(num int){
	//给返回值起名，也可以不起名
	//系统定义这个num变量，直接使用即可 ，return时默认返回这个num
	num=666
	return 
}
```

#### 无参数多个返回值的函数

```go
	
	var f2= func() (a ,b  ,c int){
		a,b,c=111,222,333
		return a,b,c
	}
	d,e,f:=f2()
```

#### 有参数并且有返回值的函数

```go

func f1(a,b int)(max,min int)  {
	if a<b {
		return b,a
	}else {
		return a,b
	}
}
```



#### 不定参数类型

```go
	var f2 = func(a int,args ...int) { //传递的实参可以是0或者多个
		fmt.Println(len(args))
		fmt.Println(a)
		//取值：
		for i := 0; i < len(args); i++ {
			fmt.Printf("args[%d]=%d\n", i, args[i])
		}
		//取值
		for i, data := range args{
			fmt.Printf("args[%d]=%d\n", i, data)
		}
		arr:=args[:2]  //从0-2  不包括2
		arr=args[2:]//从2 到结尾，包括2
		fmt.Println(arr)
	}
	f2(1, 2, 3)
```

## 递归函数

```go

func a(i int)(sum int) {
	if i==0 {
		return sum
	}
	sum=sum+i
	return sum+a(i-1)
}
a(3)//返回3+2+1
```

## 匿名函数

```go

	f1:= func() {
		fmt.Println(":这个是匿名函数")
	}
```

## 闭包

```go

	a:=10
	func() {
		a=a+10
		fmt.Println(a)
	}()
	fmt.Println(a)//20
```

## defer

defer只能放在函数的内部使用

defer是延迟调用的，等该代码作用域执行结束后执行

```go

	//1234为输出顺序，后进先出
	test:=func (x int)  {
		result:=100/x
		fmt.Println(result)
	}
	defer fmt.Println(4)
	defer fmt.Println(3)
	defer fmt.Println(2)
	test(0)   //此代码会报错，程序报错defer依然会执行defer
	fmt.Println(1)
```

# 命令行

```go

	list := os.Args   //获取执行时命令行的参数
	n:=len(list)
	fmt.Println(n)
	for i:=0;i<n ;i++  {
		fmt.Println(list[i])  //输出的是命令行输入的参数
	}
```

# 工程管理

- 分文件编程（多个源文件），必须放在src目录

- 设置GOPATH环境变量

- 同一个目录，包名必须一样

- go env查看go相关的环境路径

- 同一个目录，调用别的文件的函数，直接调用即可，无需包名引用

### 同目录的引用

```go
package main

import "fmt"

func main() {
	test() //直接调用包b的函数即可
	fmt.Println(1)
}

```

```go
package main

import "fmt"

func test()  {
	fmt.Println("这个是包b")
}
```

### 不同目录的包引用

- 不同目录，包名不一样
- 调用不同包里面的函数，格式是：包名.函数
- 被调用的包的函数需要想外暴露，需要大写

```go
package main

import (
	"fmt"
	"add"
)

func main() {
	add.Add() 
	fmt.Println(1)
}

```

```go
package add

import "fmt"

func Add()  {
	fmt.Println("这个是不同目录的包b")
}
```




## 引入包的方式

```go
import (
   "fmt"
   "os"
)
//import _ "os"

//import os "os"

//import . "fmt"
```


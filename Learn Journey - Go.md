# 类型
* bool
* string
* int/8/16/32/64\
  int不指定时默认按系统位数32或64
* unit/8/16/32/64\
  uint不指定时默认按系统位数32或64
* byte\
  unit8的别名
* rune\
  int32 的别名
* float32/64
* complex64/128

## 零值
未赋值的变量会自动赋值零值，数值类型为0，布尔类型为false，字符串为""

## 类型转换
T(v) 将v转换为T类型



# struct | 结构体
```go
type test struct{
    X int
    Y int
}

func main(){
    v:= test{1,2}
    p:= &v
    p.X = 10
}
```



# 函数

## defer
将语句推迟到函数返回后执行\
多个defer会压入栈中后进先出执行



# 数组

* len\
  获取数组长度，数组存在的元素数量
* cap\
  获取数组容量，数组可容纳的元素数量

## 切片
数组切片是数组的一段引用，更改切片会更改底层数组

```go
var a [10]int
p := a[0:10]
p = a[:]
```

对于切片而言，长度是切片实际长度，而容量则是切片的第1个元素到底层数组最后一个元素的长度

* make\
  创建切片的一种方法
  ```go
  a:= make([]int, 0, 5) //[]
  b:= make([]int, 5)    //[0,0,0,0,0]
  ```



# 映射
类似于键名数组
```go
type Vertex struct{
    lat,lon float64
}

var m = map[string]Vertex{
    "bell tower": {1.0,0.01}
}

z,p := m["isExists"]    //z为Veretex零值，p为false
```



# 反射

* reflect.ValueOf(T)\
  返回一个对象的元数据


## 类型判断
可使用switch对interface{}进行类型判断
```go
switch r:= r.(type){  //此时r会从interface{} 转为指定的类型
  case someType:
    fmt.PrintF("%v", r.Field)
}
```



# flag
为命令行提供参数功能
```go
var (
	port = flag.Int("port", 50051, "The server port")
)
```
```sh
go run main.go -port=55000
```

flag数据类型可以设为int、bool、string
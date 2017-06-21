---
title: golang中对象方法作为函数指针
date: 2017-05-19 11:10:15
categories: Technology
tags: [Linux,golang,pointer]
---

<!-- toc -->

裸函数作为指针不是什么新鲜事，其它的语言也是可以的，golang当然也可以，譬如
```go
type FT func(int)
func Fa(int){}
func Test(FT){}

Test(Fa) //pass function as parameter
```

但是像下面这样，对象实例的方法是否可以作为函数参数传递呢？
```golang
type A struct {
   // ...
}

func (a *A) Foo(bar, baz int) {}

b := new(A)
foob := b.Foo  // foob is of type func(int, int)
```

答案是肯定的，而且很智能： 
**当特定对象实例的method作为函数指针时传递时，接受者会保证在调用的时候，调用到是这个对象实例的method，method的任何操作都会针对该对象实例生效，而且不需要传任何类似于this、self指针之类的东西**

**换句话说，对象实例+method 作为绑定的整体传递给接受者的**

通过以下代码可以[验证](https://play.golang.org/p/dCeff53G4t)
```golang
package main

import (
	"fmt"
)


type Outer struct{
	a string
}

func (o *Outer)Hello(in *Inner){
   fmt.Println("Inner:",in,"\tcall\tOuter:",o.a)
}

type Inner struct{
        a string
	cb Cb
}

type Cb func(*Inner)

func (in *Inner)Register(cb Cb){
	in.cb = cb
}

func (in *Inner)Say(){
	in.cb(in)
}


func main() {
	out1 := Outer{a:"out1 instance"}
	out2 := Outer{a:"out2 instance"}
	
	fmt.Println("out1 :",&out1)
	fmt.Println("out2 :",&out2)	
	
	in1 := Inner{a:"int1 instance"}
	
	in1.Register(out1.Hello)
        in1.Say()
	in1.Register(out2.Hello)
	in1.Say()
	
}
	
```
执行起来输出如下结果
```
out1 : &{out1 instance}
out2 : &{out2 instance}
Inner: &{int1 instance 0xc6be0} 	call	Outer: out1 instance
Inner: &{int1 instance 0xc6be0} 	call	Outer: out2 instance
```


参考文章
https://groups.google.com/forum/#!topic/golang-nuts/t1r6px7yGIY
https://github.com/golang/go/issues/2280
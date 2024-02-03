---
title: C语言如何在一个.c源文件里调用另一个源文件中的函数
tags: C语言
abbrlink: 61897
date: 2024-01-05 10:57:17
---


对于C语言来说main函数是程序的入口，当我们要开发一个比较大的程序时，可能会有很多代码，这时候想要为了方便维护通常都采取模块开发，将不同类的模块写到不同的文件中

首先定义一个.h的头文件，如function.h,在里面声明将要实现的函数，如`int add(int a，int b)`;

然后新建一个源文件为`function.c`,在`function.c`的开头添加`#include "function.h"`,然后下面写头文件中已声明的函数的实现。

这样写完了之后，main函数如果要调用这个源文件中的函数，只需要在main函数的开头部分加入`#include<function.h>`，如此这般，main函数调用相应函数的时候就会自动找到程序的实现部分代码了

```c  function.h
# include<stdio.h> 
 
int add(int a,int b);
```

```c function.c
#include "function.h"
int add(int a,int b)
{
   return a+b;
}
```

```c main.c
# include<stdio.h>
# include<function.h>
 
int main()
{
   int a = 1,b =2;
   int c = add(a,b); 
   printf("%d",c);
   return 0;   
}
```
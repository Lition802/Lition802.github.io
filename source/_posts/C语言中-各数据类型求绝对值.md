---
title: C语言中 各数据类型求绝对值
tags: C语言
abbrlink: 42263
date: 2024-01-16 16:47:01
---

C语言中 各数据类型取绝对值需要的不同函数

int->abs()

long ->labs()

float ->fabsf()

double->fabs()

long double->fabsl()

举个例子
``` c
#include<stdio.h>
#include<math.h>
using namespace std;
int main(){
	float a;
	scanf("%f",&a);
	printf("%.2f",fabsf(a));
} 
```
---
title: C语言取数字的每一位
abbrlink: 59073
date: 2023-12-10 13:20:56
tags: C语言
---

常常有将一个正整数各位数字倒序排列或是统计各数字数目的题目，难点就在于如何分离出正整数中的每一位数字，本次以C语言为模板尝试一下。

# 递归法

步骤：
1. 获得该正整数的第一位数字或最后一位数字（考虑到分离出首位数字后接下来的可能为零，因此选择首先分离末位数字）
2. 对分离出一位数字的剩下数字组成的正整数重复上步操作。

```c
#include<stdio.h>
void getNum(int n)
{
   int s=0;
   if(n>0){
    s=n%10;           //分离末位数字
    printf("%d ",s);
    getNum(n/10);     //对剩下数字递归
   }
}
int main()
{
   int n;
   scanf("%d",&n);
   getNum(n);
   return 0;
}
```


# 迭代法

```c
#include<stdio.h>
#include<math.h>
void getNum(int n)
{
    int s;
    int len=(int)log10(n)+1;         //获得n的位数 
    for(int i=0;i<len;i++)
    {
        s=n%10;
        printf("%d ",s);
        n=n/10;
    }
}
int main()
{
    int n;
    scanf("%d",&n);
    getNum(n);
    return 0;
}
```

while循环形式:

```c
int j=0;
while(n>0)
{
    j++;
    n/=10;
} 
```
---
title: C语言求阶乘
abbrlink: 4928
date: 2023-12-27 00:13:38
tags: C语言
---

一大早晨马上要考试了被问到阶乘这个问题，突然间懵了，思考了一会儿才想出来。

以下是在C语言的main函数中求一个数字的阶乘的代码：

```c
#include <stdio.h>

int main() {
    int num, factorial = 1;

    printf("请输入一个数字：");
    scanf("%d", &num);

    if (num < 0) {
        printf("输入的数字必须大于等于0！\n");
        return 0;
    }

    for (int i = 1; i <= num; i++) {
        factorial *= i;
    }

    printf("%d的阶乘为：%d\n", num, factorial);

    return 0;
}
```

代码解释：

1. 首先，定义了两个变量`num`和`factorial`，其中`num`表示输入的数字，`factorial`表示阶乘的结果。

2. 使用`printf`函数提示用户输入一个数字，并使用`scanf`函数将用户输入的数字赋值给`num`变量。

3. 使用`if`语句判断用户输入的数字是否小于0，如果小于0，则输出错误信息并返回。

4. 使用`for`循环计算阶乘的结果，循环从1开始，每次乘以当前的循环变量`i`，并将结果赋值给`factorial`变量。

5. 循环结束后，使用`printf`函数输出计算出的阶乘结果。

6. 最后，返回0表示程序执行成功结束。
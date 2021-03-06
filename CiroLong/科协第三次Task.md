# 2020届电信科协第三周Task

#  本次Task DDL：10月28日 晚20:00

本次Task学习的主要内容：C中的数组、指针、字符串。

## 基础任务

1. 学习 **一维数字数组** 和 **一维字符数组** 的声明方法；学会 **一维数字数组** 的初始化方法（利用 `{……}` ），**一维字符数组**的初始化方法（ `char *s=".."` ）;学会初始化**二维数字数组**（ `{{}，{}}` ）和**二维字符数组**初始化。
2. 学会指针的赋值，求值及取值，取指针地址等指针基本操作；使用指针与for循环打印各类型数组（ `char` ， `int` ， `float` ……）中各变量的地址，并发现规律。

同时思考：为什么C语言数组中，构成数组的各个元素必须具有相同的数据类型。？

>c语言对指针和数组有“严格的对应关系”，在访问数组中某元素时，实际上是通过指针操作来完成，
>
>而指针的偏移量由数组的数据类型给出，因此必须严格限制数组元素的类型。

1. **编程实现**：用户给定一个**整数**，将该**整数**逆置之后输出。（如：输入 `123` ，输出 `321` ）。有如下要求：
   1. 对于给定的整数，请不要用字符串/字符数组存储来完成这道题目。
   
   2. 尽可能使时间复杂度小。
   
   3. 要求能够完成214748364792这个数字的逆置。
   
```c
//我的代码   
#include<stdio.h>
   int main()
   {
   	long long n,m=0;
   	scanf_s("%lld", &n);
   	while (n != 0)
   	{
   		m = 10 * m + n % 10;
   		n = n / 10;
   	}
   	printf("%lld", m);
   
   	return 0;
   }
```

  

2. **编程实现** ：给定一串任意字符串（如： `1023fase415#145#` ）。**我们确保输入的字符串中只有整数，**有如下要求：

    将其中的所有整数提取出来并存入 `int` 型数组（例子中的是 `{1023, 415, 145}` 三个整数）。并在最后使用 `for` 循环输出。
    
    ```c
    //我的代码
    #include<stdio.h>
    #include<ctype.h>
    #include <stdlib.h> 
    #include<string.h>
    #include<iostream>
    #include<algorithm>
    using namespace std;
    
    char input[1000];
    int num[100];
    
    int main()
    {
    
    	int i = 0, u = 0;				//计数
    	char* pr ;						//暂时储存
    	pr = NULL;
    	char ing[11] = "0123456789";
    	cin >> input;	
    	pr = strpbrk(input, ing);		//得到第一个数字的地址
    	while(pr != 0)
    	{
    
    		num[i] = atoi(pr);
    		i++;
    	
    		while (isdigit(pr[u]))		  //清除该串数字
    		{
    		*(pr + u) = 'a';
    		u++;
    		}
    		u = 0;
    
    
    		pr = strpbrk(input, ing);
    	}
    	num[i] = -1;
    
    		for (int i = 0; num[i] >= 0; i++)
    			cout << num[i] << endl;
    
    
    	return 0;
    }
    ```

  3.**编程实现** ：给定一串任意字符串（如： `10.23fase4.15#14.5#15$` ）。**输入的字符串中有整数也会有浮点数，**有如下要求：

1. 将其中的所有数字提取出来并存入 `double` 数组（例子中的是 `{10.23, 4.15, 14.5, 15}` 四个数字）。

   ```c
   //我的代码
   #include<ctype.h>
   #include <stdlib.h> 
   #include<string.h>
   #include<iostream>
   #include<algorithm>
   #include<math.h>
   using namespace std;
   char input[1000];
   double num[100];
   int main()
   {
   	int i = 0, u = 0;				//计数
   	char* pr;						//暂时储存
   	pr = NULL;
   	char ing[12] = "0123456789.";
   	cin >> input;
   	pr = strpbrk(input, ing);		//得到第一个数字的地址
   	while (pr != 0)
   	{
   			int y = 0;
   			while (pr[y] != '.')
   			{
   				num[i] = num[i] * 10 + (double)(*(pr+y)-48);
   				y++;
   			}
   			y++;				//跳过  '.'
   			int x = 1;
   			while (isdigit(pr[y]))
   			{
   				num[i] += (double)(pr[y]-48) /( pow(10.0,x));
   				y++;
   				x++;
   			}
   		u = 0;
   		while (isdigit(pr[u])||pr[u]=='.')		  //清除该串数字
   		{
   			*(pr + u) = 'a';
   			u++;
   		}
   		i++;		//处理下一个数
   		pr = strpbrk(input, ing);
   	}
   	num[i] = -1;
   	for (int i = 0; num[i] >= 0; i++)
   		cout << num[i] << endl;
   	return 0;
   }
   ```

   


## 提高任务

观察下列代码，思考并解释程序运行结果？（先自己想，再编写程序验证）

### 程序一

```c
#include <stdio.h>
//#include<stdlib.h>
int main()
{
    char *c[] = { "ENTER", "NEW", "POINT", "FIRST" };
    char** cp[] = { c + 3, c + 2, c + 1, c };
    char*** cpp = cp;
    printf("%s\n", **++cpp);
    printf("%s\n", *--*++cpp + 3);
    printf("%s\n", *cpp[-2] + 3);
    printf("%s\n", cpp[-1][-1] + 1);
    system("pause");
    return 0;
}
```

```c++
POINT
ER
ST
EW
//可以利用ch[a]==*(ch+a)进行转换
//也可以深入理解指针含义=-=
```



### 程序二

```c
#include <stdio.h>
struct Test
{
    int Num;
    char *pcName;
    short sDate;
    char cha[2];
    short sBa[4];
}*p;
int main()
{
    p = 0x100000;
    printf("%p\n", p + 0x1);
    printf("%p\n", (unsigned long)p + 0x1);
    printf("%p\n", (unsigned int*)p + 0x1);
    return 0;
}
```

```c
//答案
//实际上在vs上执行不了
01000014
01000001
01000004
```



### 程序三

```c
#include <stdio.h>
int main()
{
    int a[4] = { 1, 2, 3, 4 };
    int *ptr1 = (int *)(&a + 1);
    int *ptr2 = (int *)((int)a + 1);
    printf("%x\n%x\n", ptr1[-1], *ptr2);
    return 0;
}
```

```c
//output:（学习后）
4/*      a是一个包含4个int元素的数组，长度为16位（在int为4位时），&a得到a的地址，+1后地址加16位
而ptr1是一个指向int元素的指针（ptr1[-1] == *(ptr1+(-1))）向前移4位，指向a[3]的值4             */
2000000/* 根据vs的输出显示是2000000
思考：(int)a得到a数组的首元素a[0]的地址的int型，由于int型数以4字节储存,+1后右移1一个字节,储存(01)的字节退出，下一个地址的(02)进入这个新地址指向的int型数，以十六进制打印后得到2 00 00 00            */
```



## 特别提醒

本次Task题目量较多，同学们可以量力而行，做多少交多少，做不完的之后还可以补。
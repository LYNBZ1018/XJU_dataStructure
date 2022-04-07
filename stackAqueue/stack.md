# stack

#### 1.写出下列程序段的输出结果： <u>stack</u>

```c++
void main()

{  
    Stack S; 
    char x,y;

    InitStack(S);
    x='c';
    y='k';

    Push(S,x);
    Push(S,'a');
    Push(S,y);  // c a k

    Pop(S,x);  // x = k   c a
    Push(S,'t');  // c a t

    Push(S,x);  // c a t k
    Pop(S,x);  // x = k   c a t 
    Push(S,'s');  // c a t s

    while(!StackEmpty(S))
    {    
        Pop(S,y);
        printf("%c”, y);  // stac    
    }

    printf("%c”，x);  // k
    // stack
}
```

#### 2.说明线性表、栈与队的异同点

```c++
相同点 : 都是线性数据结构，都可以用顺序表或链表进行存储，栈和队列是特殊的线性表对输入和输出进行了不同的限制。

不同点 : 存取方式不同，线性表是随机存取，栈是先进后出只允许在栈顶进行插入和删除，队列是先进先出只允许在队尾进行插入在对头进行删除。
      	用途不同，栈多用于子进程调用和现场保护如递归调用函数，队列多用于多任务的处理先来先服务。
```

#### 3.栈的出栈顺序

**设有编号为1，2，3，4的四辆列车，顺序进入一个栈式结构的车站，具体写出这四辆列车开出车站的所有可能的顺序。**

```c++
// 设按照该1、2、3、4的顺序一次进入车站
// 出站的可能顺序 共有 C(2n, n) / (n + 1) = C(8, 4) / (4 + 1) = 14 种
// 1 2 3 4 
// 1 2 4 3
// 1 3 2 4
// 1 3 4 2
// 1 4 3 2
// 
// 2 1 3 4
// 2 1 4 3
// 2 3 4 1
// 2 4 3 1
// 2 3 1 4
//
// 3 2 1 4
// 3 4 2 1 
// 3 2 4 1
// 
// 4 3 2 1
```

#### 4.设计算法

**读入一个以“@”结束的字符串，判断是否是“回文”。“回文”字符串：正读和反读都相同，例如：“abcba".**

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

bool check(string str, int len)
{
    for (int i = 0; i < len / 2; i ++ )
        if (str[i] != str[len - i - 1])
            return false;
    return true;
}

int main()

{
    string str;
    cin >> str;
    int len = str.size();
    len -- ;  // 不计算 @
    
    if (check(str, len)) puts("YES");
    else puts("NO");

    return 0;
}
```




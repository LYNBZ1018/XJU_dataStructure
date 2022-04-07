# 	queue

#### 1.顺序队的”假溢出“是怎样产生的？如何知道循环队列是空还是满？

```c++
假溢出 : 队尾占用了最后一个存储空间，而队首占的不是分配的第一个空间，队列对外是满的，
但是内部空间并没有完全利用，还有一部分空的没有用，叫做假溢出。

判断循环队列是否为空 :
1) 设置一个标志，标记队列空/非空
2) 设置一个变量计算队列的长度
3) 少利用一个空间  front == (rear + 1) % MAXSIZE 
```

#### 2.设计算法

__假设在循环队列中能重复利用顺序空间中的每一个存储单元，则需另一个标志tag，以tag为0或1来区分尾指针和头指针值相同时队列的状态是”空“还是”满“。__

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 5;

typedef struct Queue {
    int data[N];
    int front;  // 头部的前一个
    int rear;  // 尾部
    bool flag;  // pop -> false   push -> true
}queue;

void seqInit(queue& seq)
{
    seq.front = 0;
    seq.rear = 0;
    seq.flag = false;
}

bool seqEmpty(queue seq)
{
    if (seq.rear == seq.front && seq.flag == false)
        return true;
    return false;
}

bool seqPush(queue& seq, int x)
{
    if (seq.front == seq.rear && seq.flag == true)
    {
        printf("不能插入 因为队列为满\n");
        return false;
    }
    seq.rear = (seq.rear + 1) % N;
    seq.data[seq.rear] = x;
    seq.flag = true;
    printf("成功插入 %d \n", x);
    return true;
}

bool seqPop(queue& seq, int& x)
{
    if (seqEmpty(seq))
    {
        printf("不能出队 因为队列为空\n");
        return false;
    }
    seq.front = (seq.front + 1) % N;
    x = seq.data[seq.front];
    printf("成功出队 %d \n", x);
    return true;
}

int main()
{
    queue q;
    seqInit(q);
    if (seqEmpty(q)) printf("队列为空\n");
    int x = 0;
    seqPop(q, x);
    seqPush(q, 1);
    seqPush(q, 2);
    seqPush(q, 3);
    seqPush(q, 4);
    seqPush(q, 5);
    seqPush(q, 6);
    seqPop(q, x);
    
    return 0;
}
```


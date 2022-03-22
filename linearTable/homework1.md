###1.设计一个算法，判断一个顺序表中的各个结点值 否有序
```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

#define MAXLEN 100

using namespace std;

struct Slist {
    int a[MAXLEN];
    int length;
}list;  // 预先定义一个顺序表


bool is_sequence(Slist list)
{
    int n = list.length;
    for (int i = 1; i < n - 1; i ++ )  // 可以判断顺序表是否是有序的（逆序和顺序都可以判断）
        if ((list.a[i] > list.a[i - 1] && list.a[i] > list.a[i + 1]) || (list.a[i] < list.a[i - 1] && list.a[i] < list.a[i + 1]))
            return false;
    return true;
}

int main()
{
    int len;
    cin >> len;
    list.length = len;
    for (int i = 0; i < len; i ++ )
        cin >> list.a[i];
    
    if (is_sequence(list))  cout << "Yes" << endl;
    else cout << "No" << endl;

    return 0;
}

****

###2.设计一个算法，在一个双向链表中值为y的结点前插入一个值为x的结点，就是使值为x的结点成为值为y的结点的前驱结点。
```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

struct Node {
    int data;
    Node* pre;
    Node* next;
}*linklist;

bool at_x_before_insert(Node* linklist, int x, int y)
{
    Node* q = new Node;
    q->data = y;
    Node* p = linklist->next;
    while (p->data != x && p != linklist)  // 找到x节点 防止转一圈没有找到x继续从头结点开始找
    {
        p = p->next;
    }
    if (p->data != x) return false;
    q->pre = p->pre;  // y的前驱指向x的前驱
    p->pre->next = q;  // x的前驱的后继指向y
    p->pre = q;  // x的前驱指向y
    q->next = p;  // y的后继指向
    return true;
}

void print(Node* linklist)
{
    Node* p = linklist->next;
    while (p != linklist)
    {
        cout << p->data << ' ';
        p = p->next;
    }
}

int main()
{
    linklist = new Node;
    linklist->next = linklist->pre = linklist;
    int len;
    cin >> len;
    Node* tail = linklist;
    for (int i = 0; i < len; i ++ )
    {
        int data;
        cin >> data;
        Node* p = new Node;
        p->data = data;
        p->next = tail->next;  // 尾插节点后继指向原尾结点后继也就是头结点
        tail->next = p;
        p->pre = tail;
        tail = p;  // 尾结点变化 采用的尾插方式
        linklist->pre = tail;  // 头结点前驱指向尾结点
    }
    
    print(linklist);
    puts("");
    int x, y;
    cin >> x >> y;
    at_x_before_insert(linklist, x, y);
    print(linklist);
    puts("");
    
    return 0;
}
```

****

###3.设计一个算法，将一个结点值为自然数的单链表拆分为两个单链表，原表中保留值为偶数的结点，而值 为奇数的结点按它们在原表中的相对次序组成一个新的单链表。
```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

struct Node {
    int data;
    Node* next;
}*linklist;

void print(Node* linklist)
{
    Node* p = linklist->next;
    while (p != NULL)
    {
        cout << p->data << ' ';
        p = p->next;
    }
}

int main()
{
    linklist = new Node;
    linklist->next = NULL;
    int len;
    cin >> len;
    Node* tail = linklist;
    for (int i = 0; i < len; i ++ )  // 采用尾插的方式插入
    {
        int data;
        cin >> data;
        Node* p = new Node;
        p->data = data;
        p->next = tail->next;
        tail->next = p;
        tail = p;
    }
    
    print(linklist);
    cout << endl;
    
    Node* link1 = new Node;
    Node* link2 = new Node;
    link2->next = NULL;
    Node* tail2 = link2;
    Node* tmp;
    Node* p = linklist->next;
    for (int i = 1; i <= len; )
    {
        if ((i + 1) % 2 == 0)  // 如果下一个数是偶数就进行修改
        {
            i += 2;
            tmp = p->next;  // 先记录这个偶节点
            p->next = tmp->next;  // 改变原链表
            p = p->next;
            tmp->next = tail2->next;  // 把偶节点放到link2中
            tail2->next = tmp;
            tail2 = tmp;
            if (i == len) break;
        }
    }
    
    link1 = linklist;
    print(link1);
    cout << endl;
    print(link2);
    cout << endl;
    
    return 0;
}
```

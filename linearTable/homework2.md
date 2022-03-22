### 1.设单链表L是一个递减有序表，设计一个算法，将x插入其中后仍保持L的有序性。
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

bool sequence_insert(Node* linklist, int x)
{
    Node* p = linklist->next;
    Node* q = new Node;
    q->data = x;
    q->next = NULL;
    if (x >= p->data)  // x比逆序的第一个还大 直接插入最前边
    {
        q->next = p;
        linklist->next = q;
        return true;
    }
    
    while (p != NULL)
    {
        int a = p->data;
        int b = 0;
        if (p->next == NULL) b = -1e9;  // 设NULL的值为负无穷
        else b = p->next->data;
        
        if (x <= a && x >= b)
        {
            q->next = p->next;
            p->next = q;
            return true;
        }
        
        p = p->next;
    }
    
    return false;
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
    
    int x;
    cin >> x;
    sequence_insert(linklist, x);
    print(linklist);
    cout << endl;
    
    return 0;
}
```

****

### 2.设计一个算法，将两个有序表合并成一个有序的单链表。
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

void create_linklist_tail_insert(Node* linklist, int len)
{
    Node* tail = linklist;
    for (int i = 0; i < len; i++)  // 采用尾插的方式插入
    {
        int data;
        cin >> data;
        Node* p = new Node;
        p->data = data;
        p->next = tail->next;
        tail->next = p;
        tail = p;
    }
}

void merge_linklist(int len1, int len2, Node* link1, Node* link2, Node* linklist)
{
    Node* p = link1->next;
    Node* q = link2->next;
    Node* tail = linklist;
    Node* tmp;

    for (int i = 0; i < len1 + len2; i++)
    {
        int a = p->data;
        int b = q->data;
        if (a <= b)
        {
            tmp = p;
            p = p->next;
            tmp->next = tail->next;
            tail->next = tmp;
            tail = tmp;
        }
        else
        {
            tmp = q;
            q = q->next;
            tmp->next = tail->next;
            tail->next = tmp;
            tail = tmp;
        }
        if (p == NULL && q != NULL)
        {
            tail->next = q;
            return;
        }
        if (p != NULL && q == NULL)
        {
            tail->next = p;
            return;
        }
    }
}

int main()
{
    linklist = new Node;
    linklist->next = NULL;
    Node* link1 = new Node;
    Node* link2 = new Node;
    link1->next = link2->next = NULL;
    int len1 = 0, len2 = 0;
    cin >> len1;
    create_linklist_tail_insert(link1, len1);
    cin >> len2;
    create_linklist_tail_insert(link2, len2);

    merge_linklist(len1, len2, link1, link2, linklist);
    delete link1;
    delete link2;

    print(linklist);
    cout << endl;

    return 0;
}
```

****

### 3.设计一个算法，对单链表按结点值从小到大进行排序。
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

void create_linklist_tail_insert(Node* linklist, int len, int a[])
{
    Node* tail = linklist;
    for (int i = 0; i < len; i++)  // 采用尾插的方式插入
    {
        int data = a[i];
        Node* p = new Node;
        p->data = data;
        p->next = tail->next;
        tail->next = p;
        tail = p;
    }
}

void sort_linklist(Node* linklist, Node* sorted_linklist)
{
    int a[100] = {0};
    int len = 0;
    Node* p = linklist->next;
    while (p != NULL)
    {
        a[len ++ ] = p->data;
        p = p->next;
    }
    sort(a, a + len);
    create_linklist_tail_insert(sorted_linklist, len, a);
}

int main()
{
    linklist = new Node;
    linklist->next = NULL;
    int len;
    int a[100] = {0};
    cin >> len;
    for (int i = 0; i < len; i ++ ) cin >> a[i];
    create_linklist_tail_insert(linklist, len, a);

    print(linklist);
    cout << endl;

    Node* sorted_linklist = new Node;
    sorted_linklist->next = NULL;
    sort_linklist(linklist, sorted_linklist);

    print(sorted_linklist);
    cout << endl;

    return 0;
}
```

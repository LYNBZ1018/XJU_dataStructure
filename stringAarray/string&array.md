## String and Array

### 1.算法实现   subStr

完成算法：将串**S**中从第**pos**个字符开始长度为**len**的字符 序列复制到串**T**中。 

```c++
void subStr(SString &T, SString S, int pos, int len)
```

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 100;

bool flag = true;

struct SString
{
    char data[N];
    int len;
};

void print(SString S)
{
    for (int i = 0; i < S.len; i ++ )
        printf("%c", S.data[i]);
    puts("");
}

int getlen(SString S)
{
    int cnt = 0;
    for (int i = 0; i < N; i ++ )
        if (S.data[i] != '\0') cnt ++ ;
        else break;
    return cnt;
}

void subStr(SString &T, SString S, int pos, int len)
{
    int n = S.len;  // S 中下标为 0 ~ n - 1
    
    if (pos >= n)  // pos 超出下标
    {
        flag = false;
        return;
    }
    
    if (pos + len - 1 >= n)  // 最后一个字符超过下标
    {
        flag = false;
        return;
    }
    
    int cnt = 0;
    for (int i = pos; i <= pos + len - 1; i ++ )
        T.data[cnt ++ ] = S.data[i];
    T.len = cnt;
}

int main()
{
    SString S, T;
    int pos, len;
    
    cout << "input a String: " << endl;
    cin >> S.data;
    S.len = getlen(S);
    cout << "input pos and len: " << endl;
    cin >> pos >> len;
    subStr(T, S, pos - 1, len);
    
    cout << "S: ";
    print(S);
    
    if (flag)
    {
        cout << "T: ";
        print(T);
    }
    else 
    {
        cout << "pos or len is false" << endl;
    }
    
    return 0;
}
```

​       

### 2.算法实现    index

完成**BF**算法（简单匹配算法）。

```c++
int index(SString S, SString T)
```

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 100;

bool flag = true;

struct SString
{
    char data[N];
    int len;
};

void print(SString S);  // 打印字符串
int getlen(SString S);  // 获得字符串的长度

int index(SString S, SString T)  // 朴素匹配  未找到返回 -1
{
    int n = S.len, m = T.len;
    for (int i = 0; i <= n - m; i ++ )
    {
        int j = 0, k = i;
        for ( ; j < m; j ++ , k ++ )
        {
            if (T.data[j] != S.data[k])
                break;
        }
        if (j == m)
            return i + 1;
    }
    return -1;
}

int main()
{
    SString S, T;
    cout << "input two String: " << endl;
    cin >> S.data >> T.data;
    S.len = getlen(S);
    T.len = getlen(T);
    
    print(S);
    print(T);
    cout << index(S, T) << endl;
    
    return 0;
}

void print(SString S)
{
    for (int i = 0; i < S.len; i ++ )
        printf("%c", S.data[i]);
    puts("");
}

int getlen(SString S)
{
    int cnt = 0;
    for (int i = 0; i < N; i ++ )
        if (S.data[i] != '\0') cnt ++ ;
        else break;
    return cnt;
}
```

​        

###   3.算法实现

完成稀疏矩阵的三元组表矩阵转置算法。

```c++
void Tran(TSMatris t,TSMatrix &tb)
```

```c++
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 100;

int q[N][N];

struct Val
{
    int r, c, data; 
};

struct TSMatris
{
    Val data[100];
    int mrow;
    int mcol;
    int cnt;
};

void init(TSMatris &t);  // 初始化 
void print(TSMatris t);  // 解压 打印

void Tran(TSMatris t, TSMatris &tb)
{
    for (int i = 0; i < t.cnt; i ++ )
    {
        Val tmp = t.data[i]; 
        tb.data[i] = {tmp.c, tmp.r, tmp.data};
    }
    tb.mrow = t.mcol;
    tb.mcol = t.mrow;
    tb.cnt = t.cnt;
}

int main()
{
    TSMatris t, tb;
    init(t);
    init(tb);
    
    int cnt = 0, cnt1 = 0;
    cout << "input number: " << endl;
    cin >> cnt;
    
    while (cnt -- )  // 稀疏矩阵的读入
    {
        int a, b, c;
        cout << cnt1 + 1<<' ' << "input row col value: " << endl;
        cin >> a >> b >> c;
        t.data[cnt1 ++ ] = {a, b, c};
        t.mrow = max(t.mrow, a);
        t.mcol = max(t.mcol, b);
        t.cnt ++ ;
    }
    
    Tran(t, tb);  // 转置
    
    print(t);
    puts("");
    print(tb);
    
    return 0;
}

void init(TSMatris &t)
{
	t.mcol = t.mrow = 0;
	t.cnt = 0;
}

void print(TSMatris t)
{
    memset (q, 0, sizeof q);
    for (int i = 0; i < t.cnt; i ++ )
    {
        int x = t.data[i].c - 1, y = t.data[i].r - 1;
        q[x][y] = t.data[i].data;
    }
    for (int i = 0; i < t.mrow; i ++ )
    {
        for (int j = 0; j < t.mcol; j ++ )
        {
            printf("%d ", q[i][j]);
        }
        puts("");
    }
}
```




## **Codeforces Round #660 (Div. 2)**



### [A. Captain Flint and Crew Recruitment](http://codeforces.com/contest/1388/problem/A)


### **题意**  

给定一个数n，如果能分解成四个不同的数，至少三个为nearly prime（nearly prime的定义：可以分解成两个不等素数的乘积）

### **思路**  

最小的nearly prime数为2×3=6，2×5=10，2×7=14，则最小的数n为31。同时为了确保四个数不相等，如果n-30的值与6/10/14相等，则输出`6 10 15 n-30-1`；否则输出`6 10 14 n-30`


### **代码** 
```
#include <iostream>
#include <cstdio>
using namespace std;
#define ll long long int
using namespace std;
const int mod = 1e9 + 7;

int main()
{
    int t;
    scanf("%d", &t);
    while (t--) {
        int n;
        scanf("%d", &n);
        int x = n - 30;
        if (n > 30)
        {
            printf("YES\n");
            if (x != 10 && x != 6 && x != 14)
                printf("6 10 14 %d\n", x);
            else {
                printf("6 10 15 %d\n", x - 1);
            }
        }
        else
            printf("NO\n");
    }
    return 0;    
}
```


### [B. Captain Flint and a Long Voyage](http://codeforces.com/contest/1388/problem/B)


### **题意**  

给定一个数n，求一个n位数的十进制数r，转化为二进制数k后，在删掉末位n位后k最大，且r越小越好

### **思路** 

为了使k越大越好，则使位数尽可能多，即8(1000),9(1001)都是四位数，故r一定有8或9组成。为了使r越小越好，应在一定长度内将9替换成8；该长度为n/4向上取整（8,9的长度为4）

### **代码** 
```
#include <iostream>
#include <cstdio>
#include<cmath>
using namespace std;
#define ll long long int
using namespace std;
const int mod = 1e9 + 7;

int main()
{
    int t;
    scanf("%d", &t);
    while (t--) {
        int n;
        scanf("%d", &n);
        int x = ceil(n*1.0/ 4);
        for (int i = 1; i <= n - x;i++) printf("9");
        for (int i = n - x + 1; i <= n; i++) printf("8");
        printf("\n");
    }
    return 0;
    
}
```

### [C. Uncle Bogdan and Country Happiness](http://codeforces.com/contest/1388/problem/C)


### **题意**  
给定n个城市，m个公民，城市之间存在连通图。每个参数的总人数$p_i$和快乐指数$h_i$，每个人在首都1号上班，下班回家的路上，每个人可能从开心变成不开心，但是不可能从不开心变为开心。问是否存在一种情况使得每个城市的幸福指数都与给定的$h_i$相同。


### **思路** 

借鉴了网上的思路orz，经过城市i开心的人有g[i]个，总人数有b[i]个。二者关系为$g[i]=\frac{b[i]+h[i]}{2}$



dfs遍历树即可

### **代码** 
```
#pragma warning(disable:4996)

#include <algorithm>
#include <iostream>
#include <cstdio>
#include<string.h>
#include<cstring>
#include<vector>
using namespace std;
typedef long long ll;
const int maxn = 1e5 + 5;
int p[maxn], h[maxn], b[maxn], g[maxn], ok;
vector<int>edge[maxn];
void dfs(int fa, int u)
{
    b[u] = p[u];
    int sum = 0;
    for (int i = 0; i < edge[u].size(); i++)
    {
        int v = edge[u][i];
        if (v != fa)
        {
            dfs(u, v);
            b[u] += b[v];
            sum += g[v];
        }
    }
    g[u] = (b[u] + h[u]) / 2;
    if ((b[u] + h[u]) % 2)
        ok = 0;
    if (sum > g[u] || g[u] < 0) ok = 0;
    if (b[u] + h[u] < 0) ok = 0;
     if(b[u] <g[u])
        ok = 0;
}
int main()
{
    int t;
    scanf("%d", &t);
    while (t--)
    {
        int n, m;
        scanf("%d%d", &n, &m);
        for (int i = 1; i <= n; i++)
            edge[i].clear();
        memset(g, 0, sizeof(g));
        memset(b, 0, sizeof(b)); 
        for (int i = 1; i <= n; i++)
            scanf("%d", &p[i]);
        for (int i = 1; i <= n; i++)
            scanf("%d", &h[i]);
        for (int i = 1, u, v; i <= n - 1; i++)
        {
            scanf("%d%d", &u, &v);
            edge[u].push_back(v);
            edge[v].push_back(u);
        }
        ok = 1;
        dfs(1, 1);
        if (ok)
            printf("YES\n");
        else
            printf("NO\n");
    }
    return 0;
}
```





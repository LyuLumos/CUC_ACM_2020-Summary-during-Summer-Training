# Codeforces Round #654 (Div. 2) 题解

### A.[Magical Sticks](https://vjudge.net/problem/CodeForces-1371A)

**题目描述：**

有n个长度大小为1，2，3，......，n的木棒，现在你可以选取其中的两个木棒来进行拼接，拼接后两根木棒成为一个，长度为它们的和，现在需要你计算对于不同的n最多可以获得多少根长度相同的木棒。

**题解：**

对于这样一个长度的序列：1，2，3，4.....，n。我们可以发现，在n是偶数的情况下，要想获得最大数量的相同长度的木棒，一定是以首尾相加后得到的长度为基准，同样对于奇数的情况，我们可以先讨论n - 1的情况，然后再加上一个单独的n就可以了，并且前n - 1个木棒获得的基准长度就是这个n

**AC代码：**

```CPP
#include<iostream>
#include<cstdio>
#include<cmath>
using namespace std;
int main()
{
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        if(n & 1) cout << (n - 1) / 2 + 1 << endl;
        else cout << n / 2 << endl;
    }
    return 0;
}
```

### B.[Magical Calendar](https://vjudge.net/problem/CodeForces-1371B)

**题目描述：**

现在可以设计一个每一周为**k(`` 1 <= k <= r``)**天的日历，并且在这个日历上选取n个方块，要求这n个方块必须边相邻，也就是对于任意一个方块总会有一个和它边相邻的方块存在。并且规定经上下平移和左右平移得到的图形相同的，我们记作是一种。现在对于给定的n,r，你可以最多得到多少种组合？

**题解：**

这个题目就找规律一点点分析就可。我们假设k天为一周

- 如果``n == k``，那么就只有唯一的一种方法。
- 如果`n > k`，那么就会存在k种方法。
- 如果`n < k`,这种情况和`n == k`的情况是一致的，所以当`k > n`后，以后的结果就都不用管了。

**AC代码：**

```cpp
#include<iostream>
#include<cmath>
#include<cstdio>
#include<cstring>
#include<algorithm>
#define ll long long
using namespace std;
int main()
{
    int t;
    scanf("%d",&t);
    while(t--){
        ll n,r,sum = 0;
        scanf("%lld%lld",&n,&r);
        if(n > r){
            sum += (r + 1)/2.0 * r;
            printf("%lld\n",sum);
        }
        else{
            sum += 1;
            n -= 1;
            sum += (n + 1)/2.0 * n;
            printf("%lld\n",sum);
        }
    }
    return 0;
}
```

### C.[A Cookie for You](https://vjudge.net/problem/CodeForces-1371C)

**题目描述：**

Anna要举办一个Cookie派对，现在他有a个香草口味的，b个巧克力口味的。她邀请了两种人，分别有m个人和n个人，这两种人选择的Cookie的方式不同：

我们假设当前有v个香草派，c个巧克力派。

- 第一种人：如果`v > c`，那么选择香草派，否则选择巧克力派。
- 第二种人：如果`v > c`，那么选择巧克力派，否则选择香草派。

并且，如果当前的客人没有拿到他想要的派，那他就会很生气

现在给出你a,b,n,m，试问会不会有客人生气。

**题解：**

贪心题，要知道，对于第一类人，他们拿的永远是最多的那个派，也就是无论如何都可以拿完，所以第一类人本身不存在生气的问题（除非人数多于派数）。那么问题就在于，第二类人永远拿的是最少的派，而又可能会出现v或者c变成0的情况，所以在派的数目足够的情况下，生气的也只能是第二类人。所以我们就需要判断，当前a,b,中最少数量的那个派能不能满足第二类人的需求，如果可以，就不会有客人生气了。

**AC代码:**

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cmath>
#include<algorithm>
#define ll long long
using namespace std;
int main()
{
    int t;
    scanf("%d",&t);
    while(t--){
        ll a,b,n,m;
        scanf("%lld%lld%lld%lld",&a,&b,&n,&m);
        if(a + b < n + m) printf("No\n");
        else{
            if(m > min(a,b)) printf("No\n");
            else printf("Yes\n");
        }
    }
    return 0;
}
```

### D.[Grid-00100](https://vjudge.net/problem/CodeForces-1371D)

**题目描述：**

给出了一个n * n的01棋盘，同时规定了1的数目是k个 ，现在要求你写出一个01棋盘，满足对于给定的f函数：
$$
f(A) = (max(SUM_R) - min(SUM_R))^2 + (max(SUM_C) - min(SUM_C)))^2
$$
要求f(A)最小。

**题解：**

其实不难看出来，当``k % n == 0``时，答案就是0，否则答案就是2。

问题是怎么放了。

``k % n == 0``时就很简单，直接每一行错开放k/n个就可以。

那么``k % n != 0``的话呢？那就前k % n 行放`k/n + 1`个，后面的放k/n个就好啦

**AC代码：**

```cpp
#include<cstdio>
#include<iostream>
#include<cstring>
#include<algorithm>
#include<cmath>
using namespace std;
const int maxn = 308;
int a[maxn][maxn];
int main()
{
    int t;
    cin >> t;
    while(t--){
        memset(a,0,sizeof(a));
        int n,k;
        cin >> n >> k;
        int flag = k % n,temp = k / n;
        if(k % n == 0){
            cout << 0 << endl;
            for(int i = 0;i < flag;i++){
                for(int j = i;j <= temp + i;j++){
                    a[i][j % n] = 1;
                }
            }
            for(int i = flag;i < n;i++){
                for(int j = i;j < temp + i;j++){
                    a[i][j % n] = 1;
                }
            }
            for(int i = 0;i < n;i++){
                for(int j = 0;j < n;j++){
                    cout << a[i][j];
                }
                cout << endl;
            }
        }
        else{
            cout << 2 << endl;
            for(int i = 0;i < flag;i++){
                for(int j = i;j <= temp + i;j++){
                    a[i][j % n] = 1;
                }
            }
            for(int i = flag;i < n;i++){
                for(int j = i;j < temp + i;j++){
                    a[i][j % n] = 1;
                }
            }
            for(int i = 0;i < n;i++){
                for(int j = 0;j < n;j++){
                    cout << a[i][j];
                }
                cout << endl;
            }
        }
    }
    return 0;
}
```


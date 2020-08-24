###### [C. Boboniu and Bit Operations](https://codeforces.com/contest/1395/problem/C)

题意：给出有n个元素的数组a，和m个元素的数组b，求数组c，使$c_1|c_2|....|c_n$的值最小。$c_i=a_i\& b_j$ ($1\leq i\leq n,1\leq j\leq m$)



$c_1|c_2|....|c_n$的值最小时，数组c中的元素应该尽可能相同，假设都是k，$c_i=a_i\& b_j=k$

```c++
#include <iostream>
#include <cmath>
#include<vector>
#include <algorithm>
using namespace std;

int n,m,sx,sy;
const int N=200+10;
int a[N],b[N],c[N];

int main()
{

    int n,m;
    cin>>n>>m;
    for(int i=1;i<=n;i++)cin>>a[i];
    for(int i=1;i<=m;i++)cin>>b[i];
    bool flag=false;
    for(int k=0;k<=512;k++)
    {
        flag=true;
        for(int i=1;i<=n;i++)
        {
            int flag1=false;
            for(int j=1;j<=m;j++)
            {
                if(((a[i]&b[j])|k)==k)
                {
                    flag1=true;
                    break;
                }
            }
            if(flag1==false)
            {
                flag=false;
                break;
            }
        }
        if(flag)
        {
            cout<<k<<endl;
            break;
        }
    }
    
    return 0;
}

```



###### [D. Boboniu Chats with Du](https://codeforces.com/contest/1395/problem/D)

题意：给出一个n个数的数组，$a_i \le m$能说话，如果$a_i>m$当天可以说话，之后的d天禁言，求能说话的$a_i$的最大总和

将$a_i \le m和a_i>m$的数分为两个数组，从大到小排序，求这两个数组的前缀和，再枚举
```c++
#include <iostream>
#include <cmath>
#include<vector>
#include <algorithm>
using namespace std;
typedef long long  ll;
const int N=1e6+10;
ll a[N],b[N];
ll sum1[N],sum2[N];
bool cmp(int x,int y)
{
    return x>y;
}
int main()
{
    ll n,m,d;
    scanf("%lld%lld%lld",&n,&d,&m);
    int cnt1=0,cnt2=0;
    for(int i=1;i<=n;i++)
    {
        ll x;
        cin>>x;
        if(x>m)a[++cnt1]=x;
        else b[++cnt2]=x;
    }
    sort(a+1,a+cnt1+1,cmp);
    sort(b+1,b+cnt2+1,cmp);
    for(int i=1;i<=cnt1;i++)sum1[i]=sum1[i-1]+a[i];
    for(int i=1;i<=cnt2;i++)sum2[i]=sum2[i-1]+b[i];
    ll res=sum2[cnt2];
    for(int i=1;i<=cnt1;i++)
    {
        ll ans=1ll*(i-1)*(d+1)+1;
        if(ans>n)break;
        res=max(res,sum1[i]+sum2[min(n-ans,(ll)cnt2)]);
    }
    printf("%lld\n",res);
    return 0;

}

```


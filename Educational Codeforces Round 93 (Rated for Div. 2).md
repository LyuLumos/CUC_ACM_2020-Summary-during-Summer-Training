##### [C. Good Subarrays](https://codeforces.com/contest/1398/problem/C)

题意：计算数组中满足$\sum_{i=l}^{r}a_i=r-l+1$的数量



$\sum_{i=l}^{r}a_i=r-l+1 \Longrightarrow \sum_{i=l}^{r}a_i-(r-l+1)=0 \Longrightarrow \sum_{i=l}^{r}a_i-\sum_{i=l}^{r}1=0$



```c++
#include<iostream>
#include <string>
#include<vector>
#include <map>
using namespace std;
const int N=1e5+100;
int a[N];

int sum[N];

int main()
{
    int t;
    scanf("%d",&t);
    while(t--)
    {
        
        int n;
        scanf("%d",&n);
        string str;
        cin>>str;
        for(int i=0;i<n;i++)
        {
            sum[i+1]=sum[i]+str[i]-'0'-1;
        }
        //for(int i=0;i<=n;i++)cout<<sum[i]<<endl;
        long long ans=0;
        map<int,int>mp;
        for(int i=0;i<=n;i++)
        {
            ans+=mp[sum[i]];
            mp[sum[i]]++;
        }
        
        printf("%lld\n",ans);
    }
    return 0;
}
```

暴力

```c++
#pragma GCC optimize("Ofast")
#pragma GCC target("avx,avx2,fma")
#pragma GCC optimization("unroll-loops")
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;
const int N=1e5+100;
long long a[N];
int sum[N];
int v[N];
int main()
{
    int t;
    scanf("%d",&t);
    while(t--)
    {
        int n;
        scanf("%d",&n);
        for(int i=1;i<=n;i++)
        {
            scanf("%1d",&v[i]);
            sum[i]=sum[i-1]+v[i];
        }
        long long ans=0;
        for(int l=1;l<=n;l++)
        {
            for(int r=l;r<=n;r++)
            {
                    if((sum[r]-sum[l-1])==(r-l+1))ans++;
                
            }
        }
        printf("%lld\n",ans);
    }
    return 0;
}
```



###### [D. Colored Rectangles](https://codeforces.com/contest/1398/problem/D)

题意：给出红绿蓝三种不同长度的木棍，每次从中选择两种组成矩形。求矩形面积最大值。

$dp[i][j][k]$代表红色取了i个，绿色取了j个，蓝颜色取了k个。

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;
const int N=210;
int dp[N][N][N];
int r[N],b[N],g[N];
int main()
{
    int x,y,z;
    scanf("%d%d%d",&x,&y,&z);
    for(int i=0;i<x;i++)cin>>r[i];
    for(int i=0;i<y;i++)cin>>g[i];
    for(int i=0;i<z;i++)cin>>b[i];
    sort(r,r+x);
    sort(g,g+y);
    sort(b,b+z);
    for(int i=0;i<=x;i++)
    {
        for(int j=0;j<=y;j++)
        {
            for(int k=0;k<=z;k++)
            {
                if(i&&j)dp[i][j][k]=max(dp[i][j][k], dp[i-1][j-1][k]+r[i-1]*g[j-1]);
                if(i&&k)dp[i][j][k]=max(dp[i][j][k], dp[i-1][j][k-1]+r[i-1]*b[k-1]);
                if(j&&k)dp[i][j][k]=max(dp[i][j][k], dp[i][j-1][k-1]+b[k-1]*g[j-1]);
            }
        }
    }
    printf("%d\n",dp[x][y][z]);
    return 0;
}
```



###### [E. Two Types of Spells](https://codeforces.com/contest/1398/problem/E)

题意：有两种法术， lightning法术，fire法术。lightning法术对怪物造成伤害，并使下一个法力的伤害加倍。可以学习或忘记法术，求最大的伤害值。



要想取得最大的伤害值，就尽可能让数值大的法术加倍，把数值小的lightning法术或者fire法术放在最前面。用两个set记录需要加倍的数和不需要加倍的数。



```c++
#include <iostream>
#include <set>
using namespace std;
typedef long long ll;
set<int>s1;
set<int>s2;

int n;
set<int>small,big;
ll sumall=0,sumbig=0;
void add(int x)
{
    sumall+=x;
    if(big.empty()||x<*big.begin())
    {
        small.insert(x);
    }
    else big.insert(x),sumbig+=x;
}
void dele(int x)
{
    sumall-=x;
    if(small.count(x))small.erase(x);
    else big.erase(x),sumbig-=x;
}
ll cal()
{
    ll ans=0;
    while(big.size()>s1.size())
    {
        int x=*big.begin();
        big.erase(x);
        sumbig-=x;
        small.insert(x);
        
    }
    while(big.size()<s1.size())
    {
        int x=*small.rbegin();
        small.erase(x);
        big.insert(x);
        sumbig+=x;
    }
    ans=sumall+sumbig;
    if(s1.size()>0&&(s2.empty()||*s2.rbegin()<*s1.begin()))
    {
        ans-=*s1.begin();
        if(!s2.empty())
        {
            ans+=*s2.rbegin();
        }
    }
    return ans;
}
int main()
{
    scanf("%d",&n);
    for(int i=0;i<n;i++)
    {
        int x,y;
        scanf("%d%d",&x,&y);
        if(y>0)
        {
            if(x==1)
            {
                s1.insert(y);
            }
            else
            {
                s2.insert(y);
            }
            add(y);
        }
        else
        {
            if(x==1)
            {
                s1.erase(-y);
            }
            else
            {
                s2.erase(-y);
            }
            dele(-y);
        }
        printf("%lld\n",cal());
    }
    return 0;
}
```


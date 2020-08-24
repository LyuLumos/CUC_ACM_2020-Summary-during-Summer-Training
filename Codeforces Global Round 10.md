###### [C. Omkar and Waterslide](https://codeforces.com/contest/1392/problem/C)

题意：给一个大小为n的数组，每次可以选择一个非递减序列将每个元素+1，求将数组变成非递减的序列的最少操作。

在$a[i-1] > a[i] $的地方操作$a[i-1]-a[i]$次，$a[i-1] \leq a[i] $不需要操作。



```c++
#include <iostream>
#include <algorithm>
using namespace std;
const int N=2e5+100;
typedef long long ll;
ll a[N];
int sum[N];
int main()
{
    int t;
    scanf("%d",&t);
    while(t--)
    {
        int n;
        scanf("%d",&n);
        
        for(int i=0;i<n;i++)scanf("%lld",&a[i]);
        ll ans=0;
        for(int i=1;i<n;i++)
        {
            ans+=max(a[i-1]-a[i],(ll)0);
        }
        printf("%lld\n",ans);
       
    }
    return 0;
}
```



###### [D. Omkar and Bed Wars](https://codeforces.com/contest/1392/problem/D)

题意：大家围成一个圈做游戏，每个人可以攻击左右的人，这意味着每个人可能受到0，1，2个攻击，如果一个人受到的攻击为1时，必须要反击回去，其他两种情况可以攻击左边或者右边的人。问需要纠正几次。

1.例如把LLLLRRLRRRLL分为LLLL，RR，L，RRR，LL几个段，首尾相同时一起计算，每段需要改变的次数为段长度/3

2.LLLLLL,输出$1+(n-1)/3$

```c++
#include <iostream>
#include <cmath>
#include<vector>
#include <algorithm>
using namespace std;



int main()
{

    int t;
    cin>>t;
    while(t--)
    {
        int n;
        string str;
        cin>>n>>str;
        vector<int>v;
        int len=1;
        for(int i=1;i<n;i++)
        {
            if(str[i]==str[i-1])len++;
            else
            {
                v.push_back(len);
                len=1;
            }
        }
        v.push_back(len);
        if(v.size()>1&&str[0]==str[n-1])
        {
            v[v.size()-1]=v.back()+v[0];
            v[0]=0;
        }
        if(v.size()==1)cout<<(n-1)/3+1<<endl;
        else
        {
            int ans=0;
            for(int i=0;i<v.size();i++)ans+=(v[i]/3);
            cout<<ans<<endl;
        }
        
    }
    
    return 0;
}

```




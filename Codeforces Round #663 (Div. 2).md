###### [C. Cyclic Permutations](https://codeforces.com/contest/1391/problem/C)

题意：n的全排列，每一种排列中每个数可以和左边第一个大于它的数建一条无向边，也可以和右边第一个大于它的数建一条无向边。求这n的全排列中能构成环的排列的数量。

当一个数左右两边都存在比这个数大的数时能构成环

```c++
#include <iostream>
#include <algorithm>
using namespace std;
typedef long long ll;
const int mod=1e9+7;
ll qmi(ll m, ll k, ll p)
{
    ll res = 1 % p, t = m;
    while (k)
    {
        if (k&1) res = res * t % p;
        t = t * t % p;
        k >>= 1;
    }
    return res;
}

int main()
{
    ll n;
    scanf("%lld",&n);
    ll ans=1;
    for(int i=1;i<=n;i++)ans=ans*i%mod;
    ll ans1=(ans-qmi(2, n-1, mod)+mod)%mod;
    printf("%lld\n",ans1);
    
    return 0;
}
```


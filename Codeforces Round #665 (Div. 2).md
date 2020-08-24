###### [C. Mere Array](https://codeforces.com/contest/1401/problem/C)

题意：给一个大小为n的数组，当两个数的最大公因数等于数组中最小的数的时候，两个数可以交换。如果可以使数组最终变成非递减的数组，输出YES。

先判断哪些位置的元素不需要改变，再判断剩下的元素是否都是数组中最小的数的倍数。

```c++
#include <iostream>
#include <cmath>
#include<vector>
#include <algorithm>
using namespace std;
const int N=1e5;
int a[N];
int main()
{
    int t;
    scanf("%d",&t);
    while(t--)
    {
        int n;
        scanf("%d",&n);
        vector<int>v;
        for(int i=1;i<=n;i++)
        {
            scanf("%d",&a[i]);
            v.push_back(a[i]);
        }
        sort(v.begin(),v.end());
        int ans=0;
        int ans1=0;
        int minn=v[0];
        for(int i=1;i<=n;i++)
        {
            if(a[i]==v[i-1])
            {
                ans++;
                continue;
            }
            if(a[i]%minn==0)ans1++;
            
        }
        if(ans+ans1==n)puts("YES");
        else puts("NO");
        
    }
    return 0;
}
```


# cf665

https://codeforces.com/contest/1401

A签到水题

```
#include<bits/stdc++.h>
using namespace std;
int main()
{
	int T,n,k;cin>>T;
	while(T--)
	{
		cin>>n>>k;
		if(n>k)
		{
			if((n-k)%2==0)puts("0");
			else puts("1");
		}
		else printf("%d\n",abs(n-k));
	}
	return 0;
}
```

B

给元素只有012的两个序列a，b，ci = ai x bi，ai > bi 时ci = ai x bi，ai = bi 时ci = 0，ai ＜bi 时 ci = - ai x bi。

知只有a2b1时ci = 2，a1b2 时ci= -2，其他都是0

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int main()
{
 int T; cin >> T;
 while (T--)
 {
  int x1, y1, z1;
  int x2, y2, z2;
  ll ans;
  cin >> x1 >> y1 >> z1;
  cin >> x2 >> y2 >> z2;
  ans = min(z1,y2);//先让a的2和b的1配对 

	z1 -= min(z1,y2);//a序列还剩几个 2
	z2 -= (z1 + x1) ;//b序列的2 和 a序列的 2和1 相结合都不会出-2，故舍去
	ans -= z2>=0 ? z2 : 0 ;
	ans <<=1;  
 	cout<<ans <<endl;
}
return 0;
}
```

C

给一个正整数序列 a,if gcd(ai , aj) == min(a)，ai aj可以互换位置，问任意次互换能否令a数组非降序。要点：所有是min(a)倍数的元素都可以互换位置

找到min(a),对于不是mi倍数的元素，排序后如果位置不变就说明没问题，否则无法实现。

```
#include<bits/stdc++.h>
using namespace std;

const int mxn = 2e5 + 10;
typedef long long ll;

int a[mxn];
int b[mxn],c[mxn];
int vis[mxn];

int T,n;

int main()
{
    
    cin >> T;
    while(T--)
	{
        cin >> n;
        memset(vis,0,sizeof(vis));
        for(int i = 1;i <= n;i++)
		{
            cin >> a[i];b[i] = a[i];
            c[i]  =a[i];
        }
		sort(c+1,c+1+n);
        int mi = c[1];
        for(int i = 1;i <= n;i++)
		{
            if(a[i] % mi != 0)
			{
                vis[i] = 1;
            }
        }

        sort(a+1,a+1+n);

        int f = 1;
        for(int i = 1;i <= n;i++)
		{
            if(vis[i] && a[i] != b[i])
			{
                f = 0;
                break;
            }
        }
        if(f==0)puts("NO");
        else puts("YES");
    }

}

```


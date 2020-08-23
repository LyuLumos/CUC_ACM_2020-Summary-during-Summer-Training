# cf659



https://codeforces.com/contest/1384

A T次提问，每次n个数，表示第i个字符串和第i+1个字符串前a[i]个字符是相同的，要求按给定的数组输出n+1个字符串

由于字符串最长200，第一个串输出200个'a',后续字符串根据a[i]修改即可，只要修改第a[i]+1个字符，就能让前a[i]个字符和前字符串保持一致。

```
#include<bits/stdc++.h>
using namespace std;
int num[500];
int main()
{
	int t,n,tmp;cin>>t;
	while(t--)
	{
		cin>>n;
		for(int i = 1;i<=n;i++)scanf("%d",num+i);
		string s(20,'a');
		cout<<s<<endl;
		for(int i = 1;i<=n;i++)
		{
			tmp = num[i];
			if(s[tmp]=='a')s[tmp]='b';
			else s[tmp] = 'a';
			cout<<s<<endl;
		}
		
	}
	return 0;
 } 
```

b1

有n个存在初始深度的海域，有个人可以从任意一个海域出发，要在2 x k x n的时长里经过全部海域，如果所处海域深度大于l人会淹死，每个时间里都可以采取移动或停止两种操作。另外在每2*k个时段里，海域深度前k秒每秒+1，后k秒每秒-1，问最后能否经历完全部海域。

设dp【i】【j】为经过i海域时为j 秒，转移方程来源于 上一秒是否移动，每次转移需要判断深度，海洋深度的变化量用前缀和可以处理，t%(2*k)就能定位到当前处于2k秒里的哪一秒。

```
#include<bits/stdc++.h>
using namespace std;
const int mxn = 500;
const int mxm = 2e4+2;
#define ms(x,y) memset(x,y,sizeof(x))
int a[mxn],up[mxn],dp[mxn][mxm],n,T,l,k;

int main()
{
	cin>>T;
	while(T--)
	{
		ms(dp,0);
		scanf("%d%d%d",&n,&k,&l);
		for(int i =0;i<=k;i++)up[i]=i;//第i秒相比开头增加的深度
		for(int i = 1;i<k;i++)up[k+i]=k-i;
		for(int i = 0;i<2*k;i++)dp[0][i]=1; 
		for(int i = 1;i<=n;i++)scanf("%d",a+i);
		for(int i = 1;i<=n;i++)
		{
			for(int j = 0;j<2*k*n;j++)
			{
				dp[i][j] = max(dp[i][j-1],dp[i-1][j-1]);
				int nw = a[i]+up[j%(2*k)];
				if(nw > l)dp[i][j] = 0;
			}
		}
		int f = 0;
		for(int i = 0;i<2*k*n;i++)
		{
			if(dp[n][i])
			{
				f=1;
				break;
			}
		}
		if(f)puts("Yes");
		else puts("No");
	}
	return 0;
}
```

C

给两个字符串a和b，定义一次操作为：指定一个字母，把a串里全部字母的元素都改成另一个元素，问至少几次操作能令字符串相等。

由于每次操作只能把元素变大，因此如果a中某元素大于b就必定无解。

二维数组t表示两个字母的对应关系，每次移动都相当于把某一列的值移动到另一列，相当于执行一次操作。

[![dFK7fP.md.png](https://s1.ax1x.com/2020/08/15/dFK7fP.md.png)](https://imgchr.com/i/dFK7fP)

```
#include<bits/stdc++.h>
using namespace std;
const int mxn = 30;
int t[mxn][mxn];
int main()
{
	int T;cin>>T;
	while(T--)
	{
		
		memset(t,0,sizeof(t));
		int n,d,ans = 0;
		string a,b;
		cin>>n>>a>>b;
		int f = 0;
		for(int i = 0;i<n;i++)
		{
			if(a[i]>b[i])
			{
				puts("-1");
				f=1;
				break;
			}
			t[(int)(b[i]-'a'+1)][(int)(a[i]-'a'+1)] = 1 ;
		}
		if(f)continue;
		for(int i = 1;i<=26;i++)//按列遍历 
		{
			f=  0;
			for(int j = i+1;j<=26;j++)//j表示行 
			{
				if(t[j][i] > 0)
				{
					if(!f)
					{
						f = 1;
						d = j-i;
					}
					else  t[j][i+d]++;
				}
			}
			ans += f;
		}
		cout<<ans<<endl;
	}
	return 0;
}
```

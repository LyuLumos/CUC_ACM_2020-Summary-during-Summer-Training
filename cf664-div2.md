# cf664 

https://codeforces.com/contest/1395

A

给a，b，c，d个红，绿，蓝，白球，每次操作能把前三种颜色的球各一个改为白色，问能否通过任意次操作令这些球排成回文序列。

能否排成回文取决于这些球的奇偶，每次操作都会改变奇偶，则比较操作0次和1次的情况即可。

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll a[5];
int main()
{
	int T;cin>>T;
	while(T--)
	{
		int sum =0;
		for(int i = 0;i<4;i++)scanf("%lld",a+i);
		for(int i = 0;i<4;i++)if(a[i]%2==1)sum++;
		if(sum <=1 )puts("YES");
		else if(a[0]&&a[1]&&a[2])
 		{ 
			for(int i = 0;i<3;i++)a[i]--;
			a[3]+=3;
			sum = 0;
			for(int i = 0;i<4;i++)if(a[i]%2==1)sum++;
	//		cout<<sum<<endl;
			if(sum <=1 )puts("YES");
			else puts("NO");
		}
		else puts("NO");
		
	}
	return 0;
}
```



B

给一个nxn矩阵和一个坐标作为起点，可以任意移动到当前行/列的任意一点，求一个方案不重复地遍历矩阵每个点。

思维题，直接移动到左上角，依行s型遍历即可。

```
#include<bits/stdc++.h>
using namespace std;
#define fi first
#define se second
const int mxn = 500;
typedef pair<int,int> pii;
vector<pii>v;
int n,m,x,y;
int vis[mxn][mxn];
int main()
{
	memset(vis,0,sizeof(vis));
	cin>>n>>m>>x>>y;
	v.push_back(make_pair(x,y));
	v.push_back(make_pair(1,y));
	v.push_back(make_pair(1,1));
	vis[x][y]=vis[1][y]=vis[1][1]=1;
	for(int i = 1;i<=n;i++)
	{
		if(i%2==1)
		{
			for(int j = 1;j<=m;j++)
			{
				if(vis[i][j] ==0)	v.push_back(make_pair(i,j));
			}
		}
		else 
		{
			for(int j = m;j>=1;j--)
			{
				if(vis[i][j]==0) v.push_back(make_pair(i,j));
			}
		}
	}
	for(int i =0;i<v.size();i++)cout<<v[i].fi<<" "<<v[i].se<<endl;
	return 0;
}
```



C

给n个元素的a数组和m个元素的b数组，对于每个ai，找到任意一个bj，得到ci = ai & bj，

问全部ci与起来的最小值。

设全部ｃｉ与起来＝ａｎｓ，从０开始枚举ａｎｓ结果，对于每个ａｎｓ，如果找到一组ｃｉ｜ａｎｓ　＝＝ａｎｓ，由于｜运算不会令结果变小，所以这个ａｎｓ就是最小的结果了。

```
#include <bits/stdc++.h>
using namespace std;
int n,m,a[209],b[209];
bool check(int x)
{
	for(int i=1;i<=n;i++)
	{
		int f=0;
		for(int j=1;j<=m;j++)
		{
			int tmp=a[i] & b[j];
			if( （tmp |ｘ）　＝＝　ｘ )	f=1;
			if( f )	break;
		}
		if( f==0 )	return false;
	}
	return true;
}
int main()
{
	cin >> n >> m;
	for(int i=1;i<=n;i++)	cin >> a[i];
	for(int i=1;i<=m;i++)	cin >> b[i];
	for(int i=0;i<(1<<9);i++)
	if( check(i) )
	{
		cout << i;
		return 0;
	}
}
```

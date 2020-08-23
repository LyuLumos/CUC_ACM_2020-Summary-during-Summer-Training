#cf662

https://codeforces.com/contest/1393

A水题

给一个nxn矩阵，轮流涂两种颜色，每次涂的格子与上一回合的格子相连，问需要几个回合。每次涂一圈，总次数就是边长/2+1。

```
#include<bits/stdc++.h>
using namespace std;
int main()
{
	int T,n;
	cin>>T;
	while(T--)
	{
		cin>>n;
		cout<<n/2+1<<endl; 
	}
	return 0;
}
```

B

给一定量的木板，问能否围成一个正方形和一个长方形（不共用边），给q次询问，每次输出当前状态能不能。

暴力计数会T，需要改成在线计数。

```
#include<bits/stdc++.h>
#define fi it->first
#define se it->second
using namespace std;
int main()
{
	
	map<int,int >mp;
	int n,q,tmp,cnt2=0,cnt4=0;
	cin>>n;
	for(int i = 1;i<=n;i++)
	{
		scanf("%d",&tmp);
		mp[tmp]++;
		if(mp[tmp]%2==0)cnt2++;
		if(mp[tmp]%4==0)cnt4++;
	}
	cin>>q;
	char ch[2];
	while(q--)
	{
		scanf("%s %d",ch,&tmp);
		//cout<<cnt2<<" "<<cnt4<<endl;
		if(ch[0]=='+')
		{
			mp[tmp]++;
			if(mp[tmp]%2==0)cnt2++;
			if(mp[tmp]%4==0)cnt4++;
		}
		else
		{
			if(mp[tmp]%2==0)cnt2--;
			if(mp[tmp]%4==0)cnt4--;
			mp[tmp]--;
		}
		if(cnt4>=1&&cnt2>=4)puts("YES");
		else puts("NO"); 
		
	 } 
	return 0;
}
```

C

给n个数字，把这些数字按照一定顺序排列后，使得数值相等的数字之间的间距的最小值最大。

举个栗子：1 1 1 2 2 2 3 3 3 4 4 6 7 8

先找到出现次数最多的1,2,3，然后确定位置：1,2,3…1,2,3…1,2,3，中间空位用来放那些次数较少的元素，设次数最多为mx，出现次数等于mx的元素个数为ct，则出现次数小于mx的元素个数就是（n-mx * ct），中间空位则是（mx-1），相除结果加上（mx-1）每个循环的长度 就是答案。

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int main()
{
	int T;cin>>T;
	while(T--)
	{
		ll n;cin>>n;
		vector<ll>cnt(n+1,0);
		ll mx = 0;
		for(int i = 1;i<=n;i++)
		{
			ll tmp ;cin>>tmp;
			cnt[tmp]++;
			mx = max(mx,cnt[tmp]);
		}
		ll ct = 0;//出现mx次的元素的个数
		for(int i = 1;i<=n;i++)
		{
			if(cnt[i] == mx)ct++;
		 } 
		
		ct += ((n-mx*ct)/(mx-1) ); 
		cout<<ct-1<<endl;
	}
	return 0;
 } 
```

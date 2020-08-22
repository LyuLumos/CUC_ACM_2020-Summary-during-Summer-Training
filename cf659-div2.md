## **Codeforces Round #659 (Div. 2)**



### [A. Common Prefixes](http://codeforces.com/contest/1384/problem/A)


### **题意**  

给定一个大小为n的数组，构造n+1个字符串，使相邻两个字符串的最长相同前缀长度为数组中的数大小

### **思路**  


先给所有字符串规定一个固定长度（数组a的最大值），输出第一个字符串是abcd……，用数组b来存一下当前字符串si，在a[i]范围内（si与si+1相同），数组b不变，直接输出作为si+1的一部分，超出a[i]后，si和si+1就不同了，给b[i]重新赋值成b[i]+1后输出，这样现在数组b存放的就是si+1,此后si+2再由当前b做出相应变化得出……

### **代码** 
```
#include<iostream>
#include<string>
#include<stdio.h>
#include<algorithm>
using namespace std;
const int maxn=105;
int a[maxn];
char b[maxn];
int main()
{
	int t;
	scanf("%d",&t);
	while(t--)
	{
		int n;
		int maxa=-1;
		scanf("%d",&n);
		for(int i=0;i<n;i++)
		{
			scanf("%d",&a[i]);
			maxa=max(a[i],maxa);
		}
		if(maxa==0)
		{
			for(int i=0;i<=n;i++)
			{
			
				for(int j=0;j<=i;j++)
				{
				
					printf("%c",97+i+j%26);
				} 
				printf("\n");	 
			}
		}
		else
		{
		
		for(int i=0;i<maxa;i++)
		{
			printf("%c",97+i%26);
			b[i]=97+i%26;
		}
		printf("\n");
		for(int i=0;i<n;i++)
		{
			for(int j=0;j<maxa;j++)
			{
				if(j<a[i])
				{
					printf("%c",b[j]);
				}
				else
				{
					printf("%c",(b[j]-97+1)%26+97);
					b[j]=(b[j]-97+1)%26+97;
				}
					
			}
			printf("\n");
		}
	}
	}
	return 0;
}
```


### [B1. Koa and the Beach (Easy Version)](http://codeforces.com/contest/1384/problem/B1)


### **题意**  

在n个位置处有各自的海水深度,每 2 * k秒，前k秒每秒深度 +1 ，后 k 秒每秒深度 -1；每秒Koa可以停留也可以去下一个海域。问他最后能不能安全到达岸边

### **思路** 

dp, 核心语句是`dp[i][j] = max(dp[i][j - 1], dp[i - 1][j - 1]);`

dp[i][j]数组代表j秒到达第i片海域是否合法

dp[i][j-1]表示上一秒在第i片海域选择不移动

dp[i-1][j-1]表示上一秒在第i-1片海域选择向右移动

最终判断dp[n][i]是否合法，合法输出YES即可

### **代码** 
```
#include <iostream>
#include <cstdio>
#include <cmath>
#include <string>
#include <cstring>
#include <stack>
#include <map>
#include <queue>
#include <vector>
#include <set>
#include <algorithm>
#include <iomanip>
	using namespace std;
const int N = 1e2 + 5, M = 2e4 + 5;
int a[105], b[300];
int dp[105][M];

int main()
{
	int t;
	cin >> t;
	while (t--)
	{
		memset(dp, 0, sizeof(dp));
		int n, k, l;
		scanf("%d %d %d", &n, &k, &l);
		for (int i = 1; i <= n; i++)
		    scanf("%d", &a[i]);

		for (int i = 0; i <= k; i++) 
			b[i] = i;
		for (int i = 1; i < k; i++) 
			b[k + i] = k - i;
		for (int i = 0; i < 2 * k; i++) 
			dp[0][i] = 1;
		for (int i = 1; i <= n; i++)
			for (int j = 0; j < 2 * k * n; j++)
			{
				dp[i][j] = max(dp[i][j - 1], dp[i - 1][j - 1]);
				if (l < b[j % (2 * k)] + a[i]) 
					dp[i][j] = 0;
			}
		int flag = 0;
		for (int i = 0; i < 2 * k * n; i++)
			if (dp[n][i])
			{ 
				flag = 1; 
				break;
			}
		if (flag) 
			printf("Yes\n");
		else 
			printf("No\n");
	}
	return 0;
}

```
### [B2. Koa and the Beach (Hard Version)](https://codeforces.com/contest/1384/problem/B2)

### **题意**  
在n个位置处有各自的海水深度，Koa有一个自己能承受的深度，海水会经历涨潮退潮，Koa可以在n个位置处停留任意时间，问他最后能不能安全到达岸边

### **思路**  
初始的时候限制区间是[-k,k]，设lim=l-d[i]，如果lim>=k则可以再把限制区间设成初始值（因为在这个点始终不会溺水），否则当前限制区间取原先的限制区间和[-lim,lim]的交集，前往下一个位置的时候区间要右移，（因为游到下一个位置需要1s，这1s里涨潮退潮还在继续）最后判断是否存在这样一个符合条件的区间，存在就输出YES，不存在就输出NO

### **代码**

```
#include<algorithm>
using namespace std;
const int maxn=3e5+5;
int d[maxn];
int main()
{
	int t;
	scanf("%d",&t);
	while(t--)
	{
		int n;
		int k,l;
		scanf("%d %d %d",&n,&k,&l);
		for(int i=0;i<n;i++)
		{
			scanf("%d",&d[i]);
		}
		int L=-k,R=k;
		int flag=1;
		for(int i=0;i<n;i++)
		{
			L++,R++;
			int tmp=l-d[i];
	
			if(tmp<0)
			{
				flag=0;
				break;
			} 
			if(tmp>=k)
			L=-k,R=k;
			else
			{
				L=max(L,-tmp);
				R=min(R,tmp);
			}
			if(L>R)
			{
				flag=0;
				break;
			}
			
		}
		if(flag)cout<<"Yes\n";
		else cout<<"No\n";
		
	}
	return 0;
}
```


### [C.String Transformation 1](https://codeforces.com/contest/1384/problem/C)

### **题意**  
将字符串A变为字符串B,字符串由a~t种字母构成，规则是可以同时改变相同字母成某一个比它大的字母，问最少需要操做几步

### **思路**  
无论如何应当先操作最小的字母到它需要的此小字母，如afa,spp,应当先操作a到p,然后操作f到p,最后操作其中一个p到s。代码如下

### **代码**  
```  
#include <algorithm>
#include <iostream>
#include <iomanip>
#include <cstring>
#include <string>
#include <cstdio>
#include <queue>
#include <stack>
#include <cmath>
#include <map>
using namespace std;
typedef long long ll;
const int maxn = 1e5 + 20;
const int mod = 1e9 + 7;
char a[maxn], b[maxn];
int main()
{
	int t;
	scanf("%d", &t);
	while (t--)
	{
		int n;
		scanf("%d", &n);
		scanf("%s", a);
		scanf("%s", b);
		int flag = 1;
		int tt[30][30] = { 0 };
		for (int i = 0; i < n; i++)
		{
			if (b[i] < a[i])
			{
				flag = 0;
				break;
			}
			if (b[i] == a[i])
				continue;
			tt[a[i] - 'a'][b[i] - 'a']++;
		}
		if (!flag)
		{
			printf("-1\n");
			continue;
		}
		int ans = 0;
		for (int i = 0; i < 25; i++)
		{
			for (int j = 0; j < 25; j++)
			{
				if (tt[i][j])
				{
					ans++;
					for (int k = j + 1; k < 25; k++)
					{
						if (tt[i][k])
							tt[j][k]++;
					}
					break;
				}
			}
			
		}
		printf("%d\n", ans);
	}
}
```  


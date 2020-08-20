## **Codeforces Round #664 (Div. 2)**


### [A. Boboniu Likes to Color Balls](https://codeforces.com/contest/1395/problem/A)  

### **题意**  
给定四种颜色的球，可以不做任何操作，也可以同时分别使一个红、绿、蓝球变成三个白球，使最后能排成回文对称直线。如果可以排成，输出YES，否则输出NO

### **思路**  

先判断不做操作时能否排成；
再判断操作一次后能否排成；如果都不能则输出NO
（之所以只判断操作一次，是因为操作两次后奇偶性不变）
 
### **代码**  
 ```
#include <algorithm>
#include <iostream>
#include <cstdio>
#include <queue>
#include <stack>
#include <cmath>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int maxn = 1e5 + 20;
const int maxm = 2e5 + 20;
const int mod = 1e9 + 7;

int main()
{
	int t, r, g, b, w;
	int ans;
	scanf("%d", &t);
	for (int i = 0; i < t; i++) {
		scanf("%d%d%d%d", &r, &g, &b, &w);
		ans = 0;		
		ans = r % 2 + g % 2 + b % 2 + w % 2;
		if (ans <= 1)//有一种颜色是单数、都是双数
			printf("Yes\n");
		else {
			if (!r || !g || !b)
				printf("No\n");
			else {
				int k = (r - 1) % 2 + (g - 1) % 2 + (b - 1) % 2 + (w + 3) % 2;
				if (k <= 1)
					printf("Yes\n");
				else
					printf("No\n");
			}
				
		}
	}
	return 0;
}
```

### [B.Boboniu Plays Chess](https://codeforces.com/contest/1395/problem/B)  

### **题意**  
给定棋盘大小，和初始位置，每次移动只能移到同一列或同一行上，要求棋盘每格都遍历一遍

### **思路**  
其实就是构建一种方式便好，直接上代码！

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
const int maxn = 2e5 + 20;
const int mod = 1e9 + 7;
int t;
int arr[maxn];
vector <int> fv;
vector <int> lv;
int brr[maxn];
int main()
{
	int a, b, c, d;
	scanf("%d %d %d %d", &a, &b, &c, &d);
	for (int i = c; i <= a; i++)
	{
		printf("%d %d\n", i, d);
	}
	for (int i = c - 1; i >= 1; i--)
	{
		printf("%d %d\n", i, d);
	}
	int p = 1, q = 1;
	if (c != 1)
	{
		while (true)
		{
			if (q == d)
			{
				q++;
			}
			if (q > b)
			{
				break;
			}
			for (int i = 1; i <= a; i++)
			{
				printf("%d %d\n", i, q);
			}
			q++;
			if (q == d)
			{
				q++;
			}
			if (q > b)
			{
				break;
			}
			for (int i = a; i >= 1; i--)
			{
				printf("%d %d\n", i, q);
			}
			q++;
		}
	}
	else if (c == 1)
	{
		while (true)
		{
			if (q == d)
			{
				q++;
			}
			if (q > b)
			{
				break;
			}
			for (int i = a; i >= 1; i--)
			{
				printf("%d %d\n", i, q);
			}
			q++;
			if (q == d)
			{
				q++;
			}
			if (q > b)
			{
				break;
			}
			
			for (int i = 1; i <= a; i++)
			{
				printf("%d %d\n", i, q);
			}
			q++;
		}
	}
}
```  





### [C.Boboniu and Bit Operations](https://codeforces.com/contest/1395/problem/C)  

### **题意**  
ci=ai&bj,其中j为任意数,求c1|c2……|cn的最小值

### **思路**  
暴力枚举便好
 
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
const int maxn = 2e5 + 20;
const int mod = 1e9 + 7;
int t;
int arr[205];
int brr[205];
int main()
{
	int n, m;
	scanf("%d %d", &n, &m);
	for (int i = 0; i < n; i++)
	{
		scanf("%d", &arr[i]);
	}
	for (int i = 0; i < m; i++)
	{
		scanf("%d", &brr[i]);
	}
	for (int i = 0; i < 1 << 9; i++)
	{
		int flag = 1;
		for (int j = 0; j < n; j++)
		{
			int ff = 0;
			for (int k = 0; k < m; k++)
			{
				if (((arr[j] & brr[k]) | i) == i)
				{
					ff = 1;
					break;
				}
			}
			if (ff == 0)
			{
				flag = 0;
				break;
			}
		}
		if (flag == 1)
		{
			printf("%d\n", i);
			return 0;
		}
	}
}
```  




### [D. Boboniu Chats with Du](https://codeforces.ml/contest/1395/problem/D)  

### **题意**   
当乐趣值大于管理员的心情阈值m时，会被禁言d天，小于m则无事发生，问在n天里怎么取得乐趣值最大的总和。 

### **思路**    
采用贪心的思想，把小于和大于m的分成两块，从大到小排序。大于m会消耗d+1天（但最后一天惹怒管理员不会被禁言，所以最后一天乐趣值必定要大于m）。然后枚举，选择惹怒管理员1次，（大于m的取一个，其他天都是小于m），2次……，答案取这些里面最大的（注意消耗的天数要小于n）。

### **代码**  
```  
#include<iostream>
#include<algorithm>
#include<cstring>
using namespace std;
typedef long long ll;
const int maxn=1e5+10;
ll n,m,d;
ll a[maxn],b[maxn];
ll pra[maxn],prb[maxn];
bool cmp(ll a,ll b)
{
    return a>b;
}
ll ans;
int main()
{
    ll i,j,x;
    ll len1=0,len2=0;
    cin>>n>>d>>m;
    for(i=1;i<=n;i++)
    {
        cin>>x;
        if(x>m)
            a[++len1]=x;
        else
            b[++len2]=x;
    }
    sort(a+1,a+len1+1,cmp);
    sort(b+1,b+len2+1,cmp);
    for(i=1;i<=len1;i++)
        pra[i]=pra[i-1]+a[i];
    for(i=1;i<=len2;i++)
        prb[i]=prb[i-1]+b[i];
    ans=prb[len2];
    for(i=1;i<=len1;i++)
    {
        int k=(i-1)*(d+1)+1;
        if(k>n)
            break;
        ll t=min(n-k,len2);
        ans=max(ans,pra[i]+prb[t]);
    }
    cout<<ans<<endl;
    return 0;
}  
```  


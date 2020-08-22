## **Codeforces Round #661 (Div. 3)**



### [A. Remove Smallest](http://codeforces.com/contest/1399/problem/A)


### **题意**  


每次选两个数，如果这两个数差的绝对值小于等于1，则删掉小的那个，如果相等，则随便删一个，问是否最后只剩一个数
### **思路**  

排序，若相邻元素差值大于1，则输出NO，否则输出YES


### **代码** 
```
#include<stdio.h>
#include<iostream>
#include<algorithm>
#include<string.h>
#include<cmath>
#pragma warning(disable:4996)
using namespace std;
typedef long long ll;
const int maxn=105;
int a[maxn];
int main()
{
	int t;
	scanf("%d",&t);
	while(t--)
	{
		int n;
		int flag=0;
		scanf("%d",&n);
		for(int i=0;i<n;i++)
		{
			scanf("%d",&a[i]);
		}
		sort(a,a+n);
		for(int i=1;i<n;i++)
		{
			if(a[i]-a[i-1]>1)
			{
				flag=1;
				break;
			}
		}
		if(flag)printf("NO\n");
		else printf("YES\n");	
	}
	return 0;
}
```

### [B. Gifts Fixing](http://codeforces.com/contest/1399/problem/B)


### **题意**  

有n份礼物，礼物又分为a,b类，要使n份中a类数量相同，b类数量相同。操作分为a类礼物减1，b类礼物减1，a、b两类同时减1。求最小的操作数
### **思路** 

分别找到a、b类中的最小值，求a,b类中每个礼物数量差的最大值之和即可
### **代码** 
```
#include<stdio.h>
#include<iostream>
#include<algorithm>
#include<string.h>
#include<cmath>
#pragma warning(disable:4996)
using namespace std;
typedef long long ll;
const int maxn=55;
int a[maxn];
int b[maxn];
int main()
{
	int t;
	scanf("%d",&t);
	while(t--)
	{
		int n;
		ll ans=0;
		scanf("%d",&n);
		ll mina=1e9+5;
		ll minb=1e9+5;
		for(int i=0;i<n;i++)
		{
			scanf("%d",&a[i]);
			if(a[i]<mina)mina=a[i];
		}
		for(int i=0;i<n;i++)
		{
			scanf("%d",&b[i]);
			if(b[i]<minb)minb=b[i];
		}
		
		for(int i=0;i<n;i++)
		{
			ans+=max(a[i]-mina,b[i]-minb);
		}
		printf("%lld\n",ans);
	}
	return 0;
}
```




### [C. Boats Competition](http://codeforces.com/contest/1399/problem/C)


### **题意**  

对n个人进行两两配对组成队伍，求最多可以组成多少对权重相同的队伍
### **思路** 

排序，2-2*n中暴力列举，双指针计算权重即可
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
int arr[55];
int brr[105];
int main()
{
	scanf("%d", &t);
	while (t--)
	{
		int n;
		int ans = 0;
		scanf("%d", &n);
		for (int i = 0; i < n; i++)
		{
			scanf("%d", &arr[i]);
		}
		sort(arr, arr + n);
		for (int i = 1; i <= 2 * n; i++)
		{
			int tmp = 0;
			int f = 0, l = n - 1;
			while (f < l)
			{
				if (arr[f] + arr[l] == i)
				{
					tmp++;
					f++;
					l--;
				}
				else if (arr[f] + arr[l] < i)
				{
					f++;
				}
				else if (arr[f] + arr[l] > i)
				{
					l--;
				}
			}
			ans = max(ans, tmp);
		}
		printf("%d\n", ans);
		
	}
} 
```

### [D.Binary String To Subsequences](https://codeforces.com/contest/1399/problem/D)

### **题意**  
找到最少有多少个1010...的子序列

### **思路**  
开两个栈，一个记录0一个记录1，分别匹配

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
//const int maxn = 2e5 + 20;
const int mod = 1e9 + 7;
#define maxn 200010
char s[maxn];
int stack0[maxn], top0, stack1[maxn], top1, a[maxn];
int main() {
	int t, n, i, k;
	scanf("%d", &t);
	while (t--) {
		scanf("%d%s", &n, s + 1);
		top0 = top1 = k = 0;
		for (i = 1; i <= n; i++) {
			if (s[i] == '0') {
				if (top1 > 0)//10
				{
					stack0[++top0] = stack1[top1--];//移到栈1
				}
				else 
				{ 
					stack0[++top0] = ++k; 
				}
				a[i] = stack0[top0];//记录i位置字母所属的子串
			}
			else {
				if (top0 > 0)//01配对
					stack1[++top1] = stack0[top0--];
				else stack1[++top1] = ++k;
				a[i] = stack1[top1];//记录i位置字母所属的子串
			}
		}
		printf("%d\n", k);
		printf("%d", a[1]);
		for (i = 2; i <= n; i++)printf(" %d", a[i]);
		printf("\n");
	}
	return 0;
}
```  
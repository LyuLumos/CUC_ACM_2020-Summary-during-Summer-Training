## **Codeforces Round #663 (Div. 2)**



### [A. Suborrays](http://codeforces.com/contest/1391/problem/A)


### **题意**  
给定整数n，找到1-n的全排列$p_iORp_{i+1}OR...p_{j-1}ORp_{j}\geqslant j-i+1$

即每个子序列的按位或之和不小于其中元素的数量
### **思路**  
x|y>=max(x,y)

输出任意序列都可满足要求


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

int main()
{
	scanf("%d", &t);
	while (t--)
	{
		int n;
		scanf("%d", &n);
		for (int i = 1; i <= n; i++)
		{
			printf("%d%c", i, i == n ? '\n' : ' ');
		}
	}
}
```

```
#include<stdio.h>
#include<algorithm>
#include<string.h>
#include<cmath>
#pragma warning(disable:4996)
using namespace std;
typedef long long ll;
int main()
{
	int t;
	scanf("%d",&t);
	while(t--)
	{
		int n;
		scanf("%d",&n);
		for(int i=0;i<n-1;i++)
		{
			printf("%d ",i+2);
		}
		printf("1\n");
	}
	return 0;
}
```

### [B. Fix You](http://codeforces.com/contest/1391/problem/B)


### **题意**  

在n×m的网格中，任意一个点按照D/R的指示都能到达最右下角的点
### **思路** 

除右下角的点，所有点都会到达最下面/最右面一行/列。到达最下行/最右列时，只有一个方向R/D可以走，计算不能到的块数即可
### **代码** 
```
#include<stdio.h>
using namespace std;
const int maxn=105;
char s[maxn][maxn];
int main(){
	int t,n,m,i,j,cnt,nr,nc;
	scanf("%d",&t);
	while(t--){
		scanf("%d%d",&n,&m);
		for(i=0;i<n;i++)scanf("%s",s[i]);
		cnt=0;
		for(i=0;i<n-1;i++)
		{
			if(s[i][m-1]!='D')cnt++;
		}
		for(i=0;i<m-1;i++)
		{
			if(s[n-1][i]!='R')cnt++;
		}
		printf("%d\n",cnt);
	}
}
```

### [C. Cyclic Permutations](http://codeforces.com/contest/1391/problem/C)


### **题意**  

给定一个n的全排列构造图，每个数可以与左边第一个大于它的数、右边第一个大于它的数连成边。求在n的全排列中可以存在环的排列数
### **思路** 

参考了网上的巧妙思路，即如果一个数的两侧都有比它大的数，则会成环。故不能成环数：以n为中心，其他数在n前/后，有$2^{n-1}$种情况。能成环可能为$n!-2^{n-1}$种
### **代码** 
```
#include <iostream>
#include <cstdio>
using namespace std;
#define ll long long int
using namespace std;
const int mod = 1e9 + 7;

ll qPow(int a, int b) {
    ll ans = 1;
    ll base = a;
    while (b) {
        if (b & 1) ans =ans*base%mod;
        base = base*base%mod;
        b >>= 1;
    }
    return ans;
}

int main()
{
    int n;
    scanf("%d", &n);
    ll ans;
    ll s = 1;
    for (int i = 1; i <= n; i++) 
        s = s*i % mod;
    ll q = qPow(2, n - 1);
    ans = ((s - q) + mod) % mod;
    cout << ans << endl;
    return 0;
    
}
```





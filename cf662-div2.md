## **Codeforces Round #662 (Div. 2)**



### [A. Rainbow Dash, Fluttershy and Chess Coloring](http://codeforces.com/contest/1393/problem/A)


### **题意**  

每回合上不同的颜色，每次只在已填好色方格的上下左右填色，求使这个棋盘颜色相间的最小操作数

### **思路**  

最后结果为n/2+1


### **代码** 
```
#include <algorithm>
#include <iostream>
#include <cstring>
#include <string>
#include <cstdio>
using namespace std;

int main()
{
    int t,n;
    scanf("%d",&t);
    while(t--){
        scanf("%d",&n);
        printf("%d\n",(n+2)/2);
    }

	return 0;
}
```


### [B. Applejack and Storages](http://codeforces.com/contest/1393/problem/B)


### **题意**  
想建一个长方形和正方形的仓库，在经过一系列的交易（进货和卖掉）之后，问还有没有足够的材料来建它的仓库。  


### **思路**   
用cnt数组统计每种长度的木材有多少个，比如cnt[1]=2，就是长度为1的木材有两块。把相同长度的木材放在一堆。再用num数组统计适数量相同的的堆。num[1]=2，就是数量为1的队有两个。因为数量为1，2，3的堆有是不能构成正方形的，就把这些木板放到一边，看剩下有多少木板，用a表示，（因为接下来是从num[4]开始，所以a=0或a>=4）。a=0,不能建仓库，a=4||5，从数量为2，3的堆里找长方形的4条边，a=6||7，从数量为2，3的堆里找长方形的两条边，a>=8就不用从数量为2，3的堆里找了。


### **代码** 
```
#include<cstdio>
#include<algorithm>
using namespace std;
const int maxn=100010;
int cnt[maxn],num[maxn];
char cmd[5];
int main(){
	int n,i,q,a,b,len=0;
	scanf("%d",&n);
	for(i=1;i<=n;i++)
	{
		scanf("%d",&a);
		cnt[a]++;
		len=max(a,len);
	}
 
	for(i=1;i<=len;i++)num[cnt[i]]++;
	scanf("%d",&q);
	while(q--){
		scanf("%s%d",cmd,&a);
		if(cmd[0]=='+')
		{	num[cnt[a]]--;
			cnt[a]++;
			num[cnt[a]]++;
			n++;
		} 
		else 
		{
			num[cnt[a]]--;
			cnt[a]--;
			num[cnt[a]]++;
			n--;
		}
 
		a=n-(num[1]*1+num[2]*2+num[3]*3);
 
		if(a==0){
			printf("NO\n"); 
		}else if(a==4||a==5){
			if(num[2]+num[3]>=2)printf("YES\n");

			else printf("NO\n");
 
		}else if(a==6||a==7){
 
			if(num[2]+num[3]>=1)printf("YES\n");
 
			else printf("NO\n");
 
		}else{
 
			printf("YES\n");
 
		} 
	} 
	return 0;
}
```

### [C. Pinkie Pie Eats Patty-cakes](http://codeforces.com/contest/1393/problem/C)

### **题意** 
给定一组数（每组都含有相同的数），求相同数之间的距离的最小值最大

距离指两个数之间所隔数的个数

### **思路** 

设出现最多次数为maxm,出现的个数为count,公式为$\frac{n-maxm*count}{maxm-1}+count-1$

### **代码** 
```
#include <algorithm>
#include <iostream>
#include <cstdio>
#include<string.h>
#include<cstring>
using namespace std;
typedef long long ll;

const int maxn = 1e5 + 20;

int a[maxn];
int main()
{
    int t, n,x,maxm=0,count;
    scanf("%d", &t);
    while (t--) {
        scanf("%d", &n);
        count = 0;
        maxm = 0;
        memset(a, 0, sizeof(a));
        for (int i = 1; i <= n; i++) {
            scanf("%d", &x);
            a[x]++;
            maxm = max(maxm, a[x]);
        }
        for (int i = 1; i <= n; i++) {
            if (maxm == a[i]) count++;
        }
        int ans = (n - maxm * count) / (maxm - 1) + count - 1;
        printf("%d\n", ans);
    }
    return 0;
}
```

### [D. Rarity and New Dress](http://codeforces.com/contest/1393/problem/D)


### **题意** 

给定一个n∗m的字符矩阵，判断有多少个相同字符能组成斜正方形

### **思路** 
动态规划

每个字符能组成个数为一个的斜正方形

对于个数为多个的斜正方形，

a**a**a

**aaa**

a**a**a

以最下面的点[i][j]为基准向上延申，如果与位置[i-1][j]、[i-1][j-1]、[i-1][j+1]、[i-2][j]处的字符相同，则可以构成斜正方形

用dp[i][j]表示(i,j)位置上的方案数

状态转移时取[i-1][j-1]、[i-1][j+1]、[i-2][j]三点处dp的最小值累加在dp[i][j]的值上（[i-1][j]处的位置已被维护）


### **代码** 
```
#include <algorithm>
#include <iostream>
#include <cstdio>
#include<string.h>
#include<cstring>
using namespace std;
typedef long long ll;

const int maxn = 2e3 + 20;

int dp[maxn][maxn];
string c[maxn];
int main()
{
    int m, n,ans=0;
    scanf("%d%d", &n, &m);
    for (int i = 0; i < n; i++)
        cin >> c[i];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            dp[i][j] = 1;
        }
    }

    for (int i = 0; i < n; i++) 
        for (int j = 0; j < m; j++) {
            if (i > 1 && j > 0 && j < m - 1) {
                char x = c[i][j];
                if ((x == c[i - 1][j]) && (x == c[i - 1][j - 1]) && (x == c[i - 1][j + 1]) && (x == c[i - 2][j])) {
                    int m = min(dp[i - 1][j - 1], dp[i - 1][j + 1]);
                    dp[i][j] = dp[i][j] + min(m, dp[i - 2][j]);
                }

            }
            ans += dp[i][j];
        }
        
   
    cout << ans << endl;
    return 0;
}
```



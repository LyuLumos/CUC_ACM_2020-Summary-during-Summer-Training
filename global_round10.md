- [Codeforces Global Round 10](#codeforces-global-round-10)
  - [A. Omkar and Password](#a-omkar-and-password)
  - [B. Omkar and Infinity Clock](#b-omkar-and-infinity-clock)
  - [C. Omkar and Waterslide](#c-omkar-and-waterslide)
  - [D. Omkar and Bed Wars](#d-omkar-and-bed-wars)
  - [E. Omkar and Duck](#e-omkar-and-duck)
  - [F. Omkar and Landslide](#f-omkar-and-landslide)

# [Codeforces Global Round 10](http://codeforces.com/contest/1392)

## [A. Omkar and Password](http://codeforces.com/contest/1392/problem/A)
可以任意合并数组相邻不相等的元素，最终数组所有元素都相同，求最短长度。

原数组元素全相同答案为n，反之为1.

## [B. Omkar and Infinity Clock](http://codeforces.com/contest/1392/problem/B)

每次找出数组最大值，a[i]=mx-a[i]，求k（1e18）次后的数组。

模拟了一下发现有规律，根据k的奇偶判断一下就好了。

分析：第一次操作之后，最大值的位置就是原来最小值的位置，之后就是最大最小值不断交换的过程。
```cpp
if(k&1) {
    for(int i=0;i<n;i++) a[i]=mx-a[i];
} else {
    for(int i=0;i<n;i++) a[i] -= mi;
}
```

## [C. Omkar and Waterslide](http://codeforces.com/contest/1392/problem/C)
给定一个序列，每次可以在一个相同高度的子段上+1，求使其变成单调不减序列最小操作次数。

答案就是下降的差值之和，举个例子，`5 1 2 3`，如果1加到了5那么23肯定也到5了。
```cpp
for(int i=1;i<n;i++) {
    if(a[i]<a[i-1]) sum+=a[i-1]-a[i];
}
```
## [D. Omkar and Bed Wars](http://codeforces.com/contest/1392/problem/D)
给定包含`RL`的字符串，分别代表当前位置上的人向右方/左方发起攻击。求最小的更改次数，使其满足：如果当前位置受到单侧攻击则向其反击，受到双侧攻击则向任意一个方向反击。所有人围成的是一个环。

观察一下，合法字符串包括`RL` `RLL` `RLLR`，只要连续出现的次数不超过三次就是合法的。全R或全L需要特判。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int t,n,len,ans,cnt;
string s;
int main() {
	scanf("%d",&t);
	while(t--) {
		vector<int> v;
		scanf("%d",&n);
		cin >> s;
		cnt=1; ans=0;
		for(int i=1;i<n;i++) {
			if(s[i]==s[i-1]) cnt++;
			else v.push_back(cnt), cnt=1;
		}
		if(cnt) v.push_back(cnt);
		len = v.size();
		if(len==1) {
			printf("%d\n", (n+2)/3);
			continue;
		}
		if(s[0]==s[s.length()-1]) v[0]+=v[--len];
		for(int i=0;i<len;i++)
			ans+=v[i]/3;
		printf("%d\n",ans);
	}
} 
```

## [E. Omkar and Duck](http://codeforces.com/contest/1392/problem/E)

这是一道交互题。

给定n，要求输出n*n的矩阵，每个值分别代表点 (i,j) 的权值，系统会给出q个合法权值w，每次要求从左上角走到右下角，只能向右或下走，**总权值恰好为w且路径唯一**。

往二进制的角度思考

如果需要恰好为w：（对角线相等）
$$
\begin{matrix}2^{2} & 2^{3} & 2^{4} & 2^{5} & 2^{6} &       2^{7} & 2^{8} & 2^{9}  \\ 2^{3} & 2^{4} & 2^{5} & 2^{6} &       2^{7} & 2^{8} & 2^{9} & 2^{10} \\ 2^{4} & 2^{5} & 2^{6} &       2^{7} & 2^{8} & 2^{9} & 2^{10} & 2^{11} \\ 2^{5} & 2^{6} &       2^{7} & 2^{8} & 2^{9} & 2^{10} & 2^{11} &       2^{12} \\ 2^{6} & 2^{7} & 2^{8} & 2^{9} & 2^{10} & 2^{11} &       2^{12} & 2^{13} \\ 2^{7} & 2^{8} & 2^{9} & 2^{10} & 2^{11} &       2^{12} & 2^{13} & 2^{14} \\ 2^{8} & 2^{9} & 2^{10} & 2^{11}       & 2^{12} & 2^{13} & 2^{14} & 2^{15} \\ 2^{9} & 2^{10} & 2^{11}       & 2^{12} & 2^{13} & 2^{14} & 2^{15} & 2^{16}       \\ \end{matrix}
$$
加上路径唯一的条件
$$
\begin{matrix} 0 & 0 & 0 & 0 & 0 & 0       & 0 & 0 \\ 2^{3} & 2^{4} & 2^{5} & 2^{6} &       2^{7} & 2^{8} & 2^{9} & 2^{10} \\ 0 & 0 & 0       & 0 & 0 & 0 & 0 & 0 \\ 2^{5} & 2^{6} &       2^{7} & 2^{8} & 2^{9} & 2^{10} & 2^{11} &       2^{12} \\ 0 & 0 & 0 & 0 & 0 & 0 & 0 &       0 \\ 2^{7} & 2^{8} & 2^{9} & 2^{10} & 2^{11} &       2^{12} & 2^{13} & 2^{14} \\ 0 & 0 & 0 & 0       & 0 & 0 & 0 & 0 \\ 2^{9} & 2^{10} & 2^{11}       & 2^{12} & 2^{13} & 2^{14} & 2^{15} & 2^{16}       \\ \end{matrix}
$$

那么其实就是在每一步判断下一步对应的二进制位上是否有1。

**注意：输出后要加上`fflush(stdout)`（scanf星人表示-_-||），C++ `cout<<endl;`可以自动清空缓存区。**

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int n,q,x,y;
ll t;

int main() {
	scanf("%d",&n);
	for(int i=1;i<=n;i++) {
		for(int j=1;j<=n;j++) {
			if(i&1) printf("0 ");
			else printf("%lld ",1LL<<(i+j));
		}
		printf("\n");
	}
	fflush(stdout);
	scanf("%d",&q);
	while(q--) {
		scanf("%lld",&t);
		x = y = 1;
//		printf("%d %d\n",x,y);
		cout << x << " " << y << endl;
		for(int i=1;i<=2*n-2;i++) {
			if(x&1) {
				if(t&(1LL<<(x+y+1))) x++;
				else y++;
			} else {
				if(t&(1LL<<(x+y+1))) y++;
				else x++;
			}
			cout << x << " " << y << endl;
//			printf("%d %d\n",x,y);
		}
	}

}
```

## [F. Omkar and Landslide](http://codeforces.com/contest/1392/problem/F)

给定数组h，如果h[i]+2<=h[i+1]，则h[i]--,h[i+1]++，一直重复到不能进行操作为止，求最终的数组。

打表找规律，先构造等差数列剩下加1即可。

打表代码
```cpp
#include <bits/stdc++.h>
#define random(a,b) ((a)+rand()%((b)-(a)+1))
using namespace std;

int n,cnt;

int a[20];

void print(int n) {
	for(int i=1;i<=n;i++) {
		printf("%d ",a[i]);
	}
	printf("\n");
}
void init(int n) {
	srand((unsigned)time(NULL));
	int sum=0;
	for(int i=1;i<=n;i++) {
		a[i]=random(a[i-1]+1,a[i-1]+8);
		sum+=a[i];
	}
	print(n);
	printf("Sum=%d, Sum/n=%.2f\n",sum,1.0*sum/n);
}

int fun(int n) {
	for(int i=1;i<n;i++) {
		while(a[i]+2<=a[i+1]) {
			a[i]++;a[i+1]--;
		}
	}
}

int check(int n) {
	for(int i=1;i<n;i++) {
		if(a[i]+2<=a[i+1]) {
			return 1;
		}
	}
	return 0;
}

int main() {
    n=6;
	init(n);
	while(check(n))  fun(n);
	print(n);
}
```
解题代码
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int maxn = 1e6 + 5;
ll n,sum;
ll a[maxn], ans[maxn];

int main() {
	scanf("%lld",&n);
	for(int i=0;i<n;i++) scanf("%lld",&a[i]), sum+=a[i];
	ans[0]=(2*sum-n*n)/(2*n);
	sum-=ans[0];
	for(int i=1;i<n;i++) {
		ans[i]=ans[i-1]+1;
		sum-=ans[i];
	}
	int j=0;
	while(sum>0) {
		sum--;
		ans[(j++)%n]++;
	}
	for(int i=0;i<n;i++) {
		printf("%lld ",ans[i]);
	}
} 
```
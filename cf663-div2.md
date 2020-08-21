# [Codeforces Round #663 (Div. 2)](https://codeforces.com/contest/1391)

- [Codeforces Round #663 (Div. 2)](#codeforces-round-663-div-2)
  - [A. Suborrays](#a-suborrays)
  - [B. Fix You](#b-fix-you)
  - [C. Cyclic Permutations](#c-cyclic-permutations)

## [A. Suborrays](https://codeforces.com/contest/1391/problem/A)

给定1-n的排列，输出一个排列使所有ij满足$p_i or p_i+1 or ... or p_j$ >= j-i+1。

事实上，任何序列都保证字段异或和大于其长度，输出任意解即可。

## [B. Fix You](https://codeforces.com/contest/1391/problem/B)

给定n×m的字符数组，只包括R和D，分别代表向右走和向下走。求至少改几个能使所有点出发都能走到右下角。

只需更改右边界的R和下边界的D

## [C. Cyclic Permutations](https://codeforces.com/contest/1391/problem/C)

给定长度为n的排列，对于每个数，将其与**大于它且在其左边最近的数**建边，再与**大于它且在其右边最近的数**建边，求所有排列结果中有环的序列数量。

比赛期间找了个规律，3个数时只有`213`和`312`有环，在看一下2、4，猜出结果为$n!-2^{n-1}$。

只要出现波谷必然有环。那么只有三种情况无环：单增、单减、单波峰，那么就是先确定n的位置，剩下n-1一个数选择放左边还是右边的问题。
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int maxn = 1e6+5;
const int mod = 1e9+7;
int n;
ll a[maxn];

ll pow_mod(ll a, ll n, ll m) {
	ll ans = 1;
	while(n) {
		if(n&1) {
			ans = (ans * a) % m;
		}
		a = (a * a) % m;
		n >>= 1;
	}
	return ans;
}


int main() {
	scanf("%d",&n);
	a[1]=1;
	for(int i=2;i<=n;i++) {
		a[i]=(a[i-1]*i)%mod;
	}
	printf("%lld\n", (a[n]-pow_mod(2,n-1,mod)+mod)%mod);
}
 
```
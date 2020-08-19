# Codeforces Global Round 10
时间：8.16
## A题
### 分析：
&ensp;&ensp;想得有点久，（太菜了）。思路就是如果这个只要有一个不同那么就一定可以合并成一个数，否则就不能合并，ans就是数组长度。
### 代码
略

## B题
### 分析：
&ensp;&ensp;花了半个小时才A出来，（思维练得有点少）。当时做的时候对数组排了一个序，然后模拟了一遍发现其实在一次操作之后数会以2为周期循环变化。然后判断k是奇数还是偶数就行了
### 代码
略

## C题
### 分析：
&ensp;&ensp;想了40min想不出来就睡觉去了，第二天看题解发现题目读错了🤐，要满足递增，看成了递减（有可能是太困了）。直接累积求和$ans+=max(a[i]-a[i+1],0)$就行了。
### 代码
略

## D题
### 分析：
&ensp;&ensp;因为不能连续出现3个一样的，如果所有人都朝一个方向打，那么答案就是$\lceil \frac{len}{3} \rceil$。否则就为连续一样的$len/3$
看了下官方题解的代码，太优雅了，最后附加一个"$"字符，以及整体的代码结构。
### 代码
```cpp
#include <ctime>
#include <cstdlib>
#include<iostream>
#include<algorithm>
#include<math.h>
#include<cstdio>
#include<string>
#include<string.h>
#include<list>
#include<queue>
#include<sstream>
#include<vector>
#include <cassert>   // assert
#include<set>
#include<map>
#include<deque>
#include<stack>
using namespace std;
#define debug(x) cout<<"###"<<x<<"###"<<endl;
const int INF=0x3f3f3f3f,mod=1e9,Maxn=2e5+10;
const double eps=1e-8;
typedef long long ll;
string str;
void solve(){
	int n;
	cin>>n;
	cin>>str;
	int ans=0,cnt=0;
	while(!str.empty()&&str[0]==str.back()){
		str.pop_back();
		cnt++;
	}
	if(str.empty()){
		ans=(cnt+2)/3;
		cout<<ans<<endl;
		return ;
	}
	str.push_back('$');
	for(int i=0;i<str.length();i++){
		cnt++;
		if(str[i]!=str[i+1]){
			ans+=cnt/3;cnt=0;
		}
	}
	cout<<ans<<endl;
}
int main(){
	int T;
	cin>>T;
	while(T--){
		solve();
	}
}

```

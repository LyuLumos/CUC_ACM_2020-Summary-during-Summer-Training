# Educational Codeforces Round 93 (Rated for Div. 2)
## 1398C - Good Subarrays
&ensp;&ensp;比赛的时候没想出O(n)的解法，之后看了下别人写的博客。感觉有点巧妙。感觉是道好题（可能是我太菜了）。
## 分析：
&ensp;&ensp;很自然想到前缀和。假设$y>=x$,即题目要求对于区间[x,y]使得等式
$$sum[y]-sum[x-1]=y-(x-1)$$成立。
然后移项可得
$$sum[y]-y=sum[x-1]-(x-1) $$
即要使得这个等式成立，然后就可以在算前缀和的时候同时算出$sum[i]-i$。如果在i之前$sum[i]-i$出现了多少次就说明有多少对符合题意。统计一下就行了。


## AC代码：
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
const int INF=0x3f3f3f3f,mod=1e9,Maxn=1e6;
const double eps=1e-8;
typedef long long ll;
map<ll,ll>mp;
int main(){
    int t,n;
    scanf("%d",&t);
    while(t--){
        mp.clear();
        scanf("%d",&n);
        ll a;
        ll ans=0,sum=0;
        mp[0]=1;
        for(int i=1;i<=n;i++){
            scanf("%1lld",&a);
            sum+=a;
            ans+=mp[sum-i];
            mp[sum-i]++;
        }
        cout<<ans<<endl;
    }
    return 0;
}
```

## 1398D - Colored Rectangles
最开始的时候想的是用贪心做，就WA了。贪心存在问题。（看数据范围应该枚举的）

### 分析：
状态：dp[i][j][k] 表示选了i个R，j个G，K个B。转移就像背包的选还是不选的问题。 具体分析见下面代码

### AC代码：
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
const int INF=0x3f3f3f3f,mod=1e9,Maxn=2e2+10;
const double eps=1e-8;
typedef long long ll;
ll dp[Maxn][Maxn][Maxn];
int r[Maxn],g[Maxn],b[Maxn];
int main(){
    int R,G,B;
    cin>>R>>G>>B;
    for(int i=1;i<=R;i++)scanf("%d",&r[i]);sort(r+1,r+1+R,greater<int>());
    for(int i=1;i<=G;i++)scanf("%d",&g[i]);sort(g+1,g+1+G,greater<int>());
    for(int i=1;i<=B;i++)scanf("%d",&b[i]);sort(b+1,b+1+B,greater<int>());
    ll ans=0;
    memset(dp,0,sizeof dp);
    for(int i=0;i<=R;i++){
        for(int j=0;j<=G;j++){//枚举
            for(int k=0;k<=B;k++){
                if(i&&j)dp[i][j][k]=max(dp[i][j][k],dp[i-1][j-1][k]+r[i]*g[j]);//选r[i],g[j] 还是不选
                if(i&&k)dp[i][j][k]=max(dp[i][j][k],dp[i-1][j][k-1]+r[i]*b[k]);// 选r[i],b[k] 还是不选
                if(j&&k)dp[i][j][k]=max(dp[i][j][k],dp[i][j-1][k-1]+g[j]*b[k]);//选g[j],b[k] 还是不选
                ans=max(ans,dp[i][j][k]);//每次枚举完更新一次答案
            }
        }
    }
//    cout<<dp[R][G][B]<<endl;
    cout<<ans<<endl;
	return 0;
}

```
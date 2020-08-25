# Codeforces Round #651 Div2 题解

### A.[Maximum GCD](https://vjudge.net/problem/CodeForces-1370A) 

**题解：**

就很离谱得一个题，手算几个答案就看出来了.....

**AC代码：**

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<map>

using namespace std;

const int maxn = 1e6 + 19;

int main()
{
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        cout << n/2 << endl;
    }
    return 0;
}
```

### B.[ GCD Compression](https://vjudge.net/problem/CodeForces-1370B)

**题解：**

题目中说gcd的值要大于1，那就让他是2把！QAQ！

咳咳这是有依据的。因为给出了2n个数，那么不管这2n个数里面有多少个奇数，我们总可以通过一开始删减两个元素来实现：对于该序列，总可以找到两个相加和为偶数的元素。那么就记录一下这两个数的**位置**（注意是**位置**！！！）,最后输出n - 1个就可以了。

**AC代码：**

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<map>
#include<utility>

using namespace std;

const int maxn = 2e5 + 18;

int a[maxn] = {},vis[maxn] = {};

map<int,pair<int,int> > mp;

int main()
{
   int t;
   cin >> t;
   while(t--){
       int n,cnt = 0;
       cin >> n;
       memset(a,0,sizeof(a));
       memset(vis,0,sizeof(vis));
       for(int i = 1;i <= 2 * n;i++) cin >> a[i];
       for(int i = 1;i <= 2 * n;i++){
           if(vis[i]) continue;
           for(int j = 1;j <= 2 * n;j++){
               if(i == j || vis[i] || vis[j]) continue;
               if((a[j] + a[i]) % 2 == 0) {
					mp[cnt++] = {i,j};
               	vis[i] = vis[j] = 1;
           	} 
			}
       }
       for(int i = 0;i < n - 1;i++){
           cout << mp[i].first << ' ' << mp[i].second << endl;
       }
   }
   return 0;
}
```

### C.[Number Game](https://vjudge.net/problem/CodeForces-1370C)

**题解：**

我们可以分为这几种情况看：

- 如果n为非1的奇数或者是2，那么一定是A获胜。
- 如果n存在奇数因子k且n/k不为2，那就一定是A获胜
- 否则就是F获胜

**AC代码：**

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cmath>
#include<algorithm>

using namespace std;

int main()
{
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        if((n != 1 && n % 2 == 1) || n == 2) cout << "Ashishgup" << endl;
        else{
            int flag = 0;
            for(int i = 3;i <= sqrt(n);i++){
                if(n % i == 0){
                    if((i % 2 == 1 && n/i != 2) || (n/i % 2 == 1 && i != 2)){
                        flag = 1;
                        break;
                    }
                }
            }
            if(flag) cout << "Ashishgup" << endl;
            else cout << "FastestFinger" << endl;
        }
    }
    return 0;
}
```


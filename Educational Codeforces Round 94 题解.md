# Educational Codeforces Round 94 题解

### A.[String Similarity](https://vjudge.net/problem/CodeForces-1400A)

**题解：**

我们发现这个二进制字符串的长度一直就是奇数，所以说我们可以直接去找这`2n - 1`个数中0和1谁是数量更多的那一个。  然后全部输出0或者1就可以了。因为最坏的情况就是数量少的全部排到左边，而且最多就是`n - 1`个数，但是明显的是多的那一方最少就是n个，所以肯定可以满足的。

**AC代码：**

```cpp
#include<iostream>
#include<cstdio>
#include<cmath>
#include<cstring>
using namespace std;
int main()
{
    int t;
    cin >> t;
    while(t--){
        int n,sum1 = 0,sum2 = 0;
        string s;
        cin >> n >> s;
        int len = s.length();
        for(int i = 0;i < len;i++){
            if(s[i] == '0') sum1++;
            else sum2++;
        }
        if(sum1 > sum2){
            for(int i = 1;i <= n;i++) cout << 0;
            cout << endl;
        }
        else{
            for(int i = 1;i <= n;i++) cout << 1;
            cout << endl;
        }
    }
    return 0;
}
```

### B.[RPG Protagonist](https://vjudge.net/problem/CodeForces-1400B)

**题解：**

这个题目一开始真就当背包做了...

但是后来发现其实就是个枚举+贪心的问题，我们肯定是优先拿重量小的，剩下的空间再去拿重量大的，所以我们可以先枚举我们自己会拿走多少重量小的，然后再对辅助进行贪心就可以。

**AC代码:**

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
        int p,f,cnts,cntw,s,w;
        cin >> p >> f >> cnts >> cntw >> s >> w;
        if(s > w){
            swap(s,w);
            swap(cnts,cntw);
        }
        int ans = 0,cnt_s = min(cnts,p/s);
        for(int i = 0;i <= cnt_s;i++){
            int sum = i,flag_s = cnts,flag_w = cntw,pp = p,ff = f;
            flag_s -= i;pp -= i * s;
            int k = min(f/s,flag_s);
            sum += k;
            ff -= k * s;flag_s -= k;
            k = min(ff/w,flag_w);
            sum += k;
            flag_w -= k;
            k = min(pp/w,flag_w);
            sum += k;
            flag_w -= k;
            ans = max(ans,sum);
        }
        cout << ans << endl;
    }
    return 0;
}
```

### C.[Binary String Reconstruction](https://vjudge.net/problem/CodeForces-1400C)

**题解：**

这又是一道长见识的题目

我们可以分析一下取值为1的情况：

```cpp
if(i + x <= n && w[i + x]) s[i] = 1;
else if(i - x > 0 && w[i - x]) s[i] = 1;
else s[i] = 0;
```

那么我们确定的是，如果当前值是0，那么对于原序列w[i - x]和w[i + x]都必须是0，所以我们可以先确定取值为0的位置，然后对得到的序列进行反推，再和给定序列比较，如果有不同元素则输出-1.

**AC代码：**

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<cmath>
using namespace std;
const int maxn = 1e5 + 19;
int main()
{
    int t;
    cin >> t;
    while(t--){
        string s;
        int x,w[maxn] = {0},ss[maxn] = {0};
        cin >> s >> x;
        int len = s.length();s = "#" + s;
        for(int i = 1;i <= len;i++) {
            w[i] = 1;
            ss[i] = 0;
        }
        for(int i = 1;i <= len;i++){
            if(s[i] == '0'){
                if(i + x <= len) w[i + x] = 0;
                if(i - x > 0) w[i - x] = 0;
            }
        }
        // for(int i = 1;i <= len;i++) cout << w[i];
        // cout << endl;
        for(int i = 1;i <= len;i++){
            if(i + x <= len && w[i + x]) ss[i] = 1;
            else if(i - x > 0 && w[i - x]) ss[i] = 1;
            else ss[i] = 0;
        }
        int flag = 1;
        // for(int i = 1;i <= len;i++) cout << ss[i];
        // cout << endl;
        for(int i = 1;i <= len;i++){
            if(ss[i] != s[i] - '0'){
                flag = 0;
                break;
            }
        }
        if(flag){
            for(int i = 1;i <= len;i++){
                cout << w[i];
            }
            cout << endl;
        }
        else{
            cout << -1 << endl;
        }
    }
    return 0;
}
```


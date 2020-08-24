###### [D. Binary String To Subsequences](https://codeforces.com/contest/1399/problem/D)

题意：给出一个字符串，构造出最少数量的1010....或0101...子序列（没有连续0或1）

用vector0记录0的下标，用vector1记录1的下标。遍历字符串，若字符为0时vector1为空，则需要增加一个新的序列，vector1不为空时把0放到上一个1所在序列。



```c++
#include <iostream>
#include <set>
#include <queue>
#include <cstring>
#include <string>
#include <stack>
using namespace std;
const int N=2e5+100;
int a[N];
bool st[N];
bool st1[N];
char str[N];
typedef pair<int, int> pii;
stack<pii>s;
int main()
{
    int t;
    scanf("%d",&t);
    while(t--)
    {
        int n;
        scanf("%d",&n);
        scanf("%s",str);
        vector<int>s[2];
        int cnt=0;
        for(int i=0;i<n;i++)
        {
            if(str[i]=='0')
            {
                if(s[1].empty())
                {
                    cnt++;
                    a[i]=cnt;
                    s[0].push_back(cnt);
                }
                else
                {
                    a[i]=s[1].back();
                    s[0].push_back(s[1].back());
                    s[1].pop_back();
                }
            }
            else
            {
                
                if(s[0].empty())
                {
                    cnt++;
                    a[i]=cnt;
                    s[1].push_back(cnt);
                }
                else
                {
                    a[i]=s[0].back();
                    s[1].push_back(s[0].back());
                    s[0].pop_back();
                }
            }
        }
        int maxx=0;
        for(int i=0;i<n;i++)
        {
            maxx=max(maxx,a[i]);
        }
        printf("%d\n",maxx);
        for(int i=0;i<n;i++)printf("%d ",a[i]);
        puts("");
    }
    return 0;
}

```


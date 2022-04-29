# P4329 [COCI2006-2007#1] Bond

We see this question and we, we can have a very naive idea.

That is to define $dp_{s,t}$ to denote the person used, to engage in the task.

Of course, we found that this method is not passable in time and space.

We also found that the order in which a person carries tasks has no effect on the answer.

So, we define dp[s] to denote the tasks done, and enumerate people directly from front to back.

It is then reduced by one dimension.

The following code needs o2 optimization to pass the test cases.
```cpp
#include<iostream>
#include<iomanip>
using namespace std;
const int N=20;
int n;double a[N][N];
double dp[1<<N];
int count(int s){
    int ret=0;
    while (s){
        if (s&1) ++ret;
        s>>=1;
    }
    return ret;
}
int main(){
    freopen("a.in","r",stdin);
    std::ios::sync_with_stdio(false);
    cin >> n;
    for (int i=0;i<n;++i)
        for (int j=0;j<n;++j)
            cin >> a[i][j],a[i][j]/=100;// cout << a[i][j] <<endl;
    dp[0]=1;
    int uphold=1<<n;
    for (int i=0;i<n;++i)
        for (int s=0;s<uphold;++s)if(count(s)==i){
            for (int j=0;j<n;++j) if (!((s>>j)&1))
            dp[s|(1<<j)]=max(dp[s|1<<j],dp[s]*a[i][j]);
        }
    cout << setprecision(6)<<dp[uphold-1]*100<<endl;


    return 0;
}
```

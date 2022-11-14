# Atcoder 130 E Common Subsequence

Set dp[i][j] represent in the S[i] and T[j]. How many subsequences there are the same. Firstly, we can use dp[i-1][j]+dp[i][j-1]Principle of capacitive repulsion
to deduct the repetitive one. Finally check whether S[i] and T[j] they are the same.
```cpp
#include<algorithm>
#include<iostream>
#include<vector>
using namespace std;
int n,m;
const int mod=1e9+7;
int main(){
    freopen("130e.in","r",stdin);
    cin >> n >> m;
    vector<int> S(n+1,0);
    vector<int> T(m+1,0);
    for (int i=1;i<=n;++i) cin >> S[i];
    for (int j=1;j<=m;++j) cin >> T[j];
    vector<vector<long long> >dp(n+1,vector<long long>(m+1,0));
    for (int i=0;i<=n;++i) dp[i][0]=1;
    for (int i=0;i<=m;++i) dp[0][i]=1;
    for (int i=1;i<=n;++i){
        for (int j=1;j<=m;++j){
            dp[i][j]=dp[i-1][j]+dp[i][j-1]-dp[i-1][j-1];
            if(S[i] == T[j]) dp[i][j] += dp[i - 1][j - 1];
            dp[i][j]+=mod;dp[i][j]%=mod;
        }
    }
    cout << dp[n][m] <<endl;
    return 0;
}
```

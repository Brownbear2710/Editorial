# Problem
[Jumping Jack: Prime Hole](https://www.hackerrank.com/contests/srbd-code-contest-2023-round-1/challenges/jacks-prime-hole)

# Solution

<details>
<summary>Idea</summary>

Two key things to notice: <br>
1. We do not care about the jumps. Rather, we will only consider hole-size to calculate the answer. <br>
2. If there is a hole of size $x$, then Jack must be able to jump at least $x+1$ bricks. <br>

So, it is clear that no hole can have a size more than $M-1$. This can be done by dynamic programming. <br>
Let's say, we are standing on position $i$. So, $i$ is a good brick. Then, we can create a hole of size $j$, where $j$ is a prime number and $j < M$. In that case, the next brick we can stand on would be $i+j+1$. So, for each $i$ we can iterate over all $j$ to calculate the ans. <br>
[Note that $0$ is also a prime number in this problem]. <br>
This gives us a solution with time complexity $O(N*M)$. This can be further optimized by only iterating over the prime numbers smaller than  $M$.
</details>

<details>
<summary>Code</summary>

```cpp
/*
    So, which of the favours
    of your Lord would you deny?
*/

#include <bits/stdc++.h>

#ifdef ADIB_PC
#include "dbg.h"
#else
#define dbg(...)
#endif

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define show(x) cout << #x << ": " << x << endl;
#define all(x) begin(x), end(x)
#define MAXN 5003
#define MOD 1000000007

vector<ll> prime;

void sv()
{
    int n = MAXN;
    vector<bool> is_prime(n+1, true);
    is_prime[0] = is_prime[1] = false;
    for (int i = 2; i <= n; i++) {
        if (is_prime[i] && (long long)i * i <= n)
        {
            for (int j = i * i; j <= n; j += i)
                is_prime[j] = false;
        }
    }
    for(int i = 2; i <= n; i++)
    {
        if(is_prime[i]) prime.push_back(i);
    }
}

int n, m;
ll dp[MAXN];
ll call(int pos)
{
    if(pos > n)
        return pos == n+1;
    if(dp[pos] != -1) return dp[pos];
    ll ret = call(pos+1) % MOD;
    for(int i = 0; i < prime.size() and prime[i]+1 <= m; i++)
    {
        if(pos + prime[i] > n+1) break;
        ret += call(pos + prime[i] + 1);
        ret %= MOD;
    }
    return dp[pos] = ret%MOD;
}


int main()
{
    sv();
    fast_IO;
    int T = 1;
    cin >> T;
    while(T--)
    {
        cin >> n >> m;
        for(int i = 0; i <= n; i++)
            dp[i] = -1;
        cout << call(0)%MOD << "\n";
    }
    return 0;
}
```

</details>

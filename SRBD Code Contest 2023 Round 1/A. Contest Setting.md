# Problem
[Contest Setting](https://www.hackerrank.com/contests/srbd-code-contest-2023-round-1/challenges/contest-setting-1)

# Solution

<details>
<summary>Idea</summary>

Let's say, <br>
> $a = \lfloor \frac{m}{2} \rfloor$ and $b = \lceil \frac{m}{2} \rceil$. <br>

Our goal is to maximize the value of m while ensuring,
> $a^2 + b^2 + m \times y \leq B$. <br>

We can just do a binary search on the calue of $m$ to find the maximum value of $m$ . After that, we can say, $N = 2^m$

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
#define MAXN 200005

int main()
{
    fast_IO;
    int T = 1;
    cin >> T;
    while(T--)
    {
        ll B;
        ll n , m, y;
        cin >> B >> y;
        ll lo = 0, hi = __lg(LLONG_MAX);
        ll ans = 0;
        while(lo <= hi)
        {
            ll m = (lo + hi) / 2;
            ll a = m/2;
            ll b = m-a;
            if(a*a + b*b + m*y <= B)
            {
                ans = m;
                lo = m + 1;
            }
            else hi = m - 1;
        }
        cout << (1LL << ans) << "\n";
    }
    return 0;
}
```
</details>
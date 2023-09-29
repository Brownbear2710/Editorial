# Problem
[Village Hidden in The Leaf](https://www.hackerrank.com/contests/srbd-code-contest-2023-round-1/challenges/village-hidden-in-the-leaf)

# Solution

<details>
<summary>Idea</summary>

Let us answer $type-1$ query first. <br>
The answer is simply,
> (position of closest prime after $X$) - p(ositon of closest prime before $X$) - 2 <br>

So, we can keep a $set$ where we will only store the position of the prime numbers. Then simply we can use $lower\_bound$ or $upper\_bound$ to find immediate next and previous prime of the number at $X^{th}$ position. <br>

Now, whenever we encounter $type-2$ query, we check if the number $Y$ is a prime or not. If it is a prime, we insert $X$ into the set. Otherwise, we remove the $X$ from the set.

Note: To avoid bound checking, we can insert position 0 and n+1 into the set. As, those position will never come in query, those will never be removed from the set.

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
#define MAXN 10000007
#define LL long long

vector<bool> is_prime(MAXN, true);

void sv()
{
    int n = MAXN;
    is_prime[0] = is_prime[1] = false;
    for (int i = 2; i < n; i++) {
        if (is_prime[i] && (long long)i * i < n)
        {
            for (int j = i * i; j < n; j += i)
                is_prime[j] = false;
        }
    }
}

int main()
{
    sv();
    fast_IO;
    int T = 1;
    cin >> T;
    while(T--)
    {
        int n, q;
        cin >> n >> q;
        vector<int> a(n+2,2);
        for(int i = 1; i <= n; i++)
            cin >> a[i];
        set<int> st;
        for(int i = 0; i < a.size(); i++)
        {
            if(is_prime[a[i]])
                st.insert(i);
        }
        while(q--)
        {
            int typ;
            cin >> typ;
            if(typ == 1)
            {
                int x;
                cin >> x;
                auto it = --st.upper_bound(x);
                auto itr = it;
                itr++;
                if(*it == x)
                    it--;
    
                int ans = (*itr) - (*it) - 2;
                cout << ans << "\n";
            }
            else
            {
                int x, y;
                cin >> x >> y;
                if(is_prime[y]) st.insert(x);
                else st.erase(x);
            }
        }
    }
    return 0;
}
```

</details>
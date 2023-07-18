# [E-Div Game](https://atcoder.jp/contests/abc169/tasks/abc169_d?lang=en)

Let's say a prime divisor $p$ can divide $N$ $k$ times. Now, to maximize the number of operations, we have to take $p^1$, $p^2$...$p^x$ where each power is unique. But $p$ can divie $N$ limited number of times which is $k$. So, sum of powers of $p$ must less than or equal to $k$.

i.e. $1+2+...+x ≤ p$

$ => \frac{x(x+1)}{2} ≤ k$

=> $ x^2 + x - 2*k ≤ 0$

=> $ x ≤ \frac{-1 + \sqrt{1 + 8k}}{2}$

$∴ x = \lfloor\frac{-1 + \sqrt{1 + 8k}}{2}\rfloor ...............(i)$

So, $x$ is the number of operations can be performed using the prime number $p$.<br> Now, for each prime divisor, we have to find how many times it can divide $N$ and then using the above formula we have to find how many operations can be performed using that prime number. Then simply add it to the final result.

<details>
<summary>C++ Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define all(x) x.begin(), x.end()

vector<ll> prime;
vector<bool> is_prime(1000005, true);

void sv()
{
    int n = 1000005;
    is_prime[0] = is_prime[1] = false;
    for (int i = 2; i*i <= n; i++)
    {
        if (is_prime[i] && i * i <= n)
        {
            for (int j = i * i; j <= n; j += i)
                is_prime[j] = false;
        }
    }
    for(int i = 2; i <= n; i++)
        if(is_prime[i]) prime.push_back(i);
}

ll calculate(ll n)
{
    int i = 0;
    ll ans = 0;
    while(n > 1 and i < prime.size() and prime[i]*prime[i] <= n)
    {
        int cnt = 0;
        while(n%prime[i] == 0)
        {
            cnt++;
            n /= prime[i];
        }
        ans += (-1 + sqrt(1+8*cnt))/2;
        i++;
    }
    if(n > 1) ans++;
    return ans;
}

int main()
{
    fast_IO;
    sv();
    ll n;
    cin >> n;
    cout << calculate(n);
    return 0;
}
```
</details>

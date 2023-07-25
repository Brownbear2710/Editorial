# [B. Dreamoon and WiFi](https://codeforces.com/problemset/problem/476/B)

Suppose the two strings are $A$ and $B$. $Value$ of string = number of $(+)$ - number of $(-)$
Let number of $(?)$ in $B$ = $Q$.
$Answer = 1$ if $Q = 0$ and $Value(A) = Value(B)$
$Answer = 0$ if abs(Value(A) - Value(B)) > Q
Now for the other case,
let us asume we have to replace $X$ number of $(?)$ to $(+)$ and $Y$ number of $(?)$ to $(-)$.
It is obvious that $X+Y = Q$ and $X-Y = Value(A) - Value(B)$
So, $X = (Q + Value(A) - Value(B)) / 2$
$Answer = (0.5^Q) *$ $($number of ways to choose $X$ from $Q)$
So, $Answer$ = $(0.5^Q) *$ $^QC_X$

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define all(x) x.begin(), x.end()

ll fact(ll x)
{
    if(x == 0) return 1;
    return x * fact(x-1);
}
 
ll comb(ll N, ll R)
{
    ll ret = fact(N) / (fact(N-R) * fact(R));
    return ret;
}

int main()
{
    fast_IO;
    string a, b;
    cin >> a >> b;
    ll A = 0, B = 0, Q = 0;
    for(auto x : a)
        if(x == '+') A++;
        else A--;
    for(auto x : b)
        if(x == '+') B++;
        else if(x == '-') B--;
        else Q++;
    if(Q == 0 && A == B)
    {
        cout << 1 << endl;
        return 0;
    }
    if(abs(A-B) > Q)
    {
        cout << 0 << endl;
        return 0;
    }
    double ans = powl(0.5, Q) * comb(Q, (Q - abs(A-B))/2);
    cout << fixed << setprecision(12) << ans << endl;
    return 0;
}
```
</details>
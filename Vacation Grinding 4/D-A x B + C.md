# [D-A x B + C](https://atcoder.jp/contests/abc179/tasks/abc179_c?lang=en)

For each pair $(A, B)$ of positive integers such that $A × B < N$, a positive integer $C$ such that $A×B+C=N$ is uniquely determined. Therefore, it is sufficient to count the number of such pairs of positive integers $(A, B)$.

When $A$ is fixed, the number of possible $B$ is $⌊\frac{A}{N−1}⌋$. Therefore, we could solve the problem by performing exhaustive search on $A$ from 1 to $N−1$.

<details>
<summary>C++ Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define all(x) x.begin(), x.end()

int main()
{
    fast_IO;
    int n, ans = 0;
    cin >> n;
    for(int i = 1; i < n; i++)
        ans += (n-1)/i;
    cout << ans;
    return 0;
}
```
</details>

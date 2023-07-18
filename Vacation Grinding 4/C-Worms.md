# [C-Worms](https://codeforces.com/problemset/problem/474/B)

There are two solutions:

1. We can make partial sums $(sum_i = a_1 + a_2 + ... + a_i)$ and then make a binary search for each query $q_i$ to find the result $j$ with the properties $sum_j - 1 < q_i$ and $sum_j ≥ q_i$. This solution has the complexity $O(n + m·log(n))$

2. We can precalculate the index of the pile for each worm and then answer for each query in O(1). This solution has the complexity O(n + m)

<details>
<summary>C++ Code</summary>
O(n + m+log(n)) solution: <br><br>

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define all(x) x.begin(), x.end()

int main()
{
    fast_IO;
    int n, m;
    cin >> n;
    vector<int> v(n+1,0);
    for(int i = 1; i <= n; i++)
    {
        int in;
        cin >> in;
        v[i] = v[i-1] + in;
    }
    cin >> m;
    while(m--)
    {
        int q;
        cin >> q;
        int x = lower_bound(v.begin(), v.end(), q) - v.begin();
        cout << x << "\n";
    }
    return 0;
}
```
</details>
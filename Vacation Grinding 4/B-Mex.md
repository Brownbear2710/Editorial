# [B-Mex](https://atcoder.jp/contests/abc245/tasks/abc245_b?lang=en)

We keep an array of size $2001$ to store the count of each number. Then Iterate from first until we find a number that never appears. This is the answer.

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
    int n;
    int cnt[2001] = {};
    cin >> n;
    for(int i = 0; i < n; i++)
    {
        int in;
        cin >> in;
        cnt[in]++;
    }
    int ans = 0;
    while(ans < 2001 and cnt[ans] > 0)
        ans++;
    cout << ans << "\n";
    return 0;
}
```
</details>
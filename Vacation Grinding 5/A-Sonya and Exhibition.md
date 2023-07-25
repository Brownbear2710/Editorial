# [A-Sonya and Exhibition](https://codeforces.com/problemset/problem/1004/B)


## Solution
It is always best to have equal number of roses and lillies in a given range. If it is not possible to divide the range into euqal number of roses and lillies then one of them should be one more in number than the other.

So, the answer is always either the string $010101010...$ or $101010...$


## Proof
Let, in a range of lenght $l$, there are $x$ roses and $y$ lillies. <br>
So, $x+y=l$ ........ $(i)$ <br>
We, have to maximize product, $P = xy$ <br>
$=> P = x(l-x)$ $........ (ii)$ <br>
Which means, $\frac{dP}{dx} = 0$ <br>
$(ii) => \frac{d}{dx}(x(l-x)) = 0$ <br>
$=> l - 2x = 0$ <br>
So, $x = l/2$ <br>
So, half of the total length of the range should be roses. Then, the other half should be Lillies.


<details>
<summary>Code</summary>

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
    cin >> n;
    for(int i = 0; i < n; i++)
        cout << i%2;
    return 0;
}
```

</details>

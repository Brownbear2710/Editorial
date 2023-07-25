# [Two Piles](https://www.codechef.com/problems/SPLITMIN?tab=statement)

## Solution
At first we sort the array that contains all elements from $a$ and $b$. <br>
There are three things to consider:

1. The answer must constain an element which is greater than equal to maximum of all $min$($a_i$, $b_i$).
This is because even though we choose the minimum values from all pairs. The maximum of all $min$($a_i$, $b_i$) must be in one of the sets.
2. To reduce the answer, it is always better to choose two adjascent element of the sorted array as the maximum value of the two different piles.
But we saw earlier that there should be at least one value $\geq$ maximum of all $min$($a_i$, $b_i$).
For now, we denote maximum of all $min$($a_i$, $b_i$) as $k$.
Let's say, $x$ and $y$ are two adjascent elements in the sorted array. If one of them is greater than $k$, only then we can use $x$ and $y$ to reduce the final answer by considering them as the maximum value of two different piles.
3. Let's say, we are considering $i^{th}$ and $(i+1)^{th}$ elements of the array. If they belong to the same pair, they cannot be used to reduce the answer. In that case, we skip that iteration.

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
    int T = 1;
    cin >> T;
    while(T--)
    {
        int n;
        cin >> n;
        vector<pair<int, int>> v;
        int k =- 1e9; // max of all min(a[i], b[i])
        for(int i = 0 ; i< n; i++)
        {
            int a, b;
            cin >> a >> b;
            v.push_back({a, i}); // second element is the number of the pair it belong to
            v.push_back({b, i});
            k = max(k, min(a, b));
        }
        sort(all(v));
        int ans = 1e9;
        for(int i = 0; i+1 < v.size(); i++)
        {
            if(v[i].second == v[i+1].second) continue; // If they belong to same pair we skip
            if(v[i].first < k && v[i+1].first < k)continue; //If both are less than k, we skip
            ans = min(ans, v[i+1].first-v[i].first);
        }
        cout << ans << "\n";
    }
    return 0;
}
```

</details>

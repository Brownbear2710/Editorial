# [D. Guessing the Greatest (easy version)](https://codeforces.com/problemset/problem/1486/C1)

<details>
<summary>Solution</summary>

This problem can be done using similar concept as binary search.
Let's say we know that the greatest number lies in the range $[l...r]$. <br>
Now, we divide the range into two equal parts $[l...m]$ and $[(m+1)...r]$. <br>
After that, we query on the range $[l...r]$. So, we will know if the second-greatest number lies in the first half or second half of the range $[l...r]$. If the number lies in the first half, i.e., $[l...m]$, we will query on the range $[l...m]$. If the index of the second-greatest number does not change after the query, it means that the greatest number is also in that same range.<br>
So, we will repeat the process in the range $[l...m]$. Otherwise, we will repeat the process in the range $[(m+1)...r]$. Either way, we are guaranteed that the range will become half.<br>
We will repeat the process until the range size is reduced to $2$. After that one query is enough to find the greatest number's index.<br>
This guarantees that number of queries will be at most $2$log$n$.

Note: Don't forget to ensure $l \neq r$ for each $query(l,r)$.

</details>

<details>
<summary>Code</summary>

```cpp
/*
    So, which of the favours
    of your Lord would you deny?
*/

// author: Brownbear2710

#include <bits/stdc++.h>

using namespace std;

int query(int l, int r)
{
    cout << "? " << l << " " << r << endl;
    int indx;
    cin >> indx;
    return indx;
}

int main()
{
    int n;
    cin >> n;
    int l = 1, r = n;
    int second_greatest = query(l,r);
    while(l < r-1)
    {
        int m1 = (l+r)/2;
        int m2 = m1+1;
        if(m1-l != r-m2) m2 = m1;
        if(l <= second_greatest and second_greatest <= m1)
        {
            int nw_second = query(l,m1);
            if(nw_second == second_greatest)
                r = m1;
            else
            {
                second_greatest = query(m2,r);
                l = m2;
            }
        }
        else
        {
            int nw_second = query(m2,r);
            if(nw_second == second_greatest)
                l = m2;
            else
            {
                second_greatest = query(l,m1);
                r = m1;
            }
        }
    }
    int ans = (query(l,r) == l ? r : l);
    cout << "! " << ans << endl;
    return 0;
}
```

</details>

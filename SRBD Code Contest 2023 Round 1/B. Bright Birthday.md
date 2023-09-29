# Problem
[Bright Birthday](https://www.hackerrank.com/contests/srbd-code-contest-2023-round-1/challenges/bright-birthday)

# Solution

<details>
<summary>Idea</summary>

There are only 15 colors possible. Each color has at most of length of 6. <br>
So, it is possible to brute force all possbile combintion of colors and check if it can be made from the given string. To do that, we have to keep the count of each letter in $S$. <br>
The answer is the maximum size of the subset among all possbile subsets which can be built.

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

string C [] = { "blue", "green", "yellow", "red", "purple", "orange", "pink", "grey", "cyan", "brown", "ash", "silver", "gold", "white", "black"};

bool possible(vector<int> cnt, int mask)
{
    for(int i = 0; i < 15; i++)
    {
        if(mask & (1<<i))
        {
            for(int j = 0; j < C[i].size(); j++)
            {
                if(cnt[C[i][j] - 'a'] == 0) return false;
                cnt[C[i][j]-'a']--;
            }
        }
    }
    return true;
}

int main()
{
    fast_IO;
    int T = 1;
    cin >> T;
    while(T--)
    {
        vector<int> cnt(26,0);
        string s;
        cin >> s;
        for(int i = 0; i < s.size(); i++)
            cnt[s[i] - 'a']++;
        int ans = 0;
        for(int mask = 0; mask < (1<<15); mask++)
        {
            if(possible(cnt, mask))
                ans = max(ans, __builtin_popcount(mask));
        }
        cout << ans << "\n";
    }
    return 0;
}
```

</details>
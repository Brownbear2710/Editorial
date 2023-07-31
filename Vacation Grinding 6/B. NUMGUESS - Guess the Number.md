# [B. NUMGUESS - Guess the Number](https://www.spoj.com/problems/NUMGUESS/en/)

<details>
<summary>Solution</summary>

Just a simple binary search.
Scan $a$ and $b$ first. Set $a$ and $b$ as lower limit and upper limit of binary search respectively. Then keep guessing until the guess is correct.

This will gurantee the minimum number of guesses.

Note: Don't forget to flush the buffer after each guess.

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

int main()
{
    int lo, hi;
    cin >> lo >> hi;
    while(lo <= hi)
    {
        int mid = (lo + hi) / 2;
        cout << mid << endl; // endl flushes the buffer

        string verdict;
        cin >> verdict;
        if(verdict == "LOW")
            lo = mid+1;
        else if(verdict == "HIGH")
            hi = mid-1;
        else
            break;
    }
    return 0;
}
```

</details>

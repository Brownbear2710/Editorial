# [F. XOR Guessing](https://codeforces.com/problemset/problem/1207/E)

<details>
<summary>Solution</summary>

For the first query, we will select integers that have $0$ in the first $7$ bits. The last $7$ bits will be used to make the numbers distinct from one another. So, whichever number is selected, the $XOR$ will produce a number that has the same bit sequence in the first $7$ bits as $x$. <br>
For, the second query, we will do similar thing but for the last $7$ bits.<br>
So, using two queries we will get the first $7$ bits and the last $7$ bits of $x$ separately. Now just combine them and print the answer.

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
    int x = 0;
    int input;

    cout << "? ";
    for(int i = 1; i <= 100; i++)
        cout << (i<<7) << " "; // First seven bits are 0s
    cout << endl;

    cin >> input;
    for(int i = 0; i < 7; i++)
    {
        int bit = (1<<i)&input;
        x = x|bit;
    }

    cout << "? ";
    for(int i = 1; i <= 100; i++)
        cout << i << " "; // last seven bits are 0s, because 100 < 2^7
    cout << endl;

    cin >> input;
    for(int i = 7; i < 14; i++)
    {
        int bit = (1<<i)&input;
        x = x|bit;
    }

    cout << "! " << x << endl;
    return 0;
}
```

</details>

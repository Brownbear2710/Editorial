# [C. Guess the Array](https://codeforces.com/problemset/problem/727/C)

<details>
<summary>Solution</summary>

The hint is in the constraints of $n$.
Let us solve the problem for the minimum value of $n$, that is, 3.<br>
For, $n = 3$, <br>
Let's make 3 queries on sum 
> $a_1 + a_2 = c_1$, $a_1 + a_3 = с_2$ and $a_2 + a_3 = c_3$.

Now, we have three equations with three unknowns.
So, we get,<br>
> $a_1 = \frac{(c_1+c_2-c_3)}{2}$ <br>
> $a_2 = \frac{c_1+c_3-c_2}{2}$ <br>
> $a_3 = \frac{c_2+c_3-c_1}{2}$ <br>

Now, if $n > 3$, we still can find the first three using the above method. For, the rest $a_i(i > 3)$, we can query $a_1 + a_i = c_i$ and find the value of $a_i = a_1-c_i$.

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

int query(int i, int j)
{
    int cij;
    cout << "? " << i << " " << j << endl;
    cin >> cij;
    return cij;
}

int main()
{
    int n;
    cin >> n;
    vector<int> a(n+1);
    int c1 = query(1,2);
    int c2 = query(1,3);
    int c3 = query(2,3);
    a[1] = (c1+c2-c3)/2;
    a[3] = c2-a[1];
    a[2] = c3-a[3];
    for(int i = 4; i <= n; i++)
    {
        int ci = query(1,i);
        a[i] = ci - a[1];
    }
    cout << "! ";
    for(int i = 1; i <= n; i++)
        cout << a[i] << " \n"[i == n];
    return 0;
}
```
</details>
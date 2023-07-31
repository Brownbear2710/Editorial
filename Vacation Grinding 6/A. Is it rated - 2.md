# [A. Is it rated - 2](https://codeforces.com/problemset/problem/1505/A)

<details>
<summary>Solution</summary>

As the problem says, it is interactive. So, we have to keep scanning the input buffer line by line. For each line scanned, print "NO".

Note: using Fast I/O will show you "Idleness limit exceeded".

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
    string s;
    while(getline(cin, s)) // getline() will throw error if it reaches end of file. That will cause the while loop to break
        cout << "NO" << endl;
    return 0;
}
```
</details>
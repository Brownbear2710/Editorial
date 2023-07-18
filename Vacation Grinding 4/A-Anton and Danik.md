# [A. Anton and Danik](https://codeforces.com/problemset/problem/734/A) <br>

Let's say $c_a$ and $c_d$ be the number of times 'A'  and 'D' appears in the string respectively. <br>
if $c_a$ > $c_d$, print "Anton" <br>
if $c_a$ < $c_d$, print "Danik" <br>
print "Friendship" otherwise <br>

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
    string s;
    cin >> n;
    cin >> s;
    int ca = count(all(s), 'A'), cd = count(all(s), 'D');
    if(ca > cd) cout << "Anton\n";
    else if(ca < cd) cout << "Danik\n";
    else cout << "Friendship\n";
    return 0;
}
```
</details>
# [E. Rudolf And Mimic](https://codeforces.com/problemset/problem/1846/F)

<details>
<summary>Hint 1</summary>

Try to use the constraint for **mimic** that it **can remain as same object for at most 2 rounds**
</details>

<details>
<summary>Hint 2</summary>

Have you considered removing 0 objects?
</details>

<details>
<summary>Solution</summary>

It is obvious that, if we remove $0$ objects for two consecutive rounds, the mimic must change it's appearance. So, wait patiently for mimic to change it's appearance for up-to $2$ rounds. When mimic changes it's appearance, remove all other objects except the object type of mimic. Now, all the remaining object types are same.

Now, we can apply same principle here. We wait for mimic to change it's appearance for up-to $2$ rounds. When mimic changes it's appearance, the index with the unique object type must be the mimic. Then just find the index and print it.

How can we find if mimic has changed it's appearance? We can keep a frequency table of the object types. When frequency of a type has changed, we can say that the mimic has changed it's appearance.

So, we totally need $2$ queries firstly to find it's object type, then $2$ queries to find it's index. So, we need $4$ rounds in total. Finally, $5^{th}$ query is the answer query.
</details>

<details>
<summary>Code</summary>

```cpp
// time-limit: 1000
// problem-url: https://codeforces.com/contest/1846/problem/F
// Then which of Allah's favor will you deny?
// author: MushfiqTalha

#include "bits/stdc++.h"
#define all(v) begin(v), end(v)
using namespace std;

int n;
vector<int> a;

void magic(int mimic, vector<int> &frq) {
  cout << "- " << n - frq[mimic] << " ";
  for (int i = 0; i < n; i++)
    if (a[i] != mimic)
      cout << i+1 << " ";
  cout << endl;

  n = frq[mimic];
  a.resize(n);
  vector<int> tmp(10);
  for (auto &i : a) cin >> i, tmp[i]++;

  if (tmp[mimic] == frq[mimic]) {
    cout << "- 0" << endl;
    for (auto &i : a) cin >> i;
  }

  for (int i = 0; i < n; i++)
    if (a[i] != mimic)
      cout << "! " << i+1 << endl;
}

int main() {
  cin.tie(NULL)->sync_with_stdio(false);

  int t;
  cin >> t;
  while (t--) {
    cin >> n;
    a.resize(n);
    vector<int> frq(10), tmp(10);
    for (auto &i : a) cin >> i, frq[i]++;

    cout << "- 0" << endl;
    for (auto &i : a) cin >> i, tmp[i]++;

    if (tmp == frq) {
      cout << "- 0" << endl;
      tmp.assign(10, 0);
      for (auto &i : a) cin >> i, tmp[i]++;
    }
    for (int i = 1; i < 10; i++)
      if (tmp[i] > frq[i])
        magic(i, tmp);
  }

  return 0;
}
```
</details>
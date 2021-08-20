---
title: 001 - Yokan Party（★4）
subtitle:
date:
categories: atcoder
tags: 二分
math: true
index_img:
banner_img: 
comment: 
---
[题目链接](https://atcoder.jp/contests/typical90/tasks/typical90_a)

---
#### 题目描述
> 有一个长度为L[cm]的木棍。有N个标记点，第i个标记点距左端点的长度为$A_{i}$[cm]。
> 你要从N个标记点中选择K个，将木棍分成K+1块。K+1块中最短的一块的长度为得分。
> 找出划分木棍时得到的分数，使分数达到最大。
>
> 限制条件
>$ 1 ≤ k ≤ n ≤ 10^{5}$
> $0 < a_{1} < a_{2}< ... < L ≦ 10^{9}$所有的输入都是整数。
---
#### 二分答案(最小值最大化)
```cpp
#include <bits/stdc++.h>
using namespace std;
#define mem(a, b) memset(a, b, sizeof(a))
#define int long long int
#define endl '\n'
typedef pair<int, int> PII;
const int mod = 1e9 + 7;
const int inf = 0x3f3f3f3f;
const int N = 1e6 + 7;

int a[N];
int n, m, k;

bool check(int x) {
    int pre = 0, cnt = 0; //上一次切的位置、切的次数
    for (int i = 1; i <= n; i++) {
        if (a[i] - pre >= x && m - a[i] >= x) {
            cnt++;
            pre = a[i];
        }
    }
    return cnt >= k; //如果切的次数大于等于k说明此时的长度小了，还能继续扩大
}
signed main() {
    cin >> n >> m >> k;
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    int l = 0, r = m;
    while (l < r) {  //二分答案，让最小值最大化
        int mid = l + r + 1 >> 1;
        if (check(mid))
            l = mid;
        else
            r = mid - 1;
    }
    cout << l << endl;
    return 0;
}
```
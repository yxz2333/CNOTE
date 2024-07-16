## AtCoder Beginner Contest 353

### [C - Sigma Problem](https://atcoder.jp/contests/abc353/tasks/abc353_c)

#### 问题陈述

对于正整数 $x$ 和 $y$ ，定义 $f(x, y)$ 为 $(x + y)$ 除以 $10^8$ 的余数。

给你一个长度为 $N$ 的正整数序列 $A = (A_1, \ldots, A_N)$ 。求下面表达式的值：

$\displaystyle \sum_{i=1}^{N-1}\sum_{j=i+1}^N f(A_i, A_j)$

#### 限制因素

* $2 \leq N \leq 3\times 10^5$
* $1 \leq A_i < 10^8$
* 所有输入值均为整数。

#### Sample Input 1

```
3
3 50000001 50000002
```

#### Sample Output 1

```
100000012
```

* $f(A_1, A_2)=50000004$
* $f(A_1, A_3)=50000005$
* $f(A_2, A_3)=3$

因此，答案为 $f(A_1, A_2) + f(A_1, A_3) + f(A_2, A_3) = 100000012$。

注意，没有要求你计算总和除以 $10^8$ 的余数。

<br>

# 题解

### 双重和优化公式、二分找大小排位

<br>

暴力会 $O(n^2)$ 过不了，要优化成 $O(n)$ 或 $O(nlog_2n)$。
那么就考虑遍历的时候能不能纯遍历数组解决，或者遍历的时候二分。
因为题目要求是求$\displaystyle \sum_{i=1}^{N-1}\sum_{j=i+1}^N f(A_i, A_j)$，也就是两数求和再求和，那么这就是个 **双重和**，计算可以用 **双重和优化公式** ：
\[(N - 1) \sum_{i=1}^{N} A_i\]
不过这题加了个条件，和要取模，那么就考虑多少对数的和大于 $1e8$，最后把双重和计算的数减掉对数的和大于 $1e8$ 的个数 **$cnt * 1e8$** 就行。
那么怎么算 $cnt$ 呢，排序后遍历用二分找  $a_k \geq 1e8 - a_i$ 的最小下标 $k$ 就行，即二分找排位，最能找到 $a_i + a_j \geq 1e8$ 的所有 $j$ 的个数了。

<br>

## 代码实现

```cpp
const int N = 3e5 + 20;
const ll M = 1e8;
ll a[N];
ll ans = 0;
void solve()
{
    ll n; cin >> n;
    fa(i, 1, n) {
        cin >> a[i];
        ans += a[i];
    }
    sort(a + 1, a + 1 + n);
    ll cnt = 0;
    fa(i, 1, n) {
        ll idx = lower_bound(a + 1, a + 1 + n, M - a[i]) - a;
        if (idx <= i) idx = i + 1;
        if (idx <= n) cnt += n - idx + 1;
    }
    cout << ans* (n - 1) - cnt *M << endl;
    return;
}
```

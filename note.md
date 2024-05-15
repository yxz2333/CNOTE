# 博弈论

## 简单博弈论

- 打表**找规律**
- 考虑**奇偶**
- 考虑是否只存在一种**特别情况** _（比如只有 1 成立，别的都不成立）_
- 转化成一般算法题

~~感觉没必要学博弈论算法~~

<br>

# 数学

## 因数相关

#### 分解因数

```cpp
vector<int>factors;
for (int i = 1: i <= x / i; i++) {
    if(x % i == 0) {
        factors.push_back(x);
        if(i != x / i)
            factors.push_back(x);
    }
}
```

#### 分解质因数

- **性质**：
  通过分解质因数寻找因数个数
  `例 72 = 2^3 * 3^2 因数个数即为(3 + 1) * (2 + 1) = 12`

```cpp
vector<int> factors;
 while (n % 2 == 0) {
    factors.push_back(2);
    n = n / 2;
}
for (int i = 3; i * i <= n; i = i + 2) {
    while (n % i == 0) {
    factors.push_back(i);
        n = n / i;
    }
}
if (n > 2)
    factors.push_back(n);
```

## 公式

#### $i^2$ 的前 $n$ 项求和公式

$1²+2²+3²+...+n²=\frac{n(n+1)(2n+1)}{6}$

#### $a_i = Ai^2 + Bi + C$ 的前 $n$ 项和的公式：

$S_n = A \cdot \frac{n(n + 1)(2n + 1)}{6} + B \cdot \frac{n(n + 1)}{2} + nC$

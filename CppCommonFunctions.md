# C++ 刷题常用函数速查手册

> 涵盖洛谷 / 力扣新手题常见需求，按头文件分组。

---

## 目录

- [`<cmath>` — 数学函数](#cmath)
- [`<iomanip>` — 输出格式控制](#iomanip)
- [`<algorithm>` — 常用算法](#algorithm)
- [`<string>` — 字符串操作](#string)
- [`<vector>` — 动态数组](#vector)
- [`<map>` / `<unordered_map>` — 映射/字典](#map)
- [`<set>` / `<unordered_set>` — 集合](#set)
- [`<stack>` / `<queue>` — 栈和队列](#stackqueue)
- [`<utility>` — 对组与交换](#utility)
- [`<numeric>` — 数值运算](#numeric)
- [`<cctype>` — 字符判断/转换](#cctype)
- [`<bitset>` — 位集](#bitset)
- [`<climits>` — 极值常量](#climits)

---

## <cmath>

### 头文件

```cpp
#include <cmath>
```

### 常用函数

| 函数 | 作用 | 示例 |
|------|------|------|
| `pow(a, b)` | a 的 b 次方（返回 double） | `pow(2, 3)` -> 8.0；整数幂用 `(int)pow(2, 3)` -> 8 |
| `sqrt(x)` | 开平方 | `sqrt(16)` -> 4.0 |
| `cbrt(x)` | 开立方 | `cbrt(8)` -> 2.0 |
| `abs(x)` | 整数绝对值（见注） | `abs(-5)` -> 5 |
| `fabs(x)` | 浮点绝对值 | `fabs(-3.14)` -> 3.14 |
| `ceil(x)` | 向上取整 | `ceil(3.1)` -> 4.0 |
| `floor(x)` | 向下取整 | `floor(3.9)` -> 3.0 |
| `round(x)` | 四舍五入 | `round(3.5)` -> 4.0 |
| `fmax(a, b)` | 浮点最大值 | `fmax(2.5, 3.7)` -> 3.7 |
| `fmin(a, b)` | 浮点最小值 | `fmin(2.5, 3.7)` -> 2.5 |
| `log(x)` | 自然对数 ln(x) | `log(2.71828)` -> 1.0 |
| `log10(x)` | 以 10 为底的对数 | `log10(100)` -> 2.0 |
| `exp(x)` | e 的 x 次方 | `exp(1)` -> 2.71828 |
| `sin/cos/tan(x)` | 三角函数（弧度） | `sin(3.14159/2)` -> 1.0 |
| `asin/acos/atan(x)` | 反三角函数 | `atan(1)*4` -> pi |
| `atan2(y, x)` | 给 (y,x) 算角度 | `atan2(1,1)` -> pi/4 |
| `hypot(x, y)` | sqrt(x^2 + y^2) | 求直角三角形斜边 |
| `fmod(a, b)` | 浮点取余 | `fmod(5.5, 2)` -> 1.5 |

> **关于 `abs`**：整数 `abs` 严格定义在 `<cstdlib>`，浮点 `abs` / `fabs` 在 `<cmath>`。但在现代 C++（C++11 起）`<cmath>` 通常也提供整数重载，所以只引 `<cmath>` 一般够用。

```cpp
// 示例：求两点距离
double dist = hypot(x1 - x2, y1 - y2);

// 示例：判断素数（i*i <= n 避免浮点精度问题）
bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; ++i)  // 只需检查到 sqrt(n)
        if (n % i == 0) return false;
    return true;
}
```

---

## <iomanip>

### 头文件

```cpp
#include <iomanip>   // 控制输出格式
#include <iostream>  // cout
```

### 常用控制符

| 控制符 | 作用 | 示例 |
|--------|------|------|
| `fixed` | 以小数形式输出浮点 | `cout << fixed << 3.0;` -> `3.000000` |
| `setprecision(n)` | 设置小数位数（与 fixed 联用） | `cout << fixed << setprecision(2) << 3.14159;` -> `3.14` |
| `setw(n)` | 设置输出宽度（右对齐） | `cout << setw(5) << 42;` -> `   42` |
| `setfill(c)` | 填充字符（配合 setw） | `cout << setfill('0') << setw(3) << 7;` -> `007` |
| `left` / `right` | 左对齐 / 右对齐 | `cout << left << setw(5) << 42;` -> `42   ` |
| `scientific` | 科学计数法 | `cout << scientific << 1234.5;` -> `1.234500e+03` |

```cpp
// 示例：保留 3 位小数
double pi = 3.1415926;
cout << fixed << setprecision(3) << pi;  // 输出: 3.142

// 示例：打印对齐的表格
cout << left << setw(10) << "Name" << setw(5) << "Score" << endl;
cout << setfill('-') << setw(15) << "" << endl;  // 分隔线
cout << setfill(' ') << left << setw(10) << "Alice" << setw(5) << 95 << endl;
```

---

## <algorithm>

### 头文件

```cpp
#include <algorithm>
```

### 常用函数

| 函数 | 作用 |
|------|------|
| `sort(begin, end)` | 升序排序 |
| `sort(begin, end, greater<>())` | 降序排序 |
| `sort(begin, end, cmp)` | 自定义排序 |
| `reverse(begin, end)` | 反转区间 |
| `max(a, b)` / `min(a, b)` | 两者最大 / 最小值 |
| `max({a, b, c})` | 多个值取最大（initializer_list） |
| `min_element(begin, end)` | 区间最小值**迭代器** |
| `max_element(begin, end)` | 区间最大值**迭代器** |
| `swap(a, b)` | 交换两变量 |
| `find(begin, end, val)` | 查找值，返回迭代器 |
| `count(begin, end, val)` | 统计 val 出现次数 |
| `binary_search(begin, end, val)` | 二分查找（需有序）返回 bool |
| `lower_bound(begin, end, val)` | 第一个 >=val 的位置 |
| `upper_bound(begin, end, val)` | 第一个 >val 的位置 |
| `unique(begin, end)` | 去重（需先排序），返回新末尾 |
| `next_permutation(begin, end)` | 下一个排列 |
| `prev_permutation(begin, end)` | 上一个排列 |
| `fill(begin, end, val)` | 区间填充某个值 |
| `random_shuffle(begin, end)` | 随机打乱（C++14 弃用，C++17 移除，不推荐） |
| `shuffle(begin, end, mt19937)` | 随机打乱（推荐，需 `<random>`） |
| `nth_element(begin, nth, end)` | 部分排序，第 n 小的在 nth 位置 |

```cpp
// 示例：排序
int arr[] = {3, 1, 4, 1, 5};
sort(arr, arr + 5);  // 升序
// 或 vector
vector<int> v = {3, 1, 4, 1, 5};
sort(v.begin(), v.end(), greater<int>());  // 降序

// 示例：自定义排序——按绝对值降序
sort(v.begin(), v.end(), [](int a, int b) {
    return abs(a) > abs(b);
});

// 示例：去重
sort(v.begin(), v.end());
v.erase(unique(v.begin(), v.end()), v.end());

// 示例：二分查找
if (binary_search(v.begin(), v.end(), 42))
    cout << "找到了";
auto it = lower_bound(v.begin(), v.end(), 42);  // 第一个 >=42 的位置
int idx = it - v.begin();  // 转成下标
```

---

## <string>

### 头文件

```cpp
#include <string>
```

### 常用操作

| 操作 | 作用 | 示例 |
|------|------|------|
| `s.length()` / `s.size()` | 字符串长度 | `"abc".length()` -> 3 |
| `s.empty()` | 是否为空 | `"".empty()` -> true |
| `s[i]` | 取第 i 个字符 | |
| `s.substr(pos, len)` | 截取子串 | `s.substr(2, 3)` |
| `s.find(t)` | 查找子串，返回位置（无则 `string::npos`） | |
| `s.rfind(t)` | 从右查找 | |
| `s.insert(pos, t)` | 在 pos 处插入 | |
| `s.erase(pos, len)` | 删除 | |
| `s.replace(pos, len, t)` | 替换 | |
| `s.push_back(c)` | 末尾加一个字符 | |
| `s.pop_back()` | 删除末尾字符 | |
| `s += t` / `s.append(t)` | 拼接 | |
| `s.compare(t)` | 比较（按字典序） | `s < t` 也可直接比较 |
| `stoi(s)` | string -> int | `stoi("123")` -> 123 |
| `stoll(s)` | string -> long long | |
| `stod(s)` | string -> double | |
| `to_string(x)` | 数字 -> string | `to_string(42)` -> `"42"` |
| `getline(cin, s)` | 读一行（含空格） | |

```cpp
// 示例：读入整行
string line;
getline(cin, line);

// 示例：用 find 分割字符串
string s = "apple,banana,grape";
size_t pos = 0;
while ((pos = s.find(',')) != string::npos) {
    cout << s.substr(0, pos) << endl;
    s.erase(0, pos + 1);
}
cout << s << endl;  // 最后一段

// 示例：回文判断
bool isPal(string s) {
    string t = s;
    reverse(t.begin(), t.end());
    return s == t;
}
```

---

## <vector>

### 头文件

```cpp
#include <vector>
```

### 常用操作

| 操作 | 作用 |
|------|------|
| `vector<int> v;` | 声明空向量 |
| `vector<int> v(n);` | n 个元素，默认值 0 |
| `vector<int> v(n, 1);` | n 个元素，初始化为 1 |
| `v.push_back(x)` | 尾部添加 |
| `v.pop_back()` | 尾部删除 |
| `v.size()` | 元素个数 |
| `v.empty()` | 是否为空 |
| `v.front()` / `v.back()` | 首 / 尾元素 |
| `v[i]` | 随机访问（无边界检查） |
| `v.at(i)` | 随机访问（有边界检查） |
| `v.clear()` | 清空 |
| `v.insert(it, x)` | 在迭代器位置插入 |
| `v.erase(it)` | 删除迭代器指向元素 |
| `v.resize(n)` | 调整大小 |

```cpp
// 示例：遍历
for (int x : v) cout << x << " ";           // 只读
for (int& x : v) x *= 2;                    // 修改
for (size_t i = 0; i < v.size(); ++i)       // 下标
    cout << v[i] << " ";

// 示例：二维 vector（n 行 m 列）
vector<vector<int>> grid(n, vector<int>(m, 0));
```

---

## <map>

### 头文件

```cpp
#include <map>           // 有序（红黑树），O(log n)
#include <unordered_map> // 无序（哈希），O(1) 平均
```

### 常用操作

| 操作 | 作用 |
|------|------|
| `map<K,V> mp;` | 声明 |
| `mp[key] = val` | 插入或修改 |
| `mp[key]` | 访问（key 不存在时自动插入默认值） |
| `mp.at(key)` | 访问（key 不存在时抛异常） |
| `mp.count(key)` | key 是否存在（0 或 1） |
| `mp.find(key)` | 返回迭代器，不存在则 `mp.end()` |
| `mp.erase(key)` | 删除 |
| `mp.size()` | 大小 |

```cpp
// 示例：统计频率
unordered_map<int, int> freq;      // 一般用 unordered_map 更快
for (int x : arr) freq[x]++;

// 示例：查找
if (mp.count(key)) { /* 存在 */ }
auto it = mp.find(key);
if (it != mp.end()) cout << it->second;
```

---

## <set>

### 头文件

```cpp
#include <set>           // 有序，O(log n)，自动去重
#include <unordered_set> // 无序，O(1) 平均
```

| 操作 | 作用 |
|------|------|
| `set<T> st;` | 声明 |
| `st.insert(x)` | 插入 |
| `st.erase(x)` | 删除 |
| `st.count(x)` | 是否存在 |
| `st.find(x)` | 返回迭代器 |
| `st.size()` | 大小 |
| `multiset<T>` | 允许重复的有序集合 |

```cpp
// 示例：去重 + 排序
set<int> st(arr.begin(), arr.end());
for (int x : st) cout << x << " ";

// 示例：找集合中比 k 大的第一个数
auto it = st.upper_bound(k);
```

---

## <stack> / <queue>

### 头文件

```cpp
#include <stack>
#include <queue>
```

### stack（栈 — 后进先出）

| `push(x)` | `pop()` | `top()` | `size()` | `empty()` |
|-----------|---------|---------|----------|-----------|

```cpp
stack<int> stk;
stk.push(1); stk.push(2);
cout << stk.top();  // 2
stk.pop();          // 删除 2
```

### queue（队列 — 先进先出）

| `push(x)` | `pop()` | `front()` | `back()` | `size()` | `empty()` |
|-----------|---------|-----------|----------|----------|-----------|

```cpp
queue<int> q;
q.push(1); q.push(2);
cout << q.front();  // 1
q.pop();            // 删除 1
```

### priority_queue（优先队列 / 大根堆）

| `push(x)` | `pop()` | `top()` | `size()` | `empty()` |
|-----------|---------|---------|----------|-----------|

```cpp
// 默认大根堆（最大值优先）
priority_queue<int> pq;
pq.push(3); pq.push(1); pq.push(5);
cout << pq.top();  // 5

// 小根堆（最小值优先）
priority_queue<int, vector<int>, greater<int>> minHeap;
minHeap.push(3); minHeap.push(1); minHeap.push(5);
cout << minHeap.top();  // 1

// 自定义比较（pair 按第一个元素）
priority_queue<pair<int, int>, vector<pair<int,int>>, greater<>> pqPair;
```

---

## <utility>

### 头文件

```cpp
#include <utility>
```

| 操作 | 作用 |
|------|------|
| `pair<T1, T2> p;` | 声明 |
| `p.first` / `p.second` | 访问两个元素 |
| `make_pair(a, b)` | 构造 pair |
| `swap(a, b)` | 交换两个变量 |

```cpp
pair<int, string> p = {1, "hello"};  // 或 make_pair(1, "hello")
cout << p.first << " " << p.second;
```

---

## <numeric>

### 头文件

```cpp
#include <numeric>
```

| 函数 | 作用 |
|------|------|
| `accumulate(begin, end, 0)` | 求和，最后一个参数是初始值 |
| `gcd(a, b)` | 最大公约数（C++17） |
| `lcm(a, b)` | 最小公倍数（C++17） |
| `iota(begin, end, start)` | 填充递增序列 |

```cpp
// 示例：求和
vector<int> v = {1, 2, 3, 4};
int sum = accumulate(v.begin(), v.end(), 0);  // 10

// 示例：连乘（初始值 1，lambda 做二元运算）
long long product = accumulate(v.begin(), v.end(), 1LL,
    [](long long a, int b) { return a * b; });

// 示例：生成 1~n
vector<int> seq(n);
iota(seq.begin(), seq.end(), 1);  // 1, 2, 3, ..., n

// 示例：最大公约数
cout << gcd(12, 18);  // 6
cout << lcm(12, 18);  // 36
```

---

## <cctype>

### 头文件

```cpp
#include <cctype>
```

| 函数 | 作用 |
|------|------|
| `isalpha(c)` | 是字母 |
| `isdigit(c)` | 是数字 |
| `isalnum(c)` | 是字母或数字 |
| `islower(c)` | 是小写字母 |
| `isupper(c)` | 是大写字母 |
| `isspace(c)` | 是空白符（空格、tab、换行） |
| `tolower(c)` | 转小写 |
| `toupper(c)` | 转大写 |

```cpp
// 示例：字符串全转小写
string s = "Hello123";
for (char& c : s) c = tolower(c);
```

---

## <bitset>

### 头文件

```cpp
#include <bitset>
```

| 操作 | 作用 |
|------|------|
| `bitset<N> bs;` | 声明 N 位的位集（全 0） |
| `bitset<N> bs(x);` | 用整数 x 的二进制初始化 |
| `bs.set(pos)` | 第 pos 位置 1 |
| `bs.reset(pos)` | 第 pos 位置 0 |
| `bs.flip(pos)` | 第 pos 位翻转 |
| `bs.test(pos)` | 第 pos 位是否为 1 |
| `bs[pos]` | 直接访问第 pos 位 |
| `bs.count()` | 1 的个数 |
| `bs.any()` | 是否有 1 |
| `bs.none()` | 是否全 0 |
| `bs.to_ullong()` | 转 unsigned long long |
| `bs.to_string()` | 转 01 字符串 |

```cpp
// 示例：十进制转二进制字符串
int n = 42;
cout << bitset<8>(n);  // 输出: 00101010
```

---

## <climits>

### 头文件

```cpp
#include <climits>
```

### 常用常量

| 常量 | 含义 |
|------|------|
| `INT_MAX` | int 最大值（约 2.1x10^9） |
| `INT_MIN` | int 最小值 |
| `LLONG_MAX` | long long 最大值（约 9.2x10^18） |
| `LLONG_MIN` | long long 最小值 |
| `UINT_MAX` | unsigned int 最大值 |

```cpp
// 示例：初始化 "最小值" 再找最大值
int maxVal = INT_MIN;
for (int x : arr) if (x > maxVal) maxVal = x;
```

---

## 万能头文件（仅竞赛用）

```cpp
#include <bits/stdc++.h>
```

> 一次性包含几乎所有 C++ 标准库头文件。编译稍慢，但在洛谷、蓝桥杯、ACM 等 OJ 上都支持。写工程代码不要用。

---

## 快速参考：常见需求 -> 对应函数

| 你想做什么 | 用什么 |
|------------|--------|
| a 的 b 次方 | `pow(a, b)` |
| 开平方 | `sqrt(x)` |
| 保留 n 位小数输出 | `cout << fixed << setprecision(n)` |
| 绝对值 | `abs(x)` / `fabs(x)` |
| 向上/向下取整 | `ceil(x)` / `floor(x)` |
| 四舍五入 | `round(x)` |
| 排序 | `sort(v.begin(), v.end())` |
| 数组求和 | `accumulate(v.begin(), v.end(), 0)` |
| 最大公约数 | `gcd(a, b)` (C++17) |
| 二分查找 | `binary_search` / `lower_bound` |
| 去重 | `sort` + `unique` + `erase` |
| 全排列 | `next_permutation` |
| 字符串转整数 | `stoi(s)` |
| 整数转字符串 | `to_string(x)` |
| 统计频率 | `unordered_map<int,int>` 用 `m[x]++` |
| 大根堆 / 小根堆 | `priority_queue` |
| 判断字符类型 | `isdigit` / `isalpha` 等 |
| 读一行含空格的字符串 | `getline(cin, s)` |
| 输出补零 | `setfill('0') << setw(n)` |
| 十进制转二进制 | `bitset<N>(n)` |
| 初始化极大/极小值 | `INT_MAX` / `INT_MIN` |

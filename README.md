<p align="center">
  <h1 align="center">📖 C++ Cheatsheet</h1>
  <p align="center">
    <strong>一站式的 C++ 刷题函数速查手册</strong><br>
    涵盖 STL 常用库、算法、容器和格式化技巧，专为竞赛编程和初学者设计。
  </p>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/language-C%2B%2B17-blue.svg" alt="C++17">
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome">
  <img src="https://img.shields.io/github/license/Donkey28/cpp-cheatsheet" alt="License">
  <img src="https://img.shields.io/github/stars/Donkey28/cpp-cheatsheet?style=social" alt="Stars">
</p>

---

## Why this exists

学 C++ 刷题时，经常遇到"这个函数在哪个头文件""保留小数怎么写""怎么排序结构体"之类的问题。每次去网上翻文档太慢了——这份速查手册就是为了**一个 `Ctrl+F` 就能找到答案**。

适合：
- 🟢 C++ 新手刷洛谷 / 力扣 / Codeforces
- 🟢 课后作业写着写着忘了函数用法的学生
- 🟢 竞赛前快速回顾常用 API 的选手

## What's inside

| 模块 | 涵盖内容 |
|------|----------|
| `<cmath>` | pow、sqrt、ceil、floor、round、三角函数、对数…… |
| `<iomanip>` | fixed、setprecision、setw、setfill 等输出格式化 |
| `<algorithm>` | sort、lower_bound、unique、next_permutation…… |
| `<string>` | substr、find、stoi、to_string、getline…… |
| `<vector>` / `<map>` / `<set>` | 容器常用操作速查 |
| `<stack>` / `<queue>` | 栈、队列、优先队列（大小根堆） |
| `<numeric>` | accumulate、gcd、lcm、iota |
| `<cctype>` | 字符判断与大小写转换 |
| `<bitset>` | 位运算与进制转换 |

👉 **[查看完整手册 ->](CppCommonFunctions.md)**

## 快速预览

```cpp
// 保留 3 位小数
cout << fixed << setprecision(3) << 3.14159;  // 3.142

// 自定义排序
sort(v.begin(), v.end(), [](int a, int b) { return abs(a) > abs(b); });

// 去重
sort(v.begin(), v.end());
v.erase(unique(v.begin(), v.end()), v.end());

// 优先队列（小根堆）
priority_queue<int, vector<int>, greater<int>> minHeap;

// 最大公约数（C++17）
cout << gcd(36, 48);  // 12

// 读整行
string line; getline(cin, line);
```

## 使用方法

1. 浏览器里直接看 -> [CppCommonFunctions.md](CppCommonFunctions.md)
2. 本地克隆：`git clone https://github.com/Donkey28/cpp-cheatsheet.git`
3. 刷题时开着，`Ctrl+F` 搜关键字

## 贡献

欢迎提 Issue 和 PR！如果发现错误或有想加入的常用函数，直接提交即可。

## License

MIT © [Donkey28](https://github.com/Donkey28)

---

<p align="center">
  ⭐ 如果这份手册帮到了你，点个 Star 让更多人看到 ⭐
</p>

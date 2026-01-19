---
title: C转C++语法
source: https://www.cnblogs.com/mfoj/articles/19447471
author:
published: 2026-01-06
created: 2026-01-09
tags:
  - clippings
---

## 第一部分：基础语法差异

### 1.1 输入输出

**C语言方式**： `printf/scanf` 或 `getchar/putchar`

```c
int a;

scanf("%d", &a);

printf("%d\n", a);
```

**C++方式**： `cin/cout`

```cpp
#include <iostream>

using namespace std;



int a;

cin >> a;            // 输入

cout << a << endl;   // 输出
```

**输入输出优化** （必须放在main开头）：

```cpp
ios::sync_with_stdio(false);  // 解除C和C++标准流同步

cin.tie(nullptr);            // 解除cin和cout的绑定

cout.tie(nullptr);

// 使用后不能混用C和C++的输入输出函数
```

### 1.2 头文件

```cpp
#include <bits/stdc++.h>  // 万能头文件（竞赛推荐）

using namespace std;      // 使用标准命名空间



// 或使用传统头文件

#include <iostream>  // 输入输出

#include <vector>    // 动态数组

#include <algorithm> // 算法库

#include <string>    // 字符串

#include <cctype>    // 字符处理
```

### 1.3 变量定义

C++允许在任意位置定义变量：

```cpp
for(int i = 0; i < n; i++) {  // 循环变量在循环内定义

    int temp = i * 2;         // 变量在需要时定义

}
```

### 1.4 数据类型扩展

```cpp
bool flag = true;    // 布尔类型，还有false

const int MAX = 100; // 常量定义

auto x = 10;         // 自动类型推导（C++11）
```

## 第二部分：常用数据结构

### 2.1 string字符串类

```cpp
#include <string>

using namespace std;



string s1 = "Hello";

string s2 = "World";



// 常用操作

int len = s1.length();             // 长度

s1.empty();                       // 判空

s1.clear();                       // 清空

s1.append(" Test");              // 追加

s1 += "!";                        // 拼接

string s3 = s1 + " " + s2;       // 拼接

string sub = s1.substr(1, 3);     // 子串

int pos = s1.find("ell");         // 查找

s1.replace(1, 3, "i");           // 替换

s1.insert(5, "Insert");          // 插入

s1.erase(5, 6);                  // 删除

int num = stoi("123");           // 字符串转int

string str = to_string(123);     // 数字转字符串
```

### 2.2 [[vector,栈和队列的定义理解|vector动态数组]]

**一维数组**：

```cpp
#include <vector>

vector<int> v;               // 定义

v.push_back(10);            // 尾部添加

v.pop_back();               // 尾部删除

v.size();                   // 大小

v.empty();                  // 判空

v.resize(100);              // 调整大小

v.reserve(1000);            // 预分配空间

v[0] = 5;                   // 访问

sort(v.begin(), v.end());   // 排序
```

**二维数组**：

```cpp
// 1. 声明n行m列

vector<vector<int>> matrix(n, vector<int>(m, 0));



// 2. 先声明后调整

vector<vector<int>> matrix;

matrix.resize(n);

for(int i = 0; i < n; i++) {

    matrix[i].resize(m, 0);

}



// 3. 直接初始化

vector<vector<int>> matrix = {

    {1, 2, 3},

    {4, 5, 6},

    {7, 8, 9}

};



// 访问和遍历

int rows = matrix.size();

int cols = matrix[0].size();

matrix[2][3] = 10;  // 访问（注意下标不要越界）



// 遍历

for(int i = 0; i < rows; i++) {

    for(int j = 0; j < cols; j++) {

        cout << matrix[i][j] << " ";

    }

    cout << endl;

}
```

### 2.3 其他常用容器

```cpp
#include <set>       // 集合（自动排序）

#include <map>       // 键值对

#include <queue>     // 队列

#include <stack>     // 栈

#include <bitset>    // 位集
```

**set集合**：

```cpp
set<int> s = {3, 1, 4, 1, 5};  // {1, 3, 4, 5}

s.insert(2);      // 插入

s.erase(3);       // 删除

s.count(2);       // 是否存在

s.find(4);        // 查找

s.lower_bound(3); // >=3的第一个元素

s.upper_bound(3); // >3的第一个元素
```

**map映射**：

```cpp
map<string, int> mp;

mp["apple"] = 5;     // 插入/修改

mp["banana"] = 3;

mp.count("apple");   // 是否存在

mp.find("apple");    // 查找

mp.erase("apple");   // 删除

mp.size();           // 大小
```

**栈和队列**：
>[!tip]+ 在 C++ 中，stk.pop() 只负责弹出，不返回栈顶元素。如果你想获取栈顶的值并弹出，必须先调用 stk.top()，然后再调用 stk.pop()。
> 

```cpp
// 栈

stack<int> stk;

stk.push(1);        // 入栈

stk.top();          // 栈顶

stk.pop();          // 出栈

stk.empty();        // 判空



// 队列

queue<int> q;

q.push(1);          // 入队

q.front();          // 队首

q.pop();            // 出队

q.back();           // 队尾

q.empty();



// 优先队列

priority_queue<int> max_heap;  // 最大堆

priority_queue<int, vector<int>, greater<int>> min_heap;  // 最小堆
```

**bitset位集**：

```cpp
bitset<8> b("11110000");  // 8位二进制

b.set();                  // 所有位置1

b.reset();                // 所有位置0

b.set(3, 1);              // 第3位置1

b.flip(2);               // 第2位取反

bool bit = b.test(2);    // 测试第2位

int cnt = b.count();     // 1的个数
```

## 第三部分：字符处理（cctype库）

```cpp
#include <cctype>  // 字符处理函数



char ch = 'A';



// 判断函数

isalpha(ch);   // 是否为字母

isdigit(ch);   // 是否为数字

isalnum(ch);   // 是否为字母或数字

islower(ch);   // 是否为小写字母

isupper(ch);   // 是否为大写字母

isspace(ch);   // 是否为空白字符

ispunct(ch);   // 是否为标点符号

isxdigit(ch);  // 是否为十六进制数字



// 转换函数

toupper('a');  // 'a' -> 'A'

tolower('B');  // 'B' -> 'b'



// 实际应用

string str = "Hello World 123!";



// 统计字符类型

int letters = 0, digits = 0, spaces = 0;

for(char c : str) {

    if(isalpha(c)) letters++;

    else if(isdigit(c)) digits++;

    else if(isspace(c)) spaces++;

}



// 转换为大写

for(char& c : str) {

    c = toupper(c);

}



// 判断回文字符串（忽略大小写和标点）

bool is_palindrome(const string& s) {

    int left = 0, right = s.length() - 1;

    while(left < right) {

        while(left < right && !isalnum(s[left])) left++;

        while(left < right && !isalnum(s[right])) right--;

        if(tolower(s[left]) != tolower(s[right])) return false;

        left++; right--;

    }

    return true;

}
```

## 第四部分：算法库函数

```cpp
#include <algorithm>

#include <numeric>

#include <functional>



vector<int> v = {3, 1, 4, 1, 5};



// 排序

sort(v.begin(), v.end());                    // 升序

sort(v.begin(), v.end(), greater<int>());    // 降序



// 查找

find(v.begin(), v.end(), 4);                 // 查找

binary_search(v.begin(), v.end(), 4);        // 二分查找

lower_bound(v.begin(), v.end(), 3);          // >=3的第一个

upper_bound(v.begin(), v.end(), 3);          // >3的第一个



// 最值

*max_element(v.begin(), v.end());           // 最大值

*min_element(v.begin(), v.end());           // 最小值



// 操作

reverse(v.begin(), v.end());                // 反转

rotate(v.begin(), v.begin()+2, v.end());    // 旋转

next_permutation(v.begin(), v.end());       // 下一个排列



// 计数

count(v.begin(), v.end(), 1);               // 计数

count_if(v.begin(), v.end(), [](int x) {  // 条件计数
    return x > 2;
});



// 累加

accumulate(v.begin(), v.end(), 0);          // 求和

fill(v.begin(), v.end(), 0);                // 填充

iota(v.begin(), v.end(), 1);                // 填充1,2,3,...
```

## 第五部分：C++11新特性

### 5.1 auto自动类型

```cpp
auto x = 10;                     // int

auto y = 3.14;                   // double

auto z = "hello";                // const char*

auto v = vector<int>(10);        // vector<int>

auto it = v.begin();            // vector<int>::iterator
```

### 5.2 范围for循环

```cpp
vector<int> v = {1, 2, 3, 4, 5};



// 只读遍历

for(int num : v) {

    cout << num << " ";

}



// 可修改遍历

for(int& num : v) {

    num *= 2;

}



// 只读引用（避免复制）

for(const int& num : v) {

    cout << num << " ";

}
```

### 5.3 Lambda表达式

```cpp
// 基本形式
auto add = [](int a, int b) { return a + b; };
cout << add(3, 4) << "\n";  // 7

// 在算法中使用
vector<int> v = {1, 2, 3, 4, 5};

// 降序排序
sort(v.begin(), v.end(), [](int a, int b) {
    return a > b;
});

// 统计大于2的元素
int cnt = count_if(v.begin(), v.end(), [](int x) {
    return x > 2;
});

// 捕获外部变量
int base = 10;
for_each(v.begin(), v.end(), [&](int& x) {
    x += base;
});
```

## 第六部分：竞赛实用模板

### 6.1 通用模板

```cpp
#include <bits/stdc++.h>

using namespace std;



// 常用宏定义

typedef long long ll;

typedef unsigned long long ull;

#define fi first

#define se second

const int INF = 0x3f3f3f3f;

const int MOD = 1e9 + 7;

const int MAXN = 1e5 + 5;



int main() {

    // 输入输出优化

    ios::sync_with_stdio(false);

    cin.tie(nullptr);

    cout.tie(nullptr);



    // 读取数据

    int n;

    cin >> n;



    vector<int> arr(n);

    for(int i = 0; i < n; i++) {

        cin >> arr[i];

    }



    // 处理逻辑

    sort(arr.begin(), arr.end());



    // 输出

    for(int num : arr) {

        cout << num << " ";

    }



    return 0;

}
```

### 6.2 快速读入

```cpp
// 整数快速读入

inline int read() {

    int x = 0, f = 1;

    char ch = getchar();

    while(ch < '0' || ch > '9') {

        if(ch == '-') f = -1;

        ch = getchar();

    }

    while(ch >= '0' && ch <= '9') {

        x = x * 10 + (ch - '0');

        ch = getchar();

    }

    return x * f;

}
```

### 6.3 实用函数

```cpp
// 检查字符串是否全是数字

bool is_all_digits(const string& s) {

    for(char c : s) {

        if(!isdigit(c)) return false;

    }

    return true;

}



// 字符串分割

vector<string> split(const string& s, char delimiter) {

    vector<string> tokens;

    string token;

    istringstream tokenStream(s);

    while(getline(tokenStream, token, delimiter)) {

        tokens.push_back(token);

    }

    return tokens;

}



// 快速幂

ll qpow(ll a, ll b, ll mod) {

    ll res = 1;

    while(b) {

        if(b & 1) res = res * a % mod;

        a = a * a % mod;

        b >>= 1;

    }

    return res;

}
```

## 第七部分：常见问题与技巧

### 7.1 性能优化

```cpp
// 1. vector预分配

vector<int> v;

v.reserve(1000000);  // 预分配空间，避免多次扩容



// 2. 使用emplace_back代替push_back

vector<pair<int, int>> v;

v.emplace_back(1, 2);  // 直接在容器中构造

v.push_back({1, 2});   // 先构造，再复制



// 3. 使用unordered_set/map提高查找速度

#include <unordered_set>

#include <unordered_map>

unordered_set<int> us;  // 哈希表实现，查找O(1)

unordered_map<int, int> um;
```

### 7.2 内存管理

```cpp
// 1. 及时清空容器

vector<int> v(1000000);

v.clear();                     // 只清空元素

vector<int>().swap(v);         // 真正释放内存



// 2. 使用移动语义

vector<int> v1 = {1, 2, 3, 4, 5};

vector<int> v2 = move(v1);    // 移动而非复制
```

### 7.3 调试技巧

```cpp
// 1. 调试输出

#ifdef DEBUG

#define debug(x) cout << #x << " = " << x << endl

#else

#define debug(x)

#endif



// 2. 运行时错误检查

vector<int> v(10);

if(idx >= 0 && idx < v.size()) {  // 检查越界

    v[idx] = 5;

}
```

## 第八部分：蓝桥杯常考题型

### 8.1 排序与查找

```cpp
// 自定义排序

struct Student {

    int id;

    int score;

    bool operator<(const Student& other) const {

        if(score != other.score)

            return score > other.score;  // 分数降序

        return id < other.id;            // id升序

    }

};



vector<Student> students;

sort(students.begin(), students.end());
```

### 8.2 模拟题

```cpp
// 日期计算

int days[] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

bool is_leap(int year) {

    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);

}
```

### 8.3 字符串处理

```cpp
// 大数运算

string add_bigint(const string& a, const string& b) {

    string res;

    int carry = 0, i = a.length() - 1, j = b.length() - 1;

    while(i >= 0 || j >= 0 || carry) {

        int sum = carry;

        if(i >= 0) sum += a[i--] - '0';

        if(j >= 0) sum += b[j--] - '0';

        res.push_back(sum % 10 + '0');

        carry = sum / 10;

    }

    reverse(res.begin(), res.end());

    return res;

}
```

## 学习建议

1. **循序渐进**：先掌握vector、sort，再学set、map
2. **多练习**：在洛谷、Codeforces等平台刷题
3. **善用STL**：STL能大幅简化代码
4. **注意效率**：大数据量时注意时间空间限制
5. **代码规范**：使用有意义的变量名，添加注释

## 常用快捷键

- `Ctrl + /`：注释/取消注释
- `Ctrl + D`：复制当前行
- `Ctrl + Shift + F`：格式化代码
- `F5`：编译运行
- `F9`：设置断点

---

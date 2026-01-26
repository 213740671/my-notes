# 📚 C++ 结构体 (Struct) 全能实战笔记

结构体是 C++ 中处理**复合数据**的核心工具。它不仅能把不同类型的数据打包，还具备类似类（Class）的强大功能。

---

## 一、 基础语法与定义

### 1.1 定义格式
```cpp
struct Student {
    int num;        // 学号
    int chinese;    // 语文成绩
    int math;       // 数学成绩
    int total = 0;  // 总分（建议设置默认初值，防止乱码）
}; // <--- 必须有分号
```

### 1.2 声明与初始化
* **传统初始化**：`Student s1; s1.num = 1;`
* **列表初始化 (C++11)**：`Student s2 = {1, 90, 80, 170};`
* **指定初始化 (C++20)**：`Student s3 = {.num = 1, .chinese = 95};` (未指定的成员自动为 0)

---

## 二、 C 与 C++ 的核心区别

| 特性 | C 语言 | C++ 语言 |
| :--- | :--- | :--- |
| **类型名** | 必须写 `struct Student` | 直接写 `Student` 即可 |
| **typedef** | 常用 `typedef` 来简化写法 | **不需要**，结构体已是“一等公民”类型 |
| **功能** | 只能存数据 | 可以包含**函数**和**构造函数** |

> **💡 避坑指南：** 在 C++ 开发中，请直接写 `struct Student {...};`。除非为了兼容极老的 C 代码，否则不要写 `typedef struct`。

---

## 三、 结构体数组：批量数据处理

### 3.1 两种存储方式对比

| 存储方式 | 语法示例 | 特点 |
| :--- | :--- | :--- |
| **原生数组** | `Student arr[100];` | 长度固定，内存分配在栈区，简单但死板。 |
| **Vector 容器** | `vector<Student> v;` | **强烈推荐**。长度动态可变，功能丰富，更安全。 |

### 3.2 访问与赋值
无论是数组还是 Vector，访问成员的方法完全一致，都使用 **点操作符 (`.`)**。

```cpp
// 场景：给数组中第 i 个学生的语文成绩单独赋值
arr[i].chinese = 95;      // 原生数组
vec[i].chinese = 95;      // vector 容器
```

---

## 四、 进阶实战：如何给单个参数赋值？

当你需要向 `vector` 添加数据但只想初始化部分成员时，有三种策略：

### 1. 先创建对象，后逐个赋值 (最稳妥)
```cpp
Student temp;
temp.num = i;
temp.chinese = 90;
// 其他成员保持默认值
students.push_back(temp);
```

### 2. 使用 C++20 指定初始化 (最优雅)
```cpp
// 明确指定给哪个成员赋值，其他成员自动初始化为 0
students.push_back({ .num = i, .chinese = 90 });
```

### 3. 直接通过下标修改 (针对已存在的对象)
```cpp
// 假设 vector 已经有数据了，直接精准打击
students[0].math = 100;
```

---

## 五、 代码规范与性能建议

1.  **命名规范**：结构体名用 **大驼峰** (`StudentInfo`)，成员名用 **小驼峰** (`chineseScore`)。
2.  **传参规范**：函数传参时，优先使用 **const 引用**，避免内存拷贝提升性能。
    * ✅ `void print(const Student& s)`
3.  **预留空间**：如果已知数据总量为 `n`，使用 `students.reserve(n)` 提前分配空间，防止 vector 频繁扩容。
4.  **现代化遍历**：
    ```cpp
    for (const auto& s : students) {
        cout << s.num << ":" << s.chinese << endl;
    }
    ```

---

## 六、 完整示例代码

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct Student {
    int num;
    int chinese = 0;
    int math = 0;
    int total = 0;
};

int main() {
    int n;
    cin >> n;
    vector<Student> students;

    for (int i = 0; i < n; i++) {
        int c, m;
        cin >> c >> m;
        
        // 快速封装并推入容器
        students.push_back({i + 1, c, m, c + m});
    }

    // 修改特定数据
    if (!students.empty()) {
        students[0].chinese = 100; // 单独修改第一个人的语文
    }

    return 0;
}
```
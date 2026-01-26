# 📘 C++ 结构体 (Struct) 深度学习笔记

结构体是 C++ 中将不同类型数据打包的“万能工具”。在现代 C++ 中，它不仅是数据的集合，更像是一个轻量级的类（Class）。

---

## 1. 基础语法与定义

### 1.1 定义格式
定义结构体就像在制定一个“模版”。
```cpp
struct Student {
    string name;    // 姓名
    int age = 18;   // 年龄（C++11 支持设置默认值）
    double score;   // 成绩
}; // <--- 重点：末尾的分号绝对不能丢！
```

### 1.2 声明与初始化
在 C++ 中，结构体名直接就是**类型名**。

```cpp
// 1. 列表初始化（C++11 最推荐，简洁明了）
Student s1 = {"小明", 20, 95.5};

// 2. 先声明再赋值
Student s2;
s2.name = "小红";
s2.score = 99.0;
```

---

## 2. C 与 C++ 的核心区别 (关于 typedef)

如果你有 C 语言背景，请务必更新这个认知：**在 C++ 中，`typedef` 是多余的。**

| 特性 | C 语言 | C++ 语言 |
| :--- | :--- | :--- |
| **类型定义** | 必须写 `struct Student s;` | 直接写 `Student s;` |
| **typedef** | 常用 `typedef struct` 避开 `struct` 关键字 | **完全不需要**，结构体是一等公民类型 |
| **功能扩展** | 只能存数据 | 内部可以写**函数**（方法）和**构造函数** |

> **💡 建议：** 在写纯 C++ 代码时，直接写 `struct Name {...};` 即可，不要再画蛇添足使用 `typedef`。

---

## 3. 结构体数组：批量数据处理

处理多个同类对象时，你可以使用“普通数组”或“Vector 容器”。

### 3.1 普通数组 (固定长度)
适用于数据量已知且不变的情况。
```cpp
Student classA[3] = {
    {"A", 18, 80},
    {"B", 18, 85},
    {"C", 18, 90}
};
// 访问：classA[0].name
```

### 3.2 Vector 数组 (动态长度 - 强烈推荐)
`std::vector` 是 C++ 处理结构体数据的“黄金搭档”，支持动态增删。
```cpp
#include <vector>

std::vector<Student> students;
students.push_back({"小强", 19, 88.0}); // 动态添加数据
```



---

## 4. 代码规范与实战技巧

为了让代码更具专业感（“大厂范儿”），请遵循以下规范：

### 4.1 命名规范
* **结构体类型名**：使用 **大驼峰** (PascalCase)，如 `UserInfo`。
* **成员变量名**：使用 **小驼峰** (camelCase) 或 **下划线** (snake_case)，如 `userAge`。

### 4.2 现代化的遍历方式
不要再使用繁琐的下标遍历，使用 `Range-based for loop`：
```cpp
// 使用 const 引用遍历：既安全又快（不会产生数据复制）
for (const auto& s : students) {
    cout << s.name << " 的分数是: " << s.score << endl;
}
```

### 4.3 传参规范
结构体可能占用很大内存，传递给函数时，**永远优先使用引用传递**。
* ❌ `void print(Student s)` —— 会复制整个结构体，浪费性能。
* ✅ `void print(const Student& s)` —— 像传指针一样快，且 `const` 保证数据不被误改。

---

## 5. 新手快速处理数据“三板斧”

如果你拿到一批数据（如：员工信息、游戏道具），请按以下流程处理：

1.  **建模**：定义一个 `struct`，包含所有必要的字段。
2.  **存储**：创建一个 `std::vector<YourStruct>`。
3.  **计算**：利用 `for (auto& item : vector)` 进行批量修改或统计。



---

## 6. 进阶：在结构体中加入“动作”
C++ 的结构体可以拥有函数，这能让数据处理更直观。
```cpp
struct Item {
    string name;
    double price;

    // 成员函数：直接处理自己的数据
    void applyDiscount(double rate) {
        price *= rate;
    }
};
```

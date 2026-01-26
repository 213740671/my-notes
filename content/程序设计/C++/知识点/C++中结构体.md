## 一、 基本语法与定义

### 1. 定义格式
定义结构体就像在制定一个“模版”。
```cpp
struct Student {
    string name;    // 姓名
    int age;        // 年龄
    double score;   // 成绩
}; // <--- 重点：末尾的分号千万不能丢！
```

### 2. 声明与初始化 (C++11 风格)
在 C++ 中，你不需要像 C 语言那样写 `struct Student s1`，直接写 `Student` 即可。

```cpp
// 方式 A：先声明再逐个赋值
Student s1;
s1.name = "阿强";
s1.age = 20;

// 方式 B：大括号列表初始化（最推荐，最快）
Student s2 = {"阿珍", 19, 98.5};

// 方式 C：部分初始化（未定义的成员会根据类型默认初始化）
Student s3 = {"小明"}; 
```

---

## 二、 C 与 C++ 的核心区别 (关于 typedef)

| 特性 | C 语言 | C++ 语言 |
| :--- | :--- | :--- |
| **类型名** | `struct Student` 才是完整类型名 | `Student` 直接就是类型名 |
| **typedef** | 必须用 `typedef` 才能省略 `struct` 关键字 | **完全不需要** `typedef`，结构体是一等公民 |
| **函数** | 结构体内不能写函数 | 结构体内可以写函数（方法） |
| **默认值** | 不支持成员默认值 | 支持（如 `int age = 18;`） |

> **💡 结论：** 在 C++ 环境下，看到 `typedef struct` 通常是为了兼容老代码。写新代码时，直接定义 `struct` 即可。

---

## 三、 新手高效处理数据：结构体 + 容器

处理大量数据时，将**结构体**与 **`std::vector`** 结合是标准做法。

### 示例：处理商品清单
```cpp
#include <iostream>
#include <vector>
#include <string>

struct Product {
    string name;
    double price;
    
    // 进阶：在结构体内定义函数
    void printInfo() {
        std::cout << "商品: " << name << " | 价格: " << price << std::endl;
    }
};

int main() {
    // 1. 使用 vector 存储多个结构体
    std::vector<Product> list = {
        {"键盘", 299.0},
        {"鼠标", 150.0},
        {"显示器", 1200.0}
    };

    // 2. 遍历处理
    for (auto &item : list) {
        item.price *= 0.9; // 全场 9 折处理
        item.printInfo();
    }
    
    return 0;
}
```

---

## 四、 避坑与进阶建议

1.  **传参优化**：
    当把结构体传给函数时，尽量使用 **引用传递** (`&`)，避免产生不必要的内存复制。
    * ❌ `void print(Student s)` (慢，复制了一份数据)
    * ✅ `void print(const Student& s)` (快，直接读取原数据)
    
2.  **默认值设定**：
    在定义时直接给初值，可以防止出现随机乱码数据：
    ```cpp
    struct User {
        int id = 0;
        bool isActive = false;
    };
    ```

3.  **内存对齐**：
    结构体的大小并不总是成员大小之和，C++ 会为了读取效率进行“内存对齐”。如果你发现 `sizeof(Struct)` 比预想的大，那是正常的。

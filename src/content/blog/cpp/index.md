---
title: "Qt 编程规范"
description: "Qt 编程规范"
date: "2025-08-14"
tags:
  - cpp
  - qt
---

## 编程规范

1. 不要用 foreach, 用 C++ 11 的 for， 因为 Qt 的 foreach（Q_FOREACH）是一种宏，它会复制容器中的元素，而不是直接引用它们
2. 想省略 Q_D 的时候，使用 d_func 不要用 d_ptr 因为 d_func() 是内联的，不会有额外的开销，是对 d_ptr 的解引用，等效于 d_ptr.data()。
3. 方法和字段按照如下顺序声明（.h）和定义（.cpp），且字段在方法前定义
  - signals:
  - public: slots, setter
  - public: getter
4. 键值对列表不需要排序的话用 QHash 而不是 QMap
5. 类成员变量的 POD 类型注意初始化赋值，销毁时也赋值
6. 注意线程之间的关系
7. 不要用 C 风格的全局变量，直接在类里面声明

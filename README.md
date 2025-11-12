<!---
{
  "id": "e2c108ad-125e-45ac-8fe1-d2e3b13f48eb",
  "teaches": "Understanding Functors in C++",
  "depends_on": ["objects", "operator overloading", "methods"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-05-20",
  "keywords": ["C++", "Functors", "Function Objects", "Operator Overloading"]
}
--->

# Understanding Functors in C++

> In this exercise you will learn what functors (function objects) are in C++. Furthermore we will explore how to implement and use them in different contexts, especially with the Standard Template Library (STL).

### Introduction

Functors, or function objects, are objects in C++ that behave like functions. This functionality is achieved by overloading the function call operator `operator()`, enabling objects of a class or struct to be used with function-call syntax. Functors are a core feature in C++ for writing flexible and efficient code, especially within generic programming and the STL.

One of the key advantages of functors is that they can maintain **internal state**. Unlike plain functions, which rely solely on parameters, a functor can store information in member variables and use this information when invoked. This stateful behavior makes functors more versatile and reusable. For example, you can design a functor that keeps track of how many times it has been called, or one that adds a fixed value to inputs based on a constructor argument.

Functors are especially useful when you need function-like behavior with the added power of encapsulated state and logic. In many STL algorithms like `std::sort`, `std::for_each`, and `std::transform`, functors serve as custom behaviors that can be passed into these algorithms for powerful and concise logic control.

Mastering functors builds a strong foundation for writing clean, object-oriented, and reusable C++ code. Their stateless and stateful variations provide great flexibility in real-world applications.

### Further Readings and Other Sources

* [cppreference on Function Objects](https://en.cppreference.com/w/cpp/named_req/FunctionObject)
* Josuttis, N. (2012). *The C++ Standard Library: A Tutorial and Reference*.
* [https://www.learncpp.com/cpp-tutorial/functors/](https://www.learncpp.com/cpp-tutorial/functors/) (LearnCpp on Functors)
* [https://www.youtube.com/watch?v=nbTSfrEfo6M](https://www.youtube.com/watch?v=nbTSfrEfo6M) (YouTube tutorial on functors)

---

### Tasks

#### Task 1: Creating a Simple Functor

1. Open your `vim` editor and create a file named `functor_basic.cpp`.
2. Write a class `Multiplier` with an overloaded `operator()` that multiplies two integers.

```cpp
#include <iostream>

class Multiplier {
public:
    int operator()(int a, int b) {
        return a * b;
    }
};

int main() {
    Multiplier mult;
    std::cout << "3 * 4 = " << mult(3, 4) << std::endl;
    return 0;
}
```

#### Task 2: Stateful Functor

This task demonstrates how functors can **maintain internal state**.

1. Create a file named `functor_stateful.cpp`.
2. Create a class `Adder` that stores an internal integer offset and adds it to each input.

```cpp
#include <iostream>

class Adder {
    int offset;
public:
    Adder(int o) : offset(o) {}

    int operator()(int x) {
        return x + offset;
    }
};

int main() {
    Adder add5(5);
    std::cout << "10 + 5 = " << add5(10) << std::endl;
    return 0;
}
```

#### Task 3: Using Functors with STL Algorithms

1. File: `functor_sort.cpp`
2. Create a custom comparator functor to sort a vector of strings by descending length.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

struct DescLength {
    bool operator()(const std::string &a, const std::string &b) {
        return a.size() > b.size();
    }
};

int main() {
    std::vector<std::string> words = {"apple", "banana", "fig", "grape"};
    std::sort(words.begin(), words.end(), DescLength());

    for (const auto &word : words) {
        std::cout << word << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

---

### Questions

1. What is the difference between a functor and a function pointer?
2. How can functors maintain internal state?
3. What are the benefits of using functors over plain functions?
4. When would you use a functor in STL algorithms?
5. Can a functor be used as a template argument? Provide an example.

---

### Advice

Think of functors as a hybrid between functions and objects. They allow you to encapsulate both behavior and data in a single callable entity. Practice using them in scenarios where you need operations to carry configuration or context. Functors are excellent for writing expressive and modular code in STL pipelines. Once you are comfortable with functors, you may also want to explore our [exercise sheet on lambda expressions](#) for a more modern and concise alternative to function objects in C++.

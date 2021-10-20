---
layout: post
title: Stack
date: 2021-10-20
---

```cpp
template <class T>
class Stack
{
    T* data;
    unsigned int size;

public:
    Stack(unsigned int size) : data(new T[size]), size(0) {}

public:
    void push(T data)
    {
        this->data[size] = data;
        size++;
    }

    T pop()
    {
        size--;
        return this->data[size];
    }
};
```

```text
          +---------------+
          |    size: 4    |
          +---+---+---+---+
          |   |   |   |   | <--- push
data ---> | 0 | 1 | 2 | 3 |
          |   |   |   |   | ---> pop
          +---+---+---+---+
```

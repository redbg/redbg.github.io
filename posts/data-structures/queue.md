---
layout: post
title: Queue
date: 2021-10-20
---

```cpp
template <class T>
class Node
{
public:
    Node* next;
    Node* prev;
    T data;

    Node(T data, Node* next = nullptr, Node* prev = nullptr) : data(data), next(next), prev(prev) {}
};

template <class T>
class Queue
{
public:
    Node<T>* head = nullptr;

    void push(T data)
    {
        if (head == nullptr)
        {
            head = new Node<T>(data);
            return;
        }

        Node<T>* node = new Node<T>(data, head);
        head->prev = node;
        head = node;
    }

    T pop()
    {
        if (head == nullptr)
        {
            return T();
        }

        Node<T>* node = head;

        while (true)
        {
            if (node->next == nullptr)
            {
                if (node == head)
                {
                    head = nullptr;
                }
                else
                {
                    node->prev->next = nullptr;
                }
                return node->data;
            }
            node = node->next;
        }
    }
};
```

```text
          +---+---+---+---+
push ---> | 3 | 2 | 1 | 0 | ---> pop
          +---+---+---+---+
```

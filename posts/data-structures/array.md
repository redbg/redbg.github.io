---
layout: post
title: Array
date: 2021-10-18
---

## 多维数组

```cpp
// [2][9][9]
char a[10][10][10] = {};
printf("%d\n", &a[2][9][9] - (char*)a);
// output:299

// [2][9][9]
char b[10 * 10 * 10] = {};
printf("%d\n", &b[(2 * (10 * 10)) + (9 * 10) + 9] - b);
// output:299
```

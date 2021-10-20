---
layout: post
title: Array
date: 2021-10-18
---

## softsec::array

```cpp
namespace softsec
{
    template <class T, size_t N>
    class array
    {
    public:
        // ============================== types ==============================

        // type
        using value_type = T;
        using size_type = size_t;
        using difference_type = ptrdiff_t;
        // pointer
        using pointer = T*;
        using const_pointer = const T*;
        // reference
        using reference = T&;
        using const_reference = const T&;

        // iterator
        using iterator = pointer;
        using const_iterator = const_pointer;
        // reverse_iterator
        using reverse_iterator = std::reverse_iterator<iterator>;
        using const_reverse_iterator = std::reverse_iterator<const_iterator>;

        // ============================== No explicit construct/copy/destroy for aggregate type ==============================

        constexpr void fill(const T& value) { std::fill_n(data(), N, value); }

        constexpr void swap(array& other) noexcept(std::_Is_nothrow_swappable<T>::value) { std::_Swap_ranges_unchecked(data(), data() + N, other.data()); }

        // ============================== iterators ==============================
        [[nodiscard]] constexpr iterator begin() noexcept { return iterator(data()); }
        [[nodiscard]] constexpr const_iterator begin() const noexcept { return const_iterator(data()); }
        [[nodiscard]] constexpr iterator end() noexcept { return iterator(data() + N); }
        [[nodiscard]] constexpr const_iterator end() const noexcept { return const_iterator(data() + N); }

        [[nodiscard]] constexpr reverse_iterator rbegin() noexcept { return reverse_iterator(end()); }
        [[nodiscard]] constexpr const_reverse_iterator rbegin() const noexcept { return const_reverse_iterator(end()); }
        [[nodiscard]] constexpr reverse_iterator rend() noexcept { return reverse_iterator(begin()); }
        [[nodiscard]] constexpr const_reverse_iterator rend() const noexcept { return const_reverse_iterator(begin()); }

        [[nodiscard]] constexpr const_iterator cbegin() const noexcept { return begin(); }
        [[nodiscard]] constexpr const_iterator cend() const noexcept { return end(); }
        [[nodiscard]] constexpr const_reverse_iterator crbegin() const noexcept { return rbegin(); }
        [[nodiscard]] constexpr const_reverse_iterator crend() const noexcept { return rend(); }

        // ============================== capacity ==============================

        [[nodiscard]] constexpr size_type size() const noexcept { return N; }
        [[nodiscard]] constexpr size_type max_size() const noexcept { return N; }
        [[nodiscard]] constexpr bool empty() const noexcept { return N == 0; }

        // ============================== element access ==============================

        // operator[]
        [[nodiscard]] constexpr reference operator[](_In_range_(0, N - 1) size_type n) noexcept { return elems[n]; }
        [[nodiscard]] constexpr const_reference operator[](_In_range_(0, N - 1) size_type n) const noexcept { return elems[n]; }

        // at()
        [[nodiscard]] constexpr reference at(size_type n)
        {
            if (n >= N)
                throw "invalid array<T, N> subscript";
            return elems[n];
        }
        [[nodiscard]] constexpr const_reference at(size_type n) const
        {
            if (n >= N)
                throw "invalid array<T, N> subscript";
            return elems[n];
        }

        // front()
        [[nodiscard]] constexpr reference front() noexcept { return elems[0]; }
        [[nodiscard]] constexpr const_reference front() const noexcept { return elems[0]; }
        // back()
        [[nodiscard]] constexpr reference back() noexcept { return elems[N - 1]; }
        [[nodiscard]] constexpr const_reference back() const noexcept { return elems[N - 1]; }

        // data()
        [[nodiscard]] constexpr T* data() noexcept { return elems; }
        [[nodiscard]] constexpr const T* data() const noexcept { return elems; }

        // Elements
        T elems[N];
    };
}
```

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

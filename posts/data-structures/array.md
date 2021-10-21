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
        using pointer = value_type*;
        using const_pointer = const value_type*;
        // reference
        using reference = value_type&;
        using const_reference = const value_type&;

        // iterator
        using iterator = pointer;
        using const_iterator = const_pointer;
        // reverse_iterator
        using reverse_iterator = std::reverse_iterator<iterator>;
        using const_reverse_iterator = std::reverse_iterator<const_iterator>;

        // ========== No explicit construct/copy/destroy for aggregate type ==========

        constexpr void fill(const reference value)
        {
            std::fill_n(data(), N, value);
        }

        // C++17
        constexpr void swap(array& other) noexcept(std::is_nothrow_swappable_v<value_type>)
        {
            std::swap_ranges(begin(), end(), other.data());
        }

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
        [[nodiscard]] constexpr reference operator[](size_type n) noexcept { return elems[n]; }
        [[nodiscard]] constexpr const_reference operator[](size_type n) const noexcept { return elems[n]; }

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
        [[nodiscard]] constexpr pointer data() noexcept { return elems; }
        [[nodiscard]] constexpr const const_pointer data() const noexcept { return elems; }

        // Elements
        value_type elems[N];
    };
}
```

## softsec::allocator

```cpp
namespace softsec
{
    template <class T>
    class allocator
    {
    public:
        // type
        using value_type = T;
        using size_type = size_t;
        using difference_type = ptrdiff_t;

        using propagate_on_container_move_assignment = std::true_type;

        // allocator()
        constexpr allocator() noexcept = default;

        constexpr allocator(const allocator&) noexcept = default;

        template <class U>
        constexpr allocator(const allocator<U>&) noexcept {}

        // allocate()
        [[nodiscard]] constexpr T* allocate(const size_t n)
        {
            return static_cast<T*>(operator new(n * sizeof(T)));
        }

        // deallocate()
        constexpr void deallocate(T* const p, const size_t n) noexcept
        {
            operator delete(p);
        }
    };
}
```

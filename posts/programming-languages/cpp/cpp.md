---
layout: post
title: C++
date: 2021-10-30
---

## 5 Lexical conventions

### 5.5 Alternative tokens

```text
+----------+-------+
|  <% %>   |  { }  |
|  <: :>   |  [ ]  |
|  %:      |  #    |
|  %:%:    |  ##   |
+----------+-------+
|  and     |  &&   |
|  bitand  |  &    |
|  bitor   |  |    |
|  or      |  ||   |
|  not     |  !    |
|  xor     |  ^    |
|  compl   |  ~    |
+----------+-------+
|  and_eq  |  &=   |
|  or_eq   |  |=   |
|  not_eq  |  !=   |
|  xor_eq  |  ^=   |
+----------+-------+
```

### 5.7 Comments

```cpp
// Single-line Comments

/*
    Multi-line Comments
*/
```

### 5.13 Literals

```cpp
#include <string>

using namespace std::string_literals;

int main()
{
    // 5.13.2 Integer
    int  binary  = 0b10  or 0B10;
    int  octal   = 0123  or 01'000'000;
    int  decimal = 123   or 1'000'000;
    int  hex     = 0x123 or 0X123;

    unsigned int u  = 123u  or 123U;
    long         l  = 123l  or 123L;
    long long    ll = 123ll or 123LL;

    unsigned long      ul  = 123ul  or 123UL;
    unsigned long long ull = 123ull or 123ULL;

    // 5.13.3 Character
    char     c0 =   'A';          // ASCII
    wchar_t  c1 =  L'\101';       // wide-character
    char8_t  c2 = u8'\x41';       // UTF-8
    char16_t c3 =  u'\u0041';     // UTF-16
    char32_t c4 =  U'\U00000041'; // UTF-32

    // Multicharacter
    int c5 = 'abcd';

    //    +------------------------+
    //    |    Escape sequences    |
    //    +------------------------+
    //    | \n   | new-line        |
    //    | \t   | horizontal tab  |
    //    | \v   | vertical tab    |
    //    | \b   | backspace       |
    //    | \r   | carriage return |
    //    | \f   | form feed       |
    //    | \a   | alert           |
    //    +------+-----------------+
    //    | \\   | backslash       |
    //    | \?   | question mark   |
    //    | \'   | single quote    |
    //    | \"   | double quote    |
    //    +------+-----------------+
    //    | \377 | octal number    |
    //    | \xFF | hex number      |
    //    +------------------------+
    // 
    //     universal-character-name
    //    +------------------------+
    //    | \u4F60      \u597D     |
    //    | \U00004F60  \U0000597D |
    //    +------------------------+

    // 5.13.4 Floating-point
    double      d  = 123.0  or 123.;
    float       f  = 123.0f or 123.F;
    long double ld = 123.0l or 123.L;

    //     floating-point-suffix
    //    +----------------------+
    //    | none   | double      |
    //    | f or F | float       |
    //    | l or L | long double |
    //    +----------------------+

    // 5.13.5 String
    const char*     s0 =   "hello";
    const char8_t*  s1 = u8"hello";
    const wchar_t*  s2 =  L"hello";
    const char16_t* s3 =  u"hello";
    const char32_t* s4 =  U"hello";

    const char*     s5 =   R"("Hello \ world")";
    const char8_t*  s6 = u8R"("Hello \ world")";
    const wchar_t*  s7 =  LR"("Hello \ world")";
    const char16_t* s8 =  uR"("Hello \ world")";
    const char32_t* s9 =  UR"("Hello \ world")";

    std::string     S0 =   "hello"s;
    std::u8string   S1 = u8"hello"s;
    std::wstring    S2 =  L"hello"s;
    std::u16string  S3 =  u"hello"s;
    std::u32string  S4 =  U"hello"s;
                    
    std::string     S5 =   R"("Hello \ world")"s;
    std::u8string   S6 = u8R"("Hello \ world")"s;
    std::wstring    S7 =  LR"("Hello \ world")"s;
    std::u16string  S8 =  uR"("Hello \ world")"s;
    std::u32string  S9 =  UR"("Hello \ world")"s;

    // 5.13.6 Boolean
    bool b = true or false;

    // 5.13.7 Pointer
    void* p = nullptr;

    return 0;
}
```

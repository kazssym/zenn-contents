---
title: std::forward の使い方 (復習)
type: tech
topics:
  - cpp
published: true
---

# コード

```cpp
template<typename T>  // 引数の型
void f(T &&t)  // 引数は右辺値参照
{
    // 最後に他の関数に渡す時に std::forward<T> で囲う
    g(std::forward<T>(t));
}
```

# 解説

関数オブジェクトを関数に渡す時に `std::function` を引数にするのはあまり美しくないので、関数テンプレートと `std::forward` を使うという話。

`f` の引数にラムダ式を直接書いた場合 `T` が右辺値参照型になるので、 `g` には右辺値参照のままで渡される一方で、変数から渡すと左辺値参照で渡されるように `std::forward` が定義されているとのこと。

---
title: C++ 参照修飾子 (ref qualifier) の再発見
emoji: 📝
type: tech
topics:
  - cpp
published: true
---

C++ の参照修飾子の使用法についてのメモです。

# 問題

メンバーにアクセスするのに不要なコピーを避けるため、以下のように参照を返すことにします。

```cpp
class X
{
    std::vector<int> vec;
public:
    auto &Vec() const noexcept { return vec; }
};
```

この場合には以下の問題があります。

```cpp
void f()
{
    const auto &v = X().Vec();
    // ここで v が無効
}
```

# 参照修飾子

ここで参照修飾子が使えることに気付きました。以下のように書き換えます。

```cpp
class X
{
    std::vector<int> vec;
public:
    auto &Vec() const & noexcept { return vec; }
    auto Vec() const && { return vec; }  //
};

void f()
{
    const auto &v = X().Vec();
    // コピーを返すので v は有効
}
```

参照修飾子の有効な使い道にようやく気付いたというだけの話でした。

おそらくムーブで返すのがベストなのでしょうが説明のため簡略化しています。

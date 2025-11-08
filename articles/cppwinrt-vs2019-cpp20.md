---
title: C++/WinRT をそれでも Visual Studio 2019 で使う話
emoji: 📝
type: tech
topics:
  - cppwinrt
  - visualstudio
published: true
---

# 発端

Visual Studio 2019 で C++/WinRT を使おうと動作を確認して C++20 を有効にしたら、必要なヘッダーをインクルードするだけで ICE が発生することが判明してしまいました。

この場合に取れる手段は三つ。

  1. Visual Studio 2022 に移行する。
  2. C++20 を諦めて C++17 に留まる。
  3. 自力で解決する。

この記事では第三の選択肢を解説します。

## 分析と対処

ICE が発生するのは `winrt/base.h` にある以下のようなコードでした。

```cpp
catch (std::out_of_range const& e)
{
    return hresult_out_of_bounds(to_hstring(e.what())).to_abi();
}
```

C++20 に固有な処理ではないので、問題を切り分けるために処理を分けていくと ICE が解消したので、これは完全にコンパイラーの問題。以下のように書き換えると良いようです。

```cpp
catch (std::out_of_range const& e)
{
    auto hr = hresult_out_of_bounds(to_hstring(e.what()));
    return hr.to_abi();
}
```

書き換えが必要なのは、 `winrt/base.h` 中に三つ、 `module.g.cpp` 中に一つ。

アップストリームでの修正は見込めないので頑張って書き換えましょう😢。

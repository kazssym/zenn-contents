---
title: C++/WinRT をそれでも Visual Studio 2019 で使う話
emoji: 📝
type: tech
topics:
  - cppwinrt
  - visualstudio
published: false
---

# 発端

Visual Studio 2019 で C++/WinRT を使おうと動作を確認して C++20 を有効にしたら、必要なヘッダーをインクルードするだけで ICE が発生することが判明してしまいました。

この場合に取れる手段は三つ。

  1. Visual Studio 2022 に移行する。
  2. C++20 を諦めて C++17 に留まる。
  3. 自力で解決する。

この記事は第三の手段を解説します。
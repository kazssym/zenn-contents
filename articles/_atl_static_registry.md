---
title: 不要になったらしい _ATL_STATIC_REGISTRY (MSVC)
emoji: 📝
type: tech
topics:
  - cpp
  - visualstudio
published: false
---

# 公式ドキュメントに書いてある情報を基にして ATL DLL を使わないように設定しようとしたら、 _ATL_STATIC_REGISTRY マクロがもう使われていないことが判明した件

[このページ](https://learn.microsoft.com/en-us/cpp/atl/setting-up-a-static-link-to-the-registrar-code-cpp-only)を基に ATL のレジストラーをプロジェクトで設定しようとして、必要なマクロ (`_ATL_STATIC_REGISTRY`) がどのように使われるか一応確認しておこうと考えたのが発端でした。そのためにヘッダー中で使われているところを検索したら全く見つからないので調べてみたら、とんでもないことが発覚したという顛末です。

この件について AI に質問すると、このマクロが依然必要であると回答するので、何かおかしいとネットで調査してみることにしました。すると、 Dev Blogs 記事 “[ATL and MFC changes and fixes in Visual Studio 2013](https://devblogs.microsoft.com/cppblog/atl-and-mfc-changes-and-fixes-in-visual-studio-2013/)” に以下の記述を発見しました。

> One of the major changes we made was to eliminate the ATL DLL altogether.  All ATL code is now static, either in the header files or in the ATL static library.

Visual Studio 2013 の時点で ATL DLL は使われなくなっていたと😢。関連のマクロがどこにも見つからないのが当然という情報でした。

どういうわけか Visual Studio のドキュメントが古い情報を書いているから AI の回答も間違えていたわけです。

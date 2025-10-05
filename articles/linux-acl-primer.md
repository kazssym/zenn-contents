---
title: Linux ACL 入門 (パート 1)
emoji: 📝
type: tech
topics:
  - linux
published: true
---

Linux のファイルシステムでは、ファイルの所有者 (ユーザー) と所属グループによりアクセス権を設定するのはよく知られているとおりですが、 Linux にはユーザーとグループそれぞれ個別に設定する機能 (ACL) もあります。

# アクセス権の確認

アクセス権の確認には `getfacl` コマンドを使います。
ここでは例として、カレント ディレクトリのアクセス権を確認してみます。

```
$ getfacl .
# file: .
# owner: user1
# group: group1
user::rwx
group::r-x
other::r-x

```

ACL を何も設定していない場合は通常このように表示されます。

# アクセス権の設定

ユーザー user2 のアクセス権を設定してみます。
アクセス権の設定には `setfacl` コマンドを使用します。

```
$ setfacl -m u:user2:rwx .
$ getfacl .
# file: .
# owner: user1
# group: group1
user::rwx
user:user2:rwx
group::r-x
mask::rwx
other::r-x

```

ユーザー user2 にアクセス権 `rwx` が設定されました。
簡単ですね。

それではまた次回……に続くかどうかは定かでない。

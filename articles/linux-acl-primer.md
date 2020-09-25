# Linux ACL 入門

Linux のファイルシステムでは、ファイルの所有者 (ユーザー) と所属グループによりアクセス権を設定するのはよく知られているとおりですが、 Linux にはユーザーとグループそれぞれ個別に設定する機能 (ACL) もあります。

## アクセス権の確認

`getfacl` コマンドを使います。例として、カレント ディレクトリのアクセス権を確認してみます。

```
$ getfacl .
# file: .
# owner: user1
# group: group1
user::rwx
group::r-x
other::r-x

$
```

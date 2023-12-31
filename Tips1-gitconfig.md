# Windows環境でのgitconfigの例

## これは何？
ある日、windows11の環境でディレクトリごとに使用するGitHubのアカウントを切り替えたいと思った。
これはその時に作成したgitconfigの例とメモ。

## 例
まずは、次の二つのファイルをユーザーのホームディレクトリに作成すれば事足りる。

.gitconfig
```bash:.gitconfig
[user]
	name = username
	email = emailaddress
[includeIf "gitdir/i:C:/src/"]
   path = "C:/Users/user/.gitconfig_sub"
```

.gitconfig_sub
```bash:.gitconfig_sub
[user]
	name = sub_username
	email = sub_emailaddress
```

## 解説
Gitのユーザー情報が保持されている.gitconfigというファイルだが、「includeIf」を使えば指定のディレクトリごとに読み込む.gitconfigを切り替えることができる。
上記の例では、
基本的に`username`というGitHubアカウントを使用しているが、
Cドライブ直下のsrcというディレクトリ配下では、CドライブにあるUsers配下のuserフォルダ内にある.gitconfig_subというファイルを読み込むように設定し、
.gitconfig_subを読み込んでいる間は`sub_username`という名のGitHubアカウントに切り替わるようになっている。

## メモ
絶対パスでのgitdirの指定の仕方に癖があった。
`gitgir/i`としてケースインセンシティブにしておいた方がいいのと、windows環境の場合は`C:/`のようにドライブの指定が必要だった。
Linuxなどの環境では`$(prefix)`を最初につけて`$(prefix)/home/`のようにしないといけないらしい。

## 終わり
開発中でも今回のような細かいところで詰まることが多いから、もっと豆知識的なものを補完していきたい。






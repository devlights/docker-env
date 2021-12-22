# これは何？

Go言語の環境です。ターミナル上でソースコードを記載して開発することを想定しています。

# ビルド

Makefileを用意しています。

```sh
$ make build
```

# 実行

Makefileを用意しています。

カレントディレクトリをバインドマウントするようにしているので

任意のディレクトリにて

```sh
$ make -f /path/to/this/Makefile run
```

とすれば、そのディレクトリをマウントした状態でコンテナ起動します。

# エイリアス設定

以下のように設定しておくと便利かもしれません。

```sh
alias go-env="make -f /path/to/this/Makefile run"
```

Debian系であれば、 .bashrc の中で ```.bash_aliases``` を読み込むようになっているので

```${HOME}/.bash_aliases``` ファイルを作り、上記の内容を記載しておくとログイン時に自動的に読み込まれます。


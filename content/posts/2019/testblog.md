---
title: ubuntu で linuxbrew を使って opencv をインストールしてみた
date: 2019-07-13
categories: [writing]
tags: [typography, elements]
language: en
slug: numbered-list-with-code
---

## はじめに
ubuntu で opencv をインストールしたときのメモです。
apt install でインストールするのは大変だと書いてあったので
今回は linuxbrew を利用する方法を試みました。

## 下記を主に参考にさせていただきました
```
https://qiita.com/thermes/items/926b478ff6e3758ecfea
https://github.com/Linuxbrew/brew
https://docs.brew.sh/Homebrew-on-Linux
```

## 必要と思われるパッケージをインストールする
### 注意
ここでインストールしたパッケージがすべて必要かどうかが検証できていません。
検証できましたら更新させていただきます。
```
$ sudo apt install build-essential curl git m4 ruby texinfo libbz2-dev libcurl4-openssl-dev libexpat-dev libncurses-dev zlib1g-dev gettext
```

## linuxbrew をインストールする
```
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"
```

## パスを通す
```
$ test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
$ test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
$ test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
$ echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile

```

## 確認する
### エラーでなければOKか？
```
$ brew doctor
```

### hello をインストールしてみる
```
$ brew install hello
```

### インストールできない場合は下記を試してみる
```
$ sudo mkdir -p /home/linuxbrew/.linuxbrew/var/homebrew/linked
$ sudo chown -R $(whoami) /home/linuxbrew/.linuxbrew/var/homebrew/linked
```

## その他
### パスの設定をするとあるが必要なのだろうか？わたしの環境では実行していません。検証できましたら更新させていただきます。
```
$ export PATH="$HOME/.linuxbrew/bin:$PATH"
$ export MANPATH="$HOME/.linuxbrew/share/man:$MANPATH"
$ export INFOPATH="$HOME/.linuxbrew/share/info:$INFOPATH"
$ export LD_LIBRARY_PATH="$HOME/.linuxbrew/lib:$LD_LIBRARY_PATH"
```

## linuxbrew で opencv をインストールする
```
$ brew install opencv
```

## さいごに
いかがでしょう？ linuxbrew さえインストールできてしまえば、opencv のインストールは簡単にできました。まだまだ粗いですが、今後はもっと改善していきたいと思います。最後まで読んでいただいてありがとうございました。
---
layout: post
title: "シェルスクリプトメモ その１〜"
date: 2014-08-26 01:50:13 +0900
comments: true
categories: 
---

シェルスクリプトメモ その１
====

仕事とかでシェルスクリプト書いててよく利用する事を備忘録的にまとめてみようかとおもいます。

コマンドの内容を変数に格納
----
```sh
# 試しにディレクトリ内のファイルの数を数えてみる
$ ls -1 | wc -l
13
#
$ filecount1=$(ls -1 | wc -l)  
$ filecount2=`(ls -1 | wc -l)`
$ echo $filecount1
13
$ echo $filecount2
13
```
変数に格納したいコマンドを```$( )```又は``` ` ` ```で囲んで変数に渡してやると実行結果が変数に格納される。

<!--more-->

コマンドの内容を配列に格納
----
`ls`や`find`の内容を個別の変数、配列として格納したい場合
```sh
$ ls
file1 file2 file3
# 普通に変数に格納する
$ files=$(ls)
$ echo $files
file1 file2 file3
# 1つの文字列として格納されている
# 配列に格納
$ files=($(ls))
$ echo files
file1
# 配列の場所を指定して参照する場合はxに場所を入力 ${files[x]}
$ echo ${files[2]}
file3
# すべて参照(forでループ)
$ for file in ${files[*]} ;do
>   echo $file
> done
file1
file2
file3

```

変数の中の文字列をマッチしたところを除外して取り出し
----
変数を展開するときにパターンマッチさせる
```sh
# ファイルのパスを格納
$ filepath=$(ls /tmp/test/file1)
$ echo ${filepath}
/tmp/test/file1
# 前方からマッチした所を除外
# 最短一致
$ echo ${filepath#*/}
tmp/test/file1
# 最長一致
$ echo ${filepath##*/}
file1

# 後方からマッチした所を除外
# 最短一致（後方から)
$ echo ${filepath%/*}
/tmp/test
# 最長一致（後方から）※今回は出力なし
$ echo ${filepath%%/*}

```

とりあえず1回めの記事なのでこれくらいでおわります。

なお、内容はちゃんと調べて記載してるわけではないので僕の理解等に間違い等ありましたらご指摘いただけると幸いです。

---
title: Emacs Lisp メモ
date: 2021-03-13
tags: ['Emacs', 'Lisp']
---

# Emacs Lisp メモ
Emacs Lispでの開発用メモ

## ループ
- while
  - 継続条件を満たす限り処理を継続
  - 仕様
	- 第1引数: 終了条件

## 文字列
- length
  - 文字列の長さを取得
  - 仕様
	- 第1引数: 対象の文字列
	- 戻り値: 対象の文字列の長さ
  - 例: 文字列の長さを受け取って変数に代入
    - ```(setq len (length "abc"))```

## 入力
- read-string
  - ユーザーからの入力を待ち受ける
  - 仕様
	- 第1引数: プロンプトとして表示する文字列
	- 戻り値: 入力された値
  - 例: 文字列を受けとって変数に代入
	- ```(setq user-input (read-string "Input >> "))```

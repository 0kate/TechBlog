---
title: メモリのセグメント機構について
date: 2021-03-20
tags: ['Intel', 'Linux']
---

# メモリのセグメント機構について
メモリのセグメント機構について学習したため、そのまとめとしてここに整理する。

---

## セグメントセレクタ
- セグメントを一意に識別するための16bitのフィールド
- 各フィールドの役割
  - RPL (0 ~ 1bit目)
	- Requestor Priviledge Level
	- セグメントセレクタをCSに読み込んださいのCPUの特権レベルを指す
  - TI (2bit目)
	- Table Indicator
	- セグメントディスクリプタがGDTにあるか、またはLDTにあるかを示す
	- GDT = 0, LDT = 1
  - インデックス (3 ~ 15bit目)
	- GDTもしくはLDTにある、セグメントディスクリプタのアドレス

## セグメントディスクリプタ
- 8byte長、対応するセグメントの特性を表す
- GDTもしくはLDTに保存される
- Linuxでの主なセグメントディスクリプタの用途
  - コードセグメントディスクリプタ
  - データセグメントディスクリプタ
- 各フィールドの役割
  - リミット (0 ~ 15bit)
	- セグメントの終端メモリアドレス = セグメント長
  - ベース (16 ~ 39bit)
	- セグメント先頭のリニアアドレス
  - タイプ (40 ~ 43bit)
	- セグメントの種類とアクセス権
  - S (44bit)
	- システムフラグ。0ならばLDTなどの重要なデータ、1ならば通常のコードセグメント・データセグメントであることを表す
  - DPL (45 ~ 46bit)
	- Descriptor Priviledge Level
	- セグメントへのアクセスを制限するために使用 (該当セグメントにアクセスするために必要な最低限のCPU権限を表す)
  - 1 (47bit)
  - AVL (52bit)
    - オペレーティングシステム用だがLinuxでは使用していない
  - 0 (53bit)

## GDT / LDT
- セグメントディスクリプタの一覧を保存するテーブル
- GDTは通常1つだけ、各プロセスごとにLDTを持つことも可能
- GDTのアドレスとサイズはCPUのgdtrレジスタに保存される
- GDT
  - Global Descriptor Table
- LDT
  - Local Descriptor Table
  
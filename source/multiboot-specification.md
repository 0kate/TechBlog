---
title: 仮想ファイルシステム(VFS)について
date: 2021-03-28
tags: ['OS', 'x86']
---

# Multiboot specificationについて
Multiboot specificationについて学習したため、そのまとめとしてここに整理する。

## Multiboot specification
- ブートローダからカーネルをロードする方法について規定した仕様
- この仕様に従って構成されているブートローダ・カーネルであれば、どのような組み合わせでも起動可能
- OS開発者は、OSイメージの先頭部分(Multiboot Header)をMultiboot specificationに準拠した形で構成し、ブートローダ開発者はMultiboot specificationに対応したOSイメージを読み込むように実装する必要がある

## 背景
- 従来、ブートローダからカーネルをロードする方法については標準化されておらず、それぞれのOSが開発者によって独自に開発されたブートローダを持っていた。
- このため、OSをインストールするたびにブートローダも再インストールする必要があり、複数のOSが共存することを困難にしていた。
- そこで、このMultiboot specificationが発案され、ブートローダ開発者・OS開発者はこの仕様に準拠することでこのような問題を解決することができた

## 技術的な仕様
- Multiboot header構成
  - magic (0 ~ 3byte)
	- ブートローダから、OSイメージがMultiboot specificationに対応しているかを判断するためのフィールド。
  - flags (4 ~ 7byte)
    - OSイメージが必要とする機能を、ブートローダ側で初期化するために指定するフィールド。
  - checksum (8 ~ 11byte)
    - magicとflagsの値を合計した値
  - header_addr (12 ~ 15byte)
    - flagsの16bitがセットされているときのみ有効
  - load_addr (16 ~ 20byte)
      - flagsの16bit目がセットされているときのみ有効
  - load_end_addr (21 ~ 23byte)
    - flagsの16bit目がセットされているときのみ有効
  - bss_end_addr (24 ~ 27byte)
    - flagsの16bit目がセットされているときのみ有効
  - entry_addr (28 ~ 31byte)
    - flagsの16bit目がセットされているときのみ有効
  - mode_type (32 ~ 35byte)
    - flagsの2bit目がセットされているときのみ有効
  - width (36 ~ 39byte)
    - flagsの2bit目がセットされているときのみ有効
  - height (40 ~ 43byte)
    - flagsの2bit目がセットされているときのみ有効
  - depth (44 ~ 47byte)
    - flagsの2bit目がセットされているときのみ有効

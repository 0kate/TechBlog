---
title: OCI Runtime Specification
date: 2021-11-27
tags: ['container', 'OCI']

---

# OCI Runtime Specification

OCI Runtime Specificationについて学習したため、そのまとめとしてここに整理する。

## OCI Runtime Specification

- OCI(Open Container Initiative)によって策定された、コンテナランタイムの実装に関する標準仕様

---

## Standard Container

OCI Runtime Specificationでは、以下の原則からなる**Standard Container**という概念が定義されている。

1. **Standard Operations**・・・標準的なコンテナに対する操作が定義されていること
2. **Content-agnostic**・・・コンテナの内容に依存せず、どのコンテナでも同じように標準操作を行うことができること
3. **Infrastracture-agnostic**・・・ラップトップでもクラウドでも、OCIによってサポートされたインフラであればどこでも実行できること
4. **Designed for automation**・・・コンテナの内容に依存しない・インフラに依存しない・標準操作が定義されている等、自動化のために適した設計がされていること
5. **Industrial-grade delivery**・・・小規模から大規模なものまで、様々なエンタープライズ分野で通用するデリバリーパイプラインが構築できること

---

## Filesystem Bundle

OCI Runtime Specificationでは、コンテナに同梱されるべきデータについて以下のように定めている。

1. **config.json**・・・コンテナの構成情報が記載されている。config.jsonという名前でコンテナ内に含まれていなければならない
2. **コンテナのrootファイルシステム**・・・config.json内に`root.path`として記載されており、コンテナ内のrootファイルシステムとしてバンドルされる

---

## Runtime and Lifecycle

OCI Runtime Specificationでは、コンテナが保持する必須プロパティ・コンテナのライフサイクルについて定義されている。

### State

コンテナが保持する必須プロパティについては、以下のように定められている。

- **ociVersion** (文字列, 必須)・・・OCI Runtime Specificationのバージョン
- **id** (文字列, 必須)・・・ホスト上でコンテナを識別するための一意のID
- **status** (文字列, 必須)・・・コンテナの状態
  - **creating**・・・コンテナが作成中である状態
  - **created**・・・コンテナが作成されているが、ユーザーによって指定されたプログラムが実行されていない状態
  - **running**・・・コンテナ内でユーザーによって指定されたプログラムが実行中である状態
  - **stopped**・・・コンテナ内のプロセスが終了した状態
- **pid** (数値, Linux上で稼働しており、statusがcreated, runningの場合のみ必須)・・・コンテナ内のプロセスのID
- **bundle** (文字列, 必須)・・・コンテナのrootファイルシステムの絶対パス
- **annotations** (マップ, 任意)・・・コンテナに関する注釈


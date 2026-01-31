# Research: TCP/IP Learning Kit

**Date**: 2026-01-31
**Branch**: `001-tcpip-learning-kit`

## 技術選定

### 1. プログラミング言語: C++17

**Decision**: C++17を採用

**Rationale**:
- POSIXソケットAPIを直接使用でき、TCP/IPの低レベルな動作を理解しやすい
- `std::string`, `std::thread` などモダンな機能で可読性を確保
- 広くサポートされており、ほとんどのLinux環境で利用可能

**Alternatives considered**:
- C: より低レベルだが、文字列操作が煩雑で教育目的には不向き
- Python: 抽象化されすぎており、ソケットAPIの本質が見えにくい
- Rust: 学習曲線が急で、TCP/IP以外の知識が必要

### 2. ビルドシステム: Makefile

**Decision**: シンプルなMakefileを採用

**Rationale**:
- 各レッスンで独立したMakefile（依存関係が明確）
- `make` コマンドだけでビルド可能（追加ツール不要）
- ビルドプロセス自体も学習対象になる

**Alternatives considered**:
- CMake: 小規模プロジェクトにはオーバーヘッド
- Meson: 普及度が低く、学習者の環境で利用できない可能性

### 3. Wireshark解析対象

**Decision**: localhostインターフェース（lo）でのキャプチャ

**Rationale**:
- 外部ネットワーク不要で安全
- ノイズが少なく、学習対象のパケットが見つけやすい
- root権限なしでもtcpdumpで代替可能

**Alternatives considered**:
- 実ネットワーク: ノイズが多く、フィルタリングが複雑
- Docker内通信: 追加セットアップが必要

## ソケットAPI使用関数

### Lesson 01で使用
| 関数 | 役割 |
|------|------|
| `socket()` | ソケット作成 |
| `bind()` | アドレス・ポート紐付け |
| `listen()` | 接続待ち開始 |
| `accept()` | 接続受け入れ |
| `connect()` | サーバーへ接続 |
| `recv()` | データ受信 |
| `send()` | データ送信 |
| `close()` | ソケット閉じる |

### Lesson 02で追加
| 関数 | 役割 |
|------|------|
| `select()` | 複数FDの監視 |
| `FD_SET()` | FDセットへ追加 |
| `FD_ISSET()` | FDの状態確認 |

## エラーハンドリング方針

教育目的のため、すべてのエラーに対して：
1. 日本語でわかりやすいエラーメッセージを表示
2. エラーの原因を説明
3. 対処法を提示

例:
```cpp
if (bind(server_fd, ...) < 0) {
    std::cerr << "エラー: ポートへのバインドに失敗しました" << std::endl;
    std::cerr << "原因: ポート " << PORT << " は既に使用中の可能性があります" << std::endl;
    std::cerr << "対処法: 別のポート番号を試すか、既存のプロセスを終了してください" << std::endl;
    exit(EXIT_FAILURE);
}
```

## デフォルトポート番号

**Decision**: 8080を使用

**Rationale**:
- 1024以上でroot権限不要
- 一般的に使われるテスト用ポート
- 覚えやすい

## 未解決事項

なし - すべての技術的な疑問が解決済み

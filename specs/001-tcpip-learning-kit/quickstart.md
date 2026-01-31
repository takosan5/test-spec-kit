# クイックスタートガイド: TCP/IP Learning Kit

## 前提条件

- Linux環境（Ubuntu 20.04以上推奨）
- g++（C++17対応）
- make
- Wireshark（Lesson 04用）

## 環境確認

```bash
# コンパイラ確認
g++ --version

# make確認
make --version

# Wireshark確認（オプション）
wireshark --version
```

## インストール

```bash
# リポジトリをクローン
git clone <repository-url>
cd tcp-ip-learning-kit
```

## レッスンの進め方

### Lesson 01: Echo Server（初めてのTCP接続）

```bash
cd lessons/01-echo-server

# ビルド
make

# ターミナル1: サーバー起動
./server

# ターミナル2: クライアント起動
./client
```

**学習ポイント**: socket(), bind(), listen(), accept(), send(), recv()

### Lesson 02: Chat（双方向通信）

```bash
cd lessons/02-chat
make
./server    # ターミナル1
./client    # ターミナル2
```

**学習ポイント**: select()による非同期I/O

### Lesson 03: Wireshark Analysis（パケット解析）

```bash
cd lessons/03-wireshark-analysis

# 1. Wiresharkを起動してloインターフェースをキャプチャ開始
# 2. フィルタを設定: tcp.port == 8080

# 3. サーバー起動
./server

# 4. クライアントで接続・通信・切断
./client

# 5. Wiresharkで以下を確認:
#    - 3ウェイハンドシェイク（SYN → SYN-ACK → ACK）
#    - データパケット（PSH-ACK）
#    - 4ウェイハンドシェイク（FIN-ACK）
```

**学習ポイント**: TCPの接続確立・データ転送・切断プロセス

## トラブルシューティング

### "Address already in use" エラー

```bash
# 使用中のポートを確認
lsof -i :8080

# プロセスを終了
kill <PID>
```

### Wiresharkでlocalhostがキャプチャできない

```bash
# loインターフェースを選択しているか確認
# または tcpdump を使用
sudo tcpdump -i lo port 8080 -X
```

## 次のステップ

各レッスンのREADME.mdに詳細な解説と演習問題があります。

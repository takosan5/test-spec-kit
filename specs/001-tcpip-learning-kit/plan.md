# Implementation Plan: TCP/IP Learning Kit

**Branch**: `001-tcpip-learning-kit` | **Date**: 2026-01-31 | **Spec**: [spec.md](./spec.md)
**Input**: Feature specification from `/specs/001-tcpip-learning-kit/spec.md`

## Summary

TCP/IP通信を実践的に学ぶための教育プロジェクト。C++とPOSIXソケットAPIを使用し、4つの段階的なレッスンで構成。各レッスンは独立して実行可能で、Wiresharkによるパケット解析を含む。

## Technical Context

**Language/Version**: C++17（モダンな機能を使いつつ、広くサポートされている）
**Primary Dependencies**: なし（POSIX標準ライブラリのみ）
**Storage**: N/A
**Testing**: 手動テスト + シェルスクリプトによる自動検証
**Target Platform**: Linux（POSIX準拠）
**Project Type**: 教育用マルチレッスンプロジェクト
**Performance Goals**: N/A（教育目的のため性能より可読性を優先）
**Constraints**: 外部ライブラリ禁止、各レッスン100行以内推奨
**Scale/Scope**: 3レッスン、各レッスン2-3ファイル

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| 原則 | 状態 | 確認内容 |
|------|------|----------|
| I. 学習優先 | ✅ PASS | コードは可読性重視、詳細なコメント付き |
| II. 段階的複雑性 | ✅ PASS | Lesson 01→04で段階的に難易度上昇 |
| III. 実践体験 | ✅ PASS | 各レッスンは即座にコンパイル・実行可能 |
| IV. 明確なドキュメント | ✅ PASS | 各レッスンにREADME、期待出力、Wiresharkガイド |
| V. シンプルさ | ✅ PASS | 標準ライブラリのみ、1ファイル1概念 |

## Project Structure

### Documentation (this feature)

```text
specs/001-tcpip-learning-kit/
├── spec.md              # 機能仕様書
├── plan.md              # この実装計画
├── research.md          # 技術リサーチ結果
├── quickstart.md        # クイックスタートガイド
├── checklists/          # 品質チェックリスト
└── tasks.md             # タスクリスト（/speckit.tasks で生成）
```

### Source Code (repository root)

```text
lessons/
├── 01-echo-server/
│   ├── README.md           # レッスン説明、学習目標、実行方法
│   ├── server.cpp          # エコーサーバー実装
│   ├── client.cpp          # クライアント実装
│   ├── Makefile            # ビルド設定
│   └── expected_output.txt # 期待される出力例
│
├── 02-chat/
│   ├── README.md
│   ├── server.cpp          # 双方向チャットサーバー
│   ├── client.cpp          # 双方向チャットクライアント
│   ├── Makefile
│   └── expected_output.txt
│
├── 03-wireshark-analysis/
│   ├── README.md           # Wireshark解析ガイド
│   ├── server.cpp          # シンプルなサーバー（解析用）
│   ├── client.cpp          # シンプルなクライアント（解析用）
│   ├── Makefile
│   ├── wireshark_guide.md  # 詳細なWireshark操作ガイド
│   └── capture_filters.txt # フィルタ例集
│
docs/
├── README.md               # プロジェクト概要、前提条件
├── SETUP.md                # 環境セットアップガイド
└── TROUBLESHOOTING.md      # よくある問題と解決策
```

**Structure Decision**: 教育プロジェクトのため、レッスン番号付きディレクトリ構造を採用。各レッスンは独立して完結し、学習者は順番に進めることも、興味のあるレッスンだけ試すことも可能。

## Implementation Approach

### Lesson 01: Echo Server（基礎）
- `socket()`, `bind()`, `listen()`, `accept()`, `recv()`, `send()`, `close()`
- 1クライアントのみ対応（シンプルさ優先）
- 接続→メッセージ送受信→切断の基本フロー

### Lesson 02: Chat（双方向通信）
- `select()` または `poll()` による非同期I/O
- サーバー・クライアント両方から入力可能
- メッセージにタイムスタンプ付与

### Lesson 03: Wireshark Analysis（パケット解析）
- Lesson 01のコードを簡略化して使用
- 3ウェイハンドシェイク、データ転送、4ウェイハンドシェイクの解析
- loインターフェースでのキャプチャ方法

## Complexity Tracking

> 違反なし - すべてのconstitution原則を満たしています

# Tasks: TCP/IP Learning Kit

**Input**: Design documents from `/specs/001-tcpip-learning-kit/`
**Prerequisites**: plan.md ✅, spec.md ✅, research.md ✅, quickstart.md ✅

**Organization**: Tasks are grouped by user story (lesson) to enable independent implementation and testing.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup (共通インフラストラクチャ)

**Purpose**: プロジェクト初期化と基本構造の作成

- [ ] T001 Create project directory structure per plan.md (`lessons/`, `docs/`)
- [ ] T002 [P] Create docs/README.md with project overview and prerequisites
- [ ] T003 [P] Create docs/SETUP.md with environment setup instructions
- [ ] T004 [P] Create docs/TROUBLESHOOTING.md with common issues and solutions

**Checkpoint**: ドキュメント基盤が完成 - レッスン実装を開始できる

---

## Phase 2: User Story 1 - 初めてのTCP接続体験 (Priority: P1) 🎯 MVP

**Goal**: プログラミング初心者がエコーサーバーを通じてTCP接続の基本を体験

**Independent Test**: サーバーを起動し、クライアントから「Hello」を送信して「Hello」が返ってくることを確認

### Implementation for User Story 1

- [ ] T005 [US1] Create lessons/01-echo-server/README.md with lesson objectives and instructions
- [ ] T006 [US1] Create lessons/01-echo-server/Makefile for building server and client
- [ ] T007 [US1] Implement lessons/01-echo-server/server.cpp with socket(), bind(), listen(), accept(), recv(), send(), close()
- [ ] T008 [US1] Implement lessons/01-echo-server/client.cpp with socket(), connect(), send(), recv(), close()
- [ ] T009 [US1] Create lessons/01-echo-server/expected_output.txt with sample session output
- [ ] T010 [US1] Add Japanese error messages with cause and solution in server.cpp and client.cpp
- [ ] T011 [US1] Add detailed comments explaining each socket API call in server.cpp and client.cpp

**Checkpoint**: Lesson 01完成 - エコーサーバーが独立して動作・テスト可能

---

## Phase 3: User Story 2 - 双方向メッセージングの理解 (Priority: P2)

**Goal**: サーバーとクライアント間で双方向にメッセージをやり取りできるチャットを体験

**Independent Test**: 2つのターミナルでサーバーとクライアントを起動し、双方からメッセージを送り合えることを確認

### Implementation for User Story 2

- [ ] T012 [US2] Create lessons/02-chat/README.md with lesson objectives and select() explanation
- [ ] T013 [US2] Create lessons/02-chat/Makefile for building server and client
- [ ] T014 [US2] Implement lessons/02-chat/server.cpp with select() for bidirectional I/O
- [ ] T015 [US2] Implement lessons/02-chat/client.cpp with select() for stdin and socket monitoring
- [ ] T016 [US2] Create lessons/02-chat/expected_output.txt with sample bidirectional chat session
- [ ] T017 [US2] Add Japanese error messages with cause and solution in server.cpp and client.cpp
- [ ] T018 [US2] Add detailed comments explaining select(), FD_SET(), FD_ISSET() in both files

**Checkpoint**: Lesson 02完成 - 双方向チャットが独立して動作・テスト可能

---

## Phase 4: User Story 3 - Wiresharkによるパケット解析体験 (Priority: P3)

**Goal**: Wiresharkを使ってTCP/IP通信の内部（3ウェイハンドシェイク、データパケット、4ウェイハンドシェイク）を視覚的に理解

**Independent Test**: サーバーとクライアント間の通信をWiresharkでキャプチャし、3ウェイハンドシェイク（SYN → SYN-ACK → ACK）を確認

### Implementation for User Story 3

- [ ] T019 [US3] Create lessons/03-wireshark-analysis/README.md with Wireshark analysis objectives
- [ ] T020 [US3] Create lessons/03-wireshark-analysis/Makefile for building server and client
- [ ] T021 [P] [US3] Implement lessons/03-wireshark-analysis/server.cpp (simplified for packet analysis)
- [ ] T022 [P] [US3] Implement lessons/03-wireshark-analysis/client.cpp (simplified for packet analysis)
- [ ] T023 [US3] Create lessons/03-wireshark-analysis/wireshark_guide.md with step-by-step Wireshark instructions
- [ ] T024 [US3] Create lessons/03-wireshark-analysis/capture_filters.txt with filter examples (tcp.port == 8080)
- [ ] T025 [US3] Add comments in server.cpp and client.cpp explaining what to observe in Wireshark

**Checkpoint**: Lesson 03完成 - Wireshark解析ガイドが独立して使用可能

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: 全レッスンに影響する改善と最終確認

- [ ] T026 Update docs/README.md with links to all lessons
- [ ] T027 Update docs/TROUBLESHOOTING.md with issues found during testing
- [ ] T028 Verify all Makefiles work correctly with `make clean && make`
- [ ] T029 Run quickstart.md validation (execute all lessons end-to-end)
- [ ] T030 Final code review for consistent Japanese error messages and comments

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: 依存なし - すぐに開始可能
- **User Story 1 (Phase 2)**: Setup完了後に開始可能
- **User Story 2 (Phase 3)**: Setup完了後に開始可能（US1と並行可能だが、学習順序としては後）
- **User Story 3 (Phase 4)**: Setup完了後に開始可能（US1/US2と並行可能だが、学習順序としては後）
- **Polish (Phase 5)**: 全User Story完了後

### User Story Dependencies

- **User Story 1 (P1)**: 他のストーリーへの依存なし - 独立してテスト可能
- **User Story 2 (P2)**: US1の知識を前提とするが、コードの依存なし - 独立してテスト可能
- **User Story 3 (P3)**: US1のコードを簡略化して使用するが、独立してテスト可能

### Parallel Opportunities

**Phase 1 (Setup)**:
```bash
# T002, T003, T004 は並行実行可能（異なるファイル）
Task: "Create docs/README.md"
Task: "Create docs/SETUP.md"
Task: "Create docs/TROUBLESHOOTING.md"
```

**Phase 4 (US3)**:
```bash
# T021, T022 は並行実行可能（異なるファイル）
Task: "Implement lessons/03-wireshark-analysis/server.cpp"
Task: "Implement lessons/03-wireshark-analysis/client.cpp"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Phase 1: Setup完了
2. Phase 2: User Story 1完了
3. **検証**: エコーサーバーが動作することを確認
4. 最小限の学習キットとしてデプロイ/共有可能

### Incremental Delivery

1. Setup完了 → 基盤準備完了
2. User Story 1完了 → テスト → MVP! (基本的なTCP接続)
3. User Story 2完了 → テスト → 双方向通信追加
4. User Story 3完了 → テスト → Wireshark解析追加
5. Polish完了 → 完成版リリース

---

## Notes

- 各レッスンは100行以内推奨（可読性優先）
- デフォルトポート: 8080
- エラーメッセージは日本語で、原因と対処法を含める
- ソースコードには各行の役割を説明するコメントを含める
- 外部ライブラリは使用しない（POSIX標準ライブラリのみ）

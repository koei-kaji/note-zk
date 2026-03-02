---
title: "LiveKit Agent Framework 学習ロードマップ"
date: "2026-02-28"
tags:
  - livekit
  - voice-agents
  - ai
draft: false
---

# LiveKit Agent Framework 学習ロードマップ

目標: LiveKitのことなら俺に聞いてくれ状態のスペシャリストになる。転職も視野に入れたガチ学習。
環境前提: ローカルPython → LiveKit Cloud（Langfuse observability）

ドキュメント参照元: [[SourceNotes/LiveKit_Agents_Documentation.md|LiveKit Agents Documentation]]

---

## 設計思想

概要 → 詳細のブレイクダウン形式。各Phaseで「大きな絵」を掴んでから細部へ。

```
Phase 0: 基礎概念      → LiveKitとは何か
Phase 1: 概念モデル    → Room/Participant/Track/Agent
Phase 2: 全体像        → Agentsフレームワークの俯瞰
Phase 3: インフラ層    → Worker/Job/Dispatchの仕組み
Phase 4: 実装層        → Session/Logic/Tools/Nodesのコア
Phase 5: モデル層      → STT/LLM/TTS/Realtimeの選択と設定
Phase 6: 本番運用      → Deploy/Observability/Langfuse
Phase 7: フロント層    → RoomIO/カメラ/画面共有/ByteStreams（実装時に参照）
```

---

## 凡例

- ⬜ 未着手
- 🔄 進行中
- ✅ 完了

---

## Phase 0: LiveKit基礎概念（概要を掴む）

| ステータス | ドキュメント | URL | ノート |
|---|---|---|---|
| ✅ | LiveKit Basics Overview | https://docs.livekit.io/intro/basics/ | [[LiteratureNotes/lit-202602281412-ynh7.md\|LiveKit Basics Overview]] |

---

## Phase 1: 概念モデル（コアの構成要素）

| ステータス | ドキュメント | URL | ノート |
|---|---|---|---|
| ✅ | Rooms, Participants, and Tracks | https://docs.livekit.io/intro/basics/rooms-participants-tracks/ | [[LiteratureNotes/lit-202602281704-hf2o.md\|Rooms, Participants, and Tracks]] |

---

## Phase 2: Agentsフレームワーク全体像（俯瞰）

| ステータス | ドキュメント | URL | ノート |
|---|---|---|---|
| ✅ | Agents Framework Introduction | https://docs.livekit.io/agents/ | [[LiteratureNotes/lit-202602282303-pgqv.md\|Agents Framework Introduction]] |
| ✅ | Voice AI Quickstart | https://docs.livekit.io/agents/start/voice-ai-quickstart/ | [[LiteratureNotes/lit-202603011301-l1zu.md\|Voice AI Quickstart]] |
| 🔄 | Multimodality Overview | https://docs.livekit.io/agents/multimodality/ | - |
| ✅ | Text and Transcriptions | https://docs.livekit.io/agents/multimodality/text/ | [[LiteratureNotes/lit-202603011637-jxho.md\|Text and Transcriptions]] |
| ✅ | Agent Speech and Audio | https://docs.livekit.io/agents/multimodality/audio/ | [[LiteratureNotes/lit-202603012120-f8sk.md\|Agent Speech and Audio]] |
| ⬜ | Vision | https://docs.livekit.io/agents/multimodality/vision/ | - |

---

## Phase 3: Agent Server（インフラ層）

| ステータス | ドキュメント | URL | ノート |
|---|---|---|---|
| ⬜ | Server Lifecycle | https://docs.livekit.io/agents/server/lifecycle/ | - |
| ⬜ | Job Lifecycle | https://docs.livekit.io/agents/server/job/ | - |
| ⬜ | Agent Dispatch | https://docs.livekit.io/agents/server/agent-dispatch/ | - |
| ⬜ | Server Startup Modes | https://docs.livekit.io/agents/server/startup-modes/ | - |

---

## Phase 4: Logic & Structure（コア実装層）

| ステータス | ドキュメント | URL | ノート |
|---|---|---|---|
| ⬜ | Logic Overview | https://docs.livekit.io/agents/logic/ | - |
| ⬜ | Agent Session | https://docs.livekit.io/agents/logic/sessions/ | - |
| ⬜ | Workflows | https://docs.livekit.io/agents/logic/workflows/ | - |
| ⬜ | Agents & Handoffs | https://docs.livekit.io/agents/logic/agents-handoffs/ | - |
| ⬜ | Tasks & Task Groups（Python only） | https://docs.livekit.io/agents/logic/tasks/ | - |
| ⬜ | Tool Definition & Use | https://docs.livekit.io/agents/logic/tools/ | - |
| ⬜ | Turn Detection & Interruptions | https://docs.livekit.io/agents/logic/turns/ | - |
| ⬜ | Pipeline Nodes & Hooks | https://docs.livekit.io/agents/logic/nodes/ | - |
| ⬜ | External Data & RAG | https://docs.livekit.io/agents/logic/external-data/ | - |

---

## Phase 5: Models（モデル選択・設定）

| ステータス | ドキュメント | URL | ノート |
|---|---|---|---|
| ⬜ | Models Overview | https://docs.livekit.io/agents/models/ | - |
| ⬜ | STT Models | https://docs.livekit.io/agents/models/stt/ | - |
| ⬜ | LLM Models | https://docs.livekit.io/agents/models/llm/ | - |
| ⬜ | TTS Models | https://docs.livekit.io/agents/models/tts/ | - |
| ⬜ | Realtime Models | https://docs.livekit.io/agents/models/realtime/ | - |

---

## Phase 6: Deploy & Observe（本番運用）

| ステータス | ドキュメント | URL | ノート |
|---|---|---|---|
| ⬜ | Agent Deployment Overview | https://docs.livekit.io/deploy/agents/ | - |
| ⬜ | Observability Overview | https://docs.livekit.io/deploy/observability/ | - |
| ⬜ | Agent Insights（LiveKit Cloud） | https://docs.livekit.io/deploy/observability/insights/ | - |
| ⬜ | Data Hooks & OpenTelemetry（Langfuse） | https://docs.livekit.io/deploy/observability/data/ | - |

---

## Phase 7: フロントエンド実装（Transport 層）

エージェント実装後、実際にフロントと繋ぐ際に必要な知識。

| ステータス | ドキュメント | URL | ノート |
|---|---|---|---|
| ⬜ | RoomIO Overview | https://docs.livekit.io/home/client/tracks/ | - |
| ⬜ | Camera and Microphone | https://docs.livekit.io/home/client/tracks/camera-microphone/ | - |
| ⬜ | Screen Sharing | https://docs.livekit.io/home/client/tracks/screenshare/ | - |
| ⬜ | Byte Streams | https://docs.livekit.io/home/client/data/byte-streams/ | - |

---

## 次にやること

**Phase 2 のMultimodality詳細を読み進める。**

次のドキュメント: **Vision** → https://docs.livekit.io/agents/multimodality/vision/

---

## 作成済みノート一覧

| 作成日 | フェーズ | ノートタイプ | タイトル |
|---|---|---|---|
| 2026-02-28 | - | SourceNote | [[SourceNotes/LiveKit_Agents_Documentation.md\|LiveKit Agents Documentation]] |
| 2026-02-28 | - | StructureNote | このノート |
| 2026-02-28 | Phase 0 | LiteratureNote | [[LiteratureNotes/lit-202602281412-ynh7.md\|LiveKit Basics Overview]] |
| 2026-02-28 | Phase 1 | LiteratureNote | [[LiteratureNotes/lit-202602281704-hf2o.md\|Rooms, Participants, and Tracks]] |
| 2026-02-28 | Phase 1 | LiteratureNote | [[LiteratureNotes/lit-202602281722-eera.md\|Webhooks and Events]] |
| 2026-02-28 | Phase 2 | LiteratureNote | [[LiteratureNotes/lit-202602282303-pgqv.md\|Agents Framework Introduction]] |
| 2026-03-01 | Phase 2 | LiteratureNote | [[LiteratureNotes/lit-202603011301-l1zu.md\|Voice AI Quickstart]] |
| 2026-03-01 | Phase 2 | LiteratureNote | [[LiteratureNotes/lit-202603011637-jxho.md\|Text and Transcriptions]] |
| 2026-03-01 | Phase 2 | LiteratureNote | [[LiteratureNotes/lit-202603012120-f8sk.md\|Agent Speech and Audio]] |
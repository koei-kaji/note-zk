---
title: "LiveKit Agents Documentation"
date: "2026-02-28"
tags:
  - livekit
  - voice-agents
  - ai
  - stt
  - tts
  - llm
draft: false
extra:
  type: "Reference"
  publication: "LiveKit"
  published_at: "2026-02-28"
  authors: ["LiveKit"]
  url: "https://docs.livekit.io/agents/"
  progress: "IN PROGRESS"
  evaluation: "5"
---

# LiveKit Agents Documentation

LiveKit Agentsフレームワークの公式ドキュメント。
音声・映像・物理AIエージェントを構築するためのリアルタイムフレームワーク。

学習ロードマップ → [[StructureNotes/LiveKit_Agent_Framework_学習ロードマップ.md|学習ロードマップ]]

---

## 学習対象ドキュメント一覧（全28ページ・確認済みURL）

### Phase 0: LiveKit基礎概念
| ドキュメント | URL |
|---|---|
| LiveKit Basics Overview | https://docs.livekit.io/intro/basics/ |

### Phase 1: 概念モデル
| ドキュメント | URL |
|---|---|
| Rooms, Participants, and Tracks | https://docs.livekit.io/intro/basics/rooms-participants-tracks/ |
| Building AI agents (intro) | https://docs.livekit.io/intro/basics/agents/ |

### Phase 2: Agentsフレームワーク全体像
| ドキュメント | URL |
|---|---|
| Agents Framework Introduction | https://docs.livekit.io/agents/ |
| Voice AI Quickstart | https://docs.livekit.io/agents/start/voice-ai-quickstart/ |
| Multimodality Overview | https://docs.livekit.io/agents/multimodality/ |

### Phase 3: Agent Server（インフラ層）
| ドキュメント | URL |
|---|---|
| Server Lifecycle | https://docs.livekit.io/agents/server/lifecycle/ |
| Job Lifecycle | https://docs.livekit.io/agents/server/job/ |
| Agent Dispatch | https://docs.livekit.io/agents/server/agent-dispatch/ |
| Server Startup Modes | https://docs.livekit.io/agents/server/startup-modes/ |

### Phase 4: Logic & Structure（コア実装層）
| ドキュメント | URL |
|---|---|
| Logic Overview | https://docs.livekit.io/agents/logic/ |
| Agent Session | https://docs.livekit.io/agents/logic/sessions/ |
| Workflows | https://docs.livekit.io/agents/logic/workflows/ |
| Agents & Handoffs | https://docs.livekit.io/agents/logic/agents-handoffs/ |
| Tasks & Task Groups（Python only） | https://docs.livekit.io/agents/logic/tasks/ |
| Tool Definition & Use | https://docs.livekit.io/agents/logic/tools/ |
| Turn Detection & Interruptions | https://docs.livekit.io/agents/logic/turns/ |
| Pipeline Nodes & Hooks | https://docs.livekit.io/agents/logic/nodes/ |
| External Data & RAG | https://docs.livekit.io/agents/logic/external-data/ |

### Phase 5: Models（モデル選択・設定）
| ドキュメント | URL |
|---|---|
| Models Overview | https://docs.livekit.io/agents/models/ |
| STT Models | https://docs.livekit.io/agents/models/stt/ |
| LLM Models | https://docs.livekit.io/agents/models/llm/ |
| TTS Models | https://docs.livekit.io/agents/models/tts/ |
| Realtime Models | https://docs.livekit.io/agents/models/realtime/ |

### Phase 6: Deploy & Observe（本番運用）
| ドキュメント | URL |
|---|---|
| Agent Deployment Overview | https://docs.livekit.io/deploy/agents/ |
| Observability Overview | https://docs.livekit.io/deploy/observability/ |
| Agent Insights (LiveKit Cloud) | https://docs.livekit.io/deploy/observability/insights/ |
| Data Hooks & OpenTelemetry（Langfuse連携） | https://docs.livekit.io/deploy/observability/data/ |

---

## 除外したドキュメントと理由

| ドキュメント | 除外理由 |
|---|---|
| Agent Builder | GUIツール。コード学習不要 |
| Playground | テストツール。学習目的外 |
| CLI deep dive | 実装時の参照用。on-demandで確認 |
| 各モデルPlugin個別ページ | 参照用。使う時に確認 |
| Telephony | 発展的トピック。基礎習得後に学ぶ |
| WebRTC Transport詳細 | 参照用。エージェント学習の主眼外 |
| Recipes | on-demand参照用 |
| Deploy quickstart | ハンズオン対象（自分で実施） |
| Deploy management/secrets/logs/builds | 実運用参照用。on-demand |

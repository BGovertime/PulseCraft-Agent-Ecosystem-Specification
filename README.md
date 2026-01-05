# PulseCraft-Agent-Ecosystem-Specification
This document outlines the architecture, communication protocols, and automation workflows for the Pulse Craft Agent system.
**PulseCraft Agent Ecosystem** (Technical Specification)

---

# 🛸 PulseCraft Agent Ecosystem Specification

This document outlines the architecture, communication protocols, and automation workflows for the PulseCraft Agent system.

## 🏗️ 1. Repository Structure

A monorepo approach to manage Agent logic, metadata, and the centralized dashboard.

```text
/pulsecraft-agents
├── .github/workflows/      # CI/CD: Auto-versioning & Validations
├── /agents/                # Core Agent Definitions (.md files)
│   ├── video_agent.md
│   ├── prompt_agent.md
│   └── ...
├── /src/
│   ├── /core/              # Event Bus & Context Manager
│   ├── /processors/        # AI & LLM Logic (Thai Language Support)
│   └── /ui/                # Dashboard & History Log Components
├── agent_manifest.json     # Single source of truth for Agent states
└── scripts/                # Automation & Maintenance scripts

```

---

## 📡 2. Core Architecture Components

### A. Event Bus (Inter-Agent Communication)

A Pub/Sub mechanism that decouples agents, allowing them to communicate via asynchronous events.

### B. Context Memory Manager

A sliding-window memory system that tracks conversation history to support natural language flow (especially for Thai pronouns/context).

### C. AI Prompt Processor

Integrated with LLM APIs to translate natural language into structured JSON actions.

* **Support:** Context-aware processing and Semantic mapping.
* **Safety:** Real-time Ethical Impact screening before action execution.

---

## 💻 3. Implementation Examples

### Event Bus & Context Logic

```javascript
// Example: Processing a contextual command in Thai
// Input: "Make it stronger" (referring to a previous 'glitch' effect)
const action = processor.processThaiPromptWithContext("เอาแรงขึ้นอีก");

// Dispatching to Video Agent
bus.publish('VIDEO_ACTION', { 
    action: action.intent, 
    value: action.value + 0.2 
});

```

### Real-time Dashboard Update

The dashboard listens for `UPDATE_KPI` and `ETHICAL_ALERT` events to render visualizations.

---

## ⚖️ 4. Ethical Impact Simulation

Managed by the **Dashboard Agent**, this system monitors AI outputs for:

* **Bias Score:** Calculating representation metrics.
* **Content Safety:** Automated flagging of high-risk commands.
* **Visual Feedback:** Real-time status bars (Green = Safe, Red = High Risk).

---

## 🚀 5. Automation Workflow (CI/CD)

The system includes a **GitHub Action** that automates version management:

1. **Trigger:** Developer updates `Version: v1.x.x` inside an `agent_name.md` file.
2. **Action:** A Python script parses all `.md` files in `/agents`.
3. **Output:** Automatically updates `agent_manifest.json` and commits the changes.
4. **Sync:** The Dashboard reflects the new version and changelog instantly.

---

## 📜 6. Activity History Log

A centralized audit trail that captures:

* **Timestamp:** Precise execution time.
* **Agent ID:** Which agent performed the action.
* **Description:** Human-readable action details.
* **Metadata:** Associated version and ethical impact status.

---

**Next Steps Recommendation:**

* Integrate **Rollback Logic** to allow users to revert Agent versions directly from the History Log.
* Implement **WebSockets** if you plan to move the Dashboard to a remote server for multi-user real-time sync.

ต้องการให้ปรับแก้ส่วนไหน หรือเพิ่มรายละเอียดเชิงลึกในส่วนใดของเอกสารภาษาอังกฤษนี้อีกไหมครับ?

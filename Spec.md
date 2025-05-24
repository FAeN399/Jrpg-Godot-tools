---
title: JRPG Desktop Tool-Suite Specification
version: 1.0
date: 2025-05-24
author: Milo Miles & ChatGPT Deep Researcher
related_documents:
  - prompt_plan.md
  - todo.md
---

# 1  Introduction & Objectives
The **JRPG Desktop Tool-Suite** is a cross-platform, Electron-based collection of productivity tools that accelerate creation of 2-D JRPGs for **Godot 4.x**.  
Primary objectives:

* **Boost productivity** – give designers “RPG Maker–level” speed with modern pipelines.  
* **Tight VS Code flow** – every file is human-readable, Git-versioned, and Copilot-friendly.  
* **Extensibility first** – plugin manifest + API so new modules slot in with zero core edits.  
* **Reliability** – test-driven from day one; CI guards regressions and export validity.  

---

# 2  Functional Requirements

| ID | Requirement |
|----|-------------|
| **FR-1** | **Map Editor** must support unlimited layers (ground, decor, collision, event, parallax). |
| **FR-2** | Editor must allow arbitrary, per-map tile sizes (16 px, 32 px, 48 px …). |
| **FR-3** | Tiles & regions store metadata: `script_id`, `encounter_table`, `notes`, `stat_mods`, `tags`. |
| **FR-4** | Map exports: Godot `.tscn`, `.tres`, and JSON (lossless round-trip). |
| **FR-5** | **Sprite Creator** provides pixel canvas, layers, onion-skin, frame-timeline. |
| **FR-6** | Sprite batch palette-swap + variant export (PNG + SpriteFrames `.tres`). |
| **FR-7** | **Level-Up & Stat Designer** allows visual and YAML/JSON editing of XP curves & formulas. |
| **FR-8** | Live preview validates formulas against sample characters in real time. |
| **FR-9** | **Scripting Assistant** embeds Monaco with GDScript 2.0 support (lint, autocomplete). |
| **FR-10** | One-click AI refactor/generation using Copilot (and pluggable local LLM endpoint). |
| **FR-11** | Undo/redo, autosave, and crash-recovery are available in every module. |
| **FR-12** | Plugin architecture detects `.tool-module.js` manifests and hot-loads UI + API. |

---

# 3  Non-Functional Requirements

* **NFR-1  Performance** – Maintain ≥ 60 fps canvas updates on mid-range 2023 laptops.  
* **NFR-2  Cross-Platform** – Windows 10+, macOS 12+, Ubuntu 22.04+.  
* **NFR-3  Accessibility** – All UI fully keyboard-navigable; color-contrast WCAG AA.  
* **NFR-4  Security** – No uncontrolled remote-code execution; sandbox AI calls.  
* **NFR-5  Documentation** – Doc-comments generate API site via TypeDoc in CI.  
* **NFR-6  Internationalization** – UTF-8 everywhere; strings externalized for i18n packs.

---

# 4  Assumptions & Constraints

* Godot target version: **4.3 LTS** (assumed stable by project beta).  
* Runtime: **Electron ^30** bundled with Node 20 LTS.  
* Users possess **GitHub Pro** + **Copilot** licences.  
* Local LLM integration assumes an HTTP endpoint returning OpenAI-compatible JSON.  
* Memory ceiling: ≤ 1 GB RAM per loaded project to remain lightweight.  

_Open questions_

* Preferred UI framework inside Electron (React + Tailwind vs. Svelte?).  
* Minimum supported Godot minor versions for `.tres` compatibility.  

---

# 5  System Architecture / Design

```mermaid
flowchart TD
    subgraph Electron App
        VSCode[[VS Code + Copilot]]
        MapEditor-->Exporter
        SpriteCreator-->Exporter
        StatDesigner-->ProjectStore
        ScriptAssistant-->ProjectStore
        PluginAPI-->ProjectStore
    end
    ProjectStore[Local Project Dir (Git)]
    Exporter-->GodotProject[/Godot 4.x Project/]
    VSCode-->ProjectStore
    CI[GitHub Actions CI]-->ProjectStore
    CI-->GodotValidation[Headless Godot Export Checks]

	•	ProjectStore – canonical single-source directory; JSON/YAML + media.
	•	Plugin API – CommonJS modules expose hooks: registerMenu, extendSchema, etc.
	•	Exporter – converts internal models ➜ .tscn/.tres + companion data.

⸻

6  Data Sources / APIs

Source	Purpose	Format
Local JSON/YAML	Tilemaps, stats, class data	JSON 5 / YAML 1.2
Godot scenes	Engine-ready assets	.tscn, .tres
Copilot API	AI code suggestions	HTTPS REST (OpenAI style)
/v1/llm/chat (optional)	Pluggable local LLM	OpenAI-compatible


⸻

7  Error-Handling Strategy
	•	Central Logger – Winston-based, writing logs/*.log per module.
	•	Graceful Degradation – corrupt map files open read-only with inline alerts.
	•	User Alerts – Toast notifications + Issues pane (stack traces collapsed).
	•	Crash Recovery – autosave snapshots every 60 s, stored in autosaves/.
	•	Exporter Validation – schema check → block export if fatal, warn if non-fatal.

⸻

8  Testing & Validation Plan

Level	Tooling	Scope
Unit	Vitest + jsdom	Module utilities, Pure functions
Component	Playwright Component Test	React/Svelte UIs
Integration	Spectron (Electron)	IPC & Autosave loops
End-to-End	Playwright + Headless Godot	Full export ➜ import round-trip
Performance	Lighthouse + custom FPS probe	Canvas redraw, memory
CI	GitHub Actions	Matrix: win/mac/linux, Node 20

All new code requires failing test ➜ implementation ➜ passing test (TDD).

⸻

9  Glossary
	•	SpriteFrames .tres – Godot resource describing animations.
	•	Monaco – VS Code’s embeddable editor component.
	•	Plugin Manifest – JSON file (tool-module.json) that declares entry script metadata.
	•	Stat Formula – expression (e.g., base + level * growth) parsed by math-expr engine.

⸻

End of spec.md

> **Next step:** add this `spec.md` to your repo (`git add spec.md && git commit -m "Add initial specification v1.0"`).  
> Let me know whenever you’re ready for the TDD execution plan, todo checklist, or any deep-dive on specific modules!

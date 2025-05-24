---
title: JRPG Desktop Tool-Suite Specification
version: 1.1
date: 2025-05-24
author: Milo Miles & ChatGPT Deep Researcher
related_documents:
  - prompt_plan.md
  - todo.md
changelog:
  - 1.1: Added Export Format section, MVP vs. Stretch scope, performance targets, packaging & docs requirements
---

# 1 Introduction & Objectives
The **JRPG Desktop Tool-Suite** is a cross-platform Electron application that accelerates creation of classic 2-D JRPGs for **Godot 4.1**.  
Objectives  
* Provide user-friendly editors (map, sprite, stats, events) with a “RPG-Maker-like” workflow  
* Generate Godot-ready scenes/resources with one-click sync  
* Remain fully open-source, modular, and test-driven  
* Deliver installers for Windows, macOS, and Linux

# 2 Functional Requirements

| ID | Requirement |
|----|-------------|
| **FR-1** | Map Editor supports unlimited layers (ground, decor, collision, event, parallax). |
| **FR-2** | Per-map arbitrary tile sizes (16 px, 32 px, 48 px …). |
| **FR-3** | Tiles / regions store metadata: `script_id`, `encounter_table`, `notes`, `stat_mods`, `tags`. |
| **FR-4** | Exports maps to `.map.json` (lossless) **and** `.tscn`. |
| **FR-5** | Sprite Creator offers pixel canvas, layers, onion-skin, timeline. |
| **FR-6** | Palette-swap & variant export: PNG + SpriteFrames `.tres`. |
| **FR-7** | Stat Designer edits XP curves & formulas (visual + YAML/JSON). |
| **FR-8** | Live stat preview & validation. |
| **FR-9** | Embedded Monaco GDScript editor with lint & autocomplete. |
| **FR-10** | AI-powered coding chat (Copilot Chat integration). |
| **FR-11** | Global undo/redo, autosave, crash-recovery across all editors. |
| **FR-12** | Plugin architecture: modules detected via manifest & hot-loaded. |

# 3 Non-Functional Requirements

* **NFR-1 Performance** – ≤ 16 ms frame time on a 200×200 map; 60 fps target.  
* **NFR-2 Cross-Platform** – Windows 10+, macOS 12+, Ubuntu 22.04+.  
* **NFR-3 Accessibility** – Full keyboard navigation; WCAG AA color contrast.  
* **NFR-4 Security** – Context isolation; minimal Node exposure.  
* **NFR-5 Documentation** – Doc comments → auto API site; user guide in `/docs`.  
* **NFR-6 Internationalization** – UTF-8; strings externalized.  
* **NFR-7 Performance Targets** – Memory ≤ 900 MB with four editors open.  
* **NFR-8 Packaging & Distribution** – Signed installers; app size ≤ 150 MB.  
* **NFR-9 Documentation UX** – Tool-tips for all UI controls.

# 4 Assumptions & Constraints

* Locked to **Godot 4.1 stable** for initial release.  
* Single-user desktop focus (v 1.0); no live multi-user editing.  
* Assets supplied by user must be properly licensed.

# 5 System Architecture / Design

```mermaid
flowchart TD
    subgraph Electron App
        MapEditor-->Exporter
        SpriteCreator-->Exporter
        StatDesigner-->ProjectStore
        ScriptAssistant-->ProjectStore
        PluginAPI-->ProjectStore
    end
    VSCode[[VS Code + Copilot]]
    ProjectStore[Local Project Dir (Git)]
    Exporter-->GodotProject[/Godot 4 Project/]
    VSCode-->ProjectStore
    CI[GitHub Actions CI]-->ProjectStore
    CI-->GodotValidation[Headless Godot Import Test]

6 Export Formats & Godot Integration

Editor	Output	Godot Path	Import Strategy
Map	*.map.json, .tscn	/maps/	Godot addon converts JSON → TileMap scene; .tscn for preview.
Database	database.yaml	/data/	Read at runtime via YAML module.
Sprites	name.png, name.tres	/sprites/	Direct SpriteFrames resource.
Events	*.evt.json	/events/	Addon parses JSON, attaches scripts.

A Godot EditorPlugin (addons/jrpg_sync/) watches an export folder and triggers automatic imports.

7 Error-Handling Strategy
	•	Central Winston logger; logs per module
	•	Graceful read-only fallback for corrupt projects
	•	Autosave snapshots every 60 s → autosaves/
	•	Recovery dialog on next launch

8 Testing & Validation Plan

Level	Tool	Scope
Unit	Vitest	Core logic
Component	React Testing Library	UI components
Integration	Spectron / Playwright	IPC, autosave
Perf	Playwright FPS probe	200×200 map benchmark
Integration-2	Headless Godot	Import exported .tscn and log “Import OK”

9 Glossary
	•	SpriteFrames .tres – Godot animation resource
	•	Monaco – VS Code editor component
	•	Map JSON schema – Canonical definition of map export
	•	ProjectStore – Local Git-tracked folder containing all assets


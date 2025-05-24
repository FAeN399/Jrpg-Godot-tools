---
title: Project To-Do Checklist
project: JRPG Desktop Tool-Suite
related_plan: prompt_plan.md
related_spec: spec.md
date: 2025-05-24
---

### Phase 1 – Infrastructure & CI
- [ ] **Repo Bootstrap & CI Skeleton** – scaffold monorepo & baseline CI (Plan 1, NFR-1, NFR-5)
- [ ] **Code Quality Tooling** – ESLint / Prettier + Husky lint test (Plan 2, NFR-3, NFR-5)

### Phase 2 – Core Services
- [ ] **ProjectStore Save/Load** – JSON round-trip test passes (Plan 3, FR-4, FR-11)
- [ ] **Plugin Loader Skeleton** – dynamic manifest loading (Plan 4, FR-12)

### Phase 3 – Application Shell
- [ ] **Electron Main Process & Window** – renderer shell with title (Plan 5, NFR-2)
- [ ] **IPC Bridge for ProjectStore** – open/save via IPC (Plan 6, FR-11)

### Phase 4 – Map Editor
- [ ] **Canvas Rendering Core** – 32×32 grid baseline (Plan 7, FR-1)
- [ ] **Layer System** – dynamic layers (Plan 8, FR-1)
- [ ] **Tile Size Configuration** – arbitrary px scaling (Plan 9, FR-2)
- [ ] **Tile Metadata Model** – CRUD metadata (Plan 10, FR-3)
- [ ] **Undo / Redo Manager** – command stack (Plan 11, FR-11)
- [ ] **Autosave & Recovery** – snapshot & dialog (Plan 12, FR-11)
- [ ] **JSON Map Exporter** – lossless export (Plan 13, FR-4)
- [ ] **Godot .tscn Exporter** – basic scene serializer (Plan 14, FR-4)

### Phase 5 – Sprite Creator
- [ ] **Sprite Canvas Baseline** – pixel canvas (Plan 15, FR-5)
- [ ] **Onion-Skin & Timeline** – frame overlay (Plan 16, FR-5)
- [ ] **Palette Swap Utility** – batch transform (Plan 17, FR-6)
- [ ] **Sprite Exporter (PNG + .tres)** – sheet & SpriteFrames (Plan 18, FR-6)

### Phase 6 – Stat Designer
- [ ] **Stat Model & Parser** – formula engine (Plan 19, FR-7)
- [ ] **Level-Up Curve Editor** – XP chart preview (Plan 20, FR-7)
- [ ] **Live Stat Validation** – real-time badges (Plan 21, FR-8)
- [ ] **YAML/JSON Dual Editing** – toggle editors (Plan 22, FR-7)

### Phase 7 – Scripting Assistant
- [ ] **Monaco GDScript Editor** – embed editor (Plan 23, FR-9)
- [ ] **Copilot Chat Integration** – AI sidebar (Plan 24, FR-10)

### Phase 8 – Core UX & Stability
- [ ] **Central Logger & Viewer** – Winston + UI (Plan 25, NFR-4)
- [ ] **Error Boundary & Toasts** – UI fallback (Plan 26, Spec§7)
- [ ] **Crash Recovery Workflow** – autosave restore (Plan 27, FR-11)

### Phase 9 – Performance & Localization
- [ ] **Performance Probe 60 FPS** – benchmark & optimize (Plan 28, NFR-1)
- [ ] **Internationalization Extraction** – externalize strings (Plan 29, NFR-6)

### Phase 10 – Plugin System
- [ ] **Plugin Hot-Reload E2E** – watcher & runtime import (Plan 30, FR-12)

### Phase 11 – Export & Integration
- [ ] **Define Export Schemas** – map/event JSON schemas & tests (Plan 31, Spec §6)
- [ ] **Godot Sync Addon** – headless import CI (Plan 32, Spec §6)

### Phase 12 – Performance & UX Enhancements
- [ ] **Benchmark Harness** – fps guard (Plan 33, NFR-7)
- [ ] **Global Undo/Redo** – extend to all editors (Plan 34, FR-11 & NFR-9)
- [ ] **Tooltip Coverage** – lint tool-tips (Plan 35, NFR-9)

### Phase 13 – Docs & Packaging
- [ ] **User Guide Skeleton** – docs outline (Plan 35, NFR-9)
- [ ] **Build Installers** – Electron Builder + CI (Plan 36, NFR-8)

### Phase 14 – Automated UI Tests
- [ ] **E2E Map Paint Test** – Playwright click → data assertion (Plan 37, UI Gap)

### Phase 15 – Release
- [ ] **Prepare v0.1.0 Release** – changelog, tag, upload installers (Plan 38)

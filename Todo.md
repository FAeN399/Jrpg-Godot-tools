---
title: Project To-Do Checklist
project: JRPG Desktop Tool-Suite
related_plan: prompt_plan.md
related_spec: spec.md
date: 2025-05-24
---

### Phase 1 – Infrastructure & CI
- [ ] **Repo Bootstrap & CI Skeleton** – scaffold monorepo and baseline CI (Plan 1, NFR-1, NFR-5)
- [ ] **Code Quality Tooling** – ESLint, Prettier, Husky hooks, failing lint test (Plan 2, NFR-3, NFR-5)

### Phase 2 – Core Services
- [ ] **ProjectStore Save/Load** – JSON save-load round-trip passes test (Plan 3, FR-4, FR-11)
- [ ] **Plugin Loader Skeleton** – dynamic manifest loading (Plan 4, FR-12)

### Phase 3 – Application Shell
- [ ] **Electron Main Process & Window** – open renderer window with title (Plan 5, NFR-2)
- [ ] **IPC Bridge for ProjectStore** – expose open/save via IPC (Plan 6, FR-11)

### Phase 4 – Map Editor
- [ ] **Canvas Rendering Core** – grid render for blank map (Plan 7, FR-1)
- [ ] **Layer System** – dynamic multi-layer stacking (Plan 8, FR-1)
- [ ] **Tile Size Configuration** – arbitrary px scaling (Plan 9, FR-2)
- [ ] **Tile Metadata Model** – CRUD metadata + persistence (Plan 10, FR-3)
- [ ] **Undo / Redo Manager** – command stack integration (Plan 11, FR-11)
- [ ] **Autosave & Snapshot Recovery** – periodic snapshots & restore (Plan 12, FR-11)
- [ ] **JSON Map Exporter** – lossless JSON exporter (Plan 13, FR-4)
- [ ] **Godot .tscn Exporter** – basic scene serializer (Plan 14, FR-4)

### Phase 5 – Sprite Creator
- [ ] **Sprite Canvas Baseline** – pixel canvas component (Plan 15, FR-5)
- [ ] **Onion-Skin & Timeline** – frame overlay + controls (Plan 16, FR-5)
- [ ] **Palette Swap Utility** – batch palette transformer (Plan 17, FR-6)
- [ ] **Sprite Exporter (PNG + .tres)** – export sheets & SpriteFrames (Plan 18, FR-6)

### Phase 6 – Stat Designer
- [ ] **Stat Model & Expression Parser** – formula engine (Plan 19, FR-7)
- [ ] **Level-Up Curve Editor UI** – XP curve chart preview (Plan 20, FR-7)
- [ ] **Live Stat Preview Validation** – real-time validation badges (Plan 21, FR-8)
- [ ] **YAML/JSON Dual Editing** – toggle & sync editors (Plan 22, FR-7)

### Phase 7 – Scripting Assistant
- [ ] **Embed Monaco GDScript Editor** – language mode & lint (Plan 23, FR-9)
- [ ] **Copilot Chat Integration** – AI refactor/generation sidebar (Plan 24, FR-10)

### Phase 8 – Core UX & Stability
- [ ] **Central Logger & Log Viewer** – Winston logger + UI panel (Plan 25, NFR-4)
- [ ] **Error Boundary & Toast Alerts** – UI fallback & notifications (Plan 26, Spec §7)
- [ ] **Crash Recovery Workflow** – autosave recovery dialog (Plan 27, FR-11, Spec §7)

### Phase 9 – Performance & Localization
- [ ] **Performance Probe 60 FPS** – Playwright FPS test & optimizations (Plan 28, NFR-1)
- [ ] **Internationalization Extraction** – string bundles & locale switch (Plan 29, NFR-6)

### Phase 10 – Plugin System
- [ ] **Plugin Hot-Reload E2E** – watcher + runtime import (Plan 30, FR-12)

### Phase 11 – Wrap-Up
- [ ] **Full Test Suite & CI Pass** – all unit, integration, E2E, perf tests green (Wrap-Up 1)
- [ ] **v0.1 Release & Tag** – create release, push tags, update changelog (Wrap-Up 2)

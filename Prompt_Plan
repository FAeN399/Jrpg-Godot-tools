---
title: Execution Plan (TDD)
project: JRPG Desktop Tool-Suite
related_spec: spec.md
version: 1.0
date: 2025-05-24
---

1. **Repo Bootstrap & CI Skeleton (covers NFR-1, NFR-5)**  
```prompt
Scaffold a new monorepo called **jrpg-tool-suite** using pnpm workspaces.  
Add sub-packages `app` (Electron), `core` (shared logic), `tests` (Vitest).  
Create GitHub Actions workflow `.github/workflows/ci.yml` that runs `pnpm install`, `pnpm test` on ubuntu-latest, macos-latest, windows-latest.  
Commit with message: "chore: bootstrap repo & CI".  

	2.	Code Quality Tooling (covers NFR-3, NFR-5)

Add ESLint (typescript-eslint, prettier) and Husky pre-commit hook that runs `pnpm lint --fix`.  
Write an initial failing lint rule test in `tests/lint.spec.ts` that asserts `core/index.ts` passes eslint.  
Commit: "chore: lint & format baseline".  

	3.	ProjectStore Save/Load (covers FR-4, FR-11)

Write a Vitest failing test in `tests/core/projectStore.spec.ts` that:  
1) creates a temp dir,  
2) calls `ProjectStore.save("map.json", {...})`,  
3) reloads with `ProjectStore.load("map.json")`,  
4) expects deep equality.  
Implement minimal `src/core/ProjectStore.ts` to pass.  
Commit: "feat(core): ProjectStore save/load v0".  

	4.	Plugin Loader Skeleton (covers FR-12)

Create failing test `tests/core/pluginLoader.spec.ts` ensuring `PluginLoader.load("./fixtures/echo-plugin")` registers a dummy command.  
Implement `src/core/PluginLoader.ts` to scan for `tool-module.json` manifests.  
Commit: "feat(core): plugin loader scaffold".  

	5.	Electron Main Process & Window (covers NFR-2)

Generate Electron main process (`packages/app/main.ts`) that opens a BrowserWindow loading `index.html`.  
Add Playwright E2E test `tests/e2e/window.spec.ts` that asserts window title "JRPG Tool-Suite".  
Implement minimal renderer with Vite + React + Tailwind CSS.  
Commit: "feat(app): electron shell with renderer".  

	6.	IPC Bridge for ProjectStore (covers FR-11)

Write failing Spectron test ensuring `ipcRenderer.invoke("project:open", path)` returns project meta.  
Expose IPC handlers in main, thin wrapper in renderer.  
Commit: "feat(app): IPC ProjectStore bridge".  

	7.	Canvas Rendering Core (covers FR-1)

Write failing Vitest + jsdom test that mounts `MapCanvas` React component and verifies it renders a 32×32 grid for a blank map.  
Implement `src/modules/map/MapCanvas.tsx` using `react-konva`.  
Commit: "feat(map): canvas grid baseline".  

	8.	Layer System (covers FR-1)

Add test `mapLayers.spec.tsx` expecting MapCanvas to stack 'ground' and 'decor' layers with correct z-index.  
Refactor MapCanvas to dynamic layer list.  
Commit: "feat(map): multi-layer support".  

	9.	Tile Size Configuration (covers FR-2)

Add failing test `tileSize.spec.ts` creating a 48 px map and asserting canvas scales correctly.  
Implement prop `tileSize` and scaling math.  
Commit: "feat(map): arbitrary tile size".  

	10.	Tile Metadata Model (covers FR-3)

Write failing test: setting metadata `{script_id:"EV01"}` on tile (2,3) persists through save/load round-trip.  
Extend ProjectStore schema + MapCanvas context menu for metadata editing.  
Commit: "feat(map): tile metadata CRUD".  

	11.	Undo / Redo Manager (covers FR-11)

Failing test: draw tile, undo, expect previous state; redo restores.  
Implement command stack in `src/lib/undoRedo.ts`.  
Wire to MapCanvas actions.  
Commit: "feat(core): undo/redo service".  

	12.	Autosave & Snapshot Recovery (covers FR-11)

Failing integration test: modify map, wait 65 s, crash process, restart; Map opens with autosaved changes.  
Implement interval snapshot to `autosaves/` and restore prompt on load.  
Commit: "feat(app): autosave snapshots".  

	13.	JSON Map Exporter (covers FR-4)

Write failing unit test: exporting a sample map yields JSON matching snapshot `fixtures/map.export.json`.  
Implement `src/exporters/jsonExporter.ts`.  
Commit: "feat(export): JSON exporter".  

	14.	Godot .tscn Exporter (covers FR-4)

Add failing test that exportGodot("scene.tscn") returns string containing `[node name="MapRoot" type="Node2D"]`.  
Implement basic `.tscn` serializer mirroring JSON structure.  
Commit: "feat(export): Godot .tscn exporter v0".  

	15.	Sprite Canvas Baseline (covers FR-5)

Failing react-testing-library test: `SpriteCanvas` renders pixel grid 64×64.  
Implement `src/modules/sprite/SpriteCanvas.tsx`.  
Commit: "feat(sprite): canvas baseline".  

	16.	Onion-Skin & Timeline (covers FR-5)

Test: advancing timeline shows previous frame at 50 % opacity.  
Add onion-skin overlay and timeline controls.  
Commit: "feat(sprite): onion-skin & timeline".  

	17.	Palette Swap Utility (covers FR-6)

Unit test: paletteSwap(green→blue) on sample PNG outputs expected hash.  
Implement `src/lib/paletteSwap.ts`.  
Commit: "feat(sprite): palette swap".  

	18.	Sprite Exporter (PNG + .tres) (covers FR-6)

Failing test: exporting frames yields `hero.png` and `hero.tres` referencing 4 animations.  
Implement exporter pipeline.  
Commit: "feat(export): sprite PNG + SpriteFrames tres".  

	19.	Stat Model & Expression Parser (covers FR-7)

Failing test: `StatFormula("base + level*2")(base=10, level=5)` returns 20.  
Implement parser with `mathjs`.  
Commit: "feat(stats): formula parser".  

	20.	Level-Up Curve Editor UI (covers FR-7)

React test: editing XP curve updates preview chart dataset length = 10 levels.  
Create `StatDesigner.tsx` with chart.js preview.  
Commit: "feat(stats): curve editor".  

	21.	Live Stat Preview Validation (covers FR-8)

Test: invalid formula shows red validation badge; fix turns badge green.  
Add live eval + schema validation.  
Commit: "feat(stats): live validation".  

	22.	YAML/JSON Dual Editing (covers FR-7)

Test: switching to YAML view then back preserves stat model integrity.  
Integrate `monaco-yaml` + sync serialization.  
Commit: "feat(stats): YAML/JSON toggle".  

	23.	Embed Monaco GDScript Editor (covers FR-9)

E2E test: opening ScriptAssistant loads Monaco with language id "gdscript".  
Install `monaco-editor` + custom language config.  
Commit: "feat(script): Monaco embed".  

	24.	Copilot Chat Integration (covers FR-10)

Mock Copilot API in test; verify chat returns code suggestion snippet.  
Implement sidebar chat using GitHub Copilot Chat API.  
Commit: "feat(script): Copilot chat".  

	25.	Central Logger & Log Viewer (covers NFR-4)

Test: `logger.error("boom")` writes entry to `logs/app.log`; LogViewer lists 1 row.  
Add Winston logger + UI.  
Commit: "feat(core): central logger".  

	26.	Error Boundary & Toast Alerts (covers 7, NFR-3)

React test: throwing error in child renders ErrorBoundary fallback UI.  
Add `ErrorBoundary` + toast notifications via `react-hot-toast`.  
Commit: "feat(ui): error handling visuals".  

	27.	Crash Recovery Workflow (covers FR-11, 7)

E2E: force process.exit(1); upon restart, RecoveryDialog suggests last autosave.  
Implement recovery dialog component.  
Commit: "feat(app): crash recovery flow".  

	28.	Performance Probe 60 FPS (covers NFR-1)

Add Playwright perf test measuring MapCanvas FPS for 5 s; expect ≥60 average.  
Optimize Konva layer batching if failing.  
Commit: "perf(map): maintain 60fps".  

	29.	Internationalization Extraction (covers NFR-6)

Unit test: calling `i18n.t("menu.file")` returns French string when locale=fr.  
Extract all hard-coded strings to JSON message bundles.  
Commit: "feat(i18n): string externalization".  

	30.	Plugin Hot-Reload E2E (covers FR-12)

E2E: drop new plugin folder into `plugins/`; app emits "Plugin Loaded: sample".  
Implement file-watcher & runtime import.  
Commit: "feat(plugin): hot-reload".  


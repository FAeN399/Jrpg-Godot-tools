---
title: Execution Plan (TDD)
project: JRPG Desktop Tool-Suite
related_spec: spec.md
version: 1.1
date: 2025-05-24
---

1. **Repo Bootstrap & CI Skeleton (covers NFR-1, NFR-5)**  
```prompt
Scaffold a new monorepo called **jrpg-tool-suite** using pnpm workspaces.  
Add sub-packages `app` (Electron), `core` (shared logic), `tests` (Vitest).  
Create GitHub Actions workflow `.github/workflows/ci.yml` that runs `pnpm install && pnpm test`
on ubuntu-latest, macos-latest, windows-latest.  
Commit: "chore: bootstrap repo & CI".

	2.	Code Quality Tooling (covers NFR-3, NFR-5)

Add ESLint (typescript-eslint, prettier) and Husky pre-commit hook running `pnpm lint --fix`.  
Create failing test `tests/lint.spec.ts` asserting `core/index.ts` passes eslint.  
Commit: "chore: lint & format baseline".

	3.	ProjectStore Save/Load (covers FR-4, FR-11)

Write Vitest failing test `tests/core/projectStore.spec.ts`:  
1) temp dir, 2) `ProjectStore.save("map.json",{a:1})`,
3) load → expect deepEqual.  
Implement `src/core/ProjectStore.ts` to pass.  
Commit: "feat(core): ProjectStore save/load v0".

	4.	Plugin Loader Skeleton (covers FR-12)

Test `tests/core/pluginLoader.spec.ts` expecting
`PluginLoader.load("./fixtures/echo-plugin")` registers dummy command.  
Implement `src/core/PluginLoader.ts` scanning `tool-module.json`.  
Commit: "feat(core): plugin loader scaffold".

	5.	Electron Main Process & Window (covers NFR-2)

Generate `packages/app/main.ts` creating BrowserWindow titled "JRPG Tool-Suite".  
Add Playwright E2E test asserting window title.  
Commit: "feat(app): electron shell with renderer".

	6.	IPC Bridge for ProjectStore (covers FR-11)

Spectron test: `ipcRenderer.invoke("project:open", path)` returns project meta.  
Expose IPC handlers in main; wrap in renderer.  
Commit: "feat(app): IPC ProjectStore bridge".

	7.	Canvas Rendering Core (covers FR-1)

Vitest + jsdom: mount `MapCanvas` and verify 32×32 grid rendered for blank map.  
Implement `src/modules/map/MapCanvas.tsx` with react-konva.  
Commit: "feat(map): canvas grid baseline".

	8.	Layer System (covers FR-1)

Test `mapLayers.spec.tsx`: MapCanvas stacks 'ground' & 'decor' layers (z-index).  
Refactor MapCanvas to dynamic layer list.  
Commit: "feat(map): multi-layer support".

	9.	Tile Size Configuration (covers FR-2)

Test `tileSize.spec.ts`: create 48 px map, assert canvas scale matches.  
Add `tileSize` prop + scaling.  
Commit: "feat(map): arbitrary tile size".

	10.	Tile Metadata Model (covers FR-3)

Test: set metadata `{script_id:"EV01"}` on tile (2,3); save/load round-trip ok.  
Extend ProjectStore schema + metadata editor UI.  
Commit: "feat(map): tile metadata CRUD".

	11.	Undo / Redo Manager (covers FR-11)

Test: draw tile → undo → expect old state; redo restores.  
Implement command stack `src/lib/undoRedo.ts`; wire to MapCanvas.  
Commit: "feat(core): undo/redo service".

	12.	Autosave & Snapshot Recovery (covers FR-11)

Integration test: modify map, wait 65 s, crash; restart → autosaved changes present.  
Implement snapshot timer to `autosaves/`; recovery dialog.  
Commit: "feat(app): autosave snapshots".

	13.	JSON Map Exporter (covers FR-4)

Unit test: export sample map → JSON matches snapshot.  
Implement `src/exporters/jsonExporter.ts`.  
Commit: "feat(export): JSON exporter".

	14.	Godot .tscn Exporter (covers FR-4)

Test: exportGodot("scene.tscn") contains `[node name="MapRoot"]`.  
Implement basic `.tscn` serializer.  
Commit: "feat(export): Godot .tscn exporter v0".

	15.	Sprite Canvas Baseline (covers FR-5)

React test: `SpriteCanvas` renders 64×64 pixel grid.  
Implement `src/modules/sprite/SpriteCanvas.tsx`.  
Commit: "feat(sprite): canvas baseline".

	16.	Onion-Skin & Timeline (covers FR-5)

Test: advancing timeline shows previous frame at 50 % opacity.  
Add onion-skin overlay + timeline controls.  
Commit: "feat(sprite): onion-skin & timeline".

	17.	Palette Swap Utility (covers FR-6)

Unit: paletteSwap(green→blue) on sample PNG → expected hash.  
Implement `src/lib/paletteSwap.ts`.  
Commit: "feat(sprite): palette swap".

	18.	Sprite Exporter (PNG + .tres) (covers FR-6)

Test: export → `hero.png` & `hero.tres` with 4 animations.  
Implement exporter pipeline.  
Commit: "feat(export): sprite PNG + SpriteFrames tres".

	19.	Stat Model & Expression Parser (covers FR-7)

Test: StatFormula("base+level*2")(10,5) == 20.  
Implement parser with mathjs.  
Commit: "feat(stats): formula parser".

	20.	Level-Up Curve Editor UI (covers FR-7)

React test: editing XP curve updates chart dataset length = 10.  
Create `StatDesigner.tsx` with chart.js preview.  
Commit: "feat(stats): curve editor".

	21.	Live Stat Preview Validation (covers FR-8)

Test: invalid formula shows red badge; fix = green badge.  
Add live eval + schema validation.  
Commit: "feat(stats): live validation".

	22.	YAML/JSON Dual Editing (covers FR-7)

Test: switch YAML → JSON preserves stat model.  
Integrate monaco-yaml + sync serialization.  
Commit: "feat(stats): YAML/JSON toggle".

	23.	Embed Monaco GDScript Editor (covers FR-9)

E2E: ScriptAssistant loads Monaco language id "gdscript".  
Add monaco editor + language config.  
Commit: "feat(script): Monaco embed".

	24.	Copilot Chat Integration (covers FR-10)

Mock Copilot API; verify chat returns code snippet.  
Implement Copilot Chat sidebar.  
Commit: "feat(script): Copilot chat".

	25.	Central Logger & Log Viewer (covers NFR-4)

Test: logger.error("boom") writes to `logs/app.log`; viewer lists 1 row.  
Add Winston logger + UI.  
Commit: "feat(core): central logger".

	26.	Error Boundary & Toast Alerts (covers Spec §7)

React test: ErrorBoundary fallback renders on throw.  
Add ErrorBoundary and react-hot-toast notifications.  
Commit: "feat(ui): error handling visuals".

	27.	Crash Recovery Workflow (covers FR-11, Spec §7)

E2E: force crash; on restart, RecoveryDialog suggests last autosave.  
Implement recovery dialog component.  
Commit: "feat(app): crash recovery flow".

	28.	Performance Probe 60 FPS (covers NFR-1)

Playwright perf test: MapCanvas FPS ≥60 over 5 s with 200×200 map.  
Optimize render batching if failing.  
Commit: "perf(map): maintain 60fps".

	29.	Internationalization Extraction (covers NFR-6)

Unit test: i18n.t("menu.file", fr) returns French string.  
Externalize strings to JSON bundles.  
Commit: "feat(i18n): string externalization".

	30.	Plugin Hot-Reload E2E (covers FR-12)

E2E: drop new plugin folder → app logs "Plugin Loaded: sample".  
Implement file-watcher & runtime import.  
Commit: "feat(plugin): hot-reload".

	31.	Define Export Schema & PoC (covers Spec §6)

Create `schemas/export.map.json` & `schemas/export.event.json`.  
Write failing Vitest asserting sample map serializes per schema.  
Commit: "feat(export): define export schemas & PoC".

	32.	Godot Sync Addon (covers Spec §6)

In Godot 4.1 project, create `addons/jrpg_sync/map_importer.gd`
converting `*.map.json` → TileMap scene.  
Add CI step: headless Godot opens exported `.map.json` and logs "Import OK".  
Commit: "feat(integration): Godot sync addon + CI headless test".

	33.	Performance Benchmark Harness (covers NFR-7)

Add Playwright script measuring FPS with 200×200 map; fail if avg frame >16 ms.  
Commit: "perf: benchmark harness & guard".

	34.	UX Polish: Global Undo/Redo (covers FR-11, NFR-9)

Extend undo stack to Sprite & Stat editors; add unit tests.  
Commit: "feat(core): global undo/redo".

	35.	Tooltips & User Guide Skeleton (covers NFR-9)

Doc-lint test: ensure every menu item has tooltip text.  
Generate `/docs/user_guide.md` with outline.  
Commit: "docs: user guide skeleton + tooltip tests".

	36.	Packaging & Installer (covers NFR-8)

Configure Electron Builder for Win/macOS/Linux.  
Add GitHub Actions release workflow building installers.  
Commit: "build: cross-platform installers".

	37.	UI End-to-End Test – Map Paint (covers Gap UI Tests)

Playwright Electron test: new map → click tile (10,10) → expect JSON tile.id != 0.  
Commit: "test(ui): map paint e2e".

	38.	Release v 0.1 & Changelog

Update `CHANGELOG.md`; tag `v0.1.0`; create GitHub release with installers.  
Commit: "chore(release): v0.1.0".


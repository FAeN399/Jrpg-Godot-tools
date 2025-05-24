# JRPG Desktop Tool-Suite

> **Create classic 2-D JRPGs for Godot 4 — faster, friendlier, and 100 % open-source.**

The **JRPG Desktop Tool-Suite** is a modular Electron application that lets designers build tile-maps, sprites, stats, and events in an “RPG-Maker-style” workflow, then **one-click-sync** everything into a Godot 4.1 project.  
It is engineered for **test-driven development**, seamless Git versioning, and AI-accelerated coding with VS Code + GitHub Copilot.

---

## ✨ Core Features

| Module | Highlights |
|--------|------------|
| **Map Editor** | Unlimited layers, arbitrary tile sizes (16/32/48 px +), per-tile metadata, instant JSON/`.tscn` export. |
| **Sprite Creator** | Pixel-art canvas with layers, onion-skin, timeline, palette-swap, PNG + SpriteFrames `.tres` output. |
| **Stat Designer** | Visual & YAML/JSON editing of XP curves and formulas with live validation & preview. |
| **Event Editor** | JSON-based event scripting (visual UI in roadmap), auto-attached in Godot via sync addon. |
| **Scripting Assistant** | Embedded Monaco editor for GDScript 2.0 plus Copilot Chat refactor/generation. |
| **Plugin API** | Hot-loadable modules discovered by manifest for future extensions. |

---

## 🚀 Quick Start

```bash
# 1. Clone & install
git clone https://github.com/your-org/jrpg-tool-suite.git
cd jrpg-tool-suite
pnpm install

# 2. Run the app (dev mode)
pnpm dev             # starts Electron + Vite + React

# 3. Run tests
pnpm test            # Vitest unit suite
pnpm test:e2e        # Playwright integration suite

# 4. Build installers
pnpm build           # creates signed installers via Electron Builder

Prerequisites
• Node 20 LTS + pnpm
• Git
• Godot 4.1 (for importing assets)
• Windows 10+ / macOS 12+ / Ubuntu 22.04+

⸻

📂 Project Structure

packages/
├─ app/              # Electron main & renderer (React + Tailwind)
├─ core/             # Shared logic, data schemas, exporters
├─ tests/            # Vitest, Playwright, Spectron specs
schemas/             # JSON/YAML export definitions
addons/jrpg_sync/    # Godot EditorPlugin for auto-import
docs/                # User guide (Markdown)


⸻

🛠 Development Workflow
	1.	Spec-first — All new features start with a spec update (spec.md).
	2.	TDD — Write a failing test → implement → refactor.
	3.	AI Assist — Use Copilot Chat for boilerplate & refactors (human review required!).
	4.	CI — GitHub Actions runs unit, integration, headless-Godot import, and performance tests on every PR.
	5.	Release — pnpm build generates signed installers; releases are tagged & uploaded automatically.

⸻

🗺 Roadmap
	•	Visual node-based Event Editor
	•	Cutscene timeline & dialogue tool
	•	Battle System designer (turn-based template)
	•	Online asset marketplace integration
	•	Multi-user collaboration & conflict-resolution UI

See todo.md for the full, test-mapped checklist.

⸻

🤝 Contributing

PRs welcome! Please:
	1.	Fork → create feature branch.
	2.	Follow the Execution Plan steps (# in prompt_plan.md).
	3.	Run pnpm lint && pnpm test && pnpm test:e2e.
	4.	Submit a pull request with clear description & linked spec section.

All code must pass CI and adhere to the project’s ESLint & Prettier rules.

⸻

📝 License

This project is licensed under the MIT License.
All bundled sample assets are CC-BY 4.0 unless noted otherwise.

⸻

💬 Support & Community
	•	Discord: discord.gg/your-server
	•	Issues / Feature Requests: https://github.com/your-org/jrpg-tool-suite/issues
	•	Docs & Tutorials: /docs/user_guide.md

Happy world-building! 🌟


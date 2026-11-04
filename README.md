<div align="center">

# O'Reilly Interactive Sprint Builder 

**Turn any technical topic, lecture, or syllabus into a self-contained, O'Reilly-styled Arabic interactive engineering handbook in a single HTML file.**

[![License: MIT](https://img.shields.io/badge/License-MIT-crimson.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Output: Single-File HTML](https://img.shields.io/badge/Output-Single--File_HTML5-006677?style=flat-square)](#)
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero_(Vanilla_JS)-2ea44f?style=flat-square)](#)
[![Language: RTL Arabic + LTR Code](https://img.shields.io/badge/Layout-Bilingual_(RTL_Arabic_%2B_LTR_Code)-d97706?style=flat-square)](#)

[📖 **How It Works**](#-core-workflow--commands) · [⚡ **Installation**](#-installation--setup) · [🧠 **Recommended Models (Argon)**](#-recommended-models--execution-strategy)

</div>

---

## 💡 Why This Skill Exists

Reading static PDFs, scattered lecture slides, or long walls of AI-generated chat text is passive and easy to forget. Technical mastery requires **experimentation, architectural trade-offs, and active recall**.

**`oreilly-interactive-sprint-builder`** transforms raw technical curricula, syllabus images, or engineering topics into rich, **single-file interactive HTML study sprints** inspired by classic **O'Reilly Media** editions.

Every generated Sprint is a 100% self-contained `.html` file that runs offline in any desktop or mobile browser—complete with custom Vanilla JS simulators, CLI emulators, diagnostic quizzes, a real-world troubleshooting cookbook, and automatic progress persistence via `localStorage`.

---

## ✨ Key Features

* 🎨 **Authentic O'Reilly Editorial Aesthetic:**
  * Signature Crimson (`#D3002D`), Editorial Paper (`#FAF8F5`), and Technical Teal (`#006677`) palette with seamless one-click **Slate Dark Mode (`#090D16`)**.
  * Custom inline `<svg>` woodcut-style animal illustrations tailored to each Sprint's theme (zero heavy Base64 bloat).
* 🌍 **Precision Bilingual Engineering Layout (RTL + LTR):**
  * Clear, deep **RTL Arabic (`dir="rtl"`)** explanations, architectural narratives, and analogies paired with strict **LTR (`dir="ltr"`, `.ltr-code`)** isolation for code blocks, terminal emulators, configuration files, and technical identifiers.
* 🧪 **Stateful Vanilla JS Interactive Labs (Every Chapter):**
  * No static theory dumps. Every chapter embeds a working interactive simulator—such as a Live CLI Emulator, Architectural Trade-off Matrix, Packet/Memory Inspector, Config Generator, or Bug Hunter.
* 🧠 **Built-in Active Recall & Diagnostics:**
  * **Chapter 0 Pre-Assessment:** 6 diagnostic questions targeting common engineering misconceptions before you begin.
  * **Per-Chapter Checkpoint Quizzes:** 4 deep-comprehension multiple-choice questions per chapter with instant visual feedback and detailed engineering explanations.
* 🧰 **Production Field Guide (Cookbook Modal) & Capstone:**
  * Includes an interactive **Capstone Project Checklist** and a slide-out **Cookbook Drawer (`درج السيناريوهات العملية`)** featuring 4–6 real-world production troubleshooting recipes.
* 💾 **Automatic `localStorage` Persistence:**
  * Remembers completed chapters, quiz answers, dark mode preferences, and capstone checkboxes across page reloads using a unique `SPRINT_STORAGE_KEY`.
* 📱 **Mobile-First & Touch-Ready:**
  * Off-canvas collapsible sidebar drawer (`#sidebarNav`), responsive table wrappers, and touch-friendly interactive controls (`min-height: 38px`) with zero horizontal overflow.

---

## 🛠️ Core Workflow & Commands

The skill operates across three specialized modes using slash commands:

| Command | Mode | Purpose |
| :--- | :--- | :--- |
| **`/details [topic / syllabus]`** | **Curriculum Architect (Chat Mode)** | Analyzes a topic, lecture notes, or syllabus image and designs a structured Sprint Blueprint (animal theme, Chapter 0 pre-assessment, Chapters 1–7 breakdown, interactive simulator specs, quizzes, and Cookbook scenarios). Outputs a ready-to-copy `/build` prompt block. |
| **`/build [Sprint blueprint]`** | **Full HTML Generator (Task Mode)** | Generates the complete, runnable, zero-dependency `<!DOCTYPE html>` file inside a single code block with zero truncation or `// TODO` placeholders. |
| **`/lab [description]`** | **Simulator Builder (Patch Mode)** | Creates or upgrades a specific interactive Vanilla JS lab or simulator module to drop into an existing Sprint file. |
| **`/fix [description]`** | **Targeted Patch (Patch Mode)** | Fixes layout issues, updates RTL/LTR alignment, or refines a specific section/simulator without regenerating the entire handbook from scratch. |

---

## 🚀 End-to-End Usage Example

### Step 1: Plan the Curriculum (`/details`)
Ask the agent to architect your topic:

```text
/details Docker Containers, Image Layers, Networking, and Production Security
```

> **What happens:** The AI breaks the topic down into a structured 7-chapter Sprint Blueprint, defines the custom interactive simulator for each chapter (e.g., *Interactive Dockerfile Layer Cache Simulator*, *Bridge vs. Host Network Packet Router*), and provides a ready-to-copy `/build` prompt at the end.

### Step 2: Generate the Interactive Handbook (`/build`)
Open a **fresh chat session** (recommended to maximize output token capacity) and paste the generated `/build` block:

```text
/build [Paste the Sprint Blueprint generated from Step 1]
```

> **What happens:** The AI dedicates 100% of its output token budget to generating the complete, self-contained `.html` file. Save it as `sprint-docker.html` and open it directly in any browser!

### Step 3: Upgrade or Patch a Section (`/lab` or `/fix`)
Want to enhance a simulator without rebuilding the entire file?

```text
/lab Create an interactive Kubernetes Pod resource request/limit OOMKilled simulator for Chapter 3
```

---

## 📦 Repository Structure

The repository is kept minimal and focused strictly on the executable skill:

```text
oreilly-interactive-sprint-builder/
├── README.md                        # Documentation, commands, and execution guide
├── SKILL.md                         # Core Agent Skill definition and workflow rules
└── references/
    ├── html-architecture.md         # Strict CSS, DOM structure, JS state, and responsive specs
    └── sprint_6_example.html        # Gold-standard reference implementation
```

---

## ⚡ Installation & Setup

### Option 1: Native Agent Skill (Gemini / Claude Code / Cursor)
If your environment supports modular Agent Skills (`SKILL.md` + `references/`):
1. Clone this repository into your skills directory:
   ```bash
   git clone [https://github.com/https://github.com/Hazem-Soliman-dev/Interactive-Sprint-Builder.git](https://github.com/Hazem-Soliman-dev/Interactive-Sprint-Builder.git)
   ```
2. Trigger the skill anytime in chat using `/details`, `/build`, `/lab`, or `/fix`.

### Option 2: Custom Gems / Claude Projects / Custom GPTs
1. Create a new **Gem** (Gemini), **Project** (Claude), or **Custom GPT** (OpenAI).
2. Paste the contents of `SKILL.md` into the **System Instructions** field.
3. Attach `references/html-architecture.md` and `references/sprint_6_example.html` under the **Knowledge / Project Files** section.

### Option 3: Direct Chat Prompting (Arena / Web Chat UI)
If using a standard chat window without a skill engine:
1. Attach or copy `SKILL.md` along with `references/html-architecture.md` in your initial message.
2. Run your `/details` and `/build` commands directly.

---

## 🧠 Recommended Models & Execution Strategy

Because `/build` generates a **complete, production-grade single-file application** (7 chapters + custom CSS + 7 interactive Vanilla JS simulators + quizzes + Cookbook modal + `localStorage` engine) in a **single pass**, your model selection is critical.

### 🏆 Why High-Endurance Coding Models Like **Argon** Excel
When executing `/build`, we strongly recommend high-output, long-context coding and reasoning models such as **Argon** (and leading frontier reasoning models):

1. **Zero-Truncation Endurance (1,500+ Lines in One Pass):**
   Standard models often fatigue after 400–500 lines and insert lazy placeholders like `<!-- Repeat for Chapters 4-7 -->` or `// TODO: implement simulator`. **Argon** strictly respects the non-truncation constraint, writing out all 7 chapters, quiz explanations, and complete JavaScript logic from `<!DOCTYPE html>` to `</html>`.
2. **Complex Stateful Vanilla JS Generation:**
   Building 7 distinct interactive simulators in a single file without ID collisions or broken event listeners requires strong code synthesis. **Argon** reliably wires DOM controls, dynamic visual feedback, and `localStorage` persistence cleanly on the first run.
3. **Strict RTL/LTR Bidirectional Hygiene:**
   Mixing Arabic technical prose with embedded CLI emulators and code blocks can easily break flexbox/grid layouts on mobile. High-precision models follow the `references/html-architecture.md` rules (`dir="rtl"` vs. `.ltr-code`) without layout drift.

### 💡 Best Practices for Maximum Quality
* **Separate Planning from Building (The 2-Session Rule):**
  Always run `/details` in one session, copy the resulting Sprint Blueprint, and run `/build` in a **brand-new chat session**. This guarantees 100% of the model's context and output token ceiling is dedicated to generating the HTML file.
* **Keep Sprints Focused:**
  If a curriculum is massive (e.g., an entire university course), let `/details` split it into **Multiple Sprints** (Sprint 1, Sprint 2, Sprint 3) and run `/build` for one Sprint at a time so every chapter gets deep explanations and rich simulators.

---

## 🤝 Contributing

Contributions, new interactive simulator templates, and architectural improvements are welcome!
1. Fork the repository.
2. Submit your improvements to `SKILL.md` or `references/html-architecture.md`.
3. Open a Pull Request.

---

## 📄 License

Distributed under the **MIT License**. Free to use, modify, and share for learners, educators, and software engineers everywhere.

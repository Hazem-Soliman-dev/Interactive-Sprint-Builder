---
name: oreilly-interactive-sprint-builder
description: Plan and build interactive Arabic O'Reilly-style Single-File HTML study sprints and technical handbooks. Trigger whenever the user uses commands like /details, /build, /lab, or /fix, or asks to design, plan, or generate an O'Reilly interactive study guide, sprint handbook, or technical curriculum in HTML.
---

# O'Reilly Interactive Sprint Builder

Design and generate comprehensive, single-file interactive Arabic technical handbooks modeled after O'Reilly Media editions, complete with interactive Vanilla JS simulators, terminal emulators, diagnostic pre-assessments, chapter quizzes, cookbook drawers, dark mode, mobile responsiveness, and `localStorage` state persistence.

## When to Use

- The user invokes `/details [topic or curriculum]` to plan and structure a technical topic or syllabus into interactive Sprints.
- The user invokes `/build [Sprint blueprint]` to generate the complete, self-contained interactive HTML file for a specific Sprint.
- The user invokes `/lab [description]` or `/fix [description]` to create, upgrade, or patch an interactive simulator or section inside an existing Sprint HTML file.
- The user shares syllabus images, lecture notes, or technical topics and asks to turn them into an O'Reilly interactive study guide.

## Core Workflow & Commands

Operate in one of three modes depending on the user's command:

### Mode 1: `/details` (Curriculum Architecture & Sprint Planning - Chat Mode)

When the user runs `/details` (or asks to plan a topic before building):

1. **Analyze the Scope**: Break down the provided topic, technology, or syllabus image into logical **Sprints** (or focus deeply on a single Sprint if specified).
2. **Design Each Sprint Blueprint**: For each Sprint, outline in clear Arabic with English technical terms:
   - **Sprint Metadata**: Title, subtitle, O'Reilly symbolic animal (Woodcut theme), and core engineering objective.
   - **Chapter 0 (Overview & Pre-Assessment)**: Summary of the roadmap and 6 diagnostic pre-assessment questions (covering common misconceptions and architectural trade-offs).
   - **Chapters 1 to 7 (Deep-Dive Engineering Chapters)**:
     - Detailed sub-sections: The engineering problem, "Under the Hood" mechanics, production best practices, and O'Reilly Callouts (`Tip`, `Note`, `Warning`).
     - **Interactive Lab / Simulator Specification**: Define the exact interactive tool for each chapter (e.g., Live CLI Emulator, Architectural Trade-off Matrix, Memory/Packet Inspector, Config Generator, or Bug Hunter).
     - **Chapter Checkpoint Quiz**: 4 multiple-choice questions testing deep comprehension.
   - **Capstone Project & Field Guide (Cookbook)**:
     - Step-by-step interactive project checklist (`Capstone Checklist`).
     - 4 to 6 real-world production scenarios and troubleshooting recipes for the Cookbook Modal (`درج السيناريوهات العملية`).
3. **Output Ready-to-Copy Blueprints**: End the response with a clean, copy-pasteable `/build` prompt block for each Sprint so the user can paste it directly into a fresh chat session to maximize output token capacity.

### Mode 2: `/build` (Full Single-File HTML Generation - Task Mode)

When the user runs `/build` with a Sprint plan or topic:

1. **Strict Single-File Output**: Output the complete, runnable, self-contained `<!DOCTYPE html>` document inside a single ```html code block without conversational filler before or after, dedicating 100% of the token budget to deep technical content and working code.
2. **Enforce the Reference Architecture**: Refer to `references/html-architecture.md` and `references/sprint_6_example.html` to ensure every UI component, CSS rule, mobile drawer behavior, and JavaScript state handler matches the exact specification.
3. **Never Truncate Content**: Write out all chapters, code snippets, quizzes, and interactive simulators in full. Never use placeholders like `<!-- Add more chapters here -->` or `// TODO`.
4. **Embed Lightweight SVG Woodcut Illustrations**: Always use clean, high-contrast inline `<svg>` woodcut-style animal illustrations rather than multi-kilobyte Base64 strings so token budget goes toward rich educational explanations and interactive labs.
5. **Persist Progress with `localStorage`**: Include the automatic `localStorage` persistence layer keyed by a unique `SPRINT_STORAGE_KEY` (e.g., `oreilly_sprint_java_01`) so completed chapters, quiz answers, dark mode preference, and capstone checkboxes survive page reloads on desktop and mobile.

### Mode 3: `/lab` or `/fix` (Targeted Simulator & Section Upgrade)

When the user runs `/lab` or `/fix`:

1. Generate either the standalone drop-in HTML + JS module for the requested interactive simulator/section, or regenerate the updated full file if requested.
2. Ensure all interactive controls use touch-friendly targets (`min-height: 38px`), RTL-safe layout with `.ltr-code` for code blocks, and dark-mode compatible classes.

## Mandatory Design & Engineering Standards

- **Language & Direction**: RTL Arabic (`dir="rtl" lang="ar"`) for explanations, analogies, and architectural narratives; strict LTR (`dir="ltr"` and `.ltr-code`) for all code blocks, CLI commands, configuration files, and technical identifiers.
- **O'Reilly Color & Typography System**:
  - Primary Crimson (`#D3002D`), Editorial Paper Background (`#FAF8F5`), Dark Mode Slate (`#090D16`), and Technical Teal (`#006677`).
  - Fonts: `Cairo` and `Inter` for UI/prose, `JetBrains Mono` for code and simulators.
- **Mobile-First Responsiveness**:
  - Prevent horizontal overflow (`overflow-x: hidden` on `html, body`).
  - Collapsible off-canvas sidebar drawer (`#sidebarNav`) with backdrop (`#mobileDrawerBackdrop`) on viewports `< 1024px`.
  - Responsive scrollable wrappers around all comparison tables and wide diagrams.
- **Interactive Richness**:
  - Every chapter must include a functional, stateful Vanilla JS lab (not static text).
  - Pre-assessment (6 questions) and per-chapter quizzes (4 questions each) must show immediate visual feedback (green/red borders) and a detailed Arabic engineering explanation (`#exp-...`).

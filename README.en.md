# Quill-rium β

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Beta](https://img.shields.io/badge/status-beta-blue)
![Powered by Claude Code](https://img.shields.io/badge/Powered%20by-Claude%20Code-blueviolet)

> **"Write your short story — all the way to the end."**

A short fiction writing framework that runs inside Claude Code.
From interview to scene writing, evaluation, and final re-rendering.

[日本語 README](README.md)

---

## Quick Start

### Requirements

- [Claude Code](https://claude.ai/code) must be installed

### 1. Clone the repository

```bash
git clone https://github.com/mizukiamano099-ops/Quillrium
cd Quillrium
```

### 2. Launch Claude Code

```bash
claude
```

### 3. Start talking

```
I want to write a new story.
```

An interview begins. Claude helps you design the title, premise, characters, and structure — then moves straight into scene writing.

---

## Basic Flow

```
Start talking
    ↓
PHASE 1: Interview
  Title / Genre / Premise / Characters / Structure / Volume
    ↓
PHASE 2: Scene Writing
  Otasuke suggestions (3 options) → You choose → Claude writes → Bucket Man review
    ↓
  (All scenes complete)
    ↓
PHASE 4: Opus Re-render (optional)
  Review Sonnet drafts → Re-write with Opus → Higher quality output
```

Each scene is saved automatically to `Story/{Title}/scenes/scene_N.md`.
Git commit and push are handled automatically.

---

## Feature Reference

### Volume Zones

Instead of a character count, Quill-rium uses volume zones — a feel-based way to set scope.
If you say "about X,000 characters," Claude converts it to a zone and confirms.

| Zone | Feel | Scenes |
|---|---|---|
| Flash fiction | Complete in one sitting | 1–2 |
| Short story | Satisfying as a standalone read | 3–5 |
| Novella | Substantial standalone read | 6–10 |
| Short series | Episodic, each chapter self-contained | Decided later |

---

### Phases

| Phase | What it does | How to trigger |
|---|---|---|
| PHASE 1 | Interview & structure design | `I want to write a new story.` |
| PHASE 2 | Scene writing | `Write scene N.` |
| PHASE 3 | Plot output (for handwriting) | `Output the plot.` |
| PHASE 4 | Opus batch re-render | `Re-render with Opus.` |

---

### Otasuke Mode (Writing Assistant)

Before each scene, Claude offers three directions to choose from.

```
A: Flow-first   ── The straightforward path to the scene's goal
B: Conflict-first── An angle that surfaces the character's wants/but tension
C: Emotion-first ── A riskier choice that builds toward the climax
```

Pick one, or say "I want it to feel like this" — then Claude writes.
Say "Otasuke OFF" to disable suggestions for the session.

---

### Bucket Man Review

After each scene, the EVAL_CHAR (default: Bucket Man) gives in-character critique.

```
"This character has no idea what she's feeling. But the reader sees everything."

★ Character consistency : ★★★
★ Scene function        : ★★★
★ Readability           : ★★☆

→ The commute section runs a little long — could be trimmed
```

Change the EVAL_CHAR field in QUILL_STATE to use a character from your own story.
Having your own character critique their own story is the intended experience.

---

### Sonnet Draft → Opus Re-render

For maximum output quality, use this two-stage flow.

```
Draft all scenes with Sonnet (fast, cheap — validate structure first)
    ↓
Switch to Opus and run PHASE 4
    ↓
Drafts are preserved as scene_N_draft.md (compare or roll back anytime)
```

Claude will suggest switching to Opus at two moments: after the interview and after all scenes are drafted.

---

### Directory Structure

```
Quill-rium/
├── CLAUDE.md              ← Instructions for Claude Code (editable)
├── engines/               ← Engine definitions (do not edit)
├── characters/
│   └── eval_cast/         ← Shared reviewer characters
├── templates/             ← Boilerplate files (do not edit)
├── samples/               ← Tutorial sample project
└── Story/
    └── {Title}/           ← Auto-generated per project
        ├── state/
        │   └── current.md ← QUILL_STATE (auto-managed)
        ├── scenes/
        ├── characters/
        │   └── main_cast/
        └── plots/
```

---

## About This Beta

This is a **beta release**. Feedback and bug reports are welcome.

- Feedback → [Issues](https://github.com/mizukiamano099-ops/Quillrium/issues)
- See `samples/osananajimi_bucket/` for a sample project walkthrough
- **Note:** The sample project and all in-app text are currently in Japanese only. English sample content is on the roadmap — apologies for the inconvenience.

---

*Quill-rium β — Powered by Claude Code*

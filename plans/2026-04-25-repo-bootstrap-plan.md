# Repo Bootstrap Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the initial Godot project repository skeleton, add navigable `AGENTS.md` guidance in key directories, and commit robust root `.gitignore` / `.gitattributes` rules.

**Architecture:** This plan creates the repository in layers: scaffold directories first, add root navigation next, then add per-directory guidance, and finally install version-control rules plus verification. The work keeps documentation local to each directory via relative Markdown links and treats `plans/` as the persistent record for future implementation plans.

**Tech Stack:** Markdown, Git, Git LFS conventions, shell commands, Godot-oriented repository structure

---

## File Structure Map

**Create directories:**

- `addons/`
- `assets/`
- `assets/audio/`
- `assets/audio/bgm/`
- `assets/audio/sfx/`
- `assets/audio/voices/`
- `assets/models/`
- `assets/raw/`
- `assets/shaders/`
- `assets/sprites/`
- `assets/textures/`
- `builds/`
- `data/`
- `data/config/`
- `data/localization/`
- `data/tables/`
- `docs/design/`
- `plans/`
- `scenes/`
- `scenes/characters/`
- `scenes/levels/`
- `scenes/main/`
- `scenes/ui/`
- `scripts/`
- `scripts/autoload/`
- `scripts/core/`
- `scripts/gameplay/`
- `scripts/ui/`
- `tools/`

**Create files:**

- `README.md`
- `AGENTS.md`
- `assets/AGENTS.md`
- `data/AGENTS.md`
- `docs/AGENTS.md`
- `plans/AGENTS.md`
- `scenes/AGENTS.md`
- `scripts/AGENTS.md`
- `.gitignore`
- `.gitattributes`

**Reference files:**

- `docs/superpowers/specs/2026-04-25-repo-bootstrap-design.md`
- `docs/superpowers/specs/base.md`

### Task 1: Scaffold Repository Directories

**Files:**
- Create: `addons/`
- Create: `assets/audio/bgm/`
- Create: `assets/audio/sfx/`
- Create: `assets/audio/voices/`
- Create: `assets/models/`
- Create: `assets/raw/`
- Create: `assets/shaders/`
- Create: `assets/sprites/`
- Create: `assets/textures/`
- Create: `builds/`
- Create: `data/config/`
- Create: `data/localization/`
- Create: `data/tables/`
- Create: `docs/design/`
- Create: `plans/`
- Create: `scenes/characters/`
- Create: `scenes/levels/`
- Create: `scenes/main/`
- Create: `scenes/ui/`
- Create: `scripts/autoload/`
- Create: `scripts/core/`
- Create: `scripts/gameplay/`
- Create: `scripts/ui/`
- Create: `tools/`

- [ ] **Step 1: Verify the target directories do not already exist unexpectedly**

```bash
find . -maxdepth 2 \( -path './scripts' -o -path './scenes' -o -path './assets' -o -path './data' -o -path './plans' \) | sort
```

Expected: Only already-known paths appear; missing scaffold directories are absent.

- [ ] **Step 2: Create the directory skeleton in one pass**

```bash
mkdir -p \
  addons \
  assets/audio/bgm \
  assets/audio/sfx \
  assets/audio/voices \
  assets/models \
  assets/raw \
  assets/shaders \
  assets/sprites \
  assets/textures \
  builds \
  data/config \
  data/localization \
  data/tables \
  docs/design \
  plans \
  scenes/characters \
  scenes/levels \
  scenes/main \
  scenes/ui \
  scripts/autoload \
  scripts/core \
  scripts/gameplay \
  scripts/ui \
  tools
```

- [ ] **Step 3: Verify the scaffold exists**

```bash
find . -maxdepth 3 \
  \( -path './addons' -o -path './assets' -o -path './assets/audio' -o -path './assets/audio/bgm' -o -path './data' -o -path './docs/design' -o -path './plans' -o -path './scenes/main' -o -path './scripts/autoload' -o -path './tools' \) \
  | sort
```

Expected: Output includes all explicitly checked scaffold paths.

- [ ] **Step 4: Commit the directory scaffold**

```bash
git add addons assets builds data docs plans scenes scripts tools
git commit -m "chore: scaffold repository directories"
```

### Task 2: Add Root Navigation Files

**Files:**
- Create: `README.md`
- Create: `AGENTS.md`

- [ ] **Step 1: Create `README.md` with repository entry guidance**

```markdown
# unity-sample

Godot 4.6 project bootstrap repository.

## Start Here

- Read [AGENTS.md](AGENTS.md) for repository-wide conventions and navigation.
- Read [repo bootstrap design](docs/superpowers/specs/2026-04-25-repo-bootstrap-design.md) for the confirmed structure design.
- Store future execution plans in [plans/](plans/).

## Directory Overview

- `scripts/` reusable scripts and systems
- `scenes/` instantiable scenes
- `assets/` imported runtime assets and raw source assets
- `data/` configuration and static tables
- `docs/` long-lived project documentation
- `plans/` implementation plans committed with the repository
```

- [ ] **Step 2: Create root `AGENTS.md` as the main navigation hub**

```markdown
# Repository Guide

## Purpose

This repository is a Godot 4.6 project bootstrap. Keep the structure readable, navigable, and easy to extend.

## Core Rules

- Put reusable scripts in `scripts/`.
- Put instantiable scenes in `scenes/`.
- Put configuration and static tables in `data/`.
- Put long-lived architecture and design notes in `docs/`.
- Put every implementation plan in `plans/`.
- Do not commit `.godot/` or exported build output.

## Directory Navigation

- [Scripts Guide](scripts/AGENTS.md)
- [Scenes Guide](scenes/AGENTS.md)
- [Assets Guide](assets/AGENTS.md)
- [Data Guide](data/AGENTS.md)
- [Docs Guide](docs/AGENTS.md)
- [Plans Guide](plans/AGENTS.md)

## Naming

- Use `snake_case` for files and directories when creating new assets or scripts.
- Use `PascalCase` for Godot class names.
- Use `snake_case` for GDScript functions and variables.

## Document Flow

- Design specs live in `docs/`.
- Execution plans live in `plans/`.
- Implementation lives in the domain directories above.
```

- [ ] **Step 3: Verify the root files render the intended navigation**

```bash
grep -n "Plans Guide\\|Directory Overview\\|Document Flow" README.md AGENTS.md
```

Expected: Matching lines confirm the root entry points exist.

- [ ] **Step 4: Commit the root navigation files**

```bash
git add README.md AGENTS.md
git commit -m "docs: add repository navigation guides"
```

### Task 3: Add `scripts/` and `scenes/` Guides

**Files:**
- Create: `scripts/AGENTS.md`
- Create: `scenes/AGENTS.md`

- [ ] **Step 1: Create `scripts/AGENTS.md`**

```markdown
# Scripts Guide

## Purpose

Use this directory for reusable scripts and systems.

## Put Here

- `autoload/` global singletons and startup scripts
- `core/` shared systems and low-level project logic
- `gameplay/` reusable gameplay scripts
- `ui/` reusable UI behavior scripts

## Do Not Put Here

- Scene-only scripts that are tightly coupled to a single scene file when colocating is clearer
- Imported assets
- Static configuration tables

## Links

- [Return to Repository Guide](../AGENTS.md)
- [Scenes Guide](../scenes/AGENTS.md)
```

- [ ] **Step 2: Create `scenes/AGENTS.md`**

```markdown
# Scenes Guide

## Purpose

Use this directory for `.tscn`-based instantiable content.

## Put Here

- `main/` entry scenes
- `levels/` level and map scenes
- `characters/` characters and interactable scene prefabs
- `ui/` UI scene prefabs

## Do Not Put Here

- Pure data tables
- Global reusable scripts better placed in `scripts/`
- Raw source art files

## Links

- [Return to Repository Guide](../AGENTS.md)
- [Scripts Guide](../scripts/AGENTS.md)
- [Data Guide](../data/AGENTS.md)
```

- [ ] **Step 3: Verify the cross-links between script and scene guides**

```bash
grep -n "Scenes Guide\\|Scripts Guide\\|Data Guide\\|Repository Guide" scripts/AGENTS.md scenes/AGENTS.md
```

Expected: Both files contain the intended relative links.

- [ ] **Step 4: Commit the script and scene guides**

```bash
git add scripts/AGENTS.md scenes/AGENTS.md
git commit -m "docs: add scripts and scenes guides"
```

### Task 4: Add `assets/`, `data/`, `docs/`, and `plans/` Guides

**Files:**
- Create: `assets/AGENTS.md`
- Create: `data/AGENTS.md`
- Create: `docs/AGENTS.md`
- Create: `plans/AGENTS.md`

- [ ] **Step 1: Create `assets/AGENTS.md`**

```markdown
# Assets Guide

## Purpose

Use this directory for source art archives and runtime asset files.

## Put Here

- `raw/` source files that artists or tools export from
- `textures/` runtime textures and UI imagery
- `sprites/` sprite sheets and animation image assets
- `audio/` voice, sound effect, and background music files
- `models/` 3D models
- `shaders/` shader source files and related shader assets

## Do Not Put Here

- Gameplay logic scripts
- Level scene files
- Static data tables

## Links

- [Return to Repository Guide](../AGENTS.md)
- [Data Guide](../data/AGENTS.md)
```

- [ ] **Step 2: Create `data/AGENTS.md`**

```markdown
# Data Guide

## Purpose

Use this directory for configuration, localization, and static gameplay tables.

## Put Here

- `config/` project-wide configuration files
- `tables/` balance tables and other static tabular data
- `localization/` translatable text assets

## Do Not Put Here

- Level scenes
- Runtime art assets
- Reusable scripts

## Links

- [Return to Repository Guide](../AGENTS.md)
- [Scenes Guide](../scenes/AGENTS.md)
- [Assets Guide](../assets/AGENTS.md)
```

- [ ] **Step 3: Create `docs/AGENTS.md`**

```markdown
# Docs Guide

## Purpose

Use this directory for long-lived reference documentation.

## Put Here

- `design/` product or game design notes
- `superpowers/specs/` approved design specs

## Do Not Put Here

- Implementation plans that belong in `plans/`
- Runtime assets
- Gameplay scripts

## Links

- [Return to Repository Guide](../AGENTS.md)
- [Plans Guide](../plans/AGENTS.md)
```

- [ ] **Step 4: Create `plans/AGENTS.md`**

```markdown
# Plans Guide

## Purpose

Use this directory to store every implementation plan committed with the repository.

## Naming

- Use `YYYY-MM-DD-topic-plan.md`.
- Keep topic names short, descriptive, and lowercase.

## Minimum Plan Contents

- goal
- scope
- implementation steps
- verification steps

## Links

- [Return to Repository Guide](../AGENTS.md)
- [Docs Guide](../docs/AGENTS.md)
```

- [ ] **Step 5: Verify guide coverage and links**

```bash
grep -n "Return to Repository Guide\\|Plans Guide\\|Docs Guide\\|Assets Guide\\|Data Guide" assets/AGENTS.md data/AGENTS.md docs/AGENTS.md plans/AGENTS.md
```

Expected: Each guide contains its intended links and role-specific headings.

- [ ] **Step 6: Commit the remaining directory guides**

```bash
git add assets/AGENTS.md data/AGENTS.md docs/AGENTS.md plans/AGENTS.md
git commit -m "docs: add repository directory guides"
```

### Task 5: Add Root `.gitignore`

**Files:**
- Create: `.gitignore`

- [ ] **Step 1: Write `.gitignore` with Godot, build, IDE, and OS exclusions**

```gitignore
# Godot cache and import artifacts
.godot/
*.import

# Export output
builds/
*.apk
*.aab
*.ipa
*.zip
*.tar
*.tar.gz

# Logs and temp files
*.log
*.tmp
*.temp

# macOS and Windows noise
.DS_Store
Thumbs.db

# IDE settings
.idea/
.vscode/*
!.vscode/extensions.json
!.vscode/settings.json
```

- [ ] **Step 2: Verify the critical ignore rules exist**

```bash
grep -n "^\\.godot/$\\|^builds/$\\|^\\.DS_Store$\\|^\\.idea/$" .gitignore
```

Expected: Matches for `.godot/`, `builds/`, `.DS_Store`, and `.idea/`.

- [ ] **Step 3: Check that `plans/` is not ignored**

```bash
grep -n "^plans/$" .gitignore || true
```

Expected: No output.

- [ ] **Step 4: Commit `.gitignore`**

```bash
git add .gitignore
git commit -m "chore: add repository gitignore"
```

### Task 6: Add Root `.gitattributes`

**Files:**
- Create: `.gitattributes`

- [ ] **Step 1: Write text normalization and Git LFS rules**

```gitattributes
# Normalize text files
*.md text eol=lf
*.gd text eol=lf
*.tscn text eol=lf
*.tres text eol=lf
*.res text eol=lf
*.cfg text eol=lf
*.json text eol=lf
*.csv text eol=lf
*.shader text eol=lf

# Git LFS tracked binaries
*.png filter=lfs diff=lfs merge=lfs -text
*.jpg filter=lfs diff=lfs merge=lfs -text
*.jpeg filter=lfs diff=lfs merge=lfs -text
*.psd filter=lfs diff=lfs merge=lfs -text
*.bmp filter=lfs diff=lfs merge=lfs -text
*.tga filter=lfs diff=lfs merge=lfs -text
*.exr filter=lfs diff=lfs merge=lfs -text
*.mp3 filter=lfs diff=lfs merge=lfs -text
*.wav filter=lfs diff=lfs merge=lfs -text
*.ogg filter=lfs diff=lfs merge=lfs -text
*.flac filter=lfs diff=lfs merge=lfs -text
*.glb filter=lfs diff=lfs merge=lfs -text
*.gltf filter=lfs diff=lfs merge=lfs -text
*.fbx filter=lfs diff=lfs merge=lfs -text
*.obj filter=lfs diff=lfs merge=lfs -text
*.blend filter=lfs diff=lfs merge=lfs -text
*.mp4 filter=lfs diff=lfs merge=lfs -text
*.mov filter=lfs diff=lfs merge=lfs -text
*.webm filter=lfs diff=lfs merge=lfs -text
*.kra filter=lfs diff=lfs merge=lfs -text
*.aseprite filter=lfs diff=lfs merge=lfs -text
```

- [ ] **Step 2: Verify representative rules exist**

```bash
grep -n "\\*\\.md text eol=lf\\|\\*\\.gd text eol=lf\\|\\*\\.png filter=lfs\\|\\*\\.wav filter=lfs\\|\\*\\.glb filter=lfs" .gitattributes
```

Expected: Matches for text normalization plus image, audio, and model LFS rules.

- [ ] **Step 3: Commit `.gitattributes`**

```bash
git add .gitattributes
git commit -m "chore: add gitattributes and lfs rules"
```

### Task 7: Final Verification Pass

**Files:**
- Modify: `README.md`
- Modify: `AGENTS.md`
- Modify: `assets/AGENTS.md`
- Modify: `data/AGENTS.md`
- Modify: `docs/AGENTS.md`
- Modify: `plans/AGENTS.md`
- Modify: `scenes/AGENTS.md`
- Modify: `scripts/AGENTS.md`
- Modify: `.gitignore`
- Modify: `.gitattributes`

- [ ] **Step 1: Print the final tree for the created structure**

```bash
find . -maxdepth 3 \
  \( -path './.git' -o -path './.godot' \) -prune -o \
  -print | sort
```

Expected: Output includes the created root files and all planned directories.

- [ ] **Step 2: Validate key relative links resolve to existing files**

```bash
test -f AGENTS.md \
  && test -f scripts/AGENTS.md \
  && test -f scenes/AGENTS.md \
  && test -f assets/AGENTS.md \
  && test -f data/AGENTS.md \
  && test -f docs/AGENTS.md \
  && test -f plans/AGENTS.md
```

Expected: Command exits with status `0`.

- [ ] **Step 3: Review git status before handoff**

```bash
git status --short
```

Expected: Only the newly created repository bootstrap files appear, with no unexpected cache files.

- [ ] **Step 4: Create the final handoff commit**

```bash
git add .
git commit -m "chore: bootstrap godot repository structure"
```

## Self-Review

- Spec coverage check: tasks cover directory scaffold, root guidance, per-directory guidance, `plans/`, `.gitignore`, `.gitattributes`, and verification.
- Placeholder scan: no `TODO`, `TBD`, or unresolved path placeholders remain.
- Consistency check: all guide links point to files created by the plan, and `plans/` is treated as a committed first-class directory throughout.

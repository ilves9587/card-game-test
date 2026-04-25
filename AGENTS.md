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

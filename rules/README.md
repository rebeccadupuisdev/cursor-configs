# Cursor Rules — Naming & Creation Guide

Cursor rules enforce consistent AI behavior across projects and use cases. They are **optional, granular instructions** that modify AI responses in specific contexts—similar to ESLint rules for code. They shape the *how* of AI interactions without changing underlying decision-making.

**Global rules** (in `~/.cursor/rules/`) are general-purpose rules that apply across all projects — things like preferred coding style, communication tone, or universal conventions.

**Project rules** (in `.cursor/rules/` within a project) are project-specific and should reflect the conventions, architecture, and requirements unique to that codebase.
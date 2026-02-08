# Cursor Personas — Naming & Creation Guide

This repository uses **Cursor personas** as opt‑in AI behavior rules to improve consistency, learning, and developer experience.

Personas are treated like **developer tooling** (similar to linters or editor config): they shape *how* the AI helps, not *what* it decides.

---

## 1. Naming Convention

All personas follow this format:

```
<scope>.<intent>[.<mode>]
```

Examples:

* `learn.tutor`
* `code.review.strict`
* `debug.trace.stepwise`
* `code.generate.fast`

### Why this matters

* Makes personas **discoverable and sortable**
* Prevents overlapping or vague personas
* Keeps behavior predictable across the team

---

## 2. Scopes (What kind of task?)

Scopes describe the **domain of work** the persona applies to. Use a small, shared vocabulary.

| Scope    | Description                              |
| -------- | ---------------------------------------- |
| `learn`  | Learning, onboarding, skill building     |
| `code`   | Writing, refactoring, reviewing code     |
| `debug`  | Bug investigation and failure analysis   |
| `docs`   | Documentation, explanations, translation |
| `design` | Architecture and system design           |
| `test`   | Testing, QA, edge cases                  |
| `ops`    | DevOps, infrastructure, deployment       |
| `meta`   | Process, standards, repo‑level rules     |

**Rule:** Don’t invent new scopes casually. If you add one, document it here.

## Domain Qualifiers (Optional)

Some personas include a **domain qualifier** between scope and intent to narrow the context
(e.g. `ml`, `python`).

Format:
```
<scope>.<domain>.<intent>
```

Examples:
- `learn.ml.tutor`
- `learn.ml.socratic`
- `code.python.review`

### When to use a domain qualifier

Use a domain qualifier when:
- The domain has **distinct concepts, vocabulary, or mental models**
- Guidance would change meaningfully without the qualifier

`ml` is a valid domain qualifier because it introduces:
- Mathematical notation and assumptions
- Statistical reasoning
- Model evaluation concepts (losses, metrics, validation)
- Experimentation workflows distinct from general programming

### When *not* to use one

Do not add a domain qualifier if:
- The behavior is general-purpose
- The domain does not significantly affect reasoning or output


---

## 3. Intents (What does the persona optimize for?)

The intent is the **core behavior** of the persona. Each persona should have *one* clear intent.

| Intent      | Description                       |
| ----------- | --------------------------------- |
| `tutor`     | Teach and explain step‑by‑step    |
| `review`    | Critique and suggest improvements |
| `generate`  | Produce working output quickly    |
| `explain`   | Clarify concepts or documentation |
| `trace`     | Follow execution step‑by‑step     |
| `audit`     | Look for risks, bugs, or gaps     |
| `optimize`  | Improve performance or clarity    |
| `translate` | Convert docs/specs into code      |
| `socratic`  | Teach by asking guided questions instead of giving direct answers |

If a persona needs two intents, split it into two personas.

Socratic intent is about **method**, not tone.
The goal is to force reasoning, trade-off analysis, and articulation of understanding.

---

## 4. Modes (Optional modifiers)

Modes are optional and should be used **sparingly**. They modify *how* the intent is applied.

| Mode           | Description                      |
| -------------- | -------------------------------- |
| `strict`       | Enforce rules, no shortcuts      |
| `gentle`       | Supportive, learning‑first       |
| `fast`         | Minimal explanation, fast output |
| `stepwise`     | One step at a time               |
| `production`   | Conservative, real‑world safe    |
| `experimental` | Exploratory, not hardened        |

Examples:

* `code.review.strict`
* `learn.tutor.gentle`
* `debug.trace.stepwise`

---

## 5. File Structure

Persona filenames must **exactly match** their persona name:

```
.cursor/personas/
├─ learn.tutor.md
├─ code.review.strict.md
├─ debug.trace.stepwise.md
```

This prevents duplication and confusion.

---

## 6. How to Create a New Persona

### Step 1 — Decide if a new persona is needed

Create a new persona only if:

* The behavior is **reusable**
* The behavior is **meaningfully different** from existing personas
* Toggling it on/off makes sense

Do **not** create personas for personal preferences or temporary moods.

---

### Step 2 — Choose a name

Ask:

1. What *kind* of task is this? → **Scope**
2. What is the AI optimizing for? → **Intent**
3. Does it need a modifier? → **Mode (optional)**

Example:

* Teaching a new framework → `learn.tutor`
* Enforcing architecture rules → `code.review.strict`

---

### Step 3 — Write the persona file

Persona files should include:

* A short description
* Clear behavioral rules
* When to use / when not to use

Skeleton:

```md
---
description: <one‑line summary>
alwaysApply: false
---

# <Persona Name>

## How to behave
- …

## When to use
- …
```

**Rules:**

* Keep language concrete and actionable
* Describe behavior, not personality
* Avoid vague terms like “be helpful” or “act senior”

---

## 7. Usage Guidelines

* Personas are **opt‑in** unless explicitly stated otherwise
* Enable them intentionally for a task, then disable
* Expect different personas to produce different outputs

If output feels wrong, first check which persona is active.

---

## 8. Design Principle (Non‑negotiable)

> Personas describe **behavior**, not **identity**.

Bad ❌

* `senior-dev`
* `nice-helper`
* `grumpy-reviewer`

Good ✅

* `code.review.strict`
* `learn.tutor`
* `debug.trace.stepwise`
* `learn.ml.socratic`

## Special Rules for Socratic Personas

Socratic personas intentionally **do not provide direct answers by default**.

They should:
- Ask leading questions
- Prompt the user to explain their reasoning
- Surface trade-offs and assumptions
- Offer hints only when the user is stuck or explicitly asks

They should *not*:
- Dump final solutions unprompted
- Provide ready-made code unless requested
- Shortcut the reasoning process

**Rationale:**  
Socratic personas are designed for deep understanding (exams, interviews, fundamentals),
not speed or copy-paste productivity.


---

## 9. Maintenance

* Review personas periodically
* Deprecate unused or overlapping personas

Small, clear personas scale better than clever ones.

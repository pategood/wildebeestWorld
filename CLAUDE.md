# Claude Code Game Studios -- Game Studio Agent Architecture

Indie game development managed through 49 coordinated Claude Code subagents.
Each agent owns a specific domain, enforcing separation of concerns and quality.

**This repo is the framework itself** — agent definitions, skills, hooks, rules,
and templates. It is NOT a game. Actual game source code lives in `src/` (empty
until `/setup-engine` and `/dev-story` are run). The "build/test" equivalent for
this meta-project is `/skill-test` (see Framework Validation below).

## Technology Stack

- **Engine**: [CHOOSE: Godot 4 / Unity / Unreal Engine 5]
- **Language**: [CHOOSE: GDScript / C# / C++ / Blueprint]
- **Version Control**: Git with trunk-based development
- **Build System**: [SPECIFY after choosing engine]
- **Asset Pipeline**: [SPECIFY after choosing engine]

> **Note**: Engine-specialist agents exist for Godot, Unity, and Unreal with
> dedicated sub-specialists. Use the set matching your engine.

## Project Structure

@.claude/docs/directory-structure.md

## Engine Version Reference

@docs/engine-reference/godot/VERSION.md

## Technical Preferences

@.claude/docs/technical-preferences.md

## Coordination Rules

@.claude/docs/coordination-rules.md

## Collaboration Protocol

**User-driven collaboration, not autonomous execution.**
Every task follows: **Question -> Options -> Decision -> Draft -> Approval**

- Agents MUST ask "May I write this to [filepath]?" before using Write/Edit tools
- Agents MUST show drafts or summaries before requesting approval
- Multi-file changes require explicit approval for the full changeset
- No commits without user instruction

@docs/COLLABORATIVE-DESIGN-PRINCIPLE.md

> **First session?** If the project has no engine configured and no game concept,
> run `/start` to begin the guided onboarding flow.

## Coding Standards

@.claude/docs/coding-standards.md

## Context Management

@.claude/docs/context-management.md

**Session recovery**: After compaction or crash, read `production/session-state/active.md`
first — it contains the current task, progress, decisions, and open questions.

## Framework Validation

This project has no game code to compile. The equivalent of "build and test" is
skill validation:

| Command | Purpose |
|---------|---------|
| `/skill-test static all` | Validate all 73 skills for structural compliance |
| `/skill-test lint <name>` | Check a specific skill's YAML and required fields |
| `/skill-test catalog` | Verify all skills are indexed in the catalog |
| `bash .claude/hooks/validate-commit.sh '{}' '{}'` | Test the pre-commit hook manually |

After editing any file in `.claude/skills/`, the `validate-skill-change.sh` hook
will automatically remind you to run `/skill-test`.

---
name: coding-agent
description: Entry point and rule set for ALL software-coding tasks in a repository. Holds the coding rules (how to read code, the pre-change checklist, verification after a change, the completion report, the commit message format) and routes to sub-skills in references/. Currently covers codebase exploration with the codebase-memory MCP knowledge graph. Use whenever the user wants to read, explore, understand, change, build, test, review, debug or refactor code, write or fix tests, or get a commit message; also when the user wants to see a codebase's architecture or structure, find where a function is defined, find who calls a function or what it calls, trace a call chain, check dependencies, assess the impact of a change, find dead code or unused functions, find high fan-in or fan-out code, pick refactor candidates, or run a code-quality audit.
---

# Coding Agent

Entry point for every coding task. Read this whole file, then follow it.

- The rules below are the coding rules from `CLAUDE.md`. In this file there are two sections: 1 (Reading code) and 2 (The S.O.P. for modifying code, with parts 2.1 to 2.5). A "section" number in this file means a section of this file, except sections 7 and 8, which mean `CLAUDE.md`.
- Sections 7 (Answering the user's questions) and 8 (Honesty) stay in `CLAUDE.md`. They still apply to every coding task. The git and safety rules are in section 2.2 of this file.
- For tools that help you explore code (section 1), see [Sub-skills](#sub-skills) and [Tool availability](#tool-availability) at the end of this file.

---

## 1. Reading code

- Explore code with the structure-aware tools the project provides first (for example a code-graph or index server, or editor diagnostics). The project's `CLAUDE.md` names them.
- Fall back to `grep`, `find`, or a whole-file read only when no such tool exists, when it does not cover the file, or when you need an exact text match.
- Do not start with a whole-file read or a repo-wide search when a targeted lookup of one symbol would do.
- Before you rely on an index for code that changed recently, confirm the index is up to date. Re-index if it is stale.
- "No result" does **not** mean "does not exist". Cross-check with a second method before you conclude something is missing.
- When you fall back from a project tool to raw search, say so in your report.

---

## 2. The S.O.P. for modifying code

Follow the standard operating procedure below whenever you modify code (or tests, docs, or config).

### 2.1 Pre-change checklist

You **MUST NOT** edit or write code until you finish these steps.

1. **Explore the code first.** Before anything else on this list, explore the area you will change by following section 1 (Reading code).
2. **Restate the goal and acceptance criteria.** Write 1 to 3 sentences: what changes, and what "done" means. If the request is ambiguous, ask the user first. Do not guess and rewrite.
3. **Get an overview** of the area you will change: module boundaries, entry points, and dependency direction.
4. **Read the current implementation** of every function or component you will change.
5. **Map the blast radius.** List all callers of each symbol you will change. Before you change a signature, return shape, data format, or API schema, you **MUST inspect every caller**.
6. **Find existing conventions.** Look up comparable existing code (naming, error handling, comment density, type annotations). New code MUST match the surrounding style.
7. **Find the matching tests.** Locate the tests that cover this area and learn the contracts they pin.
8. **Check across layers.** If you change one side of a contract (for example an API and its callers, or a schema and its consumers), check the other side. Never change one side alone.
9. **Consider every code path.** If the code branches by environment, platform, edition, or configuration, consider every branch when you change it.

### 2.2 Scope discipline, prohibitions, and git and safety

- Change only what the task needs. If you find an unrelated problem, note it and report it at the end. **Do not fix it on the side.**
- Do not add features, abstraction layers, or dependencies that were not requested.
- You **MUST NOT** modify, delete, or skip (`skip` / `xfail`) an existing test to make it pass. If a test conflicts with the new requirement, report it with an explanation and let the user decide.
- You **MUST NOT** substitute "it should work" for real execution results.
- You **MUST NOT** hide failures. If a test fails, report the failure and attach the command output.
- Unless the user explicitly asks, **do not** run `git commit` or `git push`.
- Do not run destructive operations (`rm -rf`, `git reset --hard`, force push, deleting data) without first getting the user's confirmation.
- Do not write credentials, keys, or the contents of files the project marks as sensitive into commits, output, or logs.
- The shell working directory can drift during a session. Use absolute paths in commands, or `cd` inside the same command.

### 2.3 Verification steps

"The code is written" does not mean "done". **You MUST NOT claim the task is complete before you run verification.**
Use the test, type-check, lint, and build commands the project defines. Run them from the directory the project requires.

1. **Run the existing tests.** Cover at least the tests of the modules you changed. For cross-module changes, run the full suite.
2. **Add tests.** New behavior and bug fixes MUST have matching tests. Match the style of the existing tests.
3. **Run the type check and build** when the project has them and you touched code they cover.
4. **Check against the acceptance criteria.** Go back to the criteria you wrote in step 2 of section 2.1 and map **each one** to evidence (test name, command output, observed behavior).
5. **Assess the blast radius** of your change and confirm every affected symbol is expected. If something unexpected is affected, go back and check it.
6. **Run it for real.** When feasible, actually start it and use it, instead of relying on unit tests alone. Behavior that needs hardware or services you do not have cannot be verified locally. Mark it explicitly as **unverified**.
7. **Known failures.** If the project documents known failing tests, only those may fail. Any other failure is a **regression caused by your change**. Fix it before you report.

### 2.4 Completion report format (after a code change)

Every task in which you changed something ends with a report that contains:

```
Goal:        <one sentence>
Changes:     <file:line — what was done>
Verification:
  - <command> → <result, e.g. 153 passed>
  - Acceptance criterion 1: <met / not met> — <evidence>
  - Acceptance criterion 2: ...
Unverified:  <parts that cannot be verified locally, and why; "none" if none>
Leftovers:   <unrelated problems found but not handled; "none" if none>
```

After the report, add the commit message described in section 2.5.

### 2.5 Commit message format (after a code change)

Whenever the user asks you to change code (or tests, docs, or config) and you finish, you MUST give the user a commit message for that change. Put it at the end of your reply, after the completion report (section 2.4), in one code block so the user can copy it.

- Write the message only. Do not run `git commit` or `git push` unless the user explicitly asks (section 2.2 still applies).
- Give the message only after the work is done and verified (section 2.3). If part of the change is unverified, the message MUST NOT claim that it works.
- Write the message in English, even when the conversation is in another language.
- Describe only the change you made in this task. Do not include earlier or unrelated work.
- Section 7 does not shorten the body. The body gives the detail; the first line stays short.

Format:

```
<type>: <short summary>

<detailed description of the change>
```

**Type.** Use exactly one of these, in lowercase, followed by a colon and a space:

| Type | Use for |
|---|---|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes only |
| `style` | Formatting that does not change how the code runs (whitespace, semicolons, indentation) |
| `refactor` | A code restructure that neither fixes a bug nor adds a feature |
| `perf` | A performance improvement |
| `test` | Adding or changing tests |
| `chore` | Build process or tooling changes (CI/CD, dependency updates) |
| `revert` | Undoing an earlier commit |

Pick the type that matches the main purpose of the change. If the change has unrelated parts of different types, tell the user and offer one message per part.

**Summary (first line).** One short English sentence.

- Imperative mood: "add", "fix", "remove", not "added" or "fixes".
- Aim for 50 characters or fewer. Never go over 72.
- No period at the end.

**Body (after one blank line).** The detailed version of the same change.

- Say what changed and why, in bullets, one bullet per logical change.
- Name the files, modules, or functions involved, and say what behavior is different now.
- Describe the real change only. Do not pad it.

Example (the names are made up, only the shape matters):

```
fix: reject empty username on login

- Validate the username in the login handler before the database lookup
- Return a 400 with a clear message instead of failing later with a 500
- Add a test for the empty-username case
```

---

## Sub-skills

| Task | Read this file |
|------|----------------|
| Understand structure, find callers or callees, trace calls, dependencies, impact analysis, dead code, architecture | [references/codebase-memory/SKILL.md](references/codebase-memory/SKILL.md) |

If no row matches, do the task normally. Do not force a sub-skill.

## Tool availability

`codebase-memory` is an MCP server named `codebase-memory-mcp`. It is a set of tools, not a command or a skill. It may be installed on some agents and not on others.

1. Look at your tool list for tools such as `search_graph`, `trace_path`, `get_code_snippet`, `index_repository`.
2. Your agent may add a prefix to the tool name. Claude Code shows `mcp__codebase-memory-mcp__search_graph`. The reference file uses the short names. Use whatever name your agent shows.
3. If the tools are there: use them first for structure questions. Use grep or file reads for exact text, config and non-code files.
4. If the tools are not there: tell the user the MCP server is not available in this agent. Fall back to grep, file reads and editor symbol search. Do not invent graph results. Do not try to install the server unless the user asks.

---
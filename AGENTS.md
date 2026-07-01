<!-- markdownlint-disable MD025 -->
# Tool Rules (compose-agentsmd)

- **Session gate**: before starting substantive work for each externally supplied human/operator instruction, run `compose-agentsmd` once from the project root. AGENTS.md contains the rules you operate under; stale rules cause rule violations. Do not rerun this gate within the same instruction after tool results, retries, generated continuations, or resumed execution. If you discover you skipped this step mid-session, stop, run it immediately, re-read the diff, and adjust your behavior before continuing.
- `compose-agentsmd` intentionally regenerates `AGENTS.md`; any resulting `AGENTS.md` diff is expected and must not be treated as an unexpected external change.
- If `compose-agentsmd` is not available, run it via `npx compose-agentsmd`. If `npx` is unavailable or cannot fetch the package, install it via npm with an environment-appropriate method such as `npm install -g compose-agentsmd` when global installs are permitted, or a user-local npm prefix when global installs are not permitted.
- To update shared/global rules, use `compose-agentsmd edit-rules` to locate the writable rules workspace, make changes only in that workspace, then run `compose-agentsmd apply-rules` (do not manually clone or edit the rules source repo outside this workflow).
- If you find an existing clone of the rules source repo elsewhere, do not assume it is the correct rules workspace; always treat `compose-agentsmd edit-rules` output as the source of truth.
- `compose-agentsmd apply-rules` pushes the rules workspace when `source` is GitHub (if the workspace is clean), then regenerates `AGENTS.md` with refreshed rules.
- Do not edit `AGENTS.md` directly; update the source rules and regenerate.
- `tools/tool-rules.md` is the shared rule source for all repositories that use compose-agentsmd.
- Before applying any rule updates, present the planned changes first with an ANSI-colored diff-style preview, ask for explicit approval, then make the edits.
- These tool rules live in tools/tool-rules.md in the compose-agentsmd repository; do not duplicate them in other rule modules.

Source: github:metyatech/agent-rules@HEAD/rules/domains/skill/repository.md

# Skill Repository Rules

- A skill MUST follow the Agent Skills open standard.
- `SKILL.md` frontmatter MUST contain only `name` and `description`.
- `name` MUST be lowercase alphanumeric with hyphens, at most 64 characters.
- `description` MUST explain trigger conditions.
- `SKILL.md` MUST be platform-agnostic and use intent-level wording.
- Platform-specific examples MUST live in `README.md`.
- `SKILL.md` and `README.md` SHOULD be in English.
- Skill instructions MUST be concise and action-oriented.
- A skill MUST NOT duplicate AGENTS.md global rules.
- Each skill MUST live in its own `metyatech/skill-<name>` repository with `SKILL.md` at the root.
- Each skill repository MUST include a LICENSE file.
- Skill repositories SHOULD use the MIT license unless the user specifies otherwise.
- Skill repositories MUST be public unless the user explicitly asks for a private skill.
- The GitHub repository is the canonical source of truth for a skill.
- The agent MUST NOT edit installed copies under `~/.agents/skills/<name>`.

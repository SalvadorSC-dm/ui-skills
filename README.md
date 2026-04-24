# ui-skills

A small collection of reusable **Agent Skills** (markdown instructions for AI coding assistants). Skills are plain folders containing a `SKILL.md` file plus any optional assets.

This repository is meant to be **copied or vendored** into a product repo, or kept as a reference and synced manually. It is not an npm package.

## Contents

| Path | Description |
|------|-------------|
| [`ui-prototyping/SKILL.md`](./ui-prototyping/SKILL.md) | Guides rapid UI layout exploration and design variants (branch safety, Ant Design–friendly patterns, scope limits). Originally written for **Leon App** (Next.js + Ant Design); you can adapt wording in a fork if your stack differs. |

Each skill’s `SKILL.md` may include YAML frontmatter (for example `name` and `description`) so tools can show a short label and when to apply the skill.

---

## Cursor

Cursor loads **project skills** from:

```text
<your-repo>/.cursor/skills/<skill-name>/SKILL.md
```

### Install (copy)

From a clone of this repo:

```bash
# Run inside your application repository root
mkdir -p .cursor/skills
cp -R /path/to/ui-skills/ui-prototyping .cursor/skills/
```

Commit `.cursor/skills/ui-prototyping/` if your team should share the same behavior.

### Optional: git submodule

If you prefer pulling updates from GitHub without copying by hand:

```bash
git submodule add https://github.com/SalvadorSC-dm/ui-skills.git vendor/ui-skills
# Then symlink or copy ui-prototyping into .cursor/skills/ as above
```

### Usage in Cursor

- The agent can load skills when they match the task (see Cursor docs on **Agent Skills**).
- You can also mention the skill explicitly, for example: “Follow the ui-prototyping skill for layout options.”

---

## Claude (Anthropic)

“Claude” in a company setup usually means one or more of: **Claude Code** (CLI / IDE), **Claude for desktop**, or **Claude on the web / Team** with **Projects**. Installation differs slightly.

### Claude Code (CLI, IDE extension, desktop coding)

Claude Code reads **skills** from the `.claude` directory in the project (or from `~/.claude` for personal, all-project scope). Official layout: [Explore the `.claude` directory](https://code.claude.com/docs/en/claude-directory).

**Project install (recommended for teams):**

```bash
# Run inside your application repository root
mkdir -p .claude/skills
cp -R /path/to/ui-skills/ui-prototyping .claude/skills/
```

Commit `.claude/skills/ui-prototyping/` so teammates get the same skill.

Skills are documented here: [Create skills](https://code.claude.com/en/skills). After install, you can often invoke a skill by name (for example with a `/` command matching the skill’s `name` in the frontmatter of `SKILL.md`, e.g. `ui-prototyping`) or rely on Claude to pull it in when relevant—see current Claude Code UI and docs for your version.

**Global install (only for you, all repos):**

```bash
mkdir -p ~/.claude/skills
cp -R /path/to/ui-skills/ui-prototyping ~/.claude/skills/
```

### Claude on the web, Team chat, or Projects (no `.claude` folder)

There is no automatic `SKILL.md` loader like Cursor or Claude Code. Practical options:

1. **Project / knowledge**: Upload `ui-prototyping/SKILL.md` (or the whole folder as files) into a **Project** so every thread in that project sees it.
2. **Custom instructions**: Paste an excerpt or a short pointer (“When prototyping UI, follow the attached `SKILL.md`”) into org or user instructions, and keep the full skill in Project files.
3. **Per conversation**: Paste a link to this repo or attach `SKILL.md` when you start a prototyping task.

### Claude for desktop (non–Claude Code chat)

Treat it like web Claude: use **Projects**, **knowledge**, or **custom instructions** to attach the same `SKILL.md` content so prototyping sessions stay consistent.

---

## Updating a vendored skill

When this repository changes, refresh the copy in your app:

```bash
cp /path/to/ui-skills/ui-prototyping/SKILL.md ./.cursor/skills/ui-prototyping/SKILL.md
cp /path/to/ui-skills/ui-prototyping/SKILL.md ./.claude/skills/ui-prototyping/SKILL.md   # if you use Claude Code too
```

Then commit and push your product repository as usual.

---

## License and contributions

Add a `LICENSE` if you want explicit terms. Contributions: open a PR or issue on [SalvadorSC-dm/ui-skills](https://github.com/SalvadorSC-dm/ui-skills).

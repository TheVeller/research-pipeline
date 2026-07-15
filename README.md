# research-pipeline

> **YouTube → NotebookLM → your notes, at zero LLM cost.** A Claude Code / agent skill that searches YouTube, ships the videos to Google NotebookLM for server-side deep analysis, optionally renders a deliverable (infographic, podcast, slide deck…), and writes the result straight into your knowledge base.

[![License: MIT](https://img.shields.io/badge/License-MIT-black.svg)](./LICENSE)
[![Skill](https://img.shields.io/badge/type-agent%20skill-blue.svg)](#)
[![Zero tokens](https://img.shields.io/badge/analysis-0%20LLM%20tokens-brightgreen.svg)](#why-zero-tokens)

## Why it's different

Most "research" workflows burn LLM tokens re-reading every transcript. This one doesn't. **NotebookLM does the analysis server-side on Google's infrastructure** — the agent only orchestrates the pipeline, captures `notebooklm ask` stdout, and writes the note. You can analyze 50 videos and spend nothing on analysis tokens.

## What it does

1. **Search** YouTube for a topic (`yt-dlp`) and collect the top *N* videos.
2. **Create** a dedicated NotebookLM notebook for the session.
3. **Add** every video as a source (transcripts processed automatically).
4. **Analyze** the whole corpus with one structured `notebooklm ask` — themes, insights, creator perspectives, gaps, outliers, actionable takeaways.
5. **Generate** (optional) an infographic / podcast / slide deck / mind map / flashcards.
6. **Save** a clean Markdown note (frontmatter + video table + analysis + deliverable links) to your vault.

Not just YouTube — swap step 1 for PDFs, web articles, raw text, or Google Drive files.

## Prerequisites

| Tool | Install | Purpose |
|---|---|---|
| `notebooklm` CLI | authenticate once with `notebooklm login` | Server-side analysis + deliverables |
| `yt-dlp` | `brew install yt-dlp` | YouTube search + metadata |

## Install

**Manual** — copy the skill into your agent's skills directory:

```bash
git clone https://github.com/TheVeller/research-pipeline.git
cp -R research-pipeline/skills/research-pipeline ~/.claude/skills/
```

**Via the `skills` CLI:**

```bash
npx skills add TheVeller/research-pipeline -s research-pipeline
```

## Usage

```
/research-pipeline Claude Code MCP servers

Research the top 10 YouTube videos about AI agents and give me an infographic

YouTube pipeline: find 5 videos about Obsidian workflows, analyze gaps
```

| Parameter | Default | Notes |
|---|---|---|
| `query` | — | Research topic (required) |
| `limit` | `10` | Number of videos |
| `deliverable` | none | `infographic` · `podcast` · `slides` · `mindmap` · `flashcards` |
| `save_to` | `04_Resources/Research/` | Output path in your vault |

## Why zero tokens

The agent never re-reads the scraped corpus. Analysis output is piped to a temp file and written verbatim into the note — Google's NotebookLM does the heavy lifting. See [`skills/research-pipeline/SKILL.md`](./skills/research-pipeline/SKILL.md) for the full step-by-step.

## More skills

Part of my skills collection → [**TheVeller/claude-skills**](https://github.com/TheVeller/claude-skills) (organized by category). Discover and install more agent skills via [skills.sh](https://skills.sh) (`npx skills add <owner>/<repo> -s <skill>`).

## License

MIT © [Ignacio Alberto Velásquez Franco (@TheVeller)](https://github.com/TheVeller)

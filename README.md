# RankEarly Skills

SEO for AI Agents. Most SEO tools show metrics and leave the rest to you. RankEarly skills let your agent do the research, plan the content, and move on — no dashboard tab-switching required.

Works with any AI assistant that supports skills — Claude Code, Gemini CLI, OpenAI Codex, Manus, OpenClaw, Lindy, and more.

## Available Skills

| Skill | What it does | Status |
|-------|-------------|--------|
| [Topic Research](./topic-research/SKILL.md) | Build a pillar-cluster content architecture from your product's features using keyword expansion and clustering | Live |
| [SERP Gap Analysis](./serp-gap-analysis/SKILL.md) | Assess whether a SERP is winnable and surface content opportunities from competitor weaknesses | Live |
| [Blog Title Generator](./blog-title-generator/SKILL.md) | Generate 10 scored blog title variations (title tag + H1) for a target keyword | Live |

## Install

Install all skills:

```bash
npx skills add rankearly/rankearly-skills
```

Or install a single skill:

```bash
npx skills add rankearly/rankearly-skills --skill serp-gap-analysis
```

### Manual install

Download and extract the SKILL.md into your project's `.claude/skills/` directory.

## MCP Setup

Skills run the playbook. RankEarly MCP powers the data and algorithms — live SERPs, keyword expansion, topic clustering. Connect using OAuth, no API key needed.

```bash
claude mcp add --transport http rankearly-mcp https://rankearly.pro/api/mcp
```

### MCP Tools

| Tool | Description |
|------|-------------|
| `scrape_serp` | Fetch live Google top-10 results for a query |
| `expand_keywords` | Start async keyword expansion for a topic |
| `cluster_keywords` | Group keywords into pillars and subtopics |
| `get_research_status` | Poll async task status |
| `fetch_data` | Read project and keyword library data |

## Browse skills

Visit [rankearly.pro/skills](https://www.rankearly.pro/skills) to browse skills with install instructions and workflow details.

## License

Apache 2.0 — see [LICENSE.md](./LICENSE.md).

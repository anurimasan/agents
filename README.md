# Custom Claude Code Agents

This repository contains custom subagents for Claude Code that extend its capabilities with specialized workflows.

## Available Agents

### Market Research Pipeline (Two-Agent Architecture)

This repository uses a **modular two-agent pipeline** for comprehensive market analysis:

#### 1. Market Researcher (`market-researcher`)
**Type**: Market Intelligence Specialist
**Purpose**: Deep research and data synthesis

Focuses on gathering and synthesizing raw market intelligence:
- Identifying market size (TAM) and growth rate (CAGR) from credible sources
- Discovering recent technological breakthroughs (last 12 months)
- Mapping competitive landscapes (dominant players + emerging disruptors)
- Extracting customer pain points from forums, reviews, and community discussions
- Delivering raw synthesized research findings (not formatted)

**Tools**: WebSearch, WebFetch, Bash, Read, Grep, Glob

#### 2. PRD Formatter (`prd-formatter`)
**Type**: Product Requirements Document Specialist
**Purpose**: Structure research into PRD-ready documents

Transforms raw research into polished PRD sections:
- Organizing findings into standardized sections (Market Context, Competitive Landscape, etc.)
- Identifying strategic opportunities from research insights
- Generating actionable next steps
- Maintaining professional, concise tone
- Ensuring all source citations are preserved

**Tools**: Read, Bash

#### 3. Market Scout (`market-scout`) - Orchestrator
**Type**: End-to-end Market Analysis
**Purpose**: Convenient single-agent interface

Orchestrates both agents in sequence for complete market analysis:
- Automatically delegates research to `market-researcher`
- Automatically formats output with `prd-formatter`
- Delivers final PRD-ready report

**Use this when**: You want a complete analysis in one step
**Use the modular pipeline when**: You want fine-grained control or iterative refinement

## Usage

### Option 1: Single-Agent Workflow (Recommended for Most Users)

Use `market-scout` for end-to-end analysis in one step:

```bash
# In any Claude Code session
Use the market-scout agent to analyze the "Headless CMS market"
```

**Example Prompts:**
```
Use market-scout to analyze the app builder space

I need market intelligence on AI-driven lawn mowers.
Use market-scout to identify key players and customer pain points.

What are the strategic opportunities in the enterprise observability space?
```

**Output**: Complete PRD-ready report with all sections formatted and ready to use.

---

### Option 2: Modular Two-Agent Workflow (Advanced Users)

Use the pipeline for fine-grained control and iterative refinement:

#### Step 1: Research Phase
```
Use the market-researcher agent to gather intelligence on "App Builder market"
```

**Output**: Raw synthesized research findings with all data, sources, and insights.

**When to pause here:**
- You want to review research quality before formatting
- You need to add additional research or context
- You're doing multiple research iterations

#### Step 2: Formatting Phase
```
Use the prd-formatter agent to format the research findings into a PRD structure
```

**Output**: Polished PRD-ready document with strategic opportunities and next steps.

**Benefits of Modular Approach:**
- Review and refine research before formatting
- Add your own research or context between stages
- Reformat same research multiple times for different audiences
- Debug issues by isolating research vs formatting problems

### Output Format

Market Scout delivers structured Markdown reports with these sections:

1. **Market Context**: Market size (TAM), growth rate (CAGR), maturity level, recent breakthroughs, market dynamics
2. **Competitive Landscape**: Top 3-5 players, 1-2 disruptors, with capabilities and weaknesses
3. **Customer Pain Points**: Evidence-based sentiment analysis from real user feedback
4. **Strategic Opportunities**: Actionable gaps and unmet needs
5. **Recommended Next Steps**: Areas for deeper validation

### Configuration

**All agents** are configured in `.claude/agents/` with:

| Agent | File | Tools | Model | Purpose |
|-------|------|-------|-------|---------|
| market-researcher | `market-researcher.md` | WebSearch, WebFetch, Bash, Read, Grep, Glob | Sonnet | Deep research & synthesis |
| prd-formatter | `prd-formatter.md` | Read, Bash | Sonnet | PRD formatting & structuring |
| market-scout | `market-scout.md` | WebSearch, WebFetch, Bash, Read, Grep, Glob | Sonnet | End-to-end orchestration |

**Permission Mode**: Default (asks before executing commands) for all agents

### Customization

To modify agent behavior:

1. Edit the appropriate file in `.claude/agents/`
   - Research quality → Edit `market-researcher.md`
   - Output format → Edit `prd-formatter.md`
   - Orchestration → Edit `market-scout.md`
2. Update the system prompt (after the YAML frontmatter)
3. Save and reload your Claude Code session

## Development

### Project Structure

```
agents/
├── .claude/
│   └── agents/
│       ├── market-researcher.md    # Research & synthesis agent
│       ├── prd-formatter.md        # PRD formatting agent
│       └── market-scout.md         # Orchestrator agent
├── app-builder-market-analysis-2026.md  # Example output
└── README.md                        # This file
```

### Adding New Agents

To create additional custom agents:

1. Create a new file: `.claude/agents/your-agent-name.md`
2. Define YAML frontmatter with name, description, tools, and model
3. Write the system prompt that defines agent behavior
4. Claude Code will automatically load it on next session

See `.claude/agents/market-scout.md` for a complete example.

## Best Practices

**When to Use Market Scout:**
- Early product discovery and validation
- Competitive analysis for roadmap planning
- Identifying market gaps and opportunities
- Preparing PRD market context sections
- Due diligence for new feature areas

**When NOT to Use:**
- Quick factual questions (use main Claude instead)
- Deep technical implementation (use specialized dev agents)
- Tasks requiring code editing (market-scout is read-only)

## Examples

### Example 1: New Product Category Research

```
Use market-scout to analyze "developer tools for edge computing"
```

**Output**: Full market report with Vercel, Cloudflare Workers, Deno Deploy analysis, customer pain points around debugging and cold starts, and opportunities in observability tooling.

### Example 2: Competitive Intelligence

```
I'm building a headless CMS. Use market-scout to identify what customers
complain about most with Contentful and Sanity.
```

**Output**: Customer sentiment analysis with specific pain points (pricing complexity, migration difficulties, vendor lock-in) extracted from G2, Reddit, and HackerNews.

### Example 3: Emerging Technology Assessment

```
What's happening in the AI code completion space? Use market-scout.
```

**Output**: 2025-2026 breakthroughs (multi-file context, test generation), dominant players (GitHub Copilot, Cursor, Codeium), disruptors (Supermaven), and opportunities in specialized domains.

## Contributing

To improve the Market Scout agent:

1. Fork this repository
2. Edit `.claude/agents/market-scout.md`
3. Test with various market topics
4. Submit a PR with your improvements

## Resources

- [Claude Code Sub-agents Documentation](https://code.claude.com/docs/en/sub-agents.md)
- [Hooks Configuration Guide](https://code.claude.com/docs/en/hooks-guide.md)
- [Claude Agent SDK](https://platform.claude.com/docs/en/agent-sdk/overview)

## License

MIT

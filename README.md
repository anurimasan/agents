# Custom Claude Code Agents

This repository contains custom subagents for Claude Code that extend its capabilities with specialized workflows.

## Available Agents

### Market Scout

**Type**: Senior Product Strategy Researcher
**Purpose**: Deep market analysis, competitive intelligence, and strategic opportunity identification

The Market Scout agent performs comprehensive market research by:
- Discovering recent technological breakthroughs (last 12 months)
- Mapping competitive landscapes (dominant players + emerging disruptors)
- Extracting customer pain points from forums, reviews, and community discussions
- Synthesizing findings into PRD-ready structured reports

## Usage

### Activating the Market Scout Agent

```bash
# In any Claude Code session, use the Task tool
# Claude will automatically delegate when you mention market analysis
```

### Example Prompts

**Basic Market Analysis:**
```
Use the market-scout agent to analyze the "Headless CMS market"
```

**Specific Research Request:**
```
I need market intelligence on AI-driven lawn mowers.
Use market-scout to identify key players and customer pain points.
```

**Proactive Delegation:**
```
What are the strategic opportunities in the enterprise observability space?
```
*Claude will automatically delegate to market-scout based on the description*

### Output Format

Market Scout delivers structured Markdown reports with these sections:

1. **Market Context**: Maturity level, recent breakthroughs, market dynamics
2. **Competitive Landscape**: Top 3-5 players, 1-2 disruptors, with capabilities and weaknesses
3. **Customer Pain Points**: Evidence-based sentiment analysis from real user feedback
4. **Strategic Opportunities**: Actionable gaps and unmet needs
5. **Recommended Next Steps**: Areas for deeper validation

### Configuration

The agent is configured in `.claude/agents/market-scout.md` with:

- **Tools**: WebSearch, WebFetch, Bash, Read, Grep, Glob
- **Model**: Sonnet (for superior research and synthesis)
- **Permission Mode**: Default (asks before executing commands)

### Customization

To modify the agent's behavior:

1. Edit `.claude/agents/market-scout.md`
2. Update the system prompt (after the YAML frontmatter)
3. Save and reload your Claude Code session

## Development

### Project Structure

```
agents/
├── .claude/
│   └── agents/
│       └── market-scout.md    # Market Scout subagent definition
└── README.md                   # This file
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

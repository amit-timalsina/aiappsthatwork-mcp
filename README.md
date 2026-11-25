<p align="center"><img src="assets/logo-400.png" width="96" height="96" alt="AI Apps That Work logo"></p>

# AI Apps That Work: free MCP server for people building AI apps

Your coding agent can look up what your AI features really cost and what to change: real cost per AI result, current LLM prices, model switch costs, model shutdown dates, A/B test sample sizes and LLM-judge checks.

- **Server URL:** `https://aiappsthatwork.com/mcp` (Streamable HTTP)
- **Free, read-only, no sign-up and no API key**
- **Official MCP registry:** `com.aiappsthatwork/tools`
- **Glama:** https://glama.ai/mcp/connectors/com.aiappsthatwork/tools
- **Docs:** https://aiappsthatwork.com/connect
- **The same tools in a browser:** https://aiappsthatwork.com/tools

This repository holds the setup docs and client config files. The server itself runs at aiappsthatwork.com; its code is not in this repository.

## Connect

**Claude Code**

```sh
claude mcp add --transport http ai-apps-that-work https://aiappsthatwork.com/mcp
```

Add `--scope user` to have it in every project. Or copy [`.mcp.json`](.mcp.json) into your project.

**Cursor:** add this to `~/.cursor/mcp.json` (every project) or `.cursor/mcp.json` (one project). The same file is in [`.cursor/mcp.json`](.cursor/mcp.json).

```json
{
  "mcpServers": {
    "ai-apps-that-work": { "url": "https://aiappsthatwork.com/mcp" }
  }
}
```

**VS Code:** copy [`.vscode/mcp.json`](.vscode/mcp.json) into your project.

**Claude on the web and desktop:** add a custom connector with the URL `https://aiappsthatwork.com/mcp` and leave the advanced settings empty.

**ChatGPT:** in developer mode, create an app with the URL `https://aiappsthatwork.com/mcp` and no authentication.

**Any other MCP client:** use the URL above with the Streamable HTTP transport and no authentication.

## Tools

Every tool is read-only and has a title.

| Tool | What it returns |
|---|---|
| `real_cost_per_result` | Cost per request, real cost per result that worked, monthly wasted spend, credit pricing |
| `model_switch_cost` | List prices of both models, cost per 1,000 requests on six common tasks, the break-even point, the current model's shutdown date |
| `model_prices` | List prices, context size, price source, and the dates each price was checked and last changed |
| `model_shutdowns` | Announced API shutdowns, with the replacement and source |
| `ab_test_sample_size` | Results needed per version, and days at a given volume |
| `judge_agreement` | Agreement rate, Cohen's kappa, per-verdict precision and recall, and whether to trust the judge |
| `build_judge_prompt` | A pass/fail judge prompt for one kind of AI step |
| `launch_checklist` | The AI-specific checks still to do before launch, plus a request you can hand to a coding agent |

Every answer includes a link to a page on aiappsthatwork.com that shows the same result.

## Example prompts

1. "What does Claude Fable 5.2 cost per million tokens, and when was that price last checked?"
2. "We send about 40,000 support answers a month on GPT-4o at about 3,000 tokens in and 300 out, and 70% work first time. What does each answer that works really cost us?"
3. "Is it cheaper to move our invoice extraction from GPT-4o to Gemini 3.8 Flash, and how often would Flash need to work first time to stay cheaper?"
4. "Which OpenAI and Anthropic models are being shut down in the next three months, and what replaces them?"
5. "Our prompt works first time 60% of the time and we hope a new version reaches 68%. How many results do we need per version at 200 a day?"
6. "Here are 40 verdicts from our LLM judge next to a person's verdicts. Can we trust the judge?"

## Data and limits

- Prices for text models are re-checked daily against OpenRouter and LiteLLM. Each price carries the date it was checked and the date it last changed.
- Inputs are computed in memory and thrown away. Nothing you send is stored.
- For each call the server records the kind of agent, the client's name and version as it reports them, the tool name, success or failure, and duration. Never your address, your inputs or the answer, and no id that links your calls. See https://aiappsthatwork.com/privacy.
- Each address can make 120 calls a minute.

## Other ways in

- **JSON API:** https://aiappsthatwork.com/openapi.json
- **Skill for Claude Code:** https://aiappsthatwork.com/skill/SKILL.md
- **All model prices and shutdowns as JSON:** https://aiappsthatwork.com/models.json
- **`llms.txt`:** https://aiappsthatwork.com/llms.txt

## Contact

Questions, bugs or a tool you'd like: open an issue here or write to amit@aiappsthatwork.com.

## License

The docs and config files in this repository are MIT licensed. The hosted server is free to use.

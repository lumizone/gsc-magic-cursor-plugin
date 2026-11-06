# GSC Magic for Cursor

Your own Google Search Console, Bing Webmaster Tools, Google Analytics 4, IndexNow and Core Web Vitals
data in Cursor, through the hosted [GSC Magic](https://gscmagic.com) MCP server. Fix titles, redirects,
sitemaps and structured data in the same session where the agent can see which pages lost clicks.

Ask things like:

- "Which queries on example.com are stuck in positions 4 to 20 with lots of impressions?"
- "Why did organic clicks drop last week? Show me the pages that lost the most."
- "Are the URLs in my sitemap actually indexed?"

## What is in this plugin

- **The GSC Magic MCP server** (`mcp.json`): the remote server `https://mcp.gscmagic.com/mcp` over
  Streamable HTTP. It brings 69 tools: Search Console analytics, URL inspection and sitemaps, Bing
  Webmaster Tools, GA4 reports, CrUX and PageSpeed, IndexNow, and finished SEO reports (quick wins,
  traffic drops, content decay, cannibalization, CTR outliers, brand split, index health, Google vs Bing)
  with optional PNG charts.
- **The `gsc-magic` skill**: tells the agent to discover your sites first, prefer the finished reports
  over raw rows, respect the 2 to 3 day Search Console lag, and never run a write tool without your
  go-ahead.

## Set up

1. Install GSC Magic from the Cursor Marketplace.
2. In Cursor Settings → Tools & MCP, click Connect (or "Needs login") next to `gsc-magic`, sign in to
   GSC Magic with Google or e-mail and allow access. A free account is available at
   https://app.gscmagic.com/login?mode=signup; new accounts pick which Search Console properties to
   import, and only imported properties are visible to the agent.
3. Bing data needs your Bing Webmaster API key and GA4 data needs a property linked to the site, both
   set in the dashboard under Sources (https://app.gscmagic.com/sources).

If the sign-in does not finish (older Cursor versions return to `cursor://`, which GSC Magic does not
accept), create an access token at https://app.gscmagic.com/connect and add the server by hand with an
`Authorization: Bearer gsm_...` header instead. Details: https://gscmagic.com/integrations/cursor

## Plans

Free: 1 site, 200 tool calls a month (10 a day), 14 days of stored history. Pro ($19 a month) and Agency
($34 a month): no call limit, more sites, 16 months of history, write tools, alerts. Details:
https://gscmagic.com/pricing

## What this plugin sends and runs

- Every tool call goes to GSC Magic's hosted server (`mcp.gscmagic.com`), which calls Google Search
  Console, Bing Webmaster Tools, GA4, IndexNow, CrUX and PageSpeed Insights with your own connected
  accounts. GSC Magic logs each call (tool name, site, client name, status, duration, time) for 30 days
  so you can see it in the dashboard; other arguments and results are not stored in that log.
- The plugin holds only the server address and the skill. It runs nothing on your computer, has no
  hooks or scripts, and sends no telemetry.
- Read-only by default. Write tools (sitemaps, site management, Bing URL submission and site settings,
  IndexNow) work only on paid plans after you turn on write mode in the dashboard; every tool carries
  `readOnlyHint` / `destructiveHint` annotations.

Privacy policy: https://app.gscmagic.com/privacy · Terms: https://app.gscmagic.com/terms ·
Contact: contact@gscmagic.com

## License

MIT for this repository. GSC Magic itself is a hosted service. The same plugin for Claude, Hermes Agent,
OpenClaw and Gemini CLI lives at https://github.com/lumizone/gsc-magic-agent-plugin.

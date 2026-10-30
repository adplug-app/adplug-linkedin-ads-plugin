# LinkedIn Ads MCP by AdPlug, for Grok Bot and Cursor

AdPlug is a hosted MCP server that safely connects LinkedIn Ads to Grok Bot and Cursor.

Your agent can check campaigns, flag what needs attention and, on a paid plan, make the changes you approve.

The plugin adds one remote MCP server, `https://api.adplug.app/mcp/linkedin-ads`, and nothing else. There's no code, no script and no hook in it.

## Install in Grok Bot

Send your Bot this message:

> Add a custom MCP server called AdPlug LinkedIn Ads at https://api.adplug.app/mcp/linkedin-ads

Click **Authorize** on the card it posts, then **Continue**, then sign in to AdPlug in the browser tab that opens and click **Approve**. The approval screen says "Cursor wants to access your AdPlug account". That's expected: Grok Bot connects apps through Cursor.

## Install in Cursor

Add `https://api.adplug.app/mcp/linkedin-ads` as a server in Cursor's MCP settings, or put this in `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "adplug-linkedin-ads": {
      "url": "https://api.adplug.app/mcp/linkedin-ads"
    }
  }
}
```

The first time you connect, a browser tab opens on AdPlug's sign-in. Sign in, or create a free account, and click **Approve**.

## What you need

- An AdPlug account. The free plan connects one ad platform, comes with a monthly request limit and is view only: your agent can read your accounts and preview changes, but not apply them. A paid plan lets the agent make changes: see [adplug.app/pricing](https://adplug.app/pricing).
- LinkedIn Ads connected once in AdPlug, at [adplug.app/dashboard/connections](https://adplug.app/dashboard/connections), with your own LinkedIn sign-in.

There's no API key or client ID to set up. Sign-in is OAuth 2.1 with dynamic client registration and PKCE.

## What your agent can do

- **Accounts:** every LinkedIn ad account your login can reach.
- **Reports:** campaign, creative, daily, conversion, lead gen form, demographic and reach reports.
- **Account data:** campaigns, ad sets, ads, conversions, lead forms and matched audiences.
- **Targeting:** search for job titles, companies and skills, with audience size.
- **Competitor research:** LinkedIn's public Ad Library, to look up a competitor's ads.
- **Changes:** create and edit campaigns, ad sets and ads (campaign groups, campaigns and creatives in LinkedIn's API). Send conversions through LinkedIn's Conversions API.

`adplug_get_status` tells the agent whether LinkedIn Ads is connected and what your plan allows.

## Example prompts

- "Break my recent LinkedIn Ads spend down by job seniority, with cost per conversion for each band. Flag anything with too little data to judge."
- "Which LinkedIn campaigns aren't spending their budget, and why: bid, audience size or ads? Show me the fixes as a preview."
- "For every Lead Gen Form campaign that ran recently, list completion rate and cost per lead, and tell me which form is performing worst."
- "Search the LinkedIn Ad Library for our top competitor and list their active ads with links. Summarise what they seem to be testing."

## How changes are kept safe

- **Previews:** AdPlug's change tools come in pairs: a preview, which shows the exact change without making it, and an execute, which makes it. AdPlug's tool descriptions tell the agent to preview first. That's an instruction to the agent, not a block on the server.
- **LinkedIn's Conversions API upload has no preview step.** It sends conversion events.
- New campaigns start as drafts.
- On the free plan, the change tools refuse to apply anything.
- On Max and Agency plans, a team owner can set a teammate to View only for LinkedIn Ads. AdPlug then hides and blocks the change tools for that teammate.
- Grok Bot and Cursor can also ask you before a tool runs, depending on your settings.
- Every call is logged on the [usage page](https://adplug.app/dashboard/usage) of your AdPlug dashboard.

## Your data and where it goes

Every tool call goes to one endpoint, `https://api.adplug.app/mcp/linkedin-ads`. Sign-in goes through AdPlug's pages on adplug.app and its sign-in provider, Supabase (named in api.adplug.app's OAuth metadata). The plugin adds no software and runs no scripts on your computer.

Account data travels between LinkedIn Ads and your agent through AdPlug's servers at api.adplug.app. Reports are fetched live and not kept. AdPlug logs each call's tool, ad account and time for your usage page, never its arguments or results. LinkedIn sign-in tokens are stored encrypted.

- Privacy policy: [adplug.app/privacy](https://adplug.app/privacy)
- Terms: [adplug.app/terms](https://adplug.app/terms)
- Data processing agreement: [adplug.app/dpa](https://adplug.app/dpa)

## Support and links

- Email [support@adplug.app](mailto:support@adplug.app) and Daniel Popa, AdPlug's founder, will reply, usually the same business day.
- Website: [adplug.app/integrations/linkedin-ads](https://adplug.app/integrations/linkedin-ads)
- Setup guide: [adplug.app/guides/linkedin-ads](https://adplug.app/guides/linkedin-ads)
- Every ad platform in one connector: [adplug-app/adplug-cursor-plugin](https://github.com/adplug-app/adplug-cursor-plugin)

## Licence

MIT, see [LICENSE](LICENSE). Published by AdPlug, the trading name of MEANDATA IT SRL.

# FAQ - The Operator's Brain

Common questions about the brain template, answered for operators thinking about adopting it.

If your question isn't here, [open an issue](https://github.com/ShubhashSharma/brain-template/issues) on the repo.

---

## Contents

- [Getting started](#getting-started)
- [The structure](#the-structure)
- [Claude Code and the four skills](#claude-code-and-the-four-skills)
- [Connecting to live Amazon data](#connecting-to-live-amazon-data)
- [Your data, privacy, and cost](#your-data-privacy-and-cost)
- [Is this for me?](#is-this-for-me)
- [Working with a team](#working-with-a-team)
- [Multi-brand and multi-channel](#multi-brand-and-multi-channel)
- [Troubleshooting](#troubleshooting)
- [Roadmap and contributions](#roadmap-and-contributions)

---

## Getting started

### How do I get my own copy?

Two ways:

1. **GitHub "Use this template"** (easiest) - go to https://github.com/ShubhashSharma/brain-template, click the green "Use this template" button at the top, name your copy, mark it private, then clone it locally.

2. **One-line installer** (fastest) - paste this in Terminal:
   ```
   curl -fsSL https://raw.githubusercontent.com/ShubhashSharma/brain-template/main/setup.sh | bash
   ```
   The installer handles prerequisites (Homebrew, Git, GitHub CLI, Obsidian), creates your private GitHub copy, clones it locally, and optionally wires up Claude Code.

The full first-time guide is in [QUICKSTART.md](QUICKSTART.md) - 60 minutes, end-to-end.

### Do I need to know how to code?

No. If you can install an app and copy-paste a Terminal command, you can use the brain template. Day-to-day use is just typing in markdown - same as writing in Notion or Google Docs.

The technical bit is one-time setup. Daily use is one daily note + filling in SKU pages.

### What if I'm on Windows or Linux?

The vault itself (the markdown files) works anywhere. Obsidian runs on macOS, Windows, and Linux.

The one-line installer is currently macOS only. On Windows or Linux, follow the manual path: install Obsidian, click "Use this template" on GitHub, clone with `git clone`, open the folder in Obsidian. Skip the installer.

A cross-platform installer is on the v1.4 roadmap.

### Where should I put the vault on my laptop?

Anywhere you want. `~/Documents/my-operator-brain` is what the installer defaults to. If you sync the folder via iCloud, Dropbox, or OneDrive, your `.api-key.local` file (gitignored) will sync too - generate a fresh one per device if that matters to you.

---

## The structure

### What's the atomic unit of the brain?

**One page per parent ASIN.** That's it.

Suppliers feed SKUs. Channels sell SKUs. Campaigns push SKUs. Reviews judge SKUs. Decisions move SKUs. Playbooks operationalise SKUs. Every other folder backlinks to a SKU.

That's what makes the brain feel Amazon-native rather than generic.

### What folders are in the vault?

```
wiki/
  skus/         one page per parent ASIN  (with worked example)
  suppliers/    one page per factory      (with worked example)
  channels/     amazon-us, amazon-uk, tiktok-shop-us, shopify (pre-stubbed)
  decisions/    irreversible calls log    (with worked example)
  playbooks/    prime day, BFCM, Q5, restock cycle, new launch, review crisis
  concepts/     CM3, cash cycle, TACoS, FBA fees, restock formula, review velocity
  daily/        operator daily notes      (with worked example)
  team/         internal team, sourcing, agencies (with worked example)
  ip/           trademarks, patents, compliance docs
  finance/      monthly close, cash plan, restock budget (with worked example)
raw/            unfiltered inbox
_templates/     11 starting blanks
.claude/        Claude Code skills
```

### Why markdown? Why not a database or Notion?

Three reasons:

1. **You own it.** Plain text in a Git repo. No vendor lock-in. Diffable, searchable, forkable.
2. **An LLM can read all of it.** Claude Code can ingest 90 days of daily notes plus every SKU page plus every decision in one prompt. SaaS dashboards can't do this.
3. **It compounds.** Every page links to others. The graph gets denser every week. After 6 months the brain is doing work for you that you don't remember writing into it.

Frontmatter (the YAML block at the top of every page) is structured data - queryable like a database. You're getting 80% of database benefits without the lock-in.

### Do I really need a page for every SKU?

Eventually only the ones that earn it. Start with your top 20 by CM3 contribution - that's typically 80% of your value. The long tail can wait, or get a single bulk page until they earn their own.

If you have 200 SKUs, do not try to make 200 pages on day one. Build the muscle memory on your top 20 first.

### What about decisions on SKUs I no longer sell?

Don't delete the SKU page. Set `status: discontinued` in the frontmatter and leave it. Your future self (and Claude) will need that history when something comes back, when a customer asks, or when you're considering relaunching.

Same for suppliers (`status: dropped`) and decisions (`status: superseded`).

---

## Claude Code and the four skills

### What's Claude Code, and how is it different from Claude.ai?

**Claude.ai** is the chat web UI you've probably used.

**Claude Code** is Anthropic's terminal-based agent CLI. You run it in a folder on your laptop, and it can read files, run commands, edit code, and use tools. The brain template's four skills run inside Claude Code.

You can install Claude Code from https://claude.com/claude-code or via Homebrew.

### What do the four skills do?

| Command | What it does |
|---|---|
| `/sku-audit {ASIN}` | Scores one SKU's health (CM3, ad efficiency, review velocity, inventory). Appends findings to the SKU page. |
| `/restock-memo {ASIN} --weeks=12` | Computes a restock recommendation using velocity, lead time, MOQ, and cash position. Writes a draft to `wiki/decisions/`. Never sends the PO. |
| `/wbr --week=YYYY-Wxx` | Builds the Weekly Business Review across all active SKUs and channels. |
| `/onestar-themes {ASIN} --since=90d` | Clusters recent low-star reviews by theme. Updates the SKU's tracker block. |

Full specs are in `.claude/skills/<skill-name>/SKILL.md`.

### Do the skills work without `mcp-amazon`?

Yes. By default, skills read the frontmatter you typed into your SKU pages. So you can run `/sku-audit B0EXAMPLE001` against your own numbers from day one.

When you wire up `mcp-amazon` (the companion MCP server, on the v1.1 roadmap), the skills pull live SP-API data instead. Same skills, fresher numbers.

### Can I use ChatGPT, Gemini, or Cursor instead of Claude Code?

The skill specs are plain markdown. They'd need light porting to whatever agent you prefer.

The brain itself is tool-agnostic - any agent that can read markdown files can reason about it. Claude Code is the demo because of file-system tooling and context window economics, not because the brain depends on it.

### What's MCP, and why does it matter?

MCP (Model Context Protocol) is an open standard from Anthropic that lets LLM agents talk to external tools and data sources via a standard server interface. Think of it as USB-C for AI agents.

When `mcp-amazon` is wired up, Claude Code can pull SP-API data as easily as reading a local file. No bespoke integration. Same standard works for any other MCP server you bolt on later (TikTok Shop, Shopify, your accountant's API, etc).

---

## Connecting to live Amazon data

### How does the live data connection work?

Through `mcp-amazon`, a companion MCP server. Standard SP-API auth flow:

1. Create an LWA (Login With Amazon) app in Amazon's Developer Console
2. Exchange the auth code for a refresh token
3. Store the refresh token in your local `.env`
4. The MCP server handles token rotation on every call

Your SP-API credentials never touch the brain template repo. They sit in a `.env` file that's gitignored.

### What endpoints does mcp-amazon cover?

The reference build (v1.1, on the roadmap) covers:

- Orders API (last N days, per-SKU)
- Reports API (Sales & Traffic, Search Query Performance)
- Inventory API (FBA + reserved + inbound)
- Customer Reviews (SP-API beta endpoint)
- Sponsored Products / Brands / Display via the Ads API

About 15 tools exposed total.

Financial events (refunds, reimbursements) are deferred to a later release because that endpoint is rate-limited brutally.

### Will Amazon shut down SP-API access?

SP-API is a public, documented Amazon API. Every Helium 10, Sellerboard, Smartscout, Sellesta uses it. Amazon's policy is clear - it's there for sellers to use.

The brain template has zero scraping and zero ToS-violating behaviour. The only API risk is the same one Helium 10 has - very low.

### What about Brand Analytics and Search Query Performance?

Both accessible via the Reports API. You'll need the **Selling Partner Brand Analytics** role on your LWA app (not just the basic seller role) - that's why most operators see empty SQP responses on first try. Add the role at the LWA app config stage.

A SQP-specific template is on the v1.x roadmap. For now, treat SQP as something you pull manually and capture insights into concept or decision pages.

---

## Your data, privacy, and cost

### Where does my data live?

Three places, all yours:

1. **Markdown files** on your laptop
2. **Your private GitHub repo** (the one you create from "Use this template")
3. **One inference per Claude Code skill** - the relevant context goes to Anthropic's API for that one call

Nothing is sent to me, to not a square, or to any third party. There is no SaaS layer.

### Is anything sent to a server?

The vault itself sits on your laptop and your GitHub repo. The only outbound traffic is when you actively run a Claude Code skill - then the relevant pages go to Anthropic's API for that inference.

If you're privacy-strict, you can use Anthropic's API with [zero retention](https://docs.anthropic.com/en/api/privacy) enabled, or self-host with Claude on AWS Bedrock.

### What does this cost to run?

Free. The components:

- Vault structure and templates: free, MIT licensed
- Obsidian: free for personal use
- GitHub private repo: free
- Claude Code: API spend only
- mcp-amazon (when shipped): runs locally, no hosting cost

Typical Claude Code API spend for an operator running daily skills is $20-100/month. If a single `/sku-audit` decision saves you more than that, the API is rounding error.

### Can I commercialise this? Build a product on top?

Yes. MIT licensed. Fork it, brand it, charge for it. The only ask is don't strip the original attribution from internal files - it's a five-second courtesy that matters.

If you build something good, [open an issue](https://github.com/ShubhashSharma/brain-template/issues) - genuinely curious to see it.

### What about backups?

Three layers, with no extra setup:

1. **Local laptop** (the vault folder)
2. **Cloud sync** - if you put the vault in iCloud / Dropbox / OneDrive, that's a layer
3. **Private GitHub repo** - the Obsidian Git plugin auto-pushes every 10 minutes

If your laptop dies, clone the GitHub repo and you're back in 60 seconds.

Don't put your `.api-key.local` file in iCloud - the `.gitignore` already excludes it from Git, but cloud syncs work differently. Generate fresh per device.

---

## Is this for me?

### What revenue band is this for?

| Range | Fit |
|---|---|
| Sub-$1M | Probably overkill. Use a notebook for now. Come back when you're across multiple SKUs. |
| $1M to $10M | Sweet spot. The structure pays for itself the first time you skip a restock. |
| $10M to $100M | Who I built it for. Every page is institutional memory you're not paying a CFO or COO to keep in their head. |
| $100M+ | Starting point. Fork it hard, build your own playbooks on top. |

The single best signal: count irreversible decisions you've made in the last 90 days that you can't reconstruct the rationale for. If it's more than five, you need a decision log.

### What if I'm mostly TikTok Shop or Shopify, not Amazon?

The atomic unit (one page per parent product) holds. The Amazon-specific frontmatter fields (asin, fba_fee) become optional. The TikTok Shop and Shopify channel pages are already pre-stubbed.

Live MCP companions for TikTok Shop (v1.2) and Shopify (v1.3) are on the roadmap.

A note on TikTok Shop attribution: the Marketing API only goes down to AUCTION_AD (campaign x day) granularity. Per-order attribution requires Pixel + CAPI on the storefront. The brain template's TACoS concept page calls this out.

### How is this different from Tiago Forte's Second Brain / PARA?

Tiago Forte's PARA is for general knowledge management - Projects, Areas, Resources, Archive. The brain template is operationally specific to ecom. The atomic unit isn't a "project", it's a SKU. PARA never had to think about contribution margin or restock cycles.

If you've read Forte and got value out of it, the brain template will feel familiar in shape but specific in content. If you haven't, no prerequisite reading needed.

### What if I already use Notion / ClickUp / Monday for my team?

They solve different problems. Notion / ClickUp are great for tasks, dependencies, status, SOPs. The brain template is for operational thinking - the WHY behind decisions.

You can link from a ClickUp task to a SKU page or decision page in the brain. They coexist. Many operators run both.

### What if my SOPs already work?

Keep them. The brain template is a thinking layer, not a process layer. SOPs answer "how do we do X". The brain answers "why did we decide to do X, and what did we commit to checking in 90 days".

If your decision rationale lives in your head, in Slack DMs, or in nobody's head - that's where the brain helps.

---

## Working with a team

### Can multiple people use the same vault?

Yes. Git handles the merging:

- Two operators editing different files merge cleanly
- Two operators editing the same file get a standard merge conflict, resolved like any code merge
- The Obsidian Git plugin has 30-second auto-pull that minimises conflicts in practice

If your team is more than three active editors, lean toward folder ownership: one person owns SKUs, another owns playbooks. Ten editors on one vault gets messy regardless of tool.

### Can my VA fill in SKU pages?

Yes - and they should. Each SKU page is a structured form. Tell them: "every Monday, refresh these 10 SKUs from Seller Central screenshots". Done.

VAs don't need Claude Code. They just need Obsidian and GitHub access. The skills are operator-side.

### Can my agency use this?

Yes. Most useful for them is `wiki/channels/amazon-us.md` (where you capture who has access and what they own) and the WBR generated by `/wbr` (which they can either consume or contribute to).

A useful audit: if your agency reports 22% ACoS but your TACoS calculation shows 11%, your branded share is doing the work, not their bid management. That conversation is the brain template earning its keep.

### Can my CFO or accountant use it?

The `_templates/monthly-close.md` template is structured the way an ecom-specialist accountant wants to see numbers. Filling it in monthly makes their quarterly job faster.

If your accountant is a generalist (not ecom-specialist), this template alone is worth showing them - it'll teach them which numbers actually matter for an ecom business.

### Can I share specific pages with people who don't have GitHub access?

Yes. Markdown is just plain text. Email it. Paste it into Slack. Render to PDF. Or use Obsidian Publish for client-facing pages with a custom domain (free for the first vault, paid for more).

---

## Multi-brand and multi-channel

### I have 3 brands. One vault or three?

Default to **one vault** with a `brand` frontmatter field on every SKU. Reasons:

- Cross-brand learning compounds (decisions on Brand A inform Brand B)
- Single Monday restock cycle covers all brands
- One `/wbr` shows the portfolio, not just one brand

Multiple vaults make sense if your brands have different teams, different P&Ls, or different commercial structures (e.g., one is owned by a JV partner).

You can split later if friction tells you to. Going from one vault to three is easy. The reverse is harder.

### Can I see brand-level vs SKU-level views?

Frontmatter (`brand`, `channel`, `category`) makes both views queryable via Obsidian's Dataview plugin. Pre-built queries are on the v1.x roadmap. For now, you can write your own one-line Dataview queries against the frontmatter fields.

Example:
```dataview
table revenue_30d, cm3_30d, days_on_hand
from "wiki/skus"
where brand = "Acme" and status = "active"
sort cm3_30d desc
```

---

## Troubleshooting

### "Obsidian Git can't connect to GitHub"

You need GitHub CLI installed and authenticated:
```bash
brew install gh
gh auth login
```

Then in Obsidian: Settings -> Obsidian Git -> Authentication -> use system credentials.

### "The Templater hotkey doesn't work"

Settings -> Templater -> "Template folder location" must be set to `_templates`. Without that, Templater doesn't know where to look.

### "Where do I put screenshots / Looms?"

Drop them in `raw/` for now. The `attachmentFolderPath` in `.obsidian/app.json` is set to `raw/attachments` so dragging files into a note auto-saves them there.

When a piece of `raw/` content earns its keep (a Loom transcribed into a SKU's review pattern, a screenshot informing a decision), curate the lesson into the relevant `wiki/` folder. Delete the raw if it's no longer needed.

### "My Claude Code skills aren't showing up"

Check that the skills are at `.claude/skills/<name>/SKILL.md` (with the dot). If they're at `claude/skills/`, Claude Code won't discover them.

If they're in the right place but still not loading, restart Claude Code in the vault root.

### "Setup.sh failed midway through"

Re-run it. The script is idempotent - it skips steps that already succeeded. If the failure is on Homebrew or a specific tool install, run that step manually then re-run the script.

If you hit a step that genuinely doesn't work, [open an issue](https://github.com/ShubhashSharma/brain-template/issues) with the error message.

### "I want to undo everything and start fresh"

Delete your local vault folder. Delete your private GitHub repo. Re-run the installer. Your brain is portable - there's nothing else to clean up.

---

## Roadmap and contributions

### What's on the roadmap?

| Version | What |
|---|---|
| v1.1 | Live `mcp-amazon` reference build (SP-API + Ads API hooks) |
| v1.2 | TikTok Shop MCP companion |
| v1.3 | Shopify Admin MCP companion |
| v1.4 | Linux + Windows installer |
| v1.5 | Visual builder for new SKU pages |

The roadmap is honest. If something's not on it, it's not coming soon.

### Will you maintain this?

Yes - this isn't a one-shot. The roadmap is real, pull requests welcome, issues welcome.

If you fork it and build something cool, drop me a line via the repo issues - I'd love to see it.

### Can I contribute?

Yes. Three useful contributions in priority order:

1. **Bug reports / corrections** - issues on the repo
2. **New playbooks** - if you have a runbook for something the v1 doesn't cover (Q5 supplier shutdown, brand registry attack, listing suppression recovery), submit a PR adding it to `wiki/playbooks/`
3. **New concept pages** - same idea for operator concepts the v1 doesn't cover (NetSuite integration, Walmart marketplace, Amazon Vendor Central, etc)

Submit PRs to the `main` branch. I'll review and merge.

### Where do I get help?

- **Issues / questions:** https://github.com/ShubhashSharma/brain-template/issues
- **The repo itself:** https://github.com/ShubhashSharma/brain-template
- **The setup guide:** https://brain-template-guide-shubhash-sharmas-projects.vercel.app
- **For consultancy on operator infrastructure:** https://notasquare.io

### Is there a community / Discord / Slack?

Not yet. If there's enough interest after the SSL 2026 talk, that's an obvious next step. Best signal of interest: open an issue saying "yes, I'd join a community" - if enough people do, I'll spin one up.

---

## One more thing

If you take only one thing from the brain template, take this:

**Decisions compound. Decisions you can't reconstruct compound the wrong way.**

The single most valuable folder in the brain is `wiki/decisions/`. A 5-minute decision page now is a $300K insurance policy in 18 months when you're trying to remember why you switched suppliers, why you killed a SKU, or why you made that price test.

Fill in one SKU page on day one. Fill in one decision page the first time you make a real call. The rest builds itself.

---

*Built by [not a square](https://notasquare.io). MIT licensed. Companion to the Seller Sessions Live 2026 opening talk: "Architecting the Amazon Operator's Stack".*

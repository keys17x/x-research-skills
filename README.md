# X Research Skills

Reusable Hermes skills for X/Twitter market research, account discovery, and Chinese content transformation.

This repository contains three workflow-oriented skills designed to work together:

1. **x行情观点搜索** — find what the market is saying now
2. **x高质量分析账号筛选** — find who is worth following long term
3. **x推文研究转内容** — turn external tweet flows into Chinese research/content assets

---

## What This Repo Solves

Crypto discussion on X/Twitter is noisy.

Even when the information is valuable, it is usually fragmented across:
- short-form tweets
- chart screenshots
- repeated market narratives
- low-quality marketing or engagement bait

These skills are built to convert that noisy flow into a cleaner research pipeline:

```text
raw tweets
   ↓
market-view extraction
   ↓
account discovery
   ↓
Chinese research / content assets
```

---

## Included Skills

### 1) x行情观点搜索
**Folder:** `skills/x-hangqing-guandian-sousuo/`

Search X/Twitter for BTC, ETH, or narrative-specific market-analysis tweets, filter obvious noise, and output a Chinese summary of:
- main viewpoints
- representative tweets
- consensus vs disagreement
- key price levels / structure / logic

**Typical use cases**
- “What are people saying about BTC today?”
- “What is the current ETH market split?”
- “What are the main viewpoints around a narrative like AI / DeFi / altseason?”

**Main output**
- one-line conclusion
- mainstream viewpoints
- representative tweets
- consensus vs disagreement
- risk reminder

---

### 2) x高质量分析账号筛选
**Folder:** `skills/x-gaozhiliang-fenxi-zhanghao-shaixuan/`

Discover high-quality X/Twitter analysis accounts worth following long term around BTC, ETH, or a specific narrative.

This skill is not about finding a single viral tweet.
It is about identifying stable information sources.

**Typical use cases**
- build a BTC/ETH research watchlist
- find analysts with consistent output
- separate real analysis accounts from noise and marketing accounts

**Main output**
- A / B / C tier watchlist
- account style notes
- strengths / weaknesses
- follow-up suggestions for daily monitoring

---

### 3) x推文研究转内容
**Folder:** `skills/x-tuiwen-yanjiu-zhuan-neirong/`

Turn a batch of English X/Twitter analysis tweets into Chinese research assets.

This is **not** simple translation.
It is a rewrite-and-structure workflow that focuses on:
- viewpoint extraction
- de-duplication
- clustering
- Chinese summary generation
- content draft generation

**Typical use cases**
- convert English analysis tweets into Chinese research notes
- prepare content for posts / threads / comments / topic planning
- turn high-signal tweet samples into reusable writing material

**Main output**
- research summary
- viewpoint extraction
- short post draft
- thread outline
- topic ideas

---

## Recommended Workflow

These three skills are meant to work as a chain:

```text
Raw X/Twitter content
        ↓
[1] x行情观点搜索
Find what the market is saying now
        ↓
Representative tweets + recurring authors + market split
        ↓
[2] x高质量分析账号筛选
Find who is worth tracking long term
        ↓
Research watchlist / account pool
        ↓
[3] x推文研究转内容
Turn external content into Chinese research/content assets
        ↓
Chinese summaries / drafts / topic ideas
```

### In plain language

- Use **x行情观点搜索** when you want to know **what the market is saying now**.
- Use **x高质量分析账号筛选** when you want to know **who is worth following later**.
- Use **x推文研究转内容** when you want to turn external material into **your own usable Chinese output**.

---

## Suggested Usage Patterns

### Pattern A: Fast daily market check

```text
x行情观点搜索
→ get the current market split
→ x推文研究转内容
→ create a Chinese summary or post draft
```

Best for:
- daily BTC / ETH checking
- fast market commentary
- quick content preparation

### Pattern B: Build a long-term research system

```text
x行情观点搜索
→ identify recurring useful authors
→ x高质量分析账号筛选
→ build a long-term watchlist
→ x推文研究转内容
→ produce Chinese research summaries from that watchlist
```

Best for:
- long-term signal discovery
- reducing repeated manual searching
- building an account pool with compounding value

### Pattern C: Turn an existing watchlist into content

```text
x高质量分析账号筛选
→ build the account pool
→ collect posts from the A-tier accounts
→ x推文研究转内容
→ generate reusable Chinese research/content assets
```

Best for:
- weekly or daily summaries
- topic pipelines
- systematic content production

---

## Repo Structure

```text
x-research-skills/
├── README.md
├── LICENSE
└── skills/
    ├── x-hangqing-guandian-sousuo/
    │   └── SKILL.md
    ├── x-gaozhiliang-fenxi-zhanghao-shaixuan/
    │   └── SKILL.md
    └── x-tuiwen-yanjiu-zhuan-neirong/
        └── SKILL.md
```

---

## Requirements / Context

These skills were originally written for a Hermes-style agent workflow.

They assume an environment where an agent can:
- call shell commands
- use a Twitter/X access route
- read structured output
- turn that output into Chinese summaries or content

In the original workflow, the X access route is based on a browser-auth / unofficial access pattern rather than the official X API.

That means:
- availability can change over time
- cookie/session auth may expire
- platform-side changes can break parts of the workflow

---

## Boundaries

These skills are for:
- research
- account discovery
- content preparation
- viewpoint synthesis

They are **not** for:
- direct trade signaling
- blind translation of every tweet
- treating social-media opinions as verified facts

---

## Who This Repo Is For

This repo is useful if you want to:
- monitor BTC / ETH market narratives on X/Twitter
- build a stable watchlist of quality crypto-analysis accounts
- turn English tweet streams into usable Chinese research and content
- create a cleaner information pipeline from noisy social feeds

---

## License

MIT

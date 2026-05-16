---
title: "Summary AI — User Manual"
subtitle: "AI Discord bot to summarize your conversations"
date: "2026-05-15"
documentclass: article
geometry: margin=2.2cm
fontsize: 11pt
mainfont: "Helvetica"
monofont: "Menlo"
colorlinks: true
linkcolor: NavyBlue
urlcolor: NavyBlue
toc: true
toc-depth: 2
header-includes:
  - \usepackage{fancyhdr}
  - \pagestyle{fancy}
  - \fancyhead[L]{Summary AI - User Manual}
  - \fancyhead[R]{v1.0}
  - \fancyfoot[C]{\thepage}
---

\newpage

# Welcome to Summary AI

Summary AI is a Discord bot that **summarizes your conversations** using artificial intelligence. With a single command, catch up on what was said in a channel while you were away — without scrolling through hundreds of messages.

## In 30 seconds

| Step | Action |
|---|---|
| 1 | Invite the bot to the server (link provided at purchase) |
| 2 | An admin runs `/setup` to enable the allowed channels |
| 3 | Test with `/summary` in an allowed channel |
| 4 | Enjoy the Free tier (3 lifetime credits) then upgrade when ready |

\newpage

# 1. Available commands

## `/summary` — the main command

Run `/summary` in an allowed channel. An interactive menu opens:

- **Duration**: choose a preset window (1h, 6h, 12h, 24h, 48h, 72h) or click **"Specific date..."** to enter an exact period in the format `YYYY-MM-DD HH:MM`.
- **Language**: French or English. The summary will be in this language, regardless of the original language of the messages.
- **Style**: Fast (default). Other styles will arrive in v2.

With each change, the credit estimate is updated. When you are ready, click **"Run summary"**.

**The summary contains**:
- A general summary in 3-5 sentences
- The topics discussed (bullets)
- The decisions / actions taken (or "none")
- The open questions (or "none")

Message footer: number of messages processed, license tier, credits debited, cache status.

## `/credits` — see your remaining credits

Displays a visual gauge of your credits:

- **For you**: your personal balance (free tier or personal subscription).
- **For the server** (admin only, Manage Guild permission): the server's shared balance.

## `/optout` — privacy preferences

Privacy settings menu with 4 levels + scope:

| Option | Effect in v1 |
|---|---|
| **1. Hide my name in AI summaries** | **ACTIVE**: if the admin has enabled real names in `/setup`, your Discord username is still replaced with `Member N` for you. If the admin has not enabled the option, you are already anonymized by default, so the option has no additional effect. |
| 2. Do not use my messages for long-term memory | (v2 — inactive, planned for the long-term memory feature) |
| 3. Do not use my messages for analytics | (v2 — inactive, planned for the server analytics feature) |
| **4. Fully exclude my messages from AI processing** | **ACTIVE**: your messages are replaced with `[OPT-OUT USER N]` in all summaries, regardless of the other settings |

**Scope**: "This server only" or "All servers where the bot is present".

## `/license info` and `/license redeem`

- **`/license info`**: shows your personal tier + the server tier + the prices.
- **`/license redeem code:<CODE>`**: activates a license with a code (early adopters / partners).

## `/help` and `/support`

- **`/help`**: list of all commands.
- **`/support`**: links to the support server, e-mails (general + GDPR), ToS, Privacy Policy.

## `/setup` (admin only, Manage Guild)

Configuration panel:

- **Server context**: description of the server (1,000 characters max) sent to the AI so it understands the jargon, the game's universe, etc.
- **Channels & categories**: selection of the channels where `/summary` is allowed. Each channel can have its own description (300 characters max).
- **Real names**: enables Discord usernames display in summaries (see section 4 below).
- **Testers** (Server Free only): selection of the 5 people authorized to use the bot. The admin can change a tester as long as they have not started their first summary.
- **Custom admin prompt** (Server Ultra only): personalized instructions for the AI to follow (added after the non-negotiable safety rules).

\newpage

# 2. Credit system and pricing

## 2.1. How credits are consumed

Each `/summary` consumes **1 to 10 credits** depending on the amount of text analyzed by the AI:

| Tokens consumed | Credits debited |
|---|---|
| < 8,000 | 1 credit |
| 8,000 - 25,000 | 2 credits |
| 25,000 - 60,000 | 5 credits |
| 60,000 - 120,000 | 10 credits |
| > 120,000 | refused (window too large) |

The system is **hybrid**: before each summary, an estimate is made and held. After the call to the AI, the actual cost is computed and the difference is **automatically refunded**.

## 2.2. Pricing (USD, Discord converts based on your country)

### Personal tiers

| Tier | Price | Quota | Max lookback |
|---|---|---|---|
| **Free** | $0 | 3 lifetime credits / server | 24h |
| **Personal Premium** | $2.99/month | 50 credits/month | 48h |
| **Personal Ultra** | $9.99/month | 200 credits/month | 72h |

### Server tiers

| Tier | Price | Shared quota | Channels | Individual cap |
|---|---|---|---|---|
| **Server Free** | $0 | 25 lifetime credits | 1 | 5 named testers |
| **Server Starter** | $9.99/month | 250 credits/month | 3 | configurable (default 30) |
| **Server Premium** | $24.99/month | 700 credits/month | 10 | configurable (default 50) |
| **Server Ultra** | $59.99/month | 1,600 credits/month | unlimited | configurable (default 200) |

Server Ultra also includes the **custom admin prompt**: a text the admin can add to personalize the way the AI summarizes (style, tone, particular focus).

## 2.3. Authorization logic

When you run `/summary`, the bot evaluates in this order:

1. Does the server have an active license? -> consumes the server quota (+ individual cap if configured).
2. Otherwise, do you have an active personal license? -> consumes your personal quota.
3. Otherwise, do you have any free credits left on this server? -> consumes lifetime free credits.
4. Otherwise, refusal with an upgrade proposal.

\newpage

# 3. Cache and cooldown

## 3.1. Tile cache (7 days)

To avoid recomputing the same content 50 times, Summary AI splits time into **aligned 3-hour tiles** (00h-03h, 03h-06h, 06h-09h, etc. in UTC). Each tile is summarized **only once** then stored for 7 days.

If you request `/summary 24h`, the bot will:
1. Retrieve the 7-8 covering tiles (cache hit if already computed)
2. Compute the edge fragments (the hours that do not align exactly with a tile)
3. Merge it all into a coherent summary

**Expected savings**: 50-70% of AI cost on active servers.

## 3.2. Final summary cache (1 hour)

When a summary is generated, it is retained for **1 hour**. If you request exactly the same summary within that hour:

- **If you are within your 60 min cooldown**: the summary is served **free of charge** (0 credit debited).
- **If you are out of cooldown**: the summary is served at the stored cost.

## 3.3. 60-minute cooldown per channel

You can only run one `/summary` every 60 minutes **per channel** (but you can run another `/summary` immediately in a different channel). The cooldown protects against abuse.

\newpage

# 4. Real names (admin option)

## 4.1. Default mode: anonymization

By default, Summary AI systematically **anonymizes** members in the summaries. You appear as `Member 1`, `Member 2`, etc. The AI never sees your real Discord username.

Typical anonymized summary:

> *"One member indicates they are already committed to 1900 and have taken a day off. Another says they may be available for a future Vault, but an unplanned surgery could prevent them from attending."*

## 4.2. Real names activation by admin

The administrator of a server can enable the use of Discord usernames in `/setup` -> **Enable real names** button. An explicit confirmation is required (typing the word `ACTIVER`).

Once enabled:

- Summaries display your **Discord username** instead of `Member N`
- An **automatic announcement** is sent to the configured log channel to inform the members
- The **cache duration** of summaries containing usernames is reduced to **24 hours** (instead of 7 days)

Typical de-anonymized summary:

> *"**Alice** indicates she is already committed to 1900 and has taken a day off. **Bob** says he may be available, but an unplanned surgery could prevent him from attending."*

## 4.3. How to stay anonymous even if the admin has enabled real names

Use `/optout` and check **box 1: *Hide my name in AI summaries***. Choose the scope ("this server" or "all servers"). You will be displayed as `Member N` in all future summaries, regardless of the server option.

## 4.4. Access to stored data

**Server admins have no access to the bot's database.** Discord commands never give access to other members' summaries or counters. Only the service operator has direct technical access to the database, in strict compliance with the GDPR (Article 32).

# 5. Privacy and GDPR

## 5.1. What is NOT stored

- **Discord messages** sent to OpenAI: transmitted for the summary, never persisted by the Operator.
- **No payment information**: Discord handles everything.

## 5.2. What is stored

- Discord identifiers (numeric)
- Usage counters (credits consumed)
- Audit logs (date, channel, summary size)
- Tile cache (7 days) and final summary cache (1 hour)
- Opt-out preferences

## 5.3. Your GDPR rights

| Right | Command / action |
|---|---|
| Access | E-mail to `charlesbentleypro+rgpd@gmail.com` |
| Erasure | `/optout` level 4 + e-mail for complete deletion |
| Objection | `/optout` |
| Portability | GDPR e-mail |
| Rectification | GDPR e-mail |

## 5.4. Security

- TLS 1.2+ for all communications
- **Automatic sanitization**: emails, phone numbers, URLs, API secrets are replaced with markers before transmission to OpenAI
- **Anonymization**: your messages are attributed to `Member 1`, `Member 2`... — the AI never sees your real username
- **Anti prompt-injection**: strict XML encapsulation + hardened system prompts
- Automatic detection of suspicious output with admin alert

\newpage

# 6. Summary limitations

Summary AI generates summaries via an AI (`gpt-4o-mini`). Like any AI, it may:

- Misinterpret sarcasm or an internal reference
- Miss an important detail
- Synthesize imperfectly if the conversation is very long

**The bot does not replace human reading** of critical conversations (moderation, decision-making, sanctions, contractual negotiations, etc.).

# 7. Troubleshooting

| Symptom | Likely cause | Solution |
|---|---|---|
| "You are not in the list of testers" | Server Free + you are not authorized | Ask the admin to add you via `/setup` |
| "Monthly quota reached" | Server or personal tier exhausted | Wait for the end of the month or upgrade |
| "Your lifetime free quota is exhausted" | 3 credits already consumed on this server | Subscribe to a personal tier or a server tier |
| "Cooldown active: try again in X min" | You have already run a `/summary` on this channel recently | Wait, or test on another channel |
| "This channel is not configured for /summary" | Channel not whitelisted | Ask the admin to add it via `/setup` |
| "Volume too large" | Requested window > 120,000 tokens | Reduce the time window |
| The bot does not respond | OPENAI_API_KEY not configured on the operator side | Contact the bot operator |

# 8. Contact

- **Support Discord server**: *[link to be inserted by the operator]*
- **General e-mail**: *charlesbentleypro@gmail.com*
- **GDPR e-mail**: *charlesbentleypro+rgpd@gmail.com*
- **Privacy Policy**: *https://github.com/charlox123/summary-ai-bot/blob/main/docs/legal/*
- **ToS**: *https://github.com/charlox123/summary-ai-bot/blob/main/docs/legal/*

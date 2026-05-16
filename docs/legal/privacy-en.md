---
title: "Privacy Policy"
subtitle: "Summary AI — AI Summarization Discord Bot — GDPR Compliance"
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
  - \fancyhead[L]{Summary AI - Privacy Policy}
  - \fancyhead[R]{v1.0}
  - \fancyfoot[C]{\thepage}
---

\newpage

# 1. Identity of the data controller

**Charles Bentley**, hereinafter "the Operator", is the data controller for personal data collected through the Summary AI bot within the meaning of Regulation (EU) 2016/679 ("GDPR").

- E-mail: **charlesbentleypro@gmail.com**
- Dedicated GDPR e-mail: **charlesbentleypro+rgpd@gmail.com**
- Postal address: **Buc 78530, France**

# 2. Categories of data processed

| Category | Data | Source | Retention period |
|---|---|---|---|
| **Discord identifiers** | `user_id`, `guild_id`, `channel_id` (numeric) | Discord | As long as the user/server remains active |
| **Usage counters** | Credits consumed (lifetime / monthly) | Bot | 24 months after last use |
| **Audit logs** | Date, channel, summary size, license tier | Bot | 12 months |
| **Tile cache (anonymized)** | Partial 3-hour summaries, without usernames | Bot | 7 days |
| **Tile cache (real names)** | Partial summaries containing Discord usernames, only if the server admin has enabled the option | Bot | **24 hours** (reduced TTL) |
| **Final cache** | Complete summaries served | Bot | 1 hour |
| **Discord display_names** | Only if the admin has enabled `use_real_names` AND the member has not opted out via `/optout` option 1 | Discord | Present in the tile cache (24h max) |
| **Opt-out preferences** | 4 flags + scope (server or global) | Bot | As long as the user remains active |
| **Licenses** | Tier, dates, Discord entitlement identifiers | Discord Monetization | Duration + 12 months |
| **Bot lifecycle** | Invitation / removal date per server | Bot | 30 days after removal |

**Important**: the **Discord messages** transmitted for summary generation are **never stored** by the Operator. They are transmitted to OpenAI for the duration of the processing, then purged. Only the generated summaries (synthetic texts) may be cached temporarily (see table).

# 3. Purposes and legal bases

| Purpose | GDPR legal basis |
|---|---|
| On-demand summary generation | Performance of the contract (Article 6.1.b) |
| Credit counting and billing | Performance of the contract (Article 6.1.b) |
| Caching to reduce costs | Legitimate interest (Article 6.1.f) |
| Audit logs and abuse prevention | Legitimate interest (Article 6.1.f) |
| Compliance with legal obligations | Legal obligation (Article 6.1.c) |

# 4. Processors and transfers

| Processor | Role | Location | Safeguards |
|---|---|---|---|
| **OpenAI, L.L.C.** | Summary generation (`gpt-4o-mini`) | United States | EU-US Standard Contractual Clauses, OpenAI DPA, `store=false` (no persistence or retraining) |
| **Discord Inc.** | Platform and payments | United States | SCC, EU-US Data Privacy Framework |

Sending messages to OpenAI is necessary for the execution of the service. Before transmission, the messages are **sanitized**: emails, phone numbers, URLs, Discord mentions and detectable secrets are replaced with markers `[email]`, `[phone]`, `[link]`, `@member`, `[secret]`. The participants' identifiers are **anonymized** as `Member 1`, `Member 2`, etc. — the AI never sees the real usernames.

# 5. Your rights

In accordance with Articles 15 to 22 of the GDPR, you have the following rights:

## Right of access (Article 15)

Upon written request to **charlesbentleypro+rgpd@gmail.com**, you will receive within 30 days a JSON copy of all data stored about you.

## Right to erasure / right to be forgotten (Article 17)

Discord command **`/optout`** -> check "Fully exclude my messages from AI processing" + select the scope.

Upon written request, complete deletion of all data (usage counters, audit logs, preferences) within 30 days.

## Right to object (Article 21)

Discord command **`/optout`**: 4 levels available, of which only level 4 is active in v1 (the others are planned for v2). Choice of scope (this server only / all servers).

## Right to portability (Article 20)

Upon written request: structured JSON copy of your data within 30 days.

## Right of rectification (Article 16)

Upon written request to **charlesbentleypro+rgpd@gmail.com**.

## Right to lodge a complaint

You may file a complaint with the **CNIL** (the French data protection authority, 3 Place de Fontenoy, 75007 Paris) or with the supervisory authority of your country of residence in the EU.

# 6. Security

The Operator implements:

- encryption of communications (TLS 1.2+) with Discord and OpenAI;
- storage of the OpenAI API key as an environment variable, never in the source code or in a public git repository;
- access to the database restricted to the Operator;
- **strict XML encapsulation** of user messages to prevent prompt injection attacks (any instruction found in `<transcript>` is ignored by the AI);
- **automatic detection** of suspicious output with an alert in the configured admin log channel;
- audit logs to detect abuse;
- OpenAI parameter `store=false`: no persistence or retraining.

# 7. Auto-cleanup and retention periods

An automatic task runs every 6 hours and purges:

- cache tiles older than 7 days;
- final cached summaries older than 1 hour;
- usage counters older than 24 months;
- audit logs older than 12 months.

When the bot is removed from a server, the associated data is retained for **30 days** in case it is re-invited, then purged automatically.

# 8. Minors

Discord requires a minimum age of 13 (16 in some EU countries). The Operator does not knowingly process data of minors below this age. In case of a report, the data is deleted without delay.

# 9. Breach notification

In the event of a breach likely to result in a risk to the rights and freedoms of individuals, the Operator notifies the CNIL within 72 hours (Article 33) and informs the data subjects if the risk is high (Article 34).

# 10. Changes

This policy may be modified. Substantial changes are notified 15 days before they take effect via the support Discord server and the bot's public repository.

# 11. De-anonymization and database isolation

## 11.1. Anonymization by default

By default, the AI receives messages attributed to `Member 1`, `Member 2`, etc. No Discord username is transmitted. This is the **privacy by design** configuration within the meaning of Article 25 of the GDPR.

## 11.2. Real names mode (admin opt-in)

The administrator of a server may enable the use of Discord usernames in summaries. This activation:

- requires an explicit confirmation (typing "ACTIVER")
- triggers an **automatic announcement** in the configured log channel
- **reduces the cache duration** of summaries containing usernames to 24 hours
- is logged in the database with the timestamp and identifier of the admin who enabled it

## 11.3. Individual opposition

Any member may object to the use of their username via `/optout` option 1 (*Hide my name in AI summaries*), even if the admin has enabled real names. The opposition applies to the chosen scope (this server or all servers).

The opposition via `/optout` option 4 (*Fully exclude*) replaces the member's messages with `[OPT-OUT USER N]` in all summaries, regardless of the other settings.

## 11.4. Database isolation

The Operator guarantees that:

- **server administrators have no access to the bot's database**;
- the Discord commands (`/credits`, `/setup`, `/optout`, etc.) only give access to the server configuration or the personal data of the member invoking the command;
- no Discord command allows an admin to consult the usage counters, summaries, or audit logs of another member;
- only the Operator (data controller) has direct technical access to the database, in strict compliance with Article 32 of the GDPR.

This isolation is a contractual commitment of the Operator. The technical processors (OpenAI, Discord) only receive the data strictly necessary for the execution of the service.

# 12. Contact and exercise of rights

- Dedicated GDPR e-mail: **charlesbentleypro+rgpd@gmail.com**
- Support Discord server: **[link TBD]**

The Operator commits to respond within 30 days.

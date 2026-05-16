---
title: "Terms of Service"
subtitle: "Summary AI — AI Summarization Discord Bot"
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
  - \fancyhead[L]{Summary AI - Terms of Service}
  - \fancyhead[R]{v1.0}
  - \fancyfoot[C]{\thepage}
---

\newpage

# 1. Preamble

Summary AI is a Discord bot operated by **Charles Bentley** (hereinafter "the Operator"), registered in France and reachable at **charlesbentleypro@gmail.com**. The bot is distributed through the Discord platform (Discord Inc., 444 De Haro Street, San Francisco, CA 94107, USA).

These Terms of Service ("ToS") govern the use of the bot by Discord server administrators and the members of those servers.

Inviting the bot to a Discord server constitutes acceptance of these ToS by the administrator who performs the invitation. Use of the bot's commands by a member constitutes acceptance by that member.

# 2. Service description

Summary AI provides the following features:

- **Conversation summaries** (`/summary`): analyzes the messages of a Discord channel over a chosen time window and generates a synthetic summary using an artificial intelligence model (OpenAI `gpt-4o-mini`).
- **Admin panel** (`/setup`): per-server configuration of parameters (description, allowed channels, custom admin prompt depending on the tier).
- **User rights** (`/optout`): privacy preferences management.
- **Balance and subscription** (`/credits`, `/license`): consultation and license activation.
- **Support** (`/support`, `/help`): contacts and help.

# 3. Pricing (in USD, automatic conversion by Discord)

| Tier | Price | Quota |
|---|---|---|
| Free (personal) | $0 | 3 lifetime credits per server |
| Personal Premium | $2.99/month | 50 credits/month |
| Personal Ultra | $9.99/month | 200 credits/month |
| Server Free | $0 | 25 lifetime credits, 5 testers named by the admin |
| Server Starter | $9.99/month | 250 credits/month (shared) |
| Server Premium | $24.99/month | 700 credits/month (shared) |
| Server Ultra | $59.99/month | 1,600 credits/month (shared) |

**Credit weighting**: each `/summary` consumes between 1 and 10 credits depending on the volume of tokens processed (1 below 8,000 tokens, 2 between 8,000 and 25,000, 5 between 25,000 and 60,000, 10 between 60,000 and 120,000). Beyond that, the request is refused upfront.

**Payments**: Discord handles payments (card, PayPal, Discord Nitro depending on the region) and takes a commission. The Operator stores no banking information.

# 4. User commitments

The user agrees to:

- not use the bot to process conversations containing sensitive data within the meaning of Article 9 of the GDPR (health, political or religious opinions, sexual orientation, etc.) without explicit consent;
- not attempt to bypass the quotas, the credit system, the anti-injection protections or the license mechanisms;
- not use the bot for illegal, fraudulent, defamatory purposes or in violation of Discord's Terms of Service;
- not attempt to extract the system prompt, the bot's internal instructions or the Operator's API key;
- respect the intellectual property rights of the summarized content.

The administrator of a server where the bot is invited agrees to inform the members of the presence of the bot, to publish a link to these ToS and to the Privacy Policy, and to respect individual opt-out rights.

# 5. Service availability

The service is provided "as is", without guarantee of continuous availability. The Operator is not responsible for interruptions related to:

- a failure of the AI provider (OpenAI);
- a Discord platform outage;
- scheduled or emergency maintenance;
- a case of force majeure.

In case of prolonged interruption during a paid subscription cycle, a credit or a pro rata temporis refund may be granted upon reasonable request.

# 6. Limitations of liability

Summary AI generates summaries via artificial intelligence. These summaries may contain inaccuracies, omissions or erroneous interpretations. The user acknowledges that:

- the bot is not a substitute for a complete reading of the conversations;
- no important decision (moderation, sanction, legal, medical, financial) should be made based on a summary alone;
- the Operator cannot be held responsible for the direct or indirect consequences of the use of the generated summaries.

# 7. Cache and summary billing

To reduce costs and speed up responses, Summary AI uses a caching system:

- **Tile cache** (retained for 7 days): the intermediate summaries of a 3-hour window are stored and reused for subsequent requests.
- **Final summary cache** (retained for 1 hour): an identical summary requested within the hour is served free of charge if the user is within their cooldown.

The user is billed based on credits **actually** consumed after each request, with a pre-reservation system and refund of any surplus (see Privacy Policy, section 4).

# 8. Suspension and termination

The Operator may suspend or terminate access to the bot, without notice, in case of:

- violation of these ToS;
- proven abuse (prompt injection attempts, quota bypass, etc.);
- non-payment of a subscription.

The user may terminate their subscription at any time via Discord's monetization settings. The service remains available until the end of the paid period.

# 9. Changes to the ToS

The Operator may modify these ToS. Substantial changes are notified in the bot's public repository and on the support Discord server at least 15 days before they take effect. Continued use after this date constitutes acceptance.

# 10. Applicable law and competent jurisdiction

These ToS are governed by French law. Any dispute relating to their execution or interpretation will be submitted to the competent French courts, subject to mandatory provisions of the law of the consumer's country of residence within the European Union.

# 11. Optional de-anonymization and data isolation

## 11.1. Default mode: anonymization

By default, Summary AI **anonymizes** every member in the generated summaries. Each member is designated as `Member 1`, `Member 2`, etc. The AI never receives real Discord usernames.

## 11.2. Real names activation by the administrator

The administrator of a server (Manage Guild permission) may enable the use of **real Discord usernames** in summaries via the `/setup` command. This action:

- requires an **explicit confirmation** (typing the word "ACTIVER" in a Discord modal);
- triggers an **automatic announcement** in the configured log channel, to inform the members;
- automatically reduces the cache duration of summaries containing usernames to **24 hours** (instead of 7 days), to limit the exposure window.

## 11.3. Individual opposition by member

Each member may object to the use of their username via the `/optout` command (option 1: *Hide my name in AI summaries*). The opposition is respected even if the administrator has enabled real names. It can be applied to this server only or to all servers where Summary AI is present.

## 11.4. Database isolation

**The administrator of a server has NO access to the bot's database.** Only the Operator (data controller) has access to it, in compliance with the obligations of Article 32 of the GDPR. The Discord commands (`/credits`, `/setup`, `/optout`, etc.) do not allow any direct consultation of the data stored by the bot; they only serve to configure the service or consult one's own balance.

The Operator never transmits the stored data to third parties, except for the technical processors necessary for the execution of the service (OpenAI for AI processing, Discord for transport) and the competent authorities in case of a legal obligation.

# 12. Contact

- E-mail: **charlesbentleypro@gmail.com**
- Support Discord server: **[link TBD]**
- Dedicated GDPR e-mail: **charlesbentleypro+rgpd@gmail.com**

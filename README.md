# Summary AI

> Bot Discord d'IA qui résume vos conversations en quelques secondes.
> Cache map-reduce, système de crédits hybride pre-auth/settlement, anti prompt-injection, conforme RGPD.

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://www.python.org/)
[![discord.py](https://img.shields.io/badge/discord.py-2.4+-7289da.svg)](https://discordpy.readthedocs.io/)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-orange.svg)](https://www.gnu.org/licenses/agpl-3.0)

---

## Sommaire

- [Pourquoi Summary AI ?](#pourquoi-summary-ai-)
- [Fonctionnalités](#fonctionnalités)
- [Architecture en un coup d'œil](#architecture-en-un-coup-dœil)
- [Prérequis](#prérequis)
- [Installation et démarrage rapide](#installation-et-démarrage-rapide)
- [Configuration Discord (étape par étape)](#configuration-discord-étape-par-étape)
- [Variables d'environnement](#variables-denvironnement)
- [Commandes Discord](#commandes-discord)
- [Tarification et plans](#tarification-et-plans)
- [Sécurité et conformité RGPD](#sécurité-et-conformité-rgpd)
- [Documentation complète](#documentation-complète)
- [Développement](#développement)
- [Déploiement en production](#déploiement-en-production)
- [Roadmap](#roadmap)
- [Licence](#licence)
- [Contact](#contact)

---

## Pourquoi Summary AI ?

Sur un serveur Discord actif, beaucoup de membres ratent ce qui se dit pendant leurs absences. Scroller 500 messages pour comprendre ce qui s'est passé est fastidieux.

**Summary AI** résume une fenêtre de conversation en quelques secondes via OpenAI (`gpt-4o-mini`). En une commande `/summary`, tu obtiens :

- Un résumé général en 3-5 phrases
- Les thèmes abordés
- Les décisions / actions prises
- Les questions ouvertes

Le bot est conçu pour être **rentable** (cache map-reduce qui économise 50-70 % du coût IA), **sûr** (sanitisation + anti prompt-injection), et **conforme** (privacy by default, RGPD).

---

## Fonctionnalités

- **Résumés intelligents** via OpenAI `gpt-4o-mini` avec mise en cache 7 jours / 1 heure
- **Menu interactif** Discord (View + Modal + Selects + estimation crédits live)
- **Système de crédits hybride** : pre-authorization + settlement automatique avec remboursement du surplus
- **Cache map-reduce** sur tuiles temporelles de 3 heures alignées UTC
- **Anti prompt-injection** : encapsulation XML stricte, system prompts durcis, détection automatique de sortie suspecte
- **Sanitisation** automatique : emails / téléphones / URLs / secrets API masqués avant envoi à OpenAI
- **Anonymisation par défaut** des membres (`Membre N`), avec option admin de désanonymisation
- **4 niveaux d'opt-out** RGPD + scope serveur/global
- **Panneau admin visuel** `/setup` avec sections multi-modal
- **Tâche cron auto-cleanup** toutes les 6h (purge tuiles > 7j, audits > 12 mois)
- **Lifecycle complet** : message d'accueil `on_guild_join`, purge différée à 30 jours sur `on_guild_remove`

---

## Architecture en un coup d'œil

```
summary_ai/
├── bot.py                    # Bootstrap discord.py + EXTENSIONS
├── main.py                   # Entry point asyncio
├── config.py                 # Constantes + Settings pydantic
├── cogs/                     # 8 commandes slash
│   ├── summary.py            # /summary + menu View+Modal+estimation
│   ├── setup.py              # /setup panneau admin
│   ├── data.py               # /optout privacy settings 4 niveaux
│   ├── credits.py            # /credits jauges visuelles
│   ├── license.py            # /license info + redeem
│   ├── help.py               # /help
│   ├── support.py            # /support contacts
│   └── lifecycle.py          # on_guild_join + on_guild_remove
├── services/                 # 11 services métier
│   ├── prompt_safety.py      # Sanitisation + system prompts XML
│   ├── summary_service.py    # Pipeline map-reduce (orchestrateur)
│   ├── tile_cache_service.py # Cache tuiles 3h / TTL différencié
│   ├── final_cache_service.py# Cache résumé final 1h
│   ├── concat_service.py     # Concaténation messages avant tuilage
│   ├── credit_service.py     # tokens → crédits
│   ├── quota_service.py      # Reserve/settle/refund + cooldown
│   ├── license_service.py    # Licences user/guild + codes
│   ├── consent_service.py    # Opt-out 4 niveaux + scope
│   ├── openai_client.py      # Wrapper /v1/responses
│   └── log_service.py        # Audit + alertes admin
├── database/
│   ├── models.py             # 14 modèles SQLAlchemy
│   └── session.py            # Async engine + session factory
├── tasks/
│   └── cleanup.py            # Cron asyncio toutes les 6h
└── tools/
    └── init_db.py            # Raccourci dev (sans Alembic)

migrations/
└── versions/
    ├── 0001_initial_schema.py
    └── 0002_real_names_option.py

docs/
├── manuels/
│   ├── manual-fr.{md,pdf,docx}
│   └── manual-en.{md,pdf,docx}
├── legal/
│   ├── terms-fr.{md,pdf,docx}
│   ├── terms-en.{md,pdf,docx}
│   ├── privacy-fr.{md,pdf,docx}
│   └── privacy-en.{md,pdf,docx}
└── internal/
    ├── rgpd-guide.{md,pdf}
    └── api-key-security.{md,pdf}
```

---

## Prérequis

- **Python 3.12+** (`python3 --version`)
- **Compte OpenAI** avec une clé API (`OPENAI_API_KEY`) → <https://platform.openai.com/api-keys>
- **Application Discord** créée sur le portail développeur → <https://discord.com/developers/applications>
- **Pandoc + xelatex** *(optionnel)* pour régénérer les PDFs/DOCX → `brew install pandoc` + `brew install --cask mactex`

---

## Installation et démarrage rapide

```bash
# 1. Cloner le repo
git clone https://github.com/charlox123/summary-ai-bot.git
cd summary-ai-bot

# 2. Environnement virtuel
python3 -m venv .venv
source .venv/bin/activate

# 3. Dépendances
pip install -e ".[dev]"

# 4. Configuration (le .env n'est jamais commité)
cp .env.example .env
# Édite .env pour renseigner DISCORD_TOKEN, OPENAI_API_KEY, et GUILD_ID

# 5. Base de données
alembic upgrade head

# 6. Lancer le bot
python -m summary_ai
```

Le bot doit afficher `Connecté en tant que Summary AI#XXXX` après quelques secondes. Tape `/help` dans Discord pour vérifier.

---

## Configuration Discord (étape par étape)

### 1. Créer l'application Discord

1. Va sur <https://discord.com/developers/applications>
2. Clique sur **New Application**, nomme-la `Summary AI`
3. Note l'**Application ID** (visible sur la page General Information) → c'est `DISCORD_APP_ID`

### 2. Créer le bot

1. Onglet **Bot** → clique sur **Add Bot**
2. **Privileged Gateway Intents** : active `MESSAGE CONTENT INTENT` et `SERVER MEMBERS INTENT`
3. **Reset Token** → copie le token → c'est `DISCORD_TOKEN` (à coller dans `.env`)
4. **Public Bot** : décoche si tu veux que seul toi puisses inviter le bot

### 3. Inviter le bot sur un serveur de test

1. Onglet **OAuth2 → URL Generator**
2. Scopes à cocher : `bot` et `applications.commands`
3. Bot permissions à cocher :
   - View Channels, Read Message History, Send Messages, Embed Links, Use Slash Commands
4. Copie l'URL générée, ouvre-la dans le navigateur, invite sur ton serveur de test

### 4. Récupérer le GUILD_ID

1. Active le mode développeur Discord (Settings → Advanced → Developer Mode)
2. Clic droit sur ton serveur → `Copy Server ID` → c'est `GUILD_ID`

Le `GUILD_ID` permet de synchroniser les slash commands **uniquement sur ce serveur** (plus rapide en dev). Laisse vide en prod pour sync global (~1h de propagation Discord).

---

## Variables d'environnement

Toutes les variables sont documentées dans `.env.example`. Les principales :

| Variable | Obligatoire | Description |
|---|---|---|
| `DISCORD_TOKEN` | ✓ | Token du bot Discord |
| `DISCORD_APP_ID` | ✓ | Application ID Discord |
| `OPENAI_API_KEY` | ✓ | Clé API OpenAI (commence par `sk-proj-`) |
| `GUILD_ID` | recommandé | ID du serveur de test (sync rapide des slash commands) |
| `OPENAI_MODEL` | non | Défaut `gpt-4o-mini` |
| `DATABASE_URL` | non | Défaut SQLite local `data/summary.db` |
| `LOG_LEVEL` | non | `INFO` par défaut |
| `SYNC_COMMANDS` | non | `true` par défaut (sync à chaque boot) |
| `CREDIT_PRICE_USD` | non | `0.02` ($/crédit, modifiable sans toucher au code) |
| `*_PRICE_USD` / `*_CREDITS_MONTHLY` | non | Prix et quotas de chaque tier (modifiable) |
| `TERMS_URL` / `PRIVACY_URL` | non | URLs publiques affichées dans `/support` et le welcome |
| `SUPPORT_EMAIL` / `RGPD_EMAIL` | non | Adresses affichées dans `/support` |
| `LICENSE_ACTIVATION_CODES` | non | Codes d'activation manuelle (format CSV documenté dans le code) |

⚠️ **Le fichier `.env` ne doit jamais être commité.** Il est ignoré par `.gitignore`. Voir `docs/internal/api-key-security.md` pour la procédure complète.

---

## Commandes Discord

| Commande | Public | Description |
|---|---|---|
| `/summary` | tous | Résumer une fenêtre de conversation (menu interactif) |
| `/credits` | tous | Affiche tes crédits restants + jauge serveur (admin) |
| `/optout` | tous | Préférences de confidentialité (4 niveaux + scope) |
| `/help` | tous | Liste de toutes les commandes |
| `/support` | tous | Contacts + CGU + Politique de confidentialité |
| `/license info` | tous | Affiche le tier perso + tier serveur |
| `/license redeem code:<CODE>` | tous | Activer une licence via un code |
| `/setup` | admin Manage Guild | Panneau de configuration complet |

Voir le **manuel utilisateur complet** dans `docs/manuels/manual-fr.md` (et `manual-en.md`).

---

## Tarification et plans

Tous les prix sont en USD. Discord convertit automatiquement dans la devise locale de l'utilisateur.

### Tiers personnels

| Tier | Prix | Crédits | Lookback max |
|---|---|---|---|
| Free | 0 $ | 3 à vie / serveur | 24h |
| Personal Premium | 2,99 $/mois | 50/mois | 48h |
| Personal Ultra | 9,99 $/mois | 200/mois | 72h |

### Tiers serveur (partagés entre membres)

| Tier | Prix | Crédits | Channels | Cap individuel par défaut |
|---|---|---|---|---|
| Server Free | 0 $ | 25 à vie | 1 | 5 testeurs nommés |
| Server Starter | 9,99 $/mois | 250/mois | 3 | 30 |
| Server Premium | 24,99 $/mois | 700/mois | 10 | 50 |
| Server Ultra | 59,99 $/mois | 1 600/mois | illimité | 200 |

**Pondération en crédits** par requête : 1 (< 8k tokens), 2 (8-25k), 5 (25-60k), 10 (60-120k). Au-delà, refus en amont.

Tous les paramètres tarifaires sont modifiables via `.env` sans toucher au code.

---

## Sécurité et conformité RGPD

### Anti prompt-injection

- **Encapsulation XML stricte** : tout texte utilisateur passe par `html.escape(s, quote=True)` et est isolé dans des balises `<msg>` / `<transcript>` / `<partials>`.
- **System prompts durcis** qui ordonnent à l'IA d'**ignorer** toute instruction trouvée dans le transcript.
- **Détection automatique** de marqueurs suspects (`ignore your instructions`, `voici mon prompt`, etc.) dans la sortie OpenAI → flag dans les audit logs + alerte admin.
- **Sanitisation** des messages avant envoi : emails, téléphones, URLs, mentions Discord, secrets API → remplacés par des marqueurs.

### Anonymisation par défaut

Les membres sont anonymisés en `Membre 1`, `Membre 2`, etc. L'IA ne voit jamais les vrais pseudos Discord. L'admin peut activer l'option `use_real_names` dans `/setup` (avec confirmation explicite, annonce automatique, et TTL cache réduit à 24h). Chaque membre peut s'opposer individuellement via `/optout` option 1.

### Isolation de la base de données

**Les administrateurs des serveurs n'ont AUCUN accès à la base de données du bot.** Les commandes Discord ne donnent jamais accès aux données d'autres membres. Seul l'opérateur du service (responsable de traitement) a un accès technique direct, dans le respect de l'article 32 du RGPD.

### Auto-cleanup périodique

Une tâche asyncio s'exécute toutes les 6 heures et purge automatiquement :

- Tuiles de cache > 7 jours (ou > 24h si elles contiennent des pseudos réels)
- Cache de résumés finaux > 1 heure
- Compteurs d'usage mensuels > 24 mois
- Audit logs > 12 mois
- Données des serveurs où le bot a été retiré depuis > 30 jours

### Sous-traitants

- **OpenAI L.L.C.** (USA) : génération du résumé via `gpt-4o-mini`, paramètre `store=false` (aucune persistance, aucun réentraînement)
- **Discord Inc.** (USA) : plateforme et paiements

---

## Documentation complète

### Documentation utilisateur (livrables client)

- 📘 [Manuel utilisateur FR](docs/manuels/manual-fr.md) ([PDF](docs/manuels/manual-fr.pdf) · [DOCX](docs/manuels/manual-fr.docx))
- 📕 [User manual EN](docs/manuels/manual-en.md) ([PDF](docs/manuels/manual-en.pdf) · [DOCX](docs/manuels/manual-en.docx))
- 📜 [CGU FR](docs/legal/terms-fr.md) ([PDF](docs/legal/terms-fr.pdf) · [DOCX](docs/legal/terms-fr.docx))
- 📜 [Terms of Service EN](docs/legal/terms-en.md) ([PDF](docs/legal/terms-en.pdf) · [DOCX](docs/legal/terms-en.docx))
- 🔐 [Politique de confidentialité FR](docs/legal/privacy-fr.md) ([PDF](docs/legal/privacy-fr.pdf) · [DOCX](docs/legal/privacy-fr.docx))
- 🔐 [Privacy Policy EN](docs/legal/privacy-en.md) ([PDF](docs/legal/privacy-en.pdf) · [DOCX](docs/legal/privacy-en.docx))

### Documentation interne (privée, pour l'opérateur du bot)

- ⚖️ [Guide RGPD pour l'opérateur](docs/internal/rgpd-guide.md) ([PDF](docs/internal/rgpd-guide.pdf))
- 🔑 [Guide sécurité clé API OpenAI](docs/internal/api-key-security.md) ([PDF](docs/internal/api-key-security.pdf))

### Spécifications techniques

Le **brief technique complet** est dans `../brief-v1.0.md` (au-dessus du dossier `bot/`). Source de vérité pour toute décision d'architecture, de schéma BDD, ou de format de prompt.

---

## Développement

### Lancer les tests

```bash
pytest -q
ruff check .
```

### Ajouter un cog

1. Crée `summary_ai/cogs/mon_cog.py` avec une classe `MyCog(commands.Cog)` et une fonction `async def setup(bot)`.
2. Ajoute le module à `EXTENSIONS` dans `summary_ai/bot.py`.
3. Lance le bot, vérifie via `/help` que la nouvelle commande apparaît.

### Modifier un modèle BDD (migration Alembic)

```bash
# Après avoir modifié summary_ai/database/models.py :
alembic revision --autogenerate -m "description du changement"

# Relit le fichier généré dans migrations/versions/, ajuste si besoin.
alembic upgrade head

# Pour revenir en arrière :
alembic downgrade -1
```

### Recompiler les PDFs et DOCX

```bash
cd docs
for f in legal/terms-fr legal/terms-en legal/privacy-fr legal/privacy-en \
         manuels/manual-fr manuels/manual-en \
         internal/rgpd-guide internal/api-key-security; do
  pandoc "$f.md" -o "$f.pdf" --pdf-engine=xelatex
done
for f in legal/terms-fr legal/terms-en legal/privacy-fr legal/privacy-en \
         manuels/manual-fr manuels/manual-en; do
  pandoc "$f.md" -o "$f.docx" --reference-doc="../../../tools/Rapport_Mission_Projet_3A_v2.docx"
done
```

### Conventions de code

- Python 3.12+, async partout, type annotations partout
- Lint : `ruff` strict (`E, F, I, UP, B`), ligne max 100
- Tests : `pytest` + `pytest-asyncio` (`asyncio_mode=auto`)
- Pas de commentaires inutiles ; docstring courte sur les fonctions publiques uniquement
- Imports absolus (`from summary_ai.X import Y`)

---

## Déploiement en production

### Hébergement recommandé (par ordre de simplicité)

| Plateforme | Coût | Notes |
|---|---|---|
| **Railway.app** | ~5 $/mois après crédit gratuit | Variables d'env chiffrées, deploy auto depuis GitHub |
| **Render** | gratuit 750h/mois | Idem |
| **Fly.io** | gratuit jusqu'à 3 instances | `fly secrets set OPENAI_API_KEY=...` |
| **VPS Hetzner/OVH/Scaleway** | 5-10 €/mois | Contrôle total, exige un peu d'admin Linux |

### Checklist avant prod

- [ ] Hard limit OpenAI configuré (20-50 USD/mois selon ton tier) → <https://platform.openai.com/settings/organization/limits>
- [ ] Alerte e-mail d'usage anormal activée
- [ ] `.env` rempli avec un token Discord de **prod** (pas de test)
- [ ] `alembic upgrade head` exécuté sur la base de prod
- [ ] Backup chiffré quotidien de `data/summary.db` (`sqlite3 .backup` + `gpg --encrypt`)
- [ ] DPA OpenAI signé → <https://openai.com/policies/data-processing-addendum>
- [ ] CGU/PP publiés à `TERMS_URL` / `PRIVACY_URL` configurés dans `.env`
- [ ] Serveur Discord de support créé, lien permanent dans `SUPPORT_DISCORD_URL`

Voir `docs/internal/api-key-security.md` (15 min de lecture) pour la procédure complète.

---

## Roadmap

### v1.0 (livré)

- ✅ Pipeline `/summary` map-reduce avec cache
- ✅ Système de crédits hybride pre-auth/settlement
- ✅ Anti prompt-injection
- ✅ Anonymisation par défaut + désanonymisation opt-in admin
- ✅ Auto-cleanup périodique
- ✅ Lifecycle on_guild_join / on_guild_remove

### v1.1 (prévu)

- Intégration webhook Discord Monetization (entitlements automatiques)
- Invalidation du cache quand un user passe en opt-out
- Multiplicateurs de modèle pour le paramètre `/summary style:` (rapide / équilibré / premium)
- Dashboard web simple pour l'opérateur (stats globales, top consumers)

### v2 (futur)

- Profils factuels (memory long-terme) — sera opt-in admin + opt-in user
- Analytics serveur (hot topics, tendances)
- Multi-modèle (Claude, Gemini en plus de gpt-4o-mini)

---

## Licence

**AGPL-3.0** — voir [LICENSE](LICENSE).

> Tu peux utiliser, modifier et redistribuer ce code, mais **toute version dérivée mise à disposition (y compris hébergée en SaaS) doit aussi être publiée en open-source sous AGPL-3.0**. C'est ce qui empêche un concurrent de forker le bot pour le revendre en propriétaire fermé.

Si tu veux utiliser le code dans un contexte qui ne permet pas l'AGPL (intégration propriétaire, etc.), contacte l'opérateur pour une licence commerciale séparée.

---

## Contact

- **Opérateur** : Charles Bentley
- **Adresse** : Buc 78530, France
- **E-mail général** : charlesbentleypro@gmail.com
- **E-mail RGPD dédié** : charlesbentleypro+rgpd@gmail.com
- **Serveur Discord de support** : en cours de création
- **Repo GitHub** : <https://github.com/charlox123/summary-ai-bot>

Pour toute question RGPD, demande d'accès, opposition, ou suppression de données, écris à l'e-mail RGPD. Délai légal de réponse : 30 jours.

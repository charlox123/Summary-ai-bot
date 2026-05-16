---
title: "Summary AI — Manuel utilisateur"
subtitle: "Bot Discord d'IA pour résumer vos conversations"
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
  - \fancyhead[L]{Summary AI - Manuel utilisateur}
  - \fancyhead[R]{v1.0}
  - \fancyfoot[C]{\thepage}
---

\newpage

# Bienvenue sur Summary AI

Summary AI est un bot Discord qui **résume vos conversations** avec une intelligence artificielle. En une commande, retrouvez ce qui s'est dit dans un salon en votre absence — sans avoir à scroller des centaines de messages.

## En 30 secondes

| Étape | Action |
|---|---|
| 1 | Inviter le bot sur le serveur (lien fourni à l'achat) |
| 2 | Un admin lance `/setup` pour activer les salons autorisés |
| 3 | Tester avec `/summary` dans un salon autorisé |
| 4 | Profiter du tier Free (3 crédits à vie) puis upgrade quand prêt |

\newpage

# 1. Commandes disponibles

## `/summary` — la commande principale

Lance `/summary` dans un salon autorisé. Un menu interactif s'ouvre :

- **Durée** : choisis une fenêtre prédéfinie (1h, 6h, 12h, 24h, 48h, 72h) ou clique sur **"Date précise..."** pour saisir une période exacte au format `YYYY-MM-DD HH:MM`.
- **Langue** : Français ou English. Le résumé sera dans cette langue, peu importe la langue d'origine des messages.
- **Style** : Rapide (par défaut). Les autres styles arriveront en v2.

À chaque modification, l'estimation de crédits se met à jour. Quand tu es prêt, clique sur **"Lancer le résumé"**.

**Le résumé contient** :
- Un résumé général en 3-5 phrases
- Les thèmes abordés (bullets)
- Les décisions / actions prises (ou "aucune")
- Les questions ouvertes (ou "aucune")

Pied de message : nombre de messages traités, tier de licence, crédits débités, statut cache.

## `/credits` — voir tes crédits restants

Affiche une jauge visuelle de tes crédits :

- **Pour toi** : ton solde personnel (tier free ou abonnement perso).
- **Pour le serveur** (admin uniquement, permission Manage Guild) : solde partagé du serveur.

## `/optout` — préférences de confidentialité

Menu Privacy settings à 4 niveaux + scope :

| Option | Effet en v1 |
|---|---|
| **1. Hide my name in AI summaries** | **ACTIF** : si l'admin a activé les pseudos réels dans `/setup`, ton pseudo Discord est quand même remplacé par `Membre N` te concernant. Si l'admin n'a pas activé l'option, tu es déjà anonymisé par défaut donc l'option n'a pas d'effet supplémentaire. |
| 2. Do not use my messages for long-term memory | (v2 — inactif, prévue pour la fonctionnalité de mémoire long terme) |
| 3. Do not use my messages for analytics | (v2 — inactif, prévue pour la fonctionnalité d'analytics serveur) |
| **4. Fully exclude my messages from AI processing** | **ACTIF** : tes messages sont remplacés par `[OPT-OUT USER N]` dans tous les résumés, indépendamment des autres paramètres |

**Scope** : "Ce serveur uniquement" ou "Tous les serveurs où le bot est présent".

## `/license info` et `/license redeem`

- **`/license info`** : affiche ton tier perso + le tier du serveur + les prix.
- **`/license redeem code:<CODE>`** : active une licence avec un code (early adopters / partenaires).

## `/help` et `/support`

- **`/help`** : liste de toutes les commandes.
- **`/support`** : liens vers serveur de support, e-mails (général + RGPD), CGU, Politique de confidentialité.

## `/setup` (admin uniquement, Manage Guild)

Panneau de configuration :

- **Server context** : description du serveur (1 000 caractères max) envoyée à l'IA pour qu'elle comprenne le jargon, l'univers du jeu, etc.
- **Channels & categories** : sélection des salons où `/summary` est autorisé. Chaque salon peut avoir sa propre description (300 caractères max).
- **Pseudos réels** : permet d'activer l'affichage des pseudos Discord dans les résumés (cf. section 4 ci-dessous).
- **Testers** (Server Free uniquement) : sélection des 5 personnes autorisées à utiliser le bot. L'admin peut changer un testeur tant qu'il n'a pas démarré son premier résumé.
- **Custom admin prompt** (Server Ultra uniquement) : consignes personnalisées que l'IA doit suivre (ajoutées après les règles de sécurité non négociables).

\newpage

# 2. Système de crédits et tarification

## 2.1. Comment les crédits sont consommés

Chaque `/summary` consomme **1 à 10 crédits** selon la quantité de texte analysée par l'IA :

| Tokens consommés | Crédits débités |
|---|---|
| < 8 000 | 1 crédit |
| 8 000 - 25 000 | 2 crédits |
| 25 000 - 60 000 | 5 crédits |
| 60 000 - 120 000 | 10 crédits |
| > 120 000 | refus (fenêtre trop grande) |

Le système est **hybride** : avant chaque résumé, une estimation est faite et bloquée. Après l'appel à l'IA, le coût réel est calculé et la différence est **automatiquement remboursée**.

## 2.2. Tarification (USD, Discord convertit selon ton pays)

### Tiers personnels

| Tier | Prix | Quota | Lookback max |
|---|---|---|---|
| **Free** | 0 $ | 3 crédits à vie / serveur | 24h |
| **Personal Premium** | 2,99 $/mois | 50 crédits/mois | 48h |
| **Personal Ultra** | 9,99 $/mois | 200 crédits/mois | 72h |

### Tiers serveur

| Tier | Prix | Quota partagé | Channels | Cap individuel |
|---|---|---|---|---|
| **Server Free** | 0 $ | 25 crédits à vie | 1 | 5 testeurs nommés |
| **Server Starter** | 9,99 $/mois | 250 crédits/mois | 3 | configurable (défaut 30) |
| **Server Premium** | 24,99 $/mois | 700 crédits/mois | 10 | configurable (défaut 50) |
| **Server Ultra** | 59,99 $/mois | 1 600 crédits/mois | illimité | configurable (défaut 200) |

Le Server Ultra inclut également le **custom admin prompt** : un texte que l'admin peut ajouter pour personnaliser la façon dont l'IA résume (style, ton, focus particulier).

## 2.3. Logique d'autorisation

Quand tu lances `/summary`, le bot évalue dans cet ordre :

1. Le serveur a-t-il une licence active ? -> consomme le quota serveur (+ cap individuel si configuré).
2. Sinon, as-tu une licence personnelle active ? -> consomme ton quota perso.
3. Sinon, te reste-t-il du free sur ce serveur ? -> consomme du free à vie.
4. Sinon, refus avec proposition d'upgrade.

\newpage

# 3. Cache et cooldown

## 3.1. Cache des tuiles (7 jours)

Pour ne pas recalculer 50 fois le même contenu, Summary AI découpe le temps en **tuiles de 3 heures alignées** (00h-03h, 03h-06h, 06h-09h, etc. en UTC). Chaque tuile est résumée **une seule fois** puis stockée pour 7 jours.

Si tu demandes `/summary 24h`, le bot va :
1. Récupérer les 7-8 tuiles couvrantes (cache hit si déjà calculées)
2. Calculer les fragments de bord (les heures qui ne tombent pas pile sur une tuile)
3. Fusionner le tout en un résumé cohérent

**Économie attendue** : 50-70 % du coût IA sur les serveurs actifs.

## 3.2. Cache du résumé final (1 heure)

Quand un résumé est généré, il est conservé **1 heure**. Si tu redemandes exactement le même résumé dans cette heure :

- **Si tu es dans ton cooldown 60 min** : le résumé est servi **gratuitement** (0 crédit débité).
- **Si tu es hors cooldown** : le résumé est servi au coût stocké.

## 3.3. Cooldown 60 minutes par salon

Tu ne peux lancer qu'un seul `/summary` toutes les 60 minutes **par salon** (mais tu peux lancer un autre `/summary` immédiatement dans un autre salon). Le cooldown protège contre les abus.

\newpage

# 4. Pseudos réels (option admin)

## 4.1. Mode par défaut : anonymisation

Par défaut, Summary AI **anonymise** systématiquement les membres dans les résumés. Tu apparais comme `Membre 1`, `Membre 2`, etc. L'IA ne voit jamais ton vrai pseudo Discord.

Cas typique de résumé anonymisé :

> *« Un membre indique être déjà engagé sur 1900 et avoir pris un jour de congé. Un autre dit être potentiellement disponible pour un prochain Vault, mais qu'une opération chirurgicale non planifiée pourrait l'empêcher. »*

## 4.2. Activation des pseudos réels par l'admin

L'administrateur d'un serveur peut activer l'usage des pseudos Discord dans `/setup` -> bouton **Activer pseudos réels**. Une confirmation explicite est demandée (saisir le mot `ACTIVER`).

Une fois activé :

- Les résumés affichent ton **pseudo Discord** au lieu de `Membre N`
- Une **annonce automatique** est envoyée dans le salon de logs configuré pour informer les membres
- La **durée de cache** des résumés contenant des pseudos est réduite à **24 heures** (au lieu de 7 jours)

Cas typique de résumé désanonymisé :

> *« **Alice** indique être déjà engagée sur 1900 et avoir pris un jour de congé. **Bob** dit être potentiellement disponible, mais une opération chirurgicale non planifiée pourrait l'empêcher. »*

## 4.3. Comment rester anonyme même si l'admin a activé les pseudos réels

Utilise `/optout` et coche la **case 1 : *Hide my name in AI summaries***. Choisis le scope ("ce serveur" ou "tous les serveurs"). Tu seras affiché comme `Membre N` dans tous les futurs résumés, peu importe l'option du serveur.

## 4.4. Accès aux données stockées

**Les admins du serveur n'ont aucun accès à la base de données du bot.** Les commandes Discord ne donnent jamais accès aux résumés ou aux compteurs d'autres membres. Seul l'opérateur du service a un accès technique direct à la base de données, dans le respect strict du RGPD (article 32).

# 5. Confidentialité et RGPD

## 5.1. Ce qui n'est PAS stocké

- **Les messages Discord** envoyés à OpenAI : transmis pour le résumé, jamais persistés par l'Opérateur.
- **Aucune information de paiement** : Discord gère tout.

## 5.2. Ce qui est stocké

- Identifiants Discord (numériques)
- Compteurs d'usage (crédits consommés)
- Logs d'audit (date, salon, taille du résumé)
- Cache de tuiles (7 jours) et cache de résumés finaux (1 heure)
- Préférences opt-out

## 5.3. Tes droits RGPD

| Droit | Commande / action |
|---|---|
| Accès | E-mail à `charlesbentleypro+rgpd@gmail.com` |
| Effacement | `/optout` niveau 4 + e-mail pour suppression complète |
| Opposition | `/optout` |
| Portabilité | E-mail RGPD |
| Rectification | E-mail RGPD |

## 5.4. Sécurité

- TLS 1.2+ pour toutes les communications
- **Sanitisation automatique** : emails, téléphones, URLs, secrets API sont remplacés par des marqueurs avant transmission à OpenAI
- **Anonymisation** : tes messages sont attribués à `Membre 1`, `Membre 2`... — l'IA ne voit jamais ton vrai pseudo
- **Anti prompt-injection** : encapsulation XML stricte + system prompts durcis
- Détection automatique de sortie suspecte avec alerte admin

\newpage

# 6. Limites du résumé

Summary AI génère des résumés via une IA (`gpt-4o-mini`). Comme toute IA, il peut :

- Mal interpréter un sarcasme ou une référence interne
- Manquer un détail important
- Synthétiser de façon imparfaite si la conversation est très longue

**Le bot ne remplace pas la lecture humaine** des conversations critiques (modération, prise de décision, sanctions, négociations contractuelles, etc.).

# 7. Dépannage

| Symptôme | Cause probable | Solution |
|---|---|---|
| « Tu n'es pas dans la liste des testeurs » | Server Free + tu n'es pas autorisé | Demande à l'admin de t'ajouter via `/setup` |
| « Quota mensuel atteint » | Tier serveur ou perso épuisé | Attendre la fin du mois ou upgrade |
| « Ton quota free a vie est épuisé » | 3 crédits déjà consommés sur ce serveur | Souscrire un tier perso ou un tier serveur |
| « Cooldown actif : réessaie dans X min » | Tu as déjà lancé un `/summary` sur ce salon récemment | Attendre, ou tester sur un autre salon |
| « Ce salon n'est pas configure pour /summary » | Salon non whitelisté | Demande à l'admin de l'ajouter via `/setup` |
| « Volume trop important » | Fenêtre demandée > 120 000 tokens | Réduire la fenêtre temporelle |
| Le bot ne répond pas | OPENAI_API_KEY non configurée côté opérateur | Contacter l'opérateur du bot |

# 8. Contact

- **Serveur Discord support** : *https://discord.gg/ (en cours de création - sera communiqué prochainement)*
- **E-mail général** : *charlesbentleypro@gmail.com*
- **E-mail RGPD** : *charlesbentleypro+rgpd@gmail.com*
- **Politique de confidentialité** : *https://github.com/charlox123/summary-ai-bot/blob/main/docs/legal/*
- **CGU** : *https://github.com/charlox123/summary-ai-bot/blob/main/docs/legal/*

---
title: "Conditions Générales d'Utilisation"
subtitle: "Summary AI — Bot Discord d'IA de résumé"
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
  - \fancyhead[L]{Summary AI - CGU}
  - \fancyhead[R]{v1.0}
  - \fancyfoot[C]{\thepage}
---

\newpage

# 1. Préambule

Summary AI est un bot Discord opéré par **Charles Bentley** (ci-après « l'Opérateur »), enregistré en France, joignable à **charlesbentleypro@gmail.com**. Le bot est diffusé via la plateforme Discord (Discord Inc., 444 De Haro Street, San Francisco, CA 94107, USA).

Les présentes Conditions Générales d'Utilisation (« CGU ») régissent l'utilisation du bot par les administrateurs de serveur Discord et les membres de ces serveurs.

L'invitation du bot sur un serveur Discord vaut acceptation des présentes CGU par l'administrateur qui procède à l'invitation. L'utilisation des commandes du bot par un membre vaut acceptation par ce membre.

# 2. Description du service

Summary AI propose les fonctionnalités suivantes :

- **Résumé de conversations** (`/summary`) : analyse les messages d'un salon Discord sur une fenêtre temporelle choisie et génère un résumé synthétique via une intelligence artificielle (modèle OpenAI `gpt-4o-mini`).
- **Panneau d'administration** (`/setup`) : configuration des paramètres par serveur (description, salons autorisés, prompt admin personnalisé selon le tier).
- **Droits utilisateur** (`/optout`) : gestion des préférences de confidentialité.
- **Solde et abonnement** (`/credits`, `/license`) : consultation et activation des licences.
- **Support** (`/support`, `/help`) : contacts et aide.

# 3. Tarification (en USD, conversion automatique par Discord)

| Tier | Prix | Quota |
|---|---|---|
| Free (personnel) | 0 $ | 3 crédits à vie par serveur |
| Personal Premium | 2,99 $/mois | 50 crédits/mois |
| Personal Ultra | 9,99 $/mois | 200 crédits/mois |
| Server Free | 0 $ | 25 crédits à vie, 5 testeurs nommés par admin |
| Server Starter | 9,99 $/mois | 250 crédits/mois (partagés) |
| Server Premium | 24,99 $/mois | 700 crédits/mois (partagés) |
| Server Ultra | 59,99 $/mois | 1 600 crédits/mois (partagés) |

**Pondération en crédits** : chaque `/summary` consomme entre 1 et 10 crédits selon le volume de tokens consommé (1 < 8 000 tokens, 2 entre 8 000 et 25 000, 5 entre 25 000 et 60 000, 10 entre 60 000 et 120 000). Au-delà, la requête est refusée en amont.

**Paiements** : Discord gère les paiements (carte, PayPal, Discord Nitro selon les régions) et prélève une commission. L'Opérateur ne stocke aucune information bancaire.

# 4. Engagements de l'utilisateur

L'utilisateur s'engage à :

- ne pas utiliser le bot pour traiter des conversations contenant des données sensibles au sens de l'article 9 du RGPD (santé, opinions politiques ou religieuses, orientation sexuelle, etc.) sans consentement explicite ;
- ne pas tenter de contourner les quotas, le système de crédits, les protections anti-injection ou les mécanismes de licence ;
- ne pas utiliser le bot à des fins illégales, frauduleuses, diffamatoires ou contraires aux Conditions de Service de Discord ;
- ne pas tenter d'extraire le prompt système, les instructions internes du bot ou la clé API de l'Opérateur ;
- respecter les droits de propriété intellectuelle des contenus résumés.

L'administrateur d'un serveur où le bot est invité s'engage à informer les membres de la présence du bot, à publier un lien vers les présentes CGU et la Politique de Confidentialité, et à respecter les droits d'opt-out individuels.

# 5. Disponibilité du service

Le service est fourni « tel quel », sans garantie de disponibilité continue. L'Opérateur n'est pas responsable des interruptions liées à :

- une panne du fournisseur d'IA (OpenAI) ;
- une indisponibilité de la plateforme Discord ;
- une opération de maintenance planifiée ou d'urgence ;
- un cas de force majeure.

En cas d'interruption prolongée durant un cycle d'abonnement payant, un crédit ou un remboursement prorata temporis pourra être accordé sur demande raisonnable.

# 6. Limitations de responsabilité

Summary AI génère des résumés via une intelligence artificielle. Ces résumés peuvent contenir des inexactitudes, des omissions ou des interprétations erronées. L'utilisateur reconnaît que :

- le bot ne se substitue pas à une lecture intégrale des conversations ;
- aucune décision importante (modération, sanction, juridique, médicale, financière) ne doit être prise sur la seule base d'un résumé ;
- l'Opérateur ne peut être tenu responsable des conséquences directes ou indirectes de l'utilisation des résumés générés.

# 7. Cache et facturation des résumés

Pour réduire les coûts et accélérer les réponses, Summary AI utilise un système de cache :

- **Cache des tuiles** (conservées 7 jours) : les résumés intermédiaires d'une fenêtre de 3 heures sont stockés et réutilisés pour les demandes ultérieures.
- **Cache des résumés finaux** (conservés 1 heure) : un résumé identique demandé dans l'heure est servi gratuitement si l'utilisateur est dans son cooldown.

L'utilisateur est facturé sur la base des crédits **réellement** consommés après chaque requête, avec un système de pré-réservation et remboursement du surplus (cf. Politique de confidentialité, section 4).

# 8. Suspension et résiliation

L'Opérateur peut suspendre ou résilier l'accès au bot, sans préavis, en cas de :

- violation des présentes CGU ;
- abus avéré (tentatives de prompt injection, contournement des quotas, etc.) ;
- non-paiement d'un abonnement.

L'utilisateur peut résilier à tout moment son abonnement via les paramètres de monétisation Discord. Le service reste disponible jusqu'à la fin de la période payée.

# 9. Modifications des CGU

L'Opérateur peut modifier les présentes CGU. Les modifications substantielles sont notifiées dans le dépôt public du bot et sur le serveur Discord de support au moins 15 jours avant leur entrée en vigueur. La poursuite de l'utilisation après cette date vaut acceptation.

# 10. Droit applicable et juridiction compétente

Les présentes CGU sont régies par le droit français. Tout litige relatif à leur exécution ou interprétation sera soumis aux tribunaux français compétents, sous réserve des dispositions impératives du droit du pays de résidence du consommateur dans l'Union Européenne.

# 11. Désanonymisation optionnelle et isolation des données

## 11.1. Mode par défaut : anonymisation

Par défaut, Summary AI **anonymise** tous les membres dans les résumés générés. Chaque membre est désigné par `Membre 1`, `Membre 2`, etc. L'IA ne reçoit jamais les vrais pseudos Discord.

## 11.2. Activation des pseudos réels par l'administrateur

L'administrateur d'un serveur (permission Manage Guild) peut activer l'usage des **pseudos Discord réels** dans les résumés via la commande `/setup`. Cette action :

- nécessite une **confirmation explicite** (saisie du mot "ACTIVER" dans un modal Discord) ;
- déclenche une **annonce automatique** dans le salon de logs configuré, pour informer les membres ;
- réduit automatiquement la durée de cache des résumés contenant des pseudos à **24 heures** (au lieu de 7 jours), pour limiter la fenêtre d'exposition.

## 11.3. Opposition individuelle par membre

Chaque membre peut s'opposer à l'usage de son pseudo via la commande `/optout` (option 1 : *Hide my name in AI summaries*). L'opposition est respectée même si l'administrateur a activé les pseudos réels. Elle peut être appliquée à ce serveur uniquement ou à tous les serveurs où Summary AI est présent.

## 11.4. Isolation de la base de données

**L'administrateur d'un serveur n'a AUCUN accès à la base de données du bot.** Seul l'Opérateur (responsable de traitement) y a accès, dans le respect des obligations de l'article 32 du RGPD. Les commandes Discord (`/credits`, `/setup`, `/optout`, etc.) ne permettent aucune consultation directe des données stockées par le bot ; elles ne servent qu'à configurer le service ou consulter son propre solde.

L'Opérateur ne transmet jamais les données stockées à des tiers, à l'exception des sous-traitants techniques nécessaires à l'exécution du service (OpenAI pour le traitement IA, Discord pour le transport) et des autorités compétentes en cas d'obligation légale.

# 12. Contact

- E-mail : **charlesbentleypro@gmail.com**
- Serveur Discord de support : **https://discord.gg/ (en cours de création - sera communiqué prochainement)**
- E-mail RGPD dédié : **charlesbentleypro+rgpd@gmail.com**

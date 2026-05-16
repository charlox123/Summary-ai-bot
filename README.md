# Summary AI

> Bot Discord d'IA qui résume vos conversations en quelques secondes.

Ce dépôt rassemble la **documentation légale et utilisateur publique** du bot Summary AI : Conditions Générales d'Utilisation, Politique de Confidentialité, et Manuel utilisateur, en français et en anglais.

Le code source du bot n'est pas publié dans ce dépôt.

---

## À propos de Summary AI

Summary AI est un bot Discord qui utilise l'intelligence artificielle (modèle OpenAI `gpt-4o-mini`) pour résumer les conversations d'un salon Discord sur une fenêtre temporelle choisie. En une commande, retrouvez ce qui s'est dit sans avoir à scroller des centaines de messages.

**Fonctionnalités principales** :

- Résumés intelligents avec cache (économie de coûts)
- Système de crédits transparent (1 à 10 crédits par résumé selon la taille)
- Anonymisation par défaut des participants (`Membre 1`, `Membre 2`...)
- Option de désanonymisation **opt-in administrateur** + **opt-out individuel** pour les membres
- 4 niveaux de préférences de confidentialité via `/optout`
- Conforme RGPD : aucun message stocké, cache limité dans le temps, droit d'accès, d'opposition et d'effacement

---

## Documents disponibles

### Conditions Générales d'Utilisation (CGU)

| Langue | Markdown | PDF | Word |
|---|---|---|---|
| Français | [terms-fr.md](docs/legal/terms-fr.md) | [terms-fr.pdf](docs/legal/terms-fr.pdf) | [terms-fr.docx](docs/legal/terms-fr.docx) |
| English | [terms-en.md](docs/legal/terms-en.md) | [terms-en.pdf](docs/legal/terms-en.pdf) | [terms-en.docx](docs/legal/terms-en.docx) |

### Politique de Confidentialité (RGPD)

| Langue | Markdown | PDF | Word |
|---|---|---|---|
| Français | [privacy-fr.md](docs/legal/privacy-fr.md) | [privacy-fr.pdf](docs/legal/privacy-fr.pdf) | [privacy-fr.docx](docs/legal/privacy-fr.docx) |
| English | [privacy-en.md](docs/legal/privacy-en.md) | [privacy-en.pdf](docs/legal/privacy-en.pdf) | [privacy-en.docx](docs/legal/privacy-en.docx) |

### Manuel utilisateur

| Langue | Markdown | PDF | Word |
|---|---|---|---|
| Français | [manual-fr.md](docs/manuels/manual-fr.md) | [manual-fr.pdf](docs/manuels/manual-fr.pdf) | [manual-fr.docx](docs/manuels/manual-fr.docx) |
| English | [manual-en.md](docs/manuels/manual-en.md) | [manual-en.pdf](docs/manuels/manual-en.pdf) | [manual-en.docx](docs/manuels/manual-en.docx) |

---

## Tarification

Tous les prix sont en USD. Discord convertit automatiquement dans la devise locale de l'utilisateur.

### Tiers personnels

| Tier | Prix | Crédits |
|---|---|---|
| Free | 0 $ | 3 à vie / serveur |
| Personal Premium | 2,99 $/mois | 50/mois |
| Personal Ultra | 9,99 $/mois | 200/mois |

### Tiers serveur

| Tier | Prix | Crédits (partagés) |
|---|---|---|
| Server Free | 0 $ | 25 à vie, 5 testeurs nommés |
| Server Starter | 9,99 $/mois | 250/mois |
| Server Premium | 24,99 $/mois | 700/mois |
| Server Ultra | 59,99 $/mois | 1 600/mois |

Voir le [manuel utilisateur](docs/manuels/manual-fr.md) pour les détails complets (lookback max, channels max, cap individuel).

---

## Vos droits

Pour exercer vos droits RGPD (accès, rectification, effacement, opposition, portabilité) :

- Commandes Discord directes : `/optout` (préférences), `/data show` (consulter), `/data delete` (effacer)
- E-mail dédié : **charlesbentleypro+rgpd@gmail.com**
- Délai légal de réponse : **30 jours**

Pour toute autre question, contact général : **charlesbentleypro@gmail.com**

---

## À propos de l'opérateur

- **Responsable de traitement** : Charles Bentley
- **Adresse** : Buc 78530, France
- **E-mail général** : charlesbentleypro@gmail.com
- **E-mail RGPD dédié** : charlesbentleypro+rgpd@gmail.com
- **Serveur Discord de support** : en cours de création — sera communiqué prochainement

---

## Inviter le bot sur votre serveur

Pour ajouter Summary AI à votre serveur Discord, utilisez le lien officiel d'invitation (communiqué prochainement).

Permissions requises :
- View Channels
- Read Message History
- Send Messages
- Embed Links
- Use Slash Commands

Une fois invité, un administrateur du serveur doit lancer `/setup` pour configurer les salons autorisés et démarrer le service.

---

## Copyright

© 2026 Charles Bentley. Tous droits réservés.

Les documents présents dans ce dépôt (CGU, Politique de confidentialité, Manuel utilisateur, en français et en anglais) sont publiés à des fins d'information et de transparence légale, conformément aux obligations du Règlement (UE) 2016/679 (RGPD) et des conditions de monétisation de la plateforme Discord.

Toute reproduction, redistribution ou modification à des fins commerciales nécessite une autorisation écrite préalable de l'opérateur.

Le code source du bot Summary AI n'est pas publié et reste la propriété exclusive de l'opérateur.

---
name: inventaire-reseau
description: >
  Construit l'inventaire du réseau du participant — anciens clients, prescripteurs,
  contacts dormants — par interview, enrichi de Gmail/Outlook s'il est connecté et
  de l'export LinkedIn officiel. Déclenche sur « fais l'inventaire de mon réseau »,
  « qui pourrait me recommander », « liste mes anciens clients », « remets
  l'inventaire à jour », ou l'invocation /livementor-acquisition:inventaire-reseau.
---

# Inventaire-réseau — Savoir qui réactiver

## Mandat

- **Situation** : la recommandation est le premier canal d'acquisition des indépendants, et le moins outillé. Le réseau existe — anciens clients, prescripteurs, partenaires dormants — mais sa liste n'existe nulle part : elle est éparpillée entre la mémoire du participant, sa boîte mail et LinkedIn. Sans inventaire, la réactivation reste une bonne intention.
- **Objectif** : `reseau/contacts.md` rempli — chaque contact classé en trois familles (**ancien client**, **prescripteur potentiel**, **contact dormant à potentiel**) avec sa dernière interaction et un angle de réactivation possible. En sortie, le participant sait par qui commencer.
- **Contraintes** :
  - L'interview est la source principale : elle marche toujours, sans connecteur ni export. Gmail/Outlook et l'export LinkedIn enrichissent, ils ne conditionnent rien.
  - Réseau LinkedIn : uniquement l'export officiel fourni par le participant (chemin plus bas). Pas de scraping du réseau personnel.
  - Un angle de réactivation sort de l'historique réel de la relation, jamais d'une invention. Faute de matière, la case reste vide : c'est une question à poser au participant, pas un blanc à combler.
  - Ce skill fait autorité sur le format de `reseau/contacts.md` (plus bas) ; `rediger-reactivation` le consomme.
- **Indications** :
  - L'interview, par vagues courtes plutôt qu'en questionnaire d'un bloc : les clients des 2-3 dernières années, les missions qui se sont bien passées, qui connaît du monde, qui prescrit naturellement, les partenaires passés (lieux, structures, confrères).
  - Gmail ou Outlook connecté à Cowork → repère les fils dormants : des clients sans échange depuis six mois et plus. Sinon, propose une fois la connexion, sans en faire un préalable.
  - L'export LinkedIn, si le participant veut ratisser plus large : LinkedIn → Préférences et confidentialité → « Obtenir une copie de vos données » → Relations (CSV reçu par email en quelques minutes). Le CSV donne nom, entreprise, poste, date de connexion : il ravive des noms oubliés, il ne classe rien tout seul — chaque nom retenu passe par le participant.
  - Tout le monde n'entre pas dans l'inventaire : un contact y figure parce qu'on voit pourquoi le réactiver. Quinze contacts avec un angle valent mieux que deux cents lignes de CSV recopiées.
  - L'inventaire est une photo datée. Sur « remets-le à jour », relis aussi `reseau/messages/` et `conversion/prospects/` pour rafraîchir les dernières interactions.
  - En sortie, propose par qui commencer : relation encore chaude et angle déjà clair d'abord. (L'exercice de la session : réactiver 5 contacts dans la semaine, dont 2 anciens clients et 1 demande de mise en relation.)

## `reseau/contacts.md` — le format

Une section par famille, un tableau par section :

```markdown
# Inventaire du réseau

Dernière mise à jour : YYYY-MM-DD

## Anciens clients
| Contact | Relation | Dernière interaction | Angle de réactivation |
|---|---|---|---|
| Salle Gymtonic | ateliers nutrition animés en 2024 | 2024-11 | proposer un atelier de rentrée |

## Prescripteurs potentiels
[même tableau]

## Contacts dormants à potentiel
[même tableau]
```

Exemples de classement. Camille, nutritionniste : ses anciennes patientes satisfaites en anciens clients (sources de bouche-à-oreille), les médecins, psys et coachs sportifs en prescripteurs potentiels, la salle de sport où elle donnait des ateliers en contact dormant à potentiel. Un photographe : les mariés et entreprises shootés en anciens clients, les wedding planners et agences événementielles en prescripteurs, le lieu de réception qui le recommandait autrefois en dormant.

---
name: analyser-prospect
description: >
  Creuse un prospect en profondeur (site web, presse, avis, offres d'emploi, réseaux
  sociaux…) et produit une fiche d'analyse dans prospection/analyses/, la matière première
  du futur message de prospection. Déclenche sur « analyse ce prospect », « creuse cette
  entreprise », « prépare-moi une fiche sur X », ou l'invocation
  /livementor-acquisition:analyser-prospect.
---

# Analyser-prospect — La fiche qui prépare l'approche

## Mandat

- **Situation** : une ligne de CSV ne suffit pas pour écrire un message qui ne ressemble pas à du démarchage de masse. Avant l'approche, il faut une compréhension réelle du prospect.
- **Objectif** : une fiche `prospection/analyses/{prospect}.md`, la matière première du futur message de prospection (format plus bas).
- **Contraintes** :
  - Données publiques d'entreprise uniquement ; pour les personnes, rien au-delà de leur présence professionnelle publique (LinkedIn, page équipe).
  - Ne jamais présenter une hypothèse comme un fait : le participant enverra un message basé sur cette fiche, une erreur factuelle le grille auprès du prospect.
  - Si une source ne donne rien, dis-le et passe. Une fiche honnête avec 3 angles solides vaut mieux qu'une fiche gonflée.
  - La restitution au participant tient en quelques lignes (les découvertes qui comptent), pas en une relecture du fichier.
- **Indications** :
  - Avant de creuser, lis `CLAUDE.md` (l'offre et le client idéal du participant) et la ligne du prospect dans le CSV de `prospection/` (ou ce que le participant t'en dit).
  - Si `.env.apify` n'existe pas, déroule d'abord le setup technique du skill `sourcing` : c'est lui qui fait autorité sur l'accès Apify.
  - Creuse selon la grille de lecture, choisis tes sources avec le routeur (sections plus bas).

## La grille de lecture — 7 angles

Tous les angles ne sont pas pertinents pour chaque prospect : la grille sert à ne rien oublier, pas à tout remplir. **Un angle vaut la peine d'être creusé s'il peut changer le message qu'on enverra à ce prospect.**

| Angle | Ce qu'il peut changer dans l'approche |
|---|---|
| Positionnement affiché | parler leur langue, ne pas pitcher ce qu'ils font déjà |
| Douleurs apparentes (offres d'emploi, avis) | le problème par lequel ouvrir |
| Dynamique récente (levée, recrutement, expansion, partenariat) | le « pourquoi maintenant » du message |
| Identité visuelle / éditoriale | le terrain d'une collaboration créative |
| Ton de communication | le registre du message (formel, complice, technique…) |
| Valeurs / promesse | l'angle d'affinité sincère |
| La personne qui décide | à qui on écrit, et ce qui compte pour elle |

## Sources (en coulisses)

Commence par le moins cher et le plus parlant : le site du prospect + une recherche web/presse. Élargis ensuite selon le type de prospect et les angles retenus :

| Source | Outil | Quand |
|---|---|---|
| Site web (accueil, offre, à propos, équipe, blog) | `apify/website-content-crawler` | presque toujours, en premier |
| Presse, mentions web | recherche web | presque toujours, en premier |
| Offres d'emploi récentes | `apimaestro/linkedin-jobs-scraper-api` | entreprise qui recrute → besoin latent |
| Avis Google / Trustpilot | `compass/crawler-google-places` | commerce, cabinet, lieu, service local |
| Posts LinkedIn entreprise | `harvestapi/linkedin-company-posts` | entreprise B2B active sur LinkedIn |
| Instagram | `compass/instagram-scraper` | cible visuelle (marque, média, créateur, santé/coaching) |

Mêmes réflexes que `sourcing` : sources présentées au participant en termes métier, petit test peu coûteux avant d'élargir, logique `apify-ultimate-scraper` pour les cas non prévus.

## La fiche

- **En-tête** : prospect, date, pourquoi lui (le signal qui l'a fait entrer dans le CSV).
- **Les angles creusés** : une section par angle retenu. Chaque info porte sa source et son niveau de confiance : **vérifié** (vu à la source), **probable** (recoupé), **hypothèse** (déduction à valider).
- **Angles écartés** : une ligne chacun, avec la raison. Écarter est un choix, pas un oubli — et le participant peut ne pas être d'accord.
- **À retenir pour l'approche** : les 2-3 signaux les plus exploitables, reliés à l'offre du participant.

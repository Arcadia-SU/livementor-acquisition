---
name: calendrier
description: >
  Répond aux questions sur l'état du calendrier éditorial, applique les modifications
  demandées (déplacements, statuts, dates de publication), et régénère l'artifact kanban
  calendrier-editorial. Déclenche sur « quoi en retard », « qu'est-ce qui est prévu »,
  « déplace ce post », « passe-le à publié », « mets à jour le calendrier », ou
  l'invocation /livementor-acquisition:calendrier — et automatiquement après toute
  modification d'un fichier de contenu par un autre skill (idees, rediger-*).
---

# Calendrier — L'état du contenu, à jour

## Mandat

- **Situation** : le participant pose une question sur son calendrier éditorial, demande une modification, ou veut rafraîchir la vue. La vérité vit dans `creation-de-contenu/contenus/` : un fichier par contenu, dont le front-matter porte statut, dates et format. L'artifact `calendrier-editorial` (vue kanban) n'est qu'un snapshot : ses données sont gelées à sa dernière régénération.
- **Objectif** : selon la demande — une réponse exacte (lue dans les fichiers), une modification appliquée, ou l'artifact régénéré avec un snapshot à jour.
- **Contraintes** :
  - Source unique de vérité : les fichiers `contenus/*.md`. Pas de cache, pas d'inférence — toujours relire.
  - Pas de création de nouveaux contenus : c'est le territoire d'`idees` et des `rediger-*`.
  - Toute modification respecte le schéma de fichier du skill `idees` (qui fait autorité dessus).
  - Les actions irréversibles (suppression d'un fichier, changement de date qui invalide une publication imminente) passent par une confirmation du participant.
  - Quand un autre skill modifie un fichier de `contenus/`, régénère l'artifact dans la foulée, sans qu'on te le demande.
  - À la régénération, seules les données changent (`allItems`, `SNAPSHOT_DATE`) : le HTML (CSS, layout) reste structurellement identique. Repars de la dernière version connue.
- **Indications** :
  - Les définitions opérationnelles et les cas typiques sont plus bas.
  - Si une modification crée un trou visible (plus aucun LinkedIn prévu cette semaine alors que `cadence.md` dit 3/sem), signale-le — sans bloquer la modification.
  - Si `date_prevue` figure dans le nom du fichier et change, renomme selon la convention du skill `idees` (stabilité privilégiée au-delà du statut `brouillon`).

## Définitions opérationnelles

- **En retard** = `date_prevue` dépassée et `statut` ≠ `publie`.
- **À venir** = `statut: pret`, triés par `date_prevue` croissante.
- **En cours** = `statut: brouillon`.
- **Vivier** = `statut: idee`.

## Cas typiques

- « Qu'est-ce qui est prévu cette semaine / ce mois ? » → fichiers dont `date_prevue` tombe dans la fenêtre, présentés par date.
- « Quoi en retard ? » → `date_prevue < aujourd'hui` et `statut ∈ {idee, brouillon, pret}`.
- « Combien de posts par statut / par format ? » → comptages.
- « Déplace ce post à mardi » → `date_prevue` mise à jour (+ renommage si la date est dans le nom).
- « Passe-le à publié » → `statut: publie`, `date_publiee` (le jour donné, sinon aujourd'hui), `url_publication` si fournie.
- « Supprime cette idée » → confirmation, puis suppression.
- Contenu sans `date_prevue` → il vit dans son statut (vivier, en cours…), jamais « en retard » ; propose une date si le participant veut le planifier.
- Nom de fichier et front-matter en désaccord (date, slug) → le front-matter fait foi ; signale et propose le renommage.
- Statut hors cycle (`idee` / `brouillon` / `pret` / `publie`) → signale-le et propose la correction, ne l'interprète pas en silence.

## L'artifact `calendrier-editorial`

Vue kanban par statut, en mode snapshot : les données sont des constantes JS dans le HTML (`allItems`, `SNAPSHOT_DATE`).

- **Régénérer** : lis le HTML existant (`mcp__cowork__list_artifacts` puis `Read` sur le `path` retourné), remplace le bloc `// --- DATA SNAPSHOT ---`, renvoie via `mcp__cowork__update_artifact` (id `calendrier-editorial`).
- **S'il n'existe pas encore**, crée-le (kanban par statut, une carte par contenu : sujet, format, date) puis continue en mode snapshot.
- Le rafraîchissement automatique côté client n'est pas possible (pas d'accès aux fichiers depuis l'artifact lui-même) : l'artifact reste un snapshot, et c'est ce skill qui le tient à jour.

---
name: idees
description: >
  Génère 5 à 7 idées de contenu (LinkedIn, newsletter, article) à partir des sources
  publiques listées dans sources-idees.md, chacune ancrée dans un signal observé. Crée
  un fichier au statut idee pour chaque proposition retenue. Déclenche sur « trouve-moi
  des sujets », « des idées de posts », « qu'est-ce que je peux écrire », « remplis mon
  calendrier », ou l'invocation /livementor-acquisition:idees.
---

# Idées — Des sujets ancrés dans des signaux réels

## Mandat

- **Situation** : le participant veut alimenter son calendrier éditorial. Ses fichiers de référence existent (`sources-idees.md`, `cadence.md`, `voix.md`) et `creation-de-contenu/contenus/` contient les contenus déjà capturés, à des statuts variés.
- **Objectif** : 5 à 7 propositions de sujets présentées au participant, chacune ancrée dans un signal observé sur ses sources et reliée à son positionnement. Pour chaque proposition retenue, un fichier au statut `idee` dans `creation-de-contenu/contenus/` (schéma plus bas).
- **Contraintes** :
  - Les sources interrogées viennent de `sources-idees.md`. Pas d'invention de sources.
  - Chaque proposition est ancrée dans un signal vérifiable (URL, citation, référence d'un fil de discussion). Pas de sujets plaqués sans observation.
  - Évite les doublons : lis les contenus existants de `contenus/` pour connaître les sujets déjà couverts.
  - Validation du participant idée par idée avant de créer le moindre fichier.
- **Indications** :
  - Couverture plutôt que volume : mixe plusieurs natures de signaux — questions récurrentes du client idéal, retours d'expérience, débats, actualité du secteur. Privilégie ce qui résonne avec les douleurs nommées dans `CLAUDE.md`.
  - Interroge les sources via WebSearch (découvrir) et WebFetch (lire en détail), en requêtes parallèles quand elles sont indépendantes. Pour une source que WebFetch ne lit pas (Instagram par exemple), charge le skill `sourcing` : l'accès à ces plateformes est son territoire.
  - Présente chaque idée en trois temps : (a) le signal observé en une phrase, avec sa source ; (b) l'angle pour le participant en une ou deux phrases, depuis son positionnement ; (c) le format suggéré (`linkedin` / `newsletter` / `article`).
  - La date de publication se décide avec le participant ; `cadence.md` sert de repère pour en proposer une cohérente avec son rythme. Laisse vide si non décidée : `calendrier` tranchera plus tard.
  - Si le participant apporte ses propres idées, traite-les pareil : fichier au statut `idee` après validation, `source_idee: participant`.
  - Toute écriture dans `contenus/` périme l'artifact kanban : en fin d'action, charge le skill `calendrier` pour le régénérer.

## Le fichier candidat — schéma

Ce skill fait autorité sur ce schéma ; `calendrier` et les `rediger-*` le respectent.

Nom : `creation-de-contenu/contenus/{date_prevue}-{slug}.md` — `{slug}` en kebab-case court (3-6 mots), `{date_prevue}` au format `YYYY-MM-DD`, omise du nom si non décidée. Si `date_prevue` change ensuite, le nom suit la convention (stabilité privilégiée au-delà du statut `brouillon`). Si un fichier du même nom existe déjà, présente-le au participant plutôt que d'écraser. Front-matter YAML :

```yaml
format: linkedin | newsletter | article
sujet: …
statut: idee        # puis brouillon → pret → publie
date_prevue:        # YYYY-MM-DD, vide si non décidée
date_publiee:       # vide jusqu'à publication
source_idee:        # URL ou référence du signal, ou « participant »
themes:             # douleurs du client idéal correspondantes
```

Champs qui peuvent s'ajouter au fil de la vie du fichier : `url_publication`, `metriques`.

## Recherche sur les forums type Reddit

Pertinent seulement si les sources du participant s'y prêtent (sujets discutés en anglais, ou communautés FR réellement actives). L'opérateur `site:reddit.com` dans WebSearch et le fetch HTML direct sur reddit.com sont peu fiables ; la voie qui marche est l'API JSON publique via WebFetch :

- Recherche dans un subreddit : `https://old.reddit.com/r/{subreddit}/search.json?q={mots}&restrict_sr=1&sort=top&t=year&limit=10`
- Recherche globale : `https://old.reddit.com/search.json?q={mots}&sort=relevance&t=year&limit=10`
- Lecture d'un fil (post + commentaires) : ajouter `.json` au permalink.

Requêtes en 2-3 mots du vocabulaire authentique de la cible (« meal prep overwhelmed », « wedding photographer prices »), plusieurs en parallèle plutôt qu'une optimisée, filtre après réception (`num_comments ≥ 5`). Cible FR : les communautés y sont peu actives, les sources de `sources-idees.md` sont souvent plus productives. Si l'API JSON est inaccessible, WebSearch avec « reddit » en mot-clé remonte des agrégateurs qui citent les fils.

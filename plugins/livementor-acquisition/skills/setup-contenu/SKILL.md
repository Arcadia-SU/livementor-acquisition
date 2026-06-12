---
name: setup-contenu
description: >
  Crée les trois fichiers de référence du pôle contenu dans creation-de-contenu/ :
  cadence.md (fréquence par format), sources-idees.md (où chercher des sujets) et
  voix.md (squelette de la voix éditoriale, enrichi ensuite par calibrer-voix).
  Déclenche sur « configure mon contenu », « prépare mon système de contenu »,
  « on installe la création de contenu », ou l'invocation
  /livementor-acquisition:setup-contenu. Ne calibre pas la voix en profondeur :
  c'est le rôle de calibrer-voix, qui prend la suite.
---

# Setup-contenu — Les fondations du pôle contenu

## Mandat

- **Situation** : le participant démarre la création de contenu. Son `CLAUDE.md` racine existe (client idéal, douleurs, plateformes) et le dossier `creation-de-contenu/` aussi. Aucun des trois fichiers de référence n'est censé exister : s'ils sont déjà là, c'est une reconfiguration — clarifie le périmètre voulu avant d'agir.
- **Objectif** : trois fichiers créés dans `creation-de-contenu/`, validés par le participant, qui serviront de référence à tous les autres skills contenu :
  - `cadence.md` — la fréquence par format de publication ;
  - `sources-idees.md` — les endroits où le skill `idees` ira chercher des sujets ;
  - `voix.md` — le squelette de la voix éditoriale, à enrichir ensuite par `calibrer-voix`.
- **Contraintes** :
  - Ne modifie pas `CLAUDE.md` : il appartient au skill `setup`.
  - Ne calibre pas la voix en profondeur : `voix.md` reste un squelette qui pointe vers `calibrer-voix`. C'est lui qui fait autorité sur le format des règles.
  - Validation du participant sur chacune des trois dimensions (cadence, sources, voix) avant de figer un fichier.
  - Si `CLAUDE.md` ne contient pas de client idéal nommé, ses douleurs et les plateformes de prise de parole, ne démarre pas : propose de passer (ou repasser) par le skill `setup`.
- **Indications** :
  - Lis `CLAUDE.md` d'abord : la cadence part des plateformes déjà choisies, les sources se déduisent du client idéal et de ses douleurs.
  - Defaults de cadence si rien n'est précisé : 3 posts LinkedIn/semaine, 1 newsletter/15 jours, 1 article long/mois. Propose-les, le participant ajuste.
  - Pour les sources : propose 5 à 7 endroits publiquement accessibles où son client idéal s'exprime ou s'informe — forums et groupes spécialisés, presse sectorielle, comptes LinkedIn ou Instagram pertinents, podcasts, newsletters du secteur. Privilégie la couverture de plusieurs natures de signal (questions concrètes, débats, retours d'expérience, actualité) plutôt que la quantité.
  - Les gabarits des trois fichiers sont plus bas. Les autres skills lisent ces sections : elles doivent exister même vides.
  - Crée `creation-de-contenu/contenus/` au passage s'il n'existe pas (c'est là que vivront les contenus produits).

## Les trois fichiers

### `cadence.md`

Tableau `Format | Fréquence` + date de dernière mise à jour. Exemple rempli (un photographe qui ne publie pas partout) :

```markdown
| Format | Fréquence |
|---|---|
| Post LinkedIn | 2 / semaine |
| Newsletter | 1 / mois |

_Dernière mise à jour : 2026-07-01_
```

### `sources-idees.md`

Tableau `Source | Où la trouver (URL, compte, nom) | Pourquoi pertinente` + date de dernière mise à jour. Exemple de lignes :

```markdown
| Source | Où la trouver | Pourquoi pertinente |
|---|---|---|
| Groupe Facebook « Mariage 2027 » | facebook.com/groups/… | les futures mariées y posent leurs vraies questions photo |
| Podcast « Le Studio » | son flux + notes d'épisodes | les débats du métier, matière à prise de position |
```

### `voix.md`

Sections, dans cet ordre :

- **Observations préliminaires** — placeholder : `calibrer-voix` les remplira, à partir des messages de prospection de la Session 2.
- **Règles « ce que je fais »** — placeholder.
- **Règles « ce que j'évite »** — placeholder.
- **Exemples validés** — placeholder.
- **Apprentissages détaillés** — placeholder.
- Date de dernière mise à jour.

Le format des règles appartient à `calibrer-voix` : ne préremplis rien au-delà des titres de sections.

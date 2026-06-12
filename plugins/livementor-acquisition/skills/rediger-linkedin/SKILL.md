---
name: rediger-linkedin
description: >
  Rédige un post LinkedIn dans la voix calibrée du participant et suit le contenu
  jusqu'à sa publication. Déclenche sur « rédige un post LinkedIn », « écris-moi un
  post sur X », « drafte le post », « j'ai besoin d'un post pour vendredi »,
  « je viens de publier le post », ou l'invocation
  /livementor-acquisition:rediger-linkedin.
---

# Rédiger-LinkedIn — Le post dans sa voix

## Mandat

- **Situation** : le participant veut un post LinkedIn. Trois formes d'invocation : drafter un sujet déjà capturé en `idee` dans `contenus/`, drafter un sujet nouveau, ou annoncer la publication d'un post `pret`.
- **Objectif** : un fichier de `creation-de-contenu/contenus/` au format `linkedin` dont le statut progresse — `idee → brouillon` à la première rédaction, `brouillon → pret` à la validation, `pret → publie` quand le participant signale la publication. Le corps du fichier contient le draft courant.
- **Contraintes** :
  - Format LinkedIn : 150 à 300 mots, sans formatage markdown (le feed ne le rend pas).
  - Applique toutes les règles de `voix.md` dès le premier draft, plus l'esquisse de voix de `CLAUDE.md`.
  - Drafte direct : pas de questions de cadrage avant le premier jet. Infère l'angle depuis le sujet, drafte, itère sur les critiques.
  - Aucune création silencieuse de règles de voix : si une critique révèle une règle généralisable (au-delà de ce post), propose son ajout à `voix.md` — le participant tranche, et `calibrer-voix` détient le format.
  - À la livraison d'un draft, rappelle : *« Reprends et ajuste, mets ta patte avant de publier. »*
  - Le front-matter respecte le schéma du skill `idees`.
- **Indications** :
  - Si le sujet correspond clairement à un fichier `idee` existant, continue ce fichier (statut → `brouillon`, corps remplacé par le draft). Plusieurs candidats ou ambiguïté → clarifie d'abord.
  - Si un `pret` ou `publie` couvre déjà le sujet, signale-le avant d'écrire : propose une variante ou une mise à jour, pas un duplicata silencieux.
  - Cycle : draft → critique → ajustement, jusqu'à validation explicite (« ok c'est prêt », « je valide »). À la validation, statut → `pret`.
  - Au « publié » : `date_publiee` (date du jour si non précisée), `url_publication` si fournie, statut → `publie`, corps inchangé.
  - Si `date_prevue` change ou se précise, le nom de fichier suit la convention du skill `idees` (stabilité privilégiée au-delà de `brouillon`).
  - Toute écriture dans `contenus/` périme l'artifact kanban : en fin d'action, charge le skill `calendrier` pour le régénérer.

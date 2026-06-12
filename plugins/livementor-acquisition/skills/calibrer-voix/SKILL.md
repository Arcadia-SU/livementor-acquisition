---
name: calibrer-voix
description: >
  Calibre la voix éditoriale du participant dans creation-de-contenu/voix.md, pour que
  ses contenus sonnent comme lui et pas comme une IA. Déclenche sur « calibre ma voix »,
  « travaille mon style », « affine mon ton », « apprends comment j'écris », ou
  l'invocation /livementor-acquisition:calibrer-voix. Reprenable à volonté.
---

# Calibrer-voix — La voix du participant, règle par règle

## Mandat

- **Situation** : le participant veut que ses contenus sonnent comme lui, pas comme une IA. `voix.md` existe (créé par `setup-contenu`), quasi vide en première session ou déjà garni en reprise. Et il y a déjà de la matière : les messages de prospection de la Session 2 (`prospection/messages/*.md`), où chaque couple Draft / Version finale montre ce qu'il a réécrit de sa main.
- **Objectif** : des règles réutilisables encodées dans `voix.md`, chacune traçable à une correction explicite du participant. Si possible, finir sur un draft validé sans correction : il rejoint les « Exemples validés » et sert de référence aux skills `rediger-*`.
- **Contraintes** :
  - **Aucune règle inventée.** Toute règle vient d'une correction explicite du participant — une critique en session, ou un écart Draft / Version finale du corpus S2. Pas de déduction stylistique de ton cru.
  - Les drafts d'exercice sont des posts LinkedIn : 150 à 300 mots, sans formatage markdown (le feed LinkedIn ne le rend pas).
  - Un cycle = un sujet, un draft, une critique, une ou plusieurs règles extraites. Ne mélange pas les sujets dans un même draft.
  - La session se conclut quand un draft passe sans correction, ou dès que le participant veut s'arrêter — dans les deux cas, sauvegarde l'état dans `voix.md` avant de conclure.
  - Si `voix.md` n'existe pas, propose de passer par `setup-contenu` d'abord.
- **Indications** :
  - **Commence par le corpus S2** : lis les couples Draft / Version finale dans `prospection/messages/`. Les écarts (longueur, ton, formules coupées, mots remplacés) sont tes premières hypothèses : présente-les en quelques observations, fais-les confirmer, encode celles qu'il valide en « Observations préliminaires ». Si ce corpus n'existe pas (prospection pas encore passée), démarre directement par un premier draft : les règles viendront des critiques en session.
  - Le sujet de chaque draft : pioche par défaut dans les douleurs du client idéal (`CLAUDE.md`), en évitant les sujets déjà passés (visibles dans « Apprentissages détaillés »). Le participant peut imposer son sujet à tout moment.
  - Applique dès le premier draft toutes les règles déjà présentes dans `voix.md`. En reprise, si une règle s'avère mal calibrée sur un nouveau contexte, affine-la plutôt que d'en ajouter une qui la contredit.
  - Le format d'encodage des règles est plus bas : ce skill fait autorité dessus.

## Le format des règles dans `voix.md`

Chaque règle figure à deux endroits :

- **En bullet d'une ligne** dans « Règles "ce que je fais" » ou « Règles "ce que j'évite" », avec sa source : `_(itération N)_` ou `_(corpus prospection)_`.
- **En entrée détaillée** dans « Apprentissages détaillés », sous le format : passage rejeté (citation) → correction du participant → règle extraite.

Mets à jour la date « Dernière mise à jour » en bas du fichier à chaque modification.

## Draft validé

- Toujours : ajout dans « Exemples validés » de `voix.md`.
- Et propose de le verser comme contenu candidat dans `creation-de-contenu/contenus/` (schéma du skill `idees`, `source_idee: calibrer-voix`, statut `pret`) : un post calibré est un post publiable.

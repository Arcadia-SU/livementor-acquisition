---
name: rediger-article
description: >
  Rédige un article long orienté SEO pour le site du participant, dans sa voix
  calibrée, et suit le contenu jusqu'à sa mise en ligne. Déclenche sur « rédige un
  article », « écris-moi un article sur X », « papier de fond », « article pour mon
  site », « l'article est en ligne », ou l'invocation
  /livementor-acquisition:rediger-article.
---

# Rédiger-article — Le fond qui reste

## Mandat

- **Situation** : le participant veut un article long pour son site — visée SEO long terme, et ressource à envoyer aux prospects. Trois formes d'invocation : drafter un sujet capturé en `idee`, drafter un sujet nouveau, ou annoncer la publication d'un article `pret`.
- **Objectif** : un fichier de `creation-de-contenu/contenus/` au format `article` dont le statut progresse `idee → brouillon → pret → publie`. Le corps du fichier contient le draft courant.
- **Contraintes** :
  - Format : 1200 à 2500 mots. Markdown sans restriction (titre `#`, sous-titres `##`/`###`, listes, citations, liens).
  - Structure : titre clair orienté SEO sans clickbait, introduction qui pose le problème, 3 à 6 sections dont les sous-titres portent du sens (pas « Introduction » / « Premier point »), conclusion qui ouvre vers une action concrète.
  - Applique les règles de `voix.md`, avec un ton plus posé qu'en LinkedIn : l'article a le temps de développer ses nuances. Emojis : suis `voix.md` ; à défaut quasi absents (0 à 2, jamais en titre).
  - Closing discret : découvrir l'offre, s'abonner à la newsletter ou prendre rendez-vous — jamais agressif ni générique.
  - Drafte direct : pas de questions de cadrage avant le premier jet.
  - Aucune création silencieuse de règles de voix : une règle généralisable se propose pour `voix.md`, le participant tranche, et `calibrer-voix` détient le format.
  - À la livraison d'un draft, rappelle : *« Reprends et ajuste, mets ta patte avant de publier. »*
  - Le front-matter respecte le schéma du skill `idees`.
- **Indications** :
  - Mêmes réflexes de fichier que les autres `rediger-*` : continuer un `idee` qui matche (clarifier si ambigu), signaler un doublon `pret`/`publie` avant d'écrire, `pret` à la validation explicite, `publie` avec `date_publiee` / `url_publication` (permalien du site) sans toucher au corps.
  - Sur un format long, une itération peut ne couvrir qu'une section (la critique du participant peut cibler un passage) : garde la cohérence d'ensemble du fil entre les itérations.
  - Quand l'article s'appuie sur des contenus déjà présents dans `contenus/` (consolidation de posts, approfondissement d'une newsletter), lis les fichiers sources et cite-les dans le corps (`url_publication` si présent).
  - Toute écriture dans `contenus/` périme l'artifact kanban : en fin d'action, charge le skill `calendrier` pour le régénérer.

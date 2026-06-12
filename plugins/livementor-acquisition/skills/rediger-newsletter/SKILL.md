---
name: rediger-newsletter
description: >
  Rédige une newsletter (Substack ou équivalent) dans la voix calibrée du participant
  et suit le contenu jusqu'à son envoi. Déclenche sur « rédige ma newsletter »,
  « écris la newsletter sur X », « drafte l'envoi de cette semaine », « la newsletter
  est partie », ou l'invocation /livementor-acquisition:rediger-newsletter.
---

# Rédiger-newsletter — L'envoi qui approfondit

## Mandat

- **Situation** : le participant veut produire une newsletter (format long, envoi Substack ou équivalent). Trois formes d'invocation : drafter un sujet déjà capturé en `idee`, drafter un sujet nouveau, ou annoncer la publication d'un envoi `pret`.
- **Objectif** : un fichier de `creation-de-contenu/contenus/` au format `newsletter` dont le statut progresse `idee → brouillon → pret → publie`. Le corps du fichier contient le draft courant.
- **Contraintes** :
  - Format : 600 à 1500 mots. Markdown avec parcimonie (sous-titres `##`, un peu de gras) : les plateformes d'emailing le rendent bien.
  - Structure : un hook qui peut prendre 1-2 paragraphes, 3 à 5 sections développées, une fermeture avec un CTA contextuel (répondre au mail, une ressource, une invitation — selon le sujet). Pas de CTA générique.
  - Applique toutes les règles de `voix.md` dès le premier draft, plus l'esquisse de `CLAUDE.md`. Emojis : suis `voix.md` ; à défaut, plus rares qu'en LinkedIn (0 à 3 par envoi).
  - Drafte direct : pas de questions de cadrage avant le premier jet.
  - Aucune création silencieuse de règles de voix : une règle généralisable se propose pour `voix.md`, le participant tranche, et `calibrer-voix` détient le format.
  - À la livraison d'un draft, rappelle : *« Reprends et ajuste, mets ta patte avant d'envoyer. »*
  - Le front-matter respecte le schéma du skill `idees`.
- **Indications** :
  - Mêmes réflexes de fichier que les autres `rediger-*` : continuer un `idee` existant si le sujet matche (clarifier si plusieurs candidats), signaler un doublon `pret`/`publie` avant d'écrire, statut → `pret` à la validation explicite, passage à `publie` avec `date_publiee` et `url_publication` (lien de l'envoi) sans toucher au corps.
  - Une newsletter peut citer ou approfondir un post LinkedIn déjà publié : si le participant le mentionne, lis le fichier source dans `contenus/` et fais le lien explicitement (référence dans le corps, permalink ajouté à `source_idee` si fourni).
  - Toute écriture dans `contenus/` périme l'artifact kanban : en fin d'action, charge le skill `calendrier` pour le régénérer.

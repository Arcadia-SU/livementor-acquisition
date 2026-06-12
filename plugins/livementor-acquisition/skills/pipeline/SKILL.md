---
name: pipeline
description: >
  Répond aux questions sur l'état du suivi commercial, applique les changements de
  statut des prospects en conversion, et régénère l'artifact kanban pipeline-conversion.
  Déclenche sur « mets à jour le suivi commercial », « montre mon pipeline », « où en
  est [prospect] », « passe-le en devis envoyé », « il a signé », ou l'invocation
  /livementor-acquisition:pipeline.
---

# Pipeline — Le suivi commercial, à jour

## Mandat

- **Situation** : le participant suit ses prospects en conversion, du premier contact à la signature. La vérité vit dans `conversion/prospects/` : un dossier de conversion par prospect, dont le front-matter porte statut, canal et prochaine action. L'artifact `pipeline-conversion` (vue kanban) n'est qu'un snapshot : ses données sont gelées à sa dernière régénération.
- **Objectif** : selon la demande — une réponse exacte (lue dans les dossiers), un changement appliqué, ou l'artifact régénéré avec un snapshot à jour. En première invocation : le pipeline initialisé depuis l'existant de `prospection/`.
- **Contraintes** :
  - Source unique de vérité : les fichiers `conversion/prospects/*.md`. Pas de cache, pas d'inférence — toujours relire.
  - Ce skill fait autorité sur le schéma du dossier de conversion (plus bas) ; `brief-prospect` et `rediger-followup` le respectent et font avancer le statut au fil de leurs actions.
  - Un prospect entre dans le pipeline avec l'accord du participant : pas d'import silencieux de tout le CSV.
  - Les actions irréversibles (suppression d'un dossier, passage en `perdu`) passent par une confirmation.
  - À la régénération de l'artifact, seules les données changent (`allItems`, `SNAPSHOT_DATE`) : le HTML (CSS, layout) reste structurellement identique. Repars de la dernière version connue.
- **Indications** :
  - **Premier remplissage** : propose les candidats depuis l'existant — les lignes de `prospection/prospects-*.csv` (statut `nouveau-contact`) et les fichiers `prospection/messages/*.md` dont le statut indique une réponse reçue (statut `contact-engage`). Un prospect présent des deux côtés n'apparaît qu'une fois, au statut le plus avancé. Le participant choisit qui suivre ; un dossier par prospect retenu. Crée `conversion/prospects/` au passage s'il n'existe pas.
  - Le cycle de statuts est indicatif, pas imposé : si le métier du participant en demande d'autres (acompte, second rendez-vous…), adapte la liste — en gardant la cohérence sur tous les dossiers et les colonnes de l'artifact.
  - Quand le pipeline s'affiche, signale les prospects dont `date_prochaine_action` est dépassée : c'est l'intérêt de la vue.

## Le dossier de conversion — schéma

Ce skill fait autorité sur ce schéma ; `brief-prospect` et `rediger-followup` le respectent.

Nom : `conversion/prospects/{prospect}.md` — même `{prospect}` que la fiche d'analyse et le fichier de messages, pour que tout se croise. Front-matter YAML :

```yaml
prospect: …                  # nom lisible
statut: nouveau-contact      # cycle plus bas
canal: …                     # où la conversation se passe
date_dernier_contact:        # YYYY-MM-DD
prochaine_action:            # texte court (« appel jeudi », « relancer sur le devis »)
date_prochaine_action:       # YYYY-MM-DD, vide si rien de prévu
```

Cycle de statuts (indicatif, ajustable au métier du participant) :

`nouveau-contact → contact-engage → brief-prepare → appel-fait → devis-envoye → en-reflexion → signe | perdu`

Le corps du fichier est le **journal de conversion** : les sections s'ajoutent au fil de la vie du prospect — brief d'appel (par `brief-prospect`), comptes-rendus et suivis (par `rediger-followup`), notes du participant. Chaque section est titrée et datée (`## Brief d'appel — YYYY-MM-DD`, `## Appel du YYYY-MM-DD`) pour que le journal se lise chronologiquement. On n'efface pas l'historique, on ajoute.

## Cas typiques

- « Où en est X ? » → front-matter + dernière entrée du journal, en deux phrases.
- « Il a répondu » / « on a un appel jeudi » → statut, `prochaine_action`, `date_prochaine_action`.
- Un changement de statut (« passe-le en devis envoyé », « il est en réflexion ») → statut mis à jour + `date_dernier_contact` horodatée.
- « Il a signé » → statut `signe` — et propose de noter dans le journal ce qui a fait pencher la balance (matière pour `conversion/clients-types.md`).
- « Montre le pipeline » → relis tous les dossiers, régénère l'artifact, signale les prochaines actions dépassées.
- Prospect mentionné sans dossier de conversion → propose de le faire entrer dans le pipeline, ne crée rien en silence.
- Statut inconnu dans un front-matter → le cycle est peut-être personnalisé : vérifie la cohérence avec les autres dossiers avant de proposer une correction.

## L'artifact `pipeline-conversion`

Vue kanban par statut, une carte par prospect (nom, prochaine action, date), en mode snapshot : les données sont des constantes JS dans le HTML (`allItems`, `SNAPSHOT_DATE`).

- **Régénérer** : lis le HTML existant (`mcp__cowork__list_artifacts` puis `Read` sur le `path` retourné), remplace le bloc `// --- DATA SNAPSHOT ---`, renvoie via `mcp__cowork__update_artifact` (id `pipeline-conversion`).
- **S'il n'existe pas encore**, crée-le : colonnes = cycle de statuts, cartes = prospects, même langage visuel que `calendrier-editorial` s'il existe. Puis continue en mode snapshot.
- Le rafraîchissement automatique côté client n'est pas possible (pas d'accès aux fichiers depuis l'artifact) : l'artifact reste un snapshot, c'est ce skill qui le tient à jour.

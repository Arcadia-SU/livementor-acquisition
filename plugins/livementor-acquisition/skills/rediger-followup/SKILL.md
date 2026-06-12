---
name: rediger-followup
description: >
  Transforme un appel découverte (transcription collée ou notes brutes) en suivi
  commercial : email de reformulation, mini-devis texte, relances ciblées sur les
  objections — selon ce que l'appel demande. Déclenche sur « rédige le suivi d'appel »,
  « email post-appel », « voilà la transcription de mon appel », « relance ce
  prospect », ou l'invocation /livementor-acquisition:rediger-followup.
---

# Rédiger-followup — Après l'appel, conclure

## Mandat

- **Situation** : l'appel découverte a eu lieu. C'est là que les signatures se perdent : le suivi tarde, les besoins exprimés se déforment, les objections restent sans réponse. L'entrée est ce qui existe — une transcription (Fathom, Fireflies, Noota… collée dans le chat ou lue via un connecteur), ou les notes brutes du participant (échange en personne, appel non enregistré).
- **Objectif** : le suivi rédigé et le dossier de conversion à jour — compte-rendu daté dans le journal, statut avancé, `prochaine_action` posée. Les livrables se décident au cas par cas (tableau plus bas) : tous ne servent pas à chaque appel.
- **Contraintes** :
  - C'est le participant qui envoie, depuis sa boîte : tu n'envoies jamais rien toi-même.
  - L'email de reformulation reprend les besoins du prospect **avec ses propres mots** (ceux de la transcription), pas avec le vocabulaire de l'offre du participant.
  - Applique les règles de `voix.md` si le calibrage (Session 3) est passé.
  - À la livraison d'un draft, rappelle : *« Reprends et ajuste, mets ta patte avant d'envoyer. »* — surtout sur l'email de reformulation.
  - `conversion/objections.md` appartient à ce skill : il fait autorité sur son format (plus bas). Toute réponse d'objection s'y enregistre après validation du participant, jamais en silence.
  - Mini-devis : du texte structuré, pas de PDF ni d'Excel.
  - Le dossier de conversion respecte le schéma du skill `pipeline`.
- **Indications** :
  - Commence par extraire de l'appel : besoins exprimés (avec les mots du prospect), objections — y compris celles passées sans réponse pendant l'appel — signaux d'achat, prochaine étape convenue. Restitue cette lecture en quelques lignes avant de rédiger : le participant corrige ta compréhension de l'appel avant que les drafts en héritent.
  - Sur des notes brutes plutôt qu'une transcription, les mots exacts du prospect manquent : demande les formulations qui ont marqué le participant, ce sont elles qui font l'email de reformulation.
  - Pour chaque objection, consulte `conversion/objections.md` : déjà traitée → réutilise la réponse validée en l'adaptant au prospect ; nouvelle ou réponse inadaptée → élabore avec le participant, enregistre après validation.
  - Si Gmail ou Outlook est connecté à Cowork, les emails passés peuvent fournir des reformulations qui ont déjà marché. Sinon, propose une fois la connexion (Gmail/Outlook + outil de transcription, dans les connecteurs Cowork) — en fin d'action, pas au milieu de la lecture de l'appel, et sans en faire un préalable : tout fonctionne en collant la transcription.
  - Un moment de l'appel a révélé quelque chose de généralisable sur ce type de client ? Candidat pour `conversion/clients-types.md` (le skill `brief-prospect` fait autorité dessus) — propose, le participant tranche.
  - En fin d'action : journal du dossier complété (date, compte-rendu court, livrables produits), statut mis à jour (`appel-fait`, `devis-envoye`…), `prochaine_action` datée, puis charge le skill `pipeline` pour régénérer l'artifact.

## Les trois livrables

| Livrable | Quand | Son travail |
|---|---|---|
| **Email de reformulation** | presque toujours, vite après l'appel | prouver que le participant a écouté : besoins repris avec les mots du prospect, prochaine étape claire |
| **Mini-devis texte** | quand l'appel a parlé périmètre et budget | squelette prêt à coller dans un email ou un doc : livrables, planning, prix, conditions |
| **Relances ciblées** | objection restée ouverte, ou silence après l'envoi | répondre à l'objection précise — pas « je me permets de revenir vers vous » |

## L'email de reformulation — exemple

Court, les mots du prospect entre guillemets, une prochaine étape datée. (Une nutritionniste après un appel avec une DRH :)

```text
Objet : Suite de notre échange — l'énergie de vos équipes

Bonjour Claire,

Merci pour cet échange. Ce que je retiens, avec vos mots : vos équipes
« s'écroulent après déjeuner », et les ateliers bien-être précédents ont fait
« pschitt » parce que trop théoriques. Votre priorité : du concret qui tient
dans une pause déjeuner.

Je vous envoie d'ici vendredi une proposition courte sur ce format. Si j'ai
mal compris quelque chose, dites-le moi — c'est le moment.

Camille
```

Ce qui en fait un bon email : les guillemets viennent de la transcription, la prochaine étape est datée, et il se lit en 30 secondes.

## `conversion/objections.md` — le format

Une entrée par objection, sous sa formulation la plus parlante :

```markdown
## « C'est trop cher pour nous là, maintenant »
- **Contexte** : entreprise, budget bien-être déjà engagé ailleurs.
- **Réponse validée** : … _(appel acme, 2026-07-08)_
```

Les objections proches se regroupent (une vraie objection a plusieurs formulations) : affine une entrée existante plutôt que d'en créer une quasi-jumelle. Date de dernière mise à jour en bas. Le fichier s'enrichit appel après appel, pas via un setup figé.

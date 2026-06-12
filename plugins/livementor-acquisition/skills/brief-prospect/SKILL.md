---
name: brief-prospect
description: >
  Prépare un appel découverte : compile tout ce qu'on sait du prospect (fiche
  d'analyse, audit, messages échangés) avec l'expertise clients-types du participant,
  et produit un brief compact à lire juste avant l'appel. Déclenche sur « prépare mon
  appel », « brief pour ce prospect », « j'ai un appel avec X demain », ou l'invocation
  /livementor-acquisition:brief-prospect.
---

# Brief-prospect — Préparer l'appel découverte

## Mandat

- **Situation** : un prospect a accepté un appel. Préparer cet appel mange du temps, et même préparé on rate souvent ce qui compte pour CE prospect : questions génériques, objections non anticipées — le prospect sent qu'on l'écoute mal. La matière existe pourtant : fiche d'analyse, audit, messages échangés, plus l'expertise du participant sur ses clients-types, encodée dans `conversion/clients-types.md`.
- **Objectif** : un brief compact, relisible en 2 minutes juste avant de décrocher — présenté en session et enregistré dans le dossier de conversion du prospect (section « Brief d'appel »), dont le statut passe à `brief-prepare`.
- **Contraintes** :
  - Le brief s'appuie sur du réel : ce que disent la fiche, l'audit, les messages. Une hypothèse y figure comme hypothèse — une erreur factuelle pendant l'appel grille le participant.
  - Format dimensionné par le contexte (enjeu de l'appel, matière disponible), pas par une règle fixe. Compact reste la règle : un brief qu'on ne peut pas relire en 2 minutes ne sert à rien.
  - `conversion/clients-types.md` appartient à ce skill : il fait autorité sur son format (plus bas). Toute généralisation s'y encode après validation du participant, jamais en silence.
  - Le dossier de conversion respecte le schéma du skill `pipeline`.
- **Indications** :
  - Lis tout ce qui existe sur ce prospect : son dossier `conversion/prospects/{prospect}.md` (le contexte de l'appel y est), `prospection/analyses/{prospect}.md`, son audit s'il existe (produit par le skill `/audit-[domaine]` du participant), `prospection/messages/{prospect}.md` (ce qui a été dit, le message auquel il a répondu). Ce qui manque n'est pas bloquant : un brief honnête sur matière mince vaut mieux que pas de brief — propose `analyser-prospect` si la matière est vraiment vide.
  - Si `clients-types.md` n'existe pas ou ne couvre pas ce type de client, c'est le moment d'extraire l'expertise : « pour ce type de client, qu'est-ce qu'il doit comprendre pour signer ? qu'est-ce qu'il ne faut surtout pas dire ? quelles objections reviennent ? ». Encode ses réponses après validation — le brief du jour en profite, tous les suivants aussi.
  - Le brief se critique : ce que le participant corrige (une question naïve, une objection qui n'arrive jamais chez lui) est candidat à `clients-types.md` — propose, il tranche.
  - Si le prospect n'a pas de dossier de conversion, propose de l'y faire entrer (schéma du skill `pipeline`) plutôt que de produire un brief hors pipeline.
  - En fin d'action : statut du dossier → `brief-prepare`, puis charge le skill `pipeline` pour régénérer l'artifact.

## Le brief — les quatre blocs

Le contenu varie avec le prospect, la colonne vertébrale non :

- **Ce qui compte pour cette personne** — 2-3 lignes croisant les signaux du prospect (fiche, audit, messages) avec ce que `clients-types.md` dit de son type.
- **Questions à creuser** — ce qu'on ne sait pas encore et qui change la proposition.
- **Objections à anticiper** — celles déjà rencontrées (`conversion/objections.md` si présent) + celles que le profil laisse deviner, chacune avec son angle de réponse.
- **Accroche d'ouverture** — la première minute : pourquoi lui, pourquoi maintenant, sans pitch. (« Vous me disiez que vos équipes s'écroulent après déjeuner — j'ai regardé comment d'autres boîtes de votre taille ont pris le sujet » ouvre ; « je vais vous présenter mon accompagnement » pitche.)

## `conversion/clients-types.md` — le format

Une section par type de client (`## Entreprise qui veut une intervention`, `## Particulier en accompagnement`, `## Média / podcast`…). Dedans, des bullets d'une ligne — ce qui compte pour eux, ce qu'il ne faut pas dire, les objections fréquentes — chacune datée de son origine : `_(cocréation)_` ou `_(appel {prospect}, YYYY-MM-DD)_`. Date de dernière mise à jour en bas.

Exemple (nutritionniste, type « entreprise ») :

```markdown
## Entreprise qui veut une intervention
- Doit comprendre le lien alimentation → énergie → performance au travail. _(cocréation)_
- Jamais de discours culpabilisant ni de promesse médicale. _(cocréation)_
- Objection fréquente : « nos salariés ne viendront pas » → les formats courts intégrés aux réunions d'équipe marchent mieux que l'atelier dédié. _(appel acme, 2026-07-08)_
```

Le fichier s'enrichit appel après appel, même mécanique que `voix.md`. C'est `rediger-followup` qui rapporte la matière post-appel ; toi, tu encodes.

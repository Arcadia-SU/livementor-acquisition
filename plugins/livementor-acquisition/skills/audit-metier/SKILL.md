---
name: audit-metier
description: >
  Crée avec le participant son skill d'audit personnel (audit-nutrition,
  audit-positionnement, audit-visuel…) : un entretien pour extraire son regard d'expert,
  puis ce regard est encodé dans un nouveau skill qui produira des mini-audits de
  prospects à sa façon. Déclenche sur « crée mon skill d'audit », « encode mon
  expertise », « on fait mon audit métier », ou l'invocation
  /livementor-acquisition:audit-metier.
---

# Audit-métier — Encoder le regard d'expert du participant

## Mandat

- **Situation** : le participant sait regarder un client potentiel comme personne d'autre, c'est son métier. Mais ce regard n'existe que dans sa tête. Encodé dans un skill personnel, il permet d'auditer chaque prospect à sa façon en quelques minutes — et le message d'approche passe de *« vous voulez un accompagnement ? »* à *« j'ai regardé votre site, voici 3 pistes concrètes »* : de la valeur avant la proposition.
- **Objectif** : un skill personnel `/audit-[domaine]` écrit dans `.claude/skills/`, testé sur un prospect réel, validé par le participant.
- **Contraintes** :
  - L'expertise vient du participant, pas de toi : tu extrais et tu structures, tu n'inventes pas. Ses mots, ses critères, ses signaux d'alerte.
  - Le skill généré respecte les principes « Lorsque tu créeras des skills » du `CLAUDE.md`.
  - Pas fini tant que pas testé : un audit réel, critiqué par le participant, le skill raffiné en conséquence.
- **Indications** :
  - **L'entretien d'extraction** (le cœur) : même esprit que le setup — ouvre large, puis creuse ce qui manque. Les questions qui débloquent : « quand tu regardes le site ou le profil d'un client potentiel, qu'est-ce que tu vois en 30 secondes que personne d'autre ne voit ? », « quels signaux te disent qu'il a besoin de toi ? », « quelles erreurs vois-tu tout le temps ? », « qu'est-ce qu'il ne faut surtout pas dire dans ton domaine ? ».
  - **La forme du skill généré** : il prend un prospect en entrée (une URL, la fiche `prospection/analyses/{prospect}.md` si elle existe, ou simplement ce que le participant en dit) et sort un mini-audit d'une page : ce qui va, ce qui pèche, 3-5 pistes d'approche reliées à l'offre du participant. C'est ce document qu'on attachera au message de prospection.
  - **Le test** : prends un prospect du CSV, lance le skill fraîchement créé, fais critiquer le résultat (« qu'est-ce qu'un confrère trouverait faux ou plat là-dedans ? »). Encode les corrections dans le skill, pas seulement dans l'audit du jour — c'est comme ça qu'il s'améliore à chaque passage.

## Exemples de skills générés (le nom et la grille viennent du participant)

- Nutritionniste → `/audit-nutrition` : signaux qu'une entreprise ou un média s'intéresse à l'alimentation et à l'énergie, erreurs de discours à éviter sur les troubles alimentaires.
- Coach → `/audit-positionnement` : clarté du message, client idéal visible, promesse mesurable.
- Copywriter → `/audit-textes` : hiérarchie de l'argumentaire, promesses vs preuves, appels à l'action.
- Photographe → `/audit-visuel` : cohérence du portfolio, qualité, image renvoyée vs clientèle visée.
- Thérapeute / professionnel de santé → `/audit-education` : clarté pédagogique, prudence du discours, angles de prévention, partenaires pertinents.
- Formateur → `/audit-formation` : preuves sociales, lisibilité du programme, parcours d'achat.

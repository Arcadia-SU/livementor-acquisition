# livementor-plugins

Marketplace Claude Cowork du bootcamp LiveMentor **« Un agent IA pour trouver mes clients »** (mentor : Oscar Satre / Arcadia). Contient le plugin `livementor-acquisition`.

Transforme Cowork en agent d'acquisition de bout en bout pour des indépendants non-développeurs : sourcing de prospects → prospection personnalisée → création de contenu → conversion.

## Installation (participants)

Dans Cowork → Customize → Plugins, ajouter un marketplace par URL :

```
https://github.com/Arcadia-SU/livementor-acquisition
```

Puis installer le plugin `livementor-acquisition`. Les skills deviennent disponibles via `/livementor-acquisition:<skill>`.

## Skills

| Session | Skills |
|---|---|
| **S1 — Fondations** | `setup`, `sourcing` |
| **S2 — Prospection sortante** | `analyser-prospect`, `audit-metier`, `rediger-prospection` |
| **S3 — Contenu entrant** | `setup-contenu`, `calibrer-voix`, `idees`, `calendrier`, `rediger-linkedin`, `rediger-newsletter`, `rediger-article` |
| **S4 — Conversion** | `brief-prospect`, `rediger-followup`, `pipeline` |
| **S5 — Réseau & recommandation** | `inventaire-reseau`, `rediger-reactivation` |

17 skills sur 5 sessions. Avancement détaillé : `STATUS.md`.

## Structure

```
.claude-plugin/marketplace.json     ← déclare le plugin
plugins/livementor-acquisition/
  .claude-plugin/plugin.json        ← manifeste du plugin
  skills/<skill>/SKILL.md           ← un dossier par skill
```

Source : monorepo Arcadia (`comptes/Livementor/livementor-plugins/`). Voir `STATUS.md` pour l'avancement et la question d'hébergement.

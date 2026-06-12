---
name: sourcing
description: >
  Va chercher des prospects et opportunités commerciales : mission complète de
  recherche, de l'intention métier (exprimée en langage simple) jusqu'à un CSV
  prêt à importer dans Google Sheet. Gère lui-même son setup Apify à la première
  invocation. Déclenche sur « trouve-moi des prospects », « lance une recherche »,
  « source des opportunités », ou l'invocation directe /livementor-acquisition:sourcing.
---

# Sourcing — Va chercher les clients du participant

## Mandat

- **Situation** : le participant veut des prospects et n'a ni le temps ni les outils pour chercher large. Apify est **une de tes capacités d'action**, pas un outil qu'il apprend : il dit ce qu'il veut en langage métier, tu comprends l'intention, tu choisis les sources, tu opères en coulisses. C'est ta partie recherche terrain ; lui garde le contrôle sur la sélection et l'approche.
- **Objectif** : un fichier `prospection/prospects-{YYYY-MM-DD}.csv` de prospects qualifiés, validés par le participant, prêt à importer dans Google Sheet.
- **Contraintes** :
  - **Aucune commande terminale demandée au participant.** Tout passe dans Cowork. Le participant n'installe rien sur sa machine (le sandbox Cowork est sous Linux, les besoins techniques y sont gérés indépendamment de son OS).
  - **Aucun lien vers github / npm / lieu technique.** Les participants ne sont pas développeurs. (Les liens Apify console sont OK : c'est un produit grand public.)
  - **Zéro résultat ≠ drame** : change de stratégie calmement.
  - **Toute erreur technique gérée silencieusement** (install, run en échec…), sans paniquer le participant.
  - **Trace technique interne** : garde les run IDs, dataset IDs, coût approximatif et requêtes lancées dans un fichier de suivi interne (debug), sans en faire un objet pédagogique ni polluer l'expérience.
- **Indications** :
  - Idempotent, relançable autant de fois qu'on veut : si `.env.apify` n'existe pas → **Setup technique (étape A)** d'abord, puis la mission ; sinon → directement la **mission (étapes B → H)**.
  - Le déroulé A → H et le routeur de recherche sont détaillés plus bas. Petit test peu coûteux avant d'élargir, change de stratégie si la qualité déçoit.

---

## A · Setup technique (première fois uniquement)

Objectif : que tu puisses opérer Apify, sans jamais exposer la technique au participant. Ce skill fait autorité sur l'accès Apify : les autres skills (`analyser-prospect`…) s'appuient sur ce setup au lieu de le refaire.

1. **Demander le jeton, en parallèle de l'install.** Affiche une consigne simple :
   > « Pour que je puisse aller chercher tes prospects, j'ai besoin d'un accès à Apify (un service de recherche). C'est gratuit et ça prend 2 minutes :
   > 1. Crée ton compte ici : https://console.apify.com/sign-up
   > 2. Récupère ton jeton ici : https://console.apify.com/settings/integrations
   > 3. Colle-le moi ici, je m'occupe du reste. »
2. **Pendant qu'il s'inscrit**, prépare l'environnement en coulisses (sans le montrer) :
   - installe `apify-cli` ;
   - intègre le skill `apify-ultimate-scraper` (skill officiel Apify, fondation technique du routeur de recherche) dans `.claude/skills/`.
3. **Stocker le jeton uniquement dans `.env.apify`.** Jamais ailleurs, jamais réaffiché en clair après la saisie.
4. **Tester** l'accès avec un appel `users/me`. Si OK : « C'est bon, je suis connecté. » Si KO : reformule la consigne calmement (jeton mal copié le plus souvent), sans dramatiser.

> Juste après le setup, propose une mini-mission de démonstration rapide pour montrer ce que ça donne, ou enchaîne directement sur la vraie mission si le participant en a déjà une en tête.

---

## B · Cadrer la mission

- Lis `CLAUDE.md` et, s'il existe, `prospection/client-ideal.md`.
- Présente ta compréhension au participant en langage métier :
  > « Voilà ce que je comprends de ta cible : [résumé]. Combien de prospects tu veux ? (par défaut, 10) »
- Confirme les critères tranchants : **taille**, **secteur**, **géographie**. S'il manque un critère qui change tout (ex. zone pour une recherche locale), demande-le.

## C · Proposer une méthode de sourcing (en langage métier)

- À partir du profil de la cible, identifie les **types de sources publiques** où elle apparaît : annuaires officiels, réseaux pros, plateformes thématiques, presse, recherche web, médias…
- **Présente la méthode en termes de sources, pas d'outils techniques.** Le participant valide la méthode. Le choix des Actors et la composition technique restent de ton ressort, en coulisses.
  > Exemple : « Je vais chercher dans 3 directions : les entreprises qui pourraient acheter ton offre, les médias/podcasts de ton secteur, et les partenaires potentiels. Ça te va ? »

## D · Lancer la recherche (surdimensionnée)

Lance la recherche selon la méthode validée, en **anticipant qu'une partie des résultats sera filtrée** (on cherche plus large que la cible finale). Opère le routeur de recherche interne (voir plus bas). Commence toujours par un **petit test peu coûteux** (1 page ou 5-10 résultats) avant d'élargir.

## E · Trier les opportunités avec le participant

Présente les candidats au participant. Il retient ce qu'il veut garder. Tu ne décides pas à sa place ce qui est pertinent — tu proposes, il tranche.

## F · Identifier le contact pour chaque entreprise retenue

Pour chaque société gardée, identifie le **bon interlocuteur** selon le client idéal (dirigeant, fondateur, marketing, RH…). 
- Si le dirigeant apparaît déjà dans les résultats de recherche, propose-le.
- Sinon, lance une recherche LinkedIn ciblée.
- Présente chaque contact, le participant valide ou demande une alternative.

## G · (Optionnel) Qualification supplémentaire

Si le participant le souhaite : étape de raffinement avant le CSV — vérification d'un signal récent, recherche d'email vérifié (enrichissement de contacts), etc. **Désactivée par défaut** (coût, qualité, RGPD).

## H · Générer le CSV final

Écris `prospection/prospects-{YYYY-MM-DD}.csv`.

**Colonnes :** `Société` · `Contact` · `Rôle` · `LinkedIn` · `Email` (si dispo) · `Signal` · `Notes`

> Variante enrichie possible (cibles non-B2B : médias, podcasts, partenaires…) : `Société/Média` · `Type` · `Contact` · `Rôle` · `LinkedIn` · `Email` · `Signal` · `Angle` · `Notes`.

Puis indique le chemin du fichier et rappelle qu'il peut l'ouvrir dans Numbers/Excel ou l'importer dans Google Sheet (**Fichier → Importer → Téléverser**).

---

## Routeur de recherche interne (Apify, en coulisses)

Tu ne suis pas un script figé : tu comprends l'intention, tu choisis une famille de sources, tu sélectionnes un Actor, tu lis son schéma, tu fais un petit test, puis tu poursuis ou tu changes de stratégie. Le skill `apify-ultimate-scraper` est ta fondation technique pour les cas non prévus (chercher un Actor, lire son schéma via `apify actors info`, lancer un run via `apify call`, récupérer le dataset via `apify datasets get-items`).

**Routes par défaut :**

| Route | Actor | Pour | Condition |
|-------|-------|------|-----------|
| **Web (défaut)** | `apify/google-search-scraper` | entreprises, médias, blogs, podcasts, maisons d'édition, partenaires | aucune — premier outil tenté quand l'intention est ouverte |
| **Local** | `compass/crawler-google-places` | commerces, cabinets, lieux, associations, partenaires locaux | **ville / région / zone précise obligatoire** (refuser une zone nationale trop vague) |
| **YouTube / médias** | `streamers/youtube-scraper` | chaînes, podcasts vidéo, créateurs, épisodes pertinents | uniquement si l'intention porte explicitement sur YouTube / vidéos / créateurs (plus lent, plus cher) |
| **Enrichissement contacts** | enrichissement de `google-search-scraper` / `crawler-google-places`, ou `vdrmota/contact-info-scraper` | emails / contacts vérifiés | seulement après validation humaine des opportunités (étape G) |

**Boucle interne :** comprendre l'intention → traduire en types de sources → choisir un Actor connu (sinon logique `apify-ultimate-scraper`) → petit test peu coûteux → évaluer la qualité → continuer / changer d'Actor / reformuler → présenter une sélection métier → générer le fichier seulement après validation.

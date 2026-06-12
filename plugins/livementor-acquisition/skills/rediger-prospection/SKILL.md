---
name: rediger-prospection
description: >
  Prépare la séquence d'approche d'un prospect : message initial qui s'appuie sur son
  audit, relance J+3, relance J+7, le tout enregistré dans prospection/messages/.
  Déclenche sur « écris un message d'approche », « prépare ma séquence de prospection »,
  « rédige une relance », ou l'invocation /livementor-acquisition:rediger-prospection.
---

# Rédiger-prospection — La séquence d'approche

## Mandat

- **Situation** : un prospect du CSV a été analysé, souvent audité ; c'est le moment de l'approcher. Le but n'est pas le message parfait, mais des drafts assez bons pour que le participant les fasse siens : c'est sa version qui part, jamais la tienne telle quelle.
- **Objectif** : `prospection/messages/{prospect}.md` rempli avec la séquence d'approche — par défaut trois messages (initial, relance J+3, relance J+7) — validée par le participant.
- **Contraintes** :
  - Seul le **vérifié** entre dans un message (la fiche d'analyse étiquette chaque info vérifié / probable / hypothèse). Une erreur factuelle grille le participant auprès du prospect.
  - C'est lui qui envoie, depuis son compte : tu n'envoies jamais rien toi-même.
  - Termine chaque draft par l'invite explicite : *« Mets ta patte : reformule-le comme tu l'écrirais vraiment, c'est cette voix-là que je calibrerai en Session 3. »* Sa version finale est celle qui compte.
  - Les relances ne valent que pour le silence : si le prospect répond, la séquence s'arrête — on passe en conversation réelle (le territoire des skills de conversion, Session 4).
- **Indications** :
  - Avant d'écrire, lis ce qui existe sur ce prospect : son audit (produit par le skill `/audit-[domaine]` du participant), sa fiche `prospection/analyses/{prospect}.md`, sa ligne de CSV. L'audit fournit l'accroche : s'il n'existe pas, propose de le faire d'abord, ou écris à partir de la fiche en le disant.
  - Identifie le canal d'envoi (là où vit le prospect, croisé avec le canal principal du participant — demande si c'est ambigu, la forme du message en dépend entièrement) et la relation visée (un client potentiel, un partenaire, un média ou un podcast ne s'abordent pas pareil).
  - Écris les messages ensemble dès le départ pour garantir une progression. Trois est le défaut, pas un dogme : si la relation s'y prête mal (un pitch de podcast, par exemple), adapte la séquence et dis pourquoi.
  - Si le fichier existe déjà, lis-le avant d'écrire : tu reprends une séquence en cours, tu ne repars pas de zéro.
  - Quand le participant corrige un draft, regarde ce que sa version change (longueur, ton, formules) et applique-le aux messages suivants de la séquence. N'écris pas de fichier de voix pour autant : le calibrage durable, c'est le travail de la Session 3.

## La séquence

| Message | Son travail |
|---|---|
| **Initial** | ouvrir avec de la valeur : une piste concrète de l'audit, pas une présentation de l'offre |
| **Relance J+3** | apporter quelque chose de nouveau : un autre angle de l'audit, une ressource, un constat |
| **Relance J+7** | clore poliment en laissant la porte ouverte, ou tenter un dernier angle vraiment différent |

Ce qui fait un bon message :

- **La valeur d'abord.** Le prospect doit gagner quelque chose à lire le message, même s'il ne répond jamais.
- **Court, et calibré sur le canal.** Un DM se lit sur téléphone en quelques secondes.
- **Une seule demande, modeste.** Un échange, un retour — pas « un appel de 45 minutes pour découvrir mon accompagnement ».
- **Une voix de personne, pas de commercial.** Pas de formules toutes faites, pas de flatterie d'ouverture, pas de « j'espère que vous allez bien ».

### Exemples d'ouvertures (la piste de l'audit comme accroche)

- Nutritionniste → podcast santé : « J'ai écouté votre épisode sur le sommeil. L'angle alimentation n'y était pas, et il y a deux idées contre-intuitives qui mériteraient un épisode. Je vous les partage ? »
- Photographe → restaurant : « Vos plats méritent mieux que les photos de votre fiche Google. J'en ai retravaillé une pour vous montrer la différence. »
- Copywriter → e-commerce : « Votre page d'accueil cache votre meilleure preuve (les 200 avis 5 étoiles) tout en bas. La remonter prend une heure et change le taux de conversion. »
- Coach → dirigeante qui recrute : « Vous passez de 3 à 8 salariés d'après vos annonces. C'est exactement le moment où les fondateurs me disent qu'ils n'arrivent plus à tout porter seuls. »
- Formateur → agence en croissance : « Vos 4 dernières offres demandent toutes "autonomie sur les outils IA". Former l'équipe existante coûte moins cher que de le chercher en recrutement. »

## Le fichier

Écris `prospection/messages/{prospect}.md` :

```markdown
# {Prospect}

Canal : …
Sources : [audit, fiche d'analyse]

## Message initial
### Draft
…
### Version finale (la tienne)
…
Statut : à envoyer / envoyé le … / réponse reçue

## Relance J+3
[même structure]

## Relance J+7
[même structure]
```

La structure Draft / Version finale est une interface : c'est ce couple qui servira de corpus au calibrage de voix en Session 3. Ne la change pas, et avant l'envoi, rappelle au participant de coller sa version finale dans le fichier.

---
name: rediger-reactivation
description: >
  Rédige les messages de réactivation du réseau dans la voix du participant :
  reprise de contact avec un ancien client, demande de mise en relation, relance
  douce. Déclenche sur « écris un message de réactivation », « reprends contact
  avec [contact] », « demande-lui une mise en relation », « pas de réponse à ma
  réactivation », ou l'invocation /livementor-acquisition:rediger-reactivation.
---

# Rédiger-réactivation — Le message qui ne quémande pas

## Mandat

- **Situation** : l'inventaire (`reseau/contacts.md`) dit qui réactiver et avec quel angle. Reste la gêne : « ça fait deux ans, je ne vais pas réapparaître juste pour demander un service ». Résultat, personne n'écrit — et le message générique (« je me permets de reprendre contact… ») est pire que pas de message : il confirme qu'on vient quémander.
- **Objectif** : `reseau/messages/{contact}.md` rempli — le message validé par le participant, et sa relance douce si le silence dure.
- **Contraintes** :
  - C'est le participant qui envoie, depuis son compte : tu n'envoies jamais rien toi-même.
  - Donner avant de demander : chaque message apporte quelque chose de spécifique à la relation (une ressource, une nouveauté qui concerne le contact, un constat utile) avant d'ouvrir une porte. Cet apport est le cœur du message, et il doit être réel : tu ne l'inventes jamais.
  - Applique les règles de `voix.md` si le calibrage (Session 3) est passé. Sur une relation existante, le ton juste compte encore plus qu'en prospection froide : le contact connaît la vraie voix du participant.
  - À la livraison d'un draft, rappelle : *« Reprends et ajuste, mets ta patte avant d'envoyer. »*
  - Relance : douce, à J+7, une seule — puis on laisse vivre. C'est une relation, pas une campagne : la séquence à trois messages de `rediger-prospection` n'a pas sa place ici.
  - Ce skill fait autorité sur `reseau/messages/` (format plus bas, miroir de `prospection/messages/` : le couple Draft / Version finale nourrit le même corpus de voix).
- **Indications** :
  - Pars de l'entrée du contact dans `reseau/contacts.md` : relation, dernière interaction, angle. Contact absent de l'inventaire → rédige quand même, et propose de l'y ajouter au passage (format du skill `inventaire-reseau`) : l'inventaire reste le registre.
  - Avant de rédiger, fixe l'apport avec le participant. L'angle de l'inventaire n'en est que la graine (« proposer un atelier de rentrée ») : ce que le contact gagne vraiment à lire le message — la ressource précise, la nouveauté, le constat utile — vit dans la tête du participant, pas dans le fichier. Demande-le, ne le devine pas : c'est la matière sans laquelle le message sonne creux. Si l'inventaire le porte déjà assez concret, fais-le confirmer plutôt que de le redemander.
  - Deux types de message. **Réactivation d'ancien client** : prendre de vraies nouvelles + l'apport + ouvrir la porte sans forcer. **Demande de mise en relation** : préciser qui on cherche et pourquoi + rendre le oui facile (un message transférable prêt à copier-coller) + permettre le non sans coût relationnel.
  - Le canal suit la relation : là où elle vivait (mail, WhatsApp, LinkedIn…). Demande si c'est ambigu, la forme du message en dépend.
  - Sur « pas de réponse » : rédige la relance douce en reprenant l'apport sous un autre angle, plus court que le message initial. Après elle, on laisse vivre.
  - Réponse reçue → la conversation entre dans le suivi commercial : propose l'entrée dans le pipeline (statut `contact-engage`, schéma du skill `pipeline`), puis charge le skill `pipeline` pour régénérer l'artifact. Une mise en relation qui débouche sur un appel → c'est `brief-prospect` qui prend le relais.
  - Réponse négative ou froide → clore proprement, avec un remerciement ; statut `clos` dans le fichier, pas de relance. Un réseau se réactive par vagues : un non d'aujourd'hui laisse la porte ouverte pour plus tard.

## Les deux types — exemples

**Réactivation d'ancien client.** (Camille → la salle de sport où elle animait des ateliers :)

```text
Bonjour Marc,

J'ai repensé à vous en préparant ma rentrée : les ateliers nutrition qu'on avait
montés en 2024 restent ceux où j'ai vu le plus de monde revenir d'une session à
l'autre. J'ai retravaillé le format depuis (plus court, plus pratique), et je me
disais que ça pourrait coller avec votre programmation de septembre.

Si le sujet vous intéresse, je vous en dis plus. Et sinon, prenez des nouvelles
de vos adhérents pour moi : j'en garde un très bon souvenir.

Camille
```

Ce qui le fait marcher : il s'appuie sur l'historique réel (les ateliers de 2024), il apporte quelque chose (le format retravaillé), et le non ne coûte rien. L'apport change avec le métier — un photographe rouvre avec une sélection d'archives retravaillées, un formateur avec un module nouveau, un copywriter avec un constat sur la page du client — le mécanisme, lui, ne change pas.

**Demande de mise en relation.** Le message au contact, avec le message transférable dedans :

```text
Bonjour Julie,

Petite demande directe : je développe mes interventions en entreprise sur
l'énergie au travail, et je crois me souvenir que tu connais du monde aux RH
de Decathlon. Si tu vois quelqu'un que ça pourrait intéresser, je t'ai mis un
texte transférable ci-dessous. Et si ce n'est pas le bon moment ou pas la
bonne personne, aucun souci, vraiment.

---
À transférer si tu veux :
« Je te mets en contact avec Camille, nutritionniste spécialisée dans
l'alimentation au travail. Elle anime des ateliers courts en entreprise sur
l'énergie des équipes (le coup de barre de 14h, concrètement). Si tu veux
creuser : camille@... »
```

Le message transférable fait le travail à la place de Julie : rien à rédiger, juste à transférer. C'est ça, rendre le oui facile.

**Relance douce (J+7).** Plus courte que le message initial, un angle nouveau, une seule. (Marc, resté silencieux :)

```text
Bonjour Marc,

Je repense à vous : j'ai testé le nouveau format la semaine dernière dans une
entreprise, 25 minutes chrono, et c'est celui qui a le mieux marché. Si
septembre est déjà bouclé, gardez l'idée pour janvier, tout simplement.

Camille
```

Après elle, on laisse vivre.

## `reseau/messages/{contact}.md` — le format

```markdown
# {Contact}

Canal : …
Type : réactivation / mise en relation
Source : reseau/contacts.md

## Message
### Draft
…
### Version finale (la tienne)
…
Statut : à envoyer / envoyé le … / réponse reçue / clos

## Relance douce (J+7, une seule)
[même structure]
```

Même interface que `prospection/messages/` : le couple Draft / Version finale nourrit le calibrage de voix, et avant l'envoi, rappelle au participant de coller sa version finale dans le fichier.

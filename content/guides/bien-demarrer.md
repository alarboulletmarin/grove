---
title: Bien démarrer
description: Éditer, prévisualiser et publier la base documentaire grove.
tags:
  - guide
---

Ce guide décrit le flux de travail complet pour contribuer à **grove**.

## Prérequis

- [Node.js](https://nodejs.org/) v22 ou supérieur
- `npm` v10.9.2 ou supérieur

## Prévisualiser en local

```bash
npm install      # une seule fois, installe les dépendances
npm run serve    # build + serveur local avec rechargement à chaud
```

Le site est alors disponible sur `http://localhost:8080`.

## Écrire une note

Une note est un fichier `.md` dans `content/`. Le bloc en tête (frontmatter)
définit son titre et ses métadonnées :

```markdown
---
title: Mon titre
tags:
  - exemple
---

Le contenu de la note…
```

## Syntaxe utile

Quartz comprend le Markdown étendu d'Obsidian. Quelques exemples :

- Lien interne : `[[guides/index|Guides]]` → [[guides/index|Guides]]
- Mise en forme : **gras**, *italique*, `code en ligne`
- Les callouts pour mettre en avant une information :

> [!note]
> Les callouts existent en plusieurs variantes : `note`, `tip`, `warning`, `important`…

> [!warning] À ne pas oublier
> Mettre à jour `baseUrl` dans `quartz.config.yaml` avec le domaine réel
> avant la première publication.

## Publier

Pousse simplement tes changements sur la branche `main` :

```bash
git add .
git commit -m "Ajout d'une note"
git push
```

Cloudflare Pages détecte le push, reconstruit le site et met la version en ligne
en environ une minute. Voir le `README.md` du dépôt pour la configuration de
déploiement détaillée.

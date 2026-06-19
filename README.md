# 🌳 grove

Base documentaire propulsée par [Quartz v5](https://quartz.jzhao.xyz/) et déployée sur **Cloudflare Pages**.

Le contenu vit dans `content/` sous forme de fichiers Markdown ; Quartz les transforme
en un site statique avec recherche, graphe de liens, mode sombre et explorateur.

## Démarrage rapide

```bash
npm install        # installe les dépendances (une fois)
npm run serve      # prévisualisation locale avec rechargement à chaud → http://localhost:8080
```

Pour générer le site statique sans serveur :

```bash
npm run build      # installe les plugins puis génère le site dans public/
```

> [!NOTE]
> Les commandes passent par les scripts npm (`npm run …`) plutôt que `npx quartz`.
> Quartz est le paquet racine du dépôt : npm ne crée donc pas de binaire `quartz`
> dans le `PATH`, et `npx quartz …` échoue. Les scripts appellent directement le CLI
> (`./quartz/bootstrap-cli.mjs`) et fonctionnent partout, y compris sur Cloudflare.

## Structure du dépôt

```
grove/
├── content/                  # ← le contenu Markdown (ce que tu édites)
│   ├── index.md              #   page d'accueil
│   └── guides/               #   une section = un dossier
├── quartz/                   # moteur Quartz (ne pas modifier en général)
├── quartz.config.yaml        # configuration du site (titre, thème, plugins)
├── quartz.config.default.yaml# config par défaut de référence (upstream)
├── quartz.lock.json          # versions verrouillées des plugins
├── quartz.ts                 # point d'entrée
└── public/                   # build généré (ignoré par git)
```

## Ajouter du contenu

1. Crée un fichier `.md` dans `content/` (ou un sous-dossier pour une nouvelle section).
2. Ajoute un frontmatter en tête de fichier :
   ```markdown
   ---
   title: Mon titre
   tags:
     - exemple
   ---
   ```
3. Relie tes notes avec la syntaxe `[[wikilink]]`.

Voir [le guide de démarrage](content/guides/bien-demarrer.md) pour plus de détails.

## Déploiement — Cloudflare Pages

Dans le tableau de bord Cloudflare : **Workers & Pages → Create application → Pages → Connect to Git**,
sélectionne ce dépôt puis configure :

| Option                  | Valeur          |
| ----------------------- | --------------- |
| Production branch       | `main`          |
| Framework preset        | `None`          |
| Build command           | `npm run build` |
| Build output directory  | `public`        |

La version de Node est lue depuis le fichier `.node-version` (v22), aucune variable
d'environnement supplémentaire n'est nécessaire. À chaque `git push` sur `main`,
Cloudflare reconstruit et publie le site automatiquement.

Le site est en ligne sur **<https://grove.andrea-larboullet-marin.workers.dev>**.

> [!NOTE]
> Le `baseUrl` est configuré dans `quartz.config.yaml` (utilisé par le flux RSS,
> le sitemap et les images Open Graph). En cas de changement de domaine, pense à
> le mettre à jour.

## Configuration

Tout se règle dans `quartz.config.yaml` : titre du site, thème (couleurs, polices),
langue, analytics et liste des plugins. La référence complète est documentée sur
[quartz.jzhao.xyz/configuration](https://quartz.jzhao.xyz/configuration).

## Licence

- Le moteur Quartz est sous licence MIT — voir [`LICENSE.txt`](LICENSE.txt).
- Le contenu de cette base est sous licence MIT — voir [`LICENSE`](LICENSE).

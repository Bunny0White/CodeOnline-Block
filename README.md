# Structure du dépôt CodeOnline-Block

Ce dépôt contient **162 blocks** (47 d'origine + 115 nouveaux) et la feuille de
style complète du design system, découpée en 6 fichiers dans `css/` :

- `css/index.css` — **fichier servi à `https://studios.online-corps.net/api-css/`**,
  contient uniquement les `@import` vers les 5 fichiers ci-dessous, dans l'ordre :
  ```css
  @import url('https://studio.online-corps.net/api-css/fonts.css');
  @import url('https://studio.online-corps.net/api-css/variables.css');
  @import url('https://studio.online-corps.net/api-css/reset.css');
  @import url('https://studio.online-corps.net/api-css/default.css');
  @import url('https://studio.online-corps.net/api-css/default-2.css');
  ```
- `css/fonts.css` — chargement Google Fonts (Syne, DM Sans, JetBrains Mono)
- `css/variables.css` — variables CSS globales (couleurs, espacements, etc.)
- `css/reset.css` — normalisation des styles natifs du navigateur
- `css/default.css` — design system principal (composants, sections d'origine)
- `css/default-2.css` — nouvelles classes ajoutées (kanban, comparatif, roadmap,
  process zigzag, bento, stats animées, etc.)

L'éditeur Code Online référence uniquement `https://studios.online-corps.net/api-css/`
(voir `system_script/editor.blocks.js`) — c'est donc `css/index.css` qui doit être
déployé à cette URL exacte sur votre serveur ; les 5 autres fichiers doivent être
accessibles aux chemins relatifs qu'il référence (`/api-css/fonts.css`, etc.).

Si d'autres classes sont ajoutées plus tard et que `default-2.css` devient trop
volumineux, créez un `default-3.css`, ajoutez son import à la suite dans
`index.css` — aucune limite au nombre de fichiers chaînés.


## Structure des dossiers de blocks

- `headers/` — 20 blocks d'en-tête
- `footers/` — 16 blocks de pied de page
- `body/` — 126 blocks de contenu, organisés par sous-dossier thématique :
  - `hero/` (8) — bannières d'accueil
  - `features/` (8) — mises en avant de fonctionnalités
  - `stats/` (5) — chiffres clés et statistiques
  - `pricing/` (6) — grilles tarifaires
  - `testimonials/` (6) — témoignages clients
  - `team/` (4) — présentation d'équipe
  - `faq/` (4) — questions fréquentes
  - `cta/` (6) — appels à l'action
  - `gallery/` (6) — galeries et portfolios
  - `process/` (8) — étapes, kanban, roadmap, workflow
  - `blog/` (6) — listes et mises en avant d'articles
  - `ecommerce/` (8) — boutique, panier, avis produits
  - `saas/` (6) — fonctionnalités, API, changelog
  - `restaurant/` (4) — galerie, chef, horaires, événements
  - `landing/` (8) — argumentaire de vente, garanties, comparatifs
  - + blocks d'origine (blog, ecommerce, landing, restaurant, saas — 12 fichiers
    racine du dossier `body/`)

Toute nouvelle catégorie de sous-dossier dans `body/` sera automatiquement
détectée et affichée dans l'éditeur sous ce nom.

Ne renommez pas `headers/`, `footers/`, `body/` : ces 3 noms sont utilisés tels
quels par le logiciel.

## Placeholders dynamiques [xxx]

Vous pouvez utiliser dans n'importe quel fichier .html des placeholders entre
crochets, correspondant aux clés du fichier `Site_Info.Code_Online.config` du
projet (camelCase) :

```
[siteName]       → ex: "My test"
[domain]         → ex: "test.test"
[tagline]        → ex: "test test"
[heroTitle]      → ex: "test Hero"
[heroSubtitle]   → ex: "Test test Hero"
[templateId]     → ex: "agency"
[primaryColor]   → ex: "#2563eb"
[secondaryColor] → ex: "#7c3aed"
[accentColor]    → ex: "#f59e0b"
[createdAt] / [updatedAt] → dates ISO
```

Toute clé présente dans le config est automatiquement disponible (y compris les
futures clés `custom-xxx` ajoutées par l'utilisateur, exposées en `[custom-xxx]`
côté config et résolues côté éditeur). Si une clé n'existe pas dans le config,
le placeholder `[xxx]` reste affiché tel quel (aucune erreur).

Le remplacement se fait :
- en aperçu (preview live et panneau de blocs), sans modifier le fichier source
- en mémoire dans le canvas, mis à jour automatiquement si vous modifiez le
  Site_Info après avoir posé un bloc (sauf si ce bloc a été édité manuellement)
- en dur, dans le code final exporté/sauvegardé sur disque

# Structure attendue par Code Online

Ce dépôt doit contenir, à la racine, les dossiers suivants (exactement comme ci-dessous) :

- headers/   → fichiers .html de blocs d'en-tête
- footers/   → fichiers .html de blocs de pied de page
- body/      → fichiers .html de blocs de contenu (peut contenir des sous-dossiers thématiques : blog/, ecommerce/, landing/, restaurant/, saas/, etc.)

Toute nouvelle catégorie de sous-dossier dans body/ sera automatiquement détectée et affichée dans l'éditeur sous ce nom (ex: body/blog/*.html → catégorie "blog").

Ne renommez pas headers/, footers/, body/ : ces 3 noms sont utilisés tels quels par le logiciel.

## Placeholders dynamiques [xxx]

Vous pouvez utiliser dans n'importe quel fichier .html des placeholders entre crochets,
correspondant aux clés du fichier Site_Info.Code_Online.config du projet (camelCase) :

  [siteName]       → ex: "My test"
  [domain]         → ex: "test.test"
  [tagline]        → ex: "test test"
  [heroTitle]       → ex: "test Hero"
  [heroSubtitle]    → ex: "Test test Hero"
  [templateId]      → ex: "agency"
  [primaryColor]    → ex: "#2563eb"
  [secondaryColor]  → ex: "#7c3aed"
  [accentColor]     → ex: "#f59e0b"
  [createdAt] / [updatedAt] → dates ISO

Toute clé présente dans le config est automatiquement disponible (y compris les futures clés
custom-xxx ajoutées par l'utilisateur). Si une clé n'existe pas dans le config, le placeholder
[xxx] reste affiché tel quel (aucune erreur).

Le remplacement se fait :
  - en aperçu (preview live), sans modifier le fichier source
  - en dur, dans le HTML inséré, au moment où l'utilisateur ajoute le bloc dans le canvas

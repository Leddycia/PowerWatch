# Consignes du projet final (transcription)

> **Transcription fidèle** de `docs/Consignes_Projet_Final_IA_L3.pdf` (4 pages). En cas de doute, **l'original fait foi**.
> Seuls ajouts : le titre et cet encadré d'en-tête de la transcription, les identifiants **`[C-xx]`** en gras, qui permettent de citer chaque consigne, l'index ci-dessous, l'encadré « Lecture retenue » qui le suit (interprétation de l'équipe, décision D-06, et non texte du cours) et le libellé « Pied de page de l'original » devant le texte du pied de page. Le texte n'a pas été reformulé. Les apostrophes typographiques ont été remplacées par des apostrophes droites.

## Index des consignes

| ID | Consigne (résumé) | Où dans le texte |
|---|---|---|
| C-01 | Arborescence et noms exacts des livrables ; `fiche_contribution.pdf` **à côté** du dossier projet | Étapes 1 à 5 et « Livrable à remettre » |
| C-02 | Chaque exigence est reliée au brief ; aucune exigence non justifiée | Étape 1 |
| C-03 | « Ce qui ne fait pas partie de la première version » : décisions du client à respecter | Consigne générale |
| C-04 | Souhaits « plus tard » : à classer dans le backlog, à justifier, compatibilité à vérifier | Consigne générale |
| C-05 | Règle non fixée par le client : ne pas l'inventer, la signaler comme point à décider | Consigne générale |
| C-06 | Backlog : format des US, CA observables et vérifiables, MoSCoW, ordre justifié, section « Sprint 01 » | Étape 2 |
| C-07 | Taille du Sprint 01 (6 personnes = 3 US), incrément utilisable, chargement inclus dans la 1re US | Étape 2 |
| C-08 | `prompts.md` : prompt RMTCEV avec CDC et Sprint 01 en contexte, 2 ou 3 autres prompts, au moins 1 proposition de l'IA corrigée ou rejetée | Étape 3 |
| C-09 | `version_IA.html` brut, jamais modifié ; `index.html` corrigé (facultatif si `version_IA` conforme, à dire dans le README) | Étape 4 |
| C-10 | Fichier HTML autonome : CSS, JS (et données) inclus | Règles du prototype |
| C-11 | Ouverture par double-clic, sans Internet, sans serveur, sans compte | Règles du prototype |
| C-12 | CSV chargé par un bouton « Choisir un fichier » ; données intégrées = écart à signaler et justifier dans `prompts.md` | Règles du prototype |
| C-13 | Données fictives uniquement, dans les prompts et le prototype | Règles du prototype |
| C-14 | Test sur un autre ordinateur après téléchargement depuis le Drive | Règles du prototype |
| C-15 | README : ouverture, outils, statut et capture pour chaque CA du Sprint 01 | Étape 5 |
| C-16 | Tous les membres comprennent tout le projet ; soutenance d'environ 15 min avec questions individuelles | Étape 5 et Soutenance |
| C-17 | Sprint 02 facultatif : dans le backlog, vérifié dans le README, ne compense rien | Pour aller plus loin |
| C-18 | Critères de notation : fidélité, qualité des CA, arbitrages, précision des prompts, vérification et correction de l'IA | Soutenance (rappel) |
| C-19 | Remise sur le Drive partagé, au plus tard le dimanche 18 octobre 2026 à 23 h 59 | En-tête |
| C-20 | Contenu obligatoire du cahier des charges (5 rubriques) | Étape 1 |
| C-21 | Mission : cahier des charges, backlog, délégation du Sprint 01 à l'IA, conservation de sa production, vérification et correction jusqu'aux CA ; objectif : cadrer, confier, contrôler, pas l'application la plus complète | Consigne générale |
| C-22 | Organisation en groupe (1 cas par groupe) ; outils d'IA et éditeur au choix | En-tête |
| C-23 | Le prototype réalise les user stories du Sprint 01 | Règles du prototype |

> **Lecture retenue pour C-10 et C-12 (décision D-06)** : notre cas fournit un CSV, donc les données sont chargées par le bouton (C-12) et ne sont **pas** intégrées au fichier HTML. Le CSS et le JS, eux, sont bien inclus (C-10).

---

# IA générative appliquée aux projets technologiques

## Projet final

*Du besoin client au prototype*

| | |
|---|---|
| **Organisation** | **[C-22]** Travail en groupe. Chaque groupe reçoit l'un des 11 cas proposés ; deux groupes ne travaillent pas sur le même cas. |
| **Outils** | **[C-22]** ChatGPT, Claude, Gemini, Codex ou tout autre outil d'IA ; éditeur de code au choix (VS Code ou autre). |
| **Remise** | **[C-19]** Un dossier par groupe sur le Drive partagé (par exemple Groupe_01), contenant le dossier du projet Groupe_XX_Cas_YY et la fiche fiche_contribution.pdf. |
| **Échéance** | **[C-19]** Dimanche 18 octobre 2026, à 23 h 59. |

## Consigne générale

**[C-21]** Vous recevez la demande d'un client fictif. Votre mission est de transformer ce besoin en un cahier des charges, puis en un Product Backlog. Vous déléguez ensuite à l'IA la réalisation d'un premier Sprint, vous conservez ce qu'elle a produit, puis vous vérifiez et corrigez ce résultat jusqu'à ce qu'il réponde aux critères d'acceptation.

**[C-21]** L'objectif n'est pas de produire l'application la plus complète possible. Ce qui compte, c'est de montrer que vous savez cadrer un besoin, confier une tâche précise à l'IA et contrôler son résultat.

**Lisez attentivement le brief de votre cas.**

- **[C-03]** La rubrique « Ce qui ne fait pas partie de la première version » contient des décisions déjà prises par le client : respectez-les.
- **[C-04]** Les souhaits exprimés « plus tard » ne sont pas tranchés. C'est à vous de les classer dans le Product Backlog et de justifier votre choix, en vérifiant qu'ils restent compatibles avec les règles du client.
- **[C-05]** Si un souhait dépend d'une règle que le client n'a pas encore fixée, ne l'inventez pas : signalez-le comme un point à décider.

### Ressources

- le dossier de votre cas : la demande du client (01_Demande_client.docx) ;
- pour les cas 1 à 6, le fichier CSV de données fictives fourni dans le même dossier.

## Étape 1 : Rédiger le cahier des charges

Fichier : **cahier_des_charges.md** **[C-01]**

**[C-20]**

- contexte, objectifs et acteurs ;
- exigences fonctionnelles et exigences non fonctionnelles ;
- règles métier et contraintes ;
- périmètre de la première version et hors périmètre ;
- points encore à confirmer ou à décider.

**[C-02]** Chaque exigence doit pouvoir être reliée au brief du client. N'ajoutez aucune exigence qu'aucun élément du brief ne justifie.

## Étape 2 : Construire le Product Backlog

Fichier : **product_backlog.md** **[C-01]**

**[C-06]**

- les user stories au format : **En tant que** [acteur], **je veux** [capacité ou objectif] **afin de** [valeur ou bénéfice] ;
- pour chaque user story, des critères d'acceptation observables et vérifiables ;
- la priorité de chaque user story selon la méthode MoSCoW et l'ordre du backlog, avec une justification ;
- une section « Sprint 01 » : l'objectif du Sprint et les user stories retenues.

### Taille du Sprint 01

**[C-07]**

- groupes de 4 personnes : 2 user stories ;
- groupes de 5 ou 6 personnes : 3 user stories.

Le Sprint 01 doit produire un incrément utilisable : une page qui s'ouvre et montre au moins un résultat utile au client. Le chargement des données ou l'affichage de base fait partie de la première user story ; ce n'est pas une user story à part.

## Étape 3 : Déléguer le Sprint 01 à l'IA

Fichier : **prompts.md** **[C-01]**

**[C-08]**

- le prompt de délégation du Sprint 01, rédigé selon la structure RMTCEV, en fournissant à l'IA votre cahier des charges et votre Sprint 01 comme contexte ;
- 2 ou 3 autres prompts qui ont permis à l'IA de produire un travail important. Inutile de fournir tous vos prompts ;
- au moins une proposition de l'IA que vous avez corrigée ou rejetée, avec la raison (par exemple une fonctionnalité ajoutée hors du Sprint ou une règle mal appliquée).

## Étape 4 : Produire le prototype

Dossier : **prototype/** **[C-01]**

**[C-09]**

- **version_IA.html** : la première version produite par l'IA à partir du prompt de délégation, sans aucune modification ;
- **index.html** : la version finale, après vérification et corrections.

Si, après vérification, la version produite par l'IA respecte déjà tous les critères d'acceptation du Sprint 01, le fichier index.html n'est pas obligatoire. Indiquez-le dans le README.md : version_IA.html sert alors de prototype final pour la démonstration et la vérification.

### Règles du prototype

- **[C-23]** il réalise les user stories du Sprint 01 ;
- **[C-10]** le prototype final est un fichier HTML autonome : le CSS, le JavaScript et les données sont inclus dans le fichier ;
- **[C-11]** il s'ouvre par double-clic dans un navigateur, sans connexion Internet, sans serveur et sans compte utilisateur ;
- **[C-12]** pour les cas avec un fichier CSV, la page charge ce fichier à l'aide d'un bouton « Choisir un fichier ». Si vous intégrez les données directement dans la page, cela constitue un écart par rapport à la demande du client : signalez-le et justifiez-le dans prompts.md ;
- **[C-13]** seules des données fictives sont utilisées, dans les prompts comme dans le prototype ;
- **[C-14]** avant la remise, un membre du groupe télécharge le dossier depuis le Drive et teste la page sur un autre ordinateur.

## Étape 5 : Vérifier et documenter

Fichier : **README.md** **[C-01]**

**[C-15]**

- comment ouvrir le prototype et quels outils ont été utilisés ;
- pour chaque critère d'acceptation du Sprint 01 : son statut (respecté, non respecté ou partiel) et une preuve (capture d'écran placée dans le dossier captures).

**[C-16]** Tous les membres doivent comprendre le projet dans son ensemble, et pas seulement la partie sur laquelle ils ont principalement travaillé.

## Pour aller plus loin (facultatif)

**[C-17]** Une fois le Sprint 01 terminé et vérifié, vous pouvez réaliser d'autres user stories de votre backlog dans un Sprint 02. Elles doivent figurer dans product_backlog.md, respecter les règles du client et être vérifiées dans le README.md comme celles du Sprint 01. Ce travail supplémentaire n'est pas obligatoire et ne compense pas un manque dans le travail demandé.

## Livrable à remettre

**[C-01]** **Dans le dossier de votre groupe sur le Drive** (par exemple **Groupe_01**), déposez deux éléments au même niveau : le dossier du projet **Groupe_XX_Cas_YY** et la fiche de contribution **fiche_contribution.pdf**, qui contient un tableau unique où chaque ligne indique le nom d'un membre, la partie sur laquelle il a principalement travaillé et sa contribution résumée en une phrase.

```
Groupe_01/
├── fiche_contribution.pdf
└── Groupe_01_Cas_YY/
    ├── README.md
    ├── cahier_des_charges.md
    ├── product_backlog.md
    ├── prompts.md
    ├── prototype/
    │   ├── version_IA.html
    │   └── index.html
    └── captures/
```

## Soutenance

**[C-16]**

- environ 15 minutes par groupe : une courte démonstration du prototype, puis des questions individuelles ;
- tous les membres sont interrogés, y compris sur des parties sur lesquelles ils n'ont pas principalement travaillé.

**[C-18]** **Rappel :** la note ne dépend pas de la taille du prototype. Elle dépend surtout de la fidélité au besoin du client, de la qualité des critères d'acceptation, de la pertinence de vos arbitrages, de la précision de vos prompts et de votre capacité à vérifier et à corriger le travail de l'IA.

---

*Pied de page de l'original : « IA générative appliquée aux projets technologiques | Projet final ».*

# Transmission pour R6 : traçabilité d'`index.html` (D-16)

> **Pour l'IA assistante de R6 (Petiote).** Ce fichier vient d'une session parallèle de Leddycia (Claude Code, Claude Opus 5.5, JP-28 à JP-30). Elle a créé `Groupe_01_Cas_01/prototype/index.html` et 17 captures suffixées `_index` (commit `6f59584`), sans toucher aux fichiers de R6 : un seul auteur par fichier. `ETAT_PROJET.md`, les journaux, `decisions.md`, le plan de test et le README n'ont **pas** été modifiés.
>
> **À faire par R6, après validation de Petiote (`AGENTS.md` §0, étape 6) :**
>
> 1. **Numéros** : D-16, E-29 à E-33 et JP-28 à JP-30 étaient les suivants libres au commit `6f59584`. S'ils sont déjà pris, décale-les partout, y compris dans les renvois d'un bloc à l'autre.
> 2. **Blocs 1 à 6** : colle-les tels quels à l'endroit indiqué (ce sont des ajouts ; seul le bloc 5 s'insère dans le §3 du plan de test, sans rien y réécrire).
> 3. **README (blocs 7 et 8)** : intègre la section et le tableau dans ta structure. Ils remplacent l'explication de l'absence d'`index.html` prévue par `ETAT_PROJET.md` §6.
> 4. **`ETAT_PROJET.md`**, à mettre à jour par R6 : §3, ligne « `index.html` **non créé** » (D-16 : créé ensuite, `6f59584`) ; §6, mission de R6 : la passe réduite A1 et le test depuis le Drive portent désormais sur `index.html` (le prototype présenté), Firefox compris, car seul Chrome a été testé sur `index.html` ; la mention « `index.html` : non créé » en fin de §6.
> 5. **Ce fichier** : une fois tout intégré, supprime-le dans ton commit de passation et note-le dans `travail/audits/R6_audit.md`.
>
> **Contrôles déjà faits** sur `index.html` (détail dans le bloc 6) : bloc `<script>` identique à celui de `version_IA.html` ; `version_IA.html` intact (`git diff version-ia` vide) ; aucune ressource externe ni donnée intégrée ; 20 CA, Test-P04 et contrôles transverses respectés.

## Bloc 1 : D-16

**Où** : travail/decisions.md, §1, nouvelle ligne après D-15

````markdown
| D-16 | **`index.html` d'habillage** : `Groupe_01_Cas_01/prototype/index.html` est créé pour la présentation et les textes seulement. Son bloc `<script>` est la copie exacte de celui de `version_IA.html` (aucune ligne de logique modifiée) ; aucune fonction ni information nouvelle (RG-04) ; aucune ressource externe (RG-05). Il corrige les écarts E-29 à E-31 et devient le prototype présenté dans le README ; `version_IA.html` reste intact (RG-08). Cette décision adapte la fiche 04 et `tests/plan_de_test.md` §2, qui ne prévoient `index.html` qu'en cas d'écart : E-29 et E-30 portent sur CA-02.02 (lecture stricte) et CA-02.05 (lisibilité de la mention). | validé | C-09 : « `index.html` corrigé (facultatif si `version_IA` conforme, à dire dans le README) ». Revérification complète sur `index.html` : 20 CA, Test-P04 et contrôles transverses respectés (`tests/plan_de_test.md` §4). Petiote, qui tient R6, a été prévenue avant la construction. | Leddycia, JP-28, JP-29 | 2026-10-18 |
````

## Bloc 2 : Journal des changements

**Où** : travail/decisions.md, §4, nouvelle ligne à la fin du tableau

````markdown
| 2026-10-18 | R6 (en parallèle, Leddycia) | D-16 | création → validé | `index.html` d'habillage décidé pendant R6 (JP-29) ; textes de traçabilité fournis à Petiote, qui tient les fichiers de R6 |
````

## Bloc 3 : E-29 à E-33

**Où** : travail/journal_ecarts.md, à la fin (décaler les numéros si E-29 est déjà pris)

````markdown
### E-29 : Prix de référence absent de la carte du coût (CA-02.02, lecture stricte)

- **Date / relais / membre** : 2026-10-18 / R6 (en parallèle) / Leddycia
- **Source** : `version_IA.html` (ChatGPT, GPT-4o)
- **Observé** : la carte du coût affiche le libellé « Coût estimé » (l. 596) et la description « Estimation du coût du carburant » (l. 600). Le prix « 300 gourdes par litre » n'apparaît que dans le bloc de chargement : « Prix de référence : 300 gourdes par litre » (l. 542), loin de la carte.
- **Attendu** : CA-02.02 : « son libellé contient les mots « coût estimé » et indique le prix de référence de 300 gourdes par litre ».
- **Référence** : CA-02.02, B-08, B-12, RM-01
- **Gravité** : mineur (R5 a retenu une lecture large : le prix est sur le même écran que le coût ; CA-02.02 respecté dans `tests/plan_de_test.md` §3)
- **Décision** : corrigé
- **Raison** : sous une lecture stricte (« son libellé »), le CA n'est pas respecté, et le jury peut retenir cette lecture.
- **Correction** : `index.html`, carte du coût : « Calcul du coût estimé : litres consommés × 300 gourdes par litre ». Le bloc de chargement garde « Prix de référence : 300 gourdes par litre ». Commit : `6f59584`.
- **Vérifié après correction** : oui, par l'IA assistante (texte de la carte du coût contrôlé sous Chrome 155 ; capture `US02_CA02_libelle_prix_index.png`)

### E-30 : Mention du prix non officiel en très petits caractères (CA-02.05)

- **Date / relais / membre** : 2026-10-18 / R6 (en parallèle) / Leddycia
- **Source** : `version_IA.html` (ChatGPT, GPT-4o)
- **Observé** : la mention « prix de référence de l'intendance, pas un prix officiel » (l. 602) est le plus petit texte de la page : 11 px (l. 398), sans majuscule ni point.
- **Attendu** : CA-02.05 : la mention « est visible à côté du coût » ; Q-20 : elle évite de lire le coût comme une dépense réelle (B-04).
- **Référence** : CA-02.05, B-12, Q-20
- **Gravité** : mineur (la mention est présente et à côté du coût ; R5 l'a jugée respectée)
- **Décision** : corrigé
- **Raison** : c'est la seule mise en garde sur le coût, et c'était le texte le moins lisible de la page.
- **Correction** : `index.html` : « Ce prix est un prix de référence de l'intendance, pas un prix officiel. », en 15 px, en gras, ambre foncé #8A5300 (contraste de 6,3:1 sur blanc). La mention exacte de CA-02.05 y figure mot pour mot, avec l'apostrophe droite. Commit : `6f59584`.
- **Vérifié après correction** : oui, par l'IA assistante (texte exact présent et visible, taille 15 px ; capture `US02_CA02_libelle_prix_index.png`)

### E-31 : Présentation de `version_IA.html` (contraste, tiret cadratin, pictogrammes, aide après une erreur)

- **Date / relais / membre** : 2026-10-18 / R6 (en parallèle) / Leddycia
- **Source** : `version_IA.html` (ChatGPT, GPT-4o)
- **Observé** : (1) texte secondaire gris #718096 (l. 19) : contraste de 4,02:1 sur blanc et 3,71:1 sur le fond de la page ; (2) tiret cadratin dans le titre de l'onglet, entre « PowerWatch » et « Suivi énergétique » (l. 6) ; (3) pictogrammes en caractères Unicode, au rendu variable selon les polices, dont ♨ (« sources chaudes ») pour le carburant (l. 588) et la lettre « G » pour le coût (l. 597) ; (4) après un fichier refusé, rien n'indique quoi faire.
- **Attendu** : une interface en français correct (H-03), lisible par la directrice et l'intendant (B-05a, B-05b) ; repère retenu par l'équipe pour le contraste : 4,5:1 (WCAG 2.2, critère 1.4.3) ; aucun tiret cadratin (consigne de l'équipe, JP-28).
- **Référence** : H-03, B-05a, B-05b, JP-28 ; RG-04 (rien d'ajouté au-delà du sprint)
- **Gravité** : mineur (aucun effet sur les CA)
- **Décision** : corrigé
- **Raison** : lisibilité et qualité du français ; aucune information ni fonction nouvelle.
- **Correction** : `index.html` : texte secondaire en ardoise #4A5D6E (6,8:1 sur blanc, 6,3:1 sur le fond) ; titre « PowerWatch · Suivi de la génératrice » ; pictogrammes SVG intégrés (horloge, goutte, billet, calendrier), masqués aux lecteurs d'écran ; phrase fixe affichée par le CSS seulement quand un message d'erreur est visible : « Corrigez le fichier, puis cliquez de nouveau sur « Choisir un fichier ». Le fichier d'origine n'est jamais modifié. » Les 4 tirets cadratins du script (valeurs de remise à zéro) sont conservés pour garder le script identique : ils ne sont jamais affichés, car le tableau de bord est masqué au même moment. Commit : `6f59584`.
- **Vérifié après correction** : oui, par l'IA assistante (aucun tiret cadratin ni demi-cadratin hors du script ; taille de texte minimale de 14 px ; message d'erreur et aide visibles sur `US01_CA07_colonne_manquante_index.png` et `US01_CA11_valeur_non_numerique_index.png`)

### E-32 : Proposition de l'outil de design rejetée (thème sombre, polices en ligne)

- **Date / relais / membre** : 2026-10-18 / R6 (en parallèle) / Leddycia
- **Source** : IA assistante (Claude Code, Claude Opus 5.5), compétence de design « ui-ux-pro-max » appelée à la demande de Leddycia (JP-28)
- **Observé** : système de design proposé pour PowerWatch : style « Glassmorphism » (verre dépoli, flou), fond sombre #0F172A, accent vert #22C55E, polices Fira Code et Fira Sans chargées depuis Google Fonts (`https://fonts.googleapis.com/css2?family=Fira+Code…`), et une structure de page commerciale (accroche, appel à l'action « Start trial / Contact »).
- **Attendu** : un seul fichier HTML sans aucune ressource externe (RG-05, C-10, C-11, P-05) ; aucune fonction hors sprint, dont le mode sombre (RG-04, P-08) ; un outil interne hors ligne et sans compte (B-16, B-17).
- **Référence** : RG-05, P-05, C-11, RG-04, P-08, B-16
- **Gravité** : majeur (appliquée, la police en ligne aurait fait échouer le contrôle « aucune ressource externe »)
- **Décision** : rejeté
- **Raison** : polices téléchargées depuis Internet ; thème sombre et effets de verre hors sprint ; page commerciale sans rapport avec le besoin.
- **Correction** : seconde recherche plus ciblée (style clair et accessible), puis direction retenue par l'IA et validée par Leddycia : fond clair, une seule couleur vive (ambre), polices déjà présentes sur l'ordinateur (Bahnschrift, Segoe UI) avec polices de repli.
- **Vérifié après correction** : oui, par l'IA assistante (motif d'`AGENTS.md` §7, `url(`, `src=` et `<link` : aucune occurrence dans `index.html` ; une seule requête pendant la vérification, le fichier local lui-même)

### E-33 : Icône d'onglet proposée puis retirée

- **Date / relais / membre** : 2026-10-18 / R6 (en parallèle) / Leddycia
- **Source** : IA assistante (Claude Code, Claude Opus 5.5), plan d'habillage (JP-28)
- **Observé** : le plan prévoyait d'intégrer le logo comme icône d'onglet, ce qui ajoute une balise `<link rel="icon">` à `index.html`.
- **Attendu** : les contrôles transverses de R5 vérifient l'absence de `<link` (`tests/plan_de_test.md` §3, « Aucune ressource externe »).
- **Référence** : RG-05, P-05
- **Gravité** : mineur (l'icône aurait été intégrée au fichier, sans appel réseau, mais le contrôle aurait signalé la balise)
- **Décision** : rejeté
- **Raison** : garder un contrôle simple et identique à celui de R5 ; l'icône n'apporte rien aux CA.
- **Correction** : aucune icône d'onglet ; le logo reste dans l'en-tête de la page.
- **Vérifié après correction** : oui, par l'IA assistante (`<link` : 0 occurrence)
````

## Bloc 4 : JP-28 à JP-30

**Où** : travail/journal_prompts.md, à la fin (décaler les numéros si JP-28 est déjà pris)

````markdown
### JP-28 : Habillage du prototype, logo et question sur `index.html`

- **Relais / membre** : R6 (en parallèle, pendant le relais de Petiote) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5), avec les compétences « ui-ux-pro-max » et « design »
- **Date et heure** : 2026-10-18, 16:36
- **Prompt (texte exact)** :
  > Pendant que Petiote travaille, prepare-moi un plan pour faire un design plus propre et original du systeme. Si je m'en souviens bien, c'etait preciser qu'on pouvait faire notre propre index.html non?
  >
  > use /ui-ux-pro-max /design
  > Cree un logo pour powerwatch et assure-toi que tout est en parfait francais, sans em-dash et user-friendly.
- **Ce qu'il a produit** : réponse à la question (C-09 permet `index.html`, mais la fiche 04 et le plan de test §2 le limitent : d'où D-16) ; logo PowerWatch en SVG (soleil levant lu comme un cadran, aiguille en forme d'éclair pour la génératrice) ; plan d'habillage avec maquette, tableau des textes avant et après, éléments à ne pas toucher, horaire et limite de 19 h 30 ; page de proposition privée sur claude.ai. Proposition de l'outil de design rejetée : E-32 ; icône d'onglet retirée : E-33.
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a validé le plan et prévenu Petiote avant la construction (JP-29).
- **Candidat pour `prompts.md`** : oui, pour §3 (proposition d'IA rejetée, E-32).

### JP-29 : Construction d'`index.html`

- **Relais / membre** : R6 (en parallèle) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 17:13
- **Prompt (texte exact)** :
  > Oui, construis index.html selon le plan. J'ai prévenu Petiote.
- **Ce qu'il a produit** : `Groupe_01_Cas_01/prototype/index.html`, dont le bloc `<script>` est copié à l'identique depuis `version_IA.html` ; vérification automatique complète (Chrome 155 sans interface, fuseau `America/Port-au-Prince` et réseau coupé par émulation, chargement par le vrai `<input type="file">`) : 37 contrôles, 0 non respecté ; 17 captures suffixées `_index` ; textes de traçabilité pour Petiote (D-16, E-29 à E-33, JP-28 à JP-30, README, plan de test §4). Corrections faites par l'IA en cours de route : mise en page sur téléphone (bouton et liste trop étroits à 390 px) ; capture de CA-01.06 ajoutée, car l'écran d'octobre avait été pris après Septembre et non après « Toute la période ».
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a validé le commit et le push (17:35, texte exact : « Oui, commite et pousse index.html et les 17 captures _index sur main. ») ; commit `6f59584`, poussé sur `main`.
- **Candidat pour `prompts.md`** : non (prompt court ; le contenu utile est dans E-29 à E-33).

### JP-30 : Transmission des textes de traçabilité à R6

- **Relais / membre** : R6 (en parallèle) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 17:37
- **Prompt (texte exact)** :
  > Push les textes pour Petiote et indique a son agent de les prendre en compte
- **Ce qu'il a produit** : `travail/transmission_R6_index.md` (blocs à intégrer par R6 : D-16, E-29 à E-33, JP-28 à JP-30, plan de test §4, README), commité et poussé sur `main` sans toucher aux fichiers de R6 ; message envoyé à la session Claude Code ouverte dans le dépôt pour l'audit de R6.
- **Ce que l'humain a vérifié ou corrigé** : à compléter par Petiote (intégration des blocs).
- **Candidat pour `prompts.md`** : non.
````

## Bloc 5 : Rectificatif

**Où** : tests/plan_de_test.md, §3, ligne à ajouter juste sous « index.html : non créé… »

````markdown
**Rectificatif (2026-10-18, D-16)** : `index.html` a été créé ensuite, pour l'habillage seulement (script identique à `version_IA.html`). Ses résultats sont au §4 ; ce tableau garde les résultats de R5 sur `version_IA.html`.
````

## Bloc 6 : §4

**Où** : tests/plan_de_test.md, nouvelle section à la fin du fichier

````markdown
## 4. Résultats d'exécution sur `index.html` (2026-10-18, D-16)

**Version testée** : `Groupe_01_Cas_01/prototype/index.html`. Son bloc `<script>` est identique, caractère pour caractère, à celui de `version_IA.html` (15 712 caractères ; empreinte SHA-256 du bloc commençant par `2f733dff58e7a89f`, fins de ligne LF). `version_IA.html` est intact (`git diff version-ia` vide).
**Environnement** : Windows 11 Pro ; Google Chrome 155.0.8059.80 sans interface, piloté par le protocole DevTools (chargement par le vrai `<input type="file">`, période choisie par l'événement `change`) ; fuseau du navigateur `America/Port-au-Prince` par émulation (décalage de 240 min au 01/09/2026 ; témoin du piège P-01 : `new Date("2026-09-01")` donne ici le 31/8) ; réseau coupé par émulation. Script de pilotage conservé hors du dépôt. Firefox n'a pas été testé sur `index.html` : à vérifier lors du test depuis le Drive sur un autre PC (fiche 06).
**Empreinte du CSV** : `320155c7…a84b` avant et après les tests.
**Listes ouvertes** : une liste déroulante ne se capture pas sans interface ; pour CA-01.03 et CA-01.10, la liste est affichée en entier pendant la capture (attribut `size`), puis remise dans son état normal.

| CA | Observé sur `index` | Statut | Capture |
|---|---|---|---|
| CA-01.01 | Bouton « Choisir un fichier » ; indicateurs masqués ; réseau coupé | respecté | `US01_CA01_etat_initial_index.png` |
| CA-01.02 | Sans erreur ; « Toute la période » ; 97 h ; 280,0 L | respecté | `US01_CA02_toute_periode_index.png` |
| CA-01.03 | « Août 2026 », « Septembre 2026 », « Octobre 2026 », « Toute la période » | respecté | `US01_CA03_liste_periodes_index.png` |
| CA-01.04 | 24 h / 71,0 L ; 30 h / 84,0 L ; 43 h / 125,0 L ; 97 h / 280,0 L | respecté | `US01_CA04_aout_index.png`, `_septembre_index`, `_octobre_index`, `US01_CA02_toute_periode_index.png` |
| CA-01.05 | 24 h, 30 h, 43 h ; ni 26 h, ni 32 h, ni 39 h | respecté | `US01_CA05_fuseau_haiti_index.png` (montage des 3 mois) |
| CA-01.06 | Toute la période puis Octobre, sans rechargement : 43 h ; 125,0 L | respecté | `US01_CA06_changement_octobre_index.png` |
| CA-01.07 | f02 : « Erreur à la ligne 1 (en-tête) : la colonne obligatoire « litres_carburant » est absente. » ; indicateurs masqués ; aide affichée | respecté | `US01_CA07_colonne_manquante_index.png` |
| CA-01.08 | Empreinte identique avant et après ; 0 champ éditable ; seul bouton : « Choisir un fichier » ; 0 lien | respecté | `US01_CA08_lecture_seule_index.png` |
| CA-01.09 | f06 puis original : Toute la période ; 97 h ; 280,0 L | respecté | `US01_CA09_reinitialisation_index.png` |
| CA-01.10 | f06 : « Août 2026 », « Septembre 2026 », « Toute la période » ; 54 h ; 155,0 L | respecté | `US01_CA10_fichier_partiel_index.png` |
| CA-01.11 | f03 : « Erreur à la ligne 3 : la valeur de « heures_generatrice » doit être un nombre valide positif ou nul. » ; indicateurs masqués | respecté | `US01_CA11_valeur_non_numerique_index.png` |
| CA-02.01 | 21 300 ; 25 200 ; 37 500 ; 84 000 gourdes | respecté | captures de CA-01.04 |
| CA-02.02 | Carte du coût : « Coût estimé » et « Calcul du coût estimé : litres consommés × 300 gourdes par litre » (E-29) | respecté | `US02_CA02_libelle_prix_index.png` |
| CA-02.03 | Août puis Septembre : 25 200 gourdes | respecté | `US01_CA04_septembre_index.png` (pris juste après Août) |
| CA-02.04 | 21 300, 25 200, 37 500 gourdes ; ni 23 100, ni 27 000, ni 33 900 | respecté | `US01_CA05_fuseau_haiti_index.png` |
| CA-02.05 | « Ce prix est un prix de référence de l'intendance, pas un prix officiel. », dans la carte du coût, 15 px (E-30) | respecté | `US02_CA02_libelle_prix_index.png` |
| CA-03.01 | 06/08/2026 (5 h) ; 08/09/2026 (5 h) ; 02/10/2026 (5 h) ; 06/08/2026 (5 h) | respecté | captures de CA-01.04 |
| CA-03.02 | f01 : 06/08, 08/09, 02/10, 06/08 (5 h) | respecté | `US03_CA02_lignes_melangees_index.png` (montage des 4 périodes) |
| CA-03.03 | f04, Août : « Aucun fonctionnement de la génératrice sur la période » (0 h ; 0,0 L ; 0 gourdes) | respecté | `US03_CA03_sans_generatrice_index.png` |
| CA-03.04 | 06/08, 08/09, 02/10 ; ni 05/08, ni 07/09, ni 01/10 | respecté | `US01_CA05_fuseau_haiti_index.png` |
| Test-P04 | f05 : 2 h ; 0,3 L ; 90 gourdes ; 03/08/2026 (1 h) | respecté | `TEST_P04_arrondi_decimales_index.png` |

**Contrôles transverses sur `index.html`**

| Contrôle | Observé | Statut |
|---|---|---|
| Hors ligne | Réseau coupé par émulation pendant toute la passe ; une seule requête, le fichier local lui-même | respecté |
| Aucune ressource externe | Motif d'`AGENTS.md` §7, `url(`, `src=`, `<link` : aucune occurrence | respecté |
| Aucune donnée intégrée | `2026-08-03` absent du source ; à l'ouverture, aucune valeur calculée | respecté |
| Lecture seule | Empreinte du CSV identique ; aucun champ éditable, aucun export | respecté |
| Hors sprint | Script identique à `version_IA.html` ; aucune information ni fonction ajoutée | respecté |
| Rechargement (P-09) | f04 puis original : 97 h ; 280,0 L | respecté |
| Lisibilité | Taille de texte minimale : 14 px ; aucun tiret cadratin ni demi-cadratin hors du script | respecté |
| Téléphone | Largeur de 390 px : pas de défilement horizontal | respecté |
````

## Bloc 7 : Section README

**Où** : Groupe_01_Cas_01/README.md, section sur le prototype (remplace « expliquer l'absence d'index.html »)

````markdown
## Prototype

Le dossier `prototype/` contient deux fichiers. Ils s'ouvrent par double-clic, sans Internet, sans serveur et sans compte.

| Fichier | Rôle |
|---|---|
| `prototype/index.html` | **Version à utiliser.** Même calcul que `version_IA.html`, présentation et textes revus. |
| `prototype/version_IA.html` | Première sortie brute de l'IA déléguée (ChatGPT, GPT-4o), jamais modifiée (C-09). |

**Pourquoi un `index.html` alors que `version_IA.html` respectait les CA ?** La vérification de R5 a trouvé les 20 CA respectés. Une relecture plus stricte a relevé deux points faibles : le prix de 300 gourdes par litre n'était pas dans la carte du coût (CA-02.02, E-29), et la mention « prix de référence de l'intendance, pas un prix officiel » était le plus petit texte de la page, en 11 px (CA-02.05, E-30). S'y ajoutent un contraste insuffisant, un tiret cadratin dans le titre et des pictogrammes peu clairs (E-31). L'équipe a donc décidé (D-16) de créer `index.html` pour la présentation seulement.

**Ce qui ne change pas** : tout le code JavaScript. Le bloc `<script>` d'`index.html` est la copie exacte de celui de `version_IA.html` : mêmes calculs, mêmes messages, mêmes formats. Aucune fonction n'est ajoutée (pas de graphique, d'export ni de mode sombre).

**Ce qui change** : un logo PowerWatch dessiné en SVG dans la page ; le prix dans la carte du coût ; la mention du prix non officiel en phrase lisible ; deux étapes numérotées (« Charger le fichier du registre », « Choisir la période ») ; une aide après une erreur ; des couleurs plus contrastées ; des pictogrammes dessinés au lieu de caractères spéciaux ; un affichage adapté au téléphone.

**Vérification** : `index.html` a été revérifié entièrement (Chrome 155, fuseau d'Haïti et réseau coupé par émulation) : 20 CA, Test-P04 et contrôles transverses respectés (`tests/plan_de_test.md` §4). Les captures d'`index.html` portent le suffixe `_index` ; celles de `version_IA.html` (R5) sont conservées.
````

## Bloc 8 : Tableau README

**Où** : Groupe_01_Cas_01/README.md, tableau des CA (à fusionner avec le tableau en cours)

````markdown
| CA | Statut | Capture `index.html` | Capture `version_IA.html` (R5) |
|---|---|---|---|
| CA-01.01 | respecté | [US01_CA01_etat_initial_index.png](captures/US01_CA01_etat_initial_index.png) | [US01_CA01_etat_initial.png](captures/US01_CA01_etat_initial.png) |
| CA-01.02 | respecté | [US01_CA02_toute_periode_index.png](captures/US01_CA02_toute_periode_index.png) | [US01_CA02_chargement_toute_periode.png](captures/US01_CA02_chargement_toute_periode.png) |
| CA-01.03 | respecté | [US01_CA03_liste_periodes_index.png](captures/US01_CA03_liste_periodes_index.png) | [US01_CA03_liste_periodes.png](captures/US01_CA03_liste_periodes.png) |
| CA-01.04 | respecté | [août](captures/US01_CA04_aout_index.png), [septembre](captures/US01_CA04_septembre_index.png), [octobre](captures/US01_CA04_octobre_index.png), [toute la période](captures/US01_CA02_toute_periode_index.png) | [US01_CA04_aout.png](captures/US01_CA04_aout.png) et suivantes |
| CA-01.05 | respecté | [US01_CA05_fuseau_haiti_index.png](captures/US01_CA05_fuseau_haiti_index.png) | [US01_CA05_fuseau_haiti.png](captures/US01_CA05_fuseau_haiti.png) |
| CA-01.06 | respecté | [US01_CA06_changement_octobre_index.png](captures/US01_CA06_changement_octobre_index.png) | [US01_CA06_changement_octobre.png](captures/US01_CA06_changement_octobre.png) |
| CA-01.07 | respecté | [US01_CA07_colonne_manquante_index.png](captures/US01_CA07_colonne_manquante_index.png) | [US01_CA07_colonne_manquante.png](captures/US01_CA07_colonne_manquante.png) |
| CA-01.08 | respecté | [US01_CA08_lecture_seule_index.png](captures/US01_CA08_lecture_seule_index.png) | [US01_CA08_lecture_seule.png](captures/US01_CA08_lecture_seule.png) |
| CA-01.09 | respecté | [US01_CA09_reinitialisation_index.png](captures/US01_CA09_reinitialisation_index.png) | [US01_CA09_reinitialisation_cumul.png](captures/US01_CA09_reinitialisation_cumul.png) |
| CA-01.10 | respecté | [US01_CA10_fichier_partiel_index.png](captures/US01_CA10_fichier_partiel_index.png) | [US01_CA10_fichier_partiel.png](captures/US01_CA10_fichier_partiel.png) |
| CA-01.11 | respecté | [US01_CA11_valeur_non_numerique_index.png](captures/US01_CA11_valeur_non_numerique_index.png) | [US01_CA11_valeur_non_numerique.png](captures/US01_CA11_valeur_non_numerique.png) |
| CA-02.01 | respecté | captures de CA-01.04 | [US02_CA01_cout_aout.png](captures/US02_CA01_cout_aout.png) et suivantes |
| CA-02.02 | respecté | [US02_CA02_libelle_prix_index.png](captures/US02_CA02_libelle_prix_index.png) | [US02_CA02_libelle_prix_reference.png](captures/US02_CA02_libelle_prix_reference.png) |
| CA-02.03 | respecté | [US01_CA04_septembre_index.png](captures/US01_CA04_septembre_index.png) | [US02_CA03_changement_cout.png](captures/US02_CA03_changement_cout.png) |
| CA-02.04 | respecté | [US01_CA05_fuseau_haiti_index.png](captures/US01_CA05_fuseau_haiti_index.png) | [US02_CA04_fuseau_cout.png](captures/US02_CA04_fuseau_cout.png) |
| CA-02.05 | respecté | [US02_CA02_libelle_prix_index.png](captures/US02_CA02_libelle_prix_index.png) | [US02_CA05_mention_officielle.png](captures/US02_CA05_mention_officielle.png) |
| CA-03.01 | respecté | captures de CA-01.04 | [US03_CA01_jour_max_aout.png](captures/US03_CA01_jour_max_aout.png) et suivantes |
| CA-03.02 | respecté | [US03_CA02_lignes_melangees_index.png](captures/US03_CA02_lignes_melangees_index.png) | [US03_CA02_lignes_melangees_aout.png](captures/US03_CA02_lignes_melangees_aout.png) et suivantes |
| CA-03.03 | respecté | [US03_CA03_sans_generatrice_index.png](captures/US03_CA03_sans_generatrice_index.png) | [US03_CA03_sans_generatrice.png](captures/US03_CA03_sans_generatrice.png) |
| CA-03.04 | respecté | [US01_CA05_fuseau_haiti_index.png](captures/US01_CA05_fuseau_haiti_index.png) | [US03_CA04_fuseau_jour_max.png](captures/US03_CA04_fuseau_jour_max.png) |
| Test-P04 | respecté | [TEST_P04_arrondi_decimales_index.png](captures/TEST_P04_arrondi_decimales_index.png) | [TEST_P04_arrondi_decimales.png](captures/TEST_P04_arrondi_decimales.png) |
````

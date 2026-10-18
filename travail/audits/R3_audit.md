# Audit d'entrée : relais R3 (Leddycia, Claude Code / Claude Opus 5.5, 2026-10-18 11:52)

## Livrable audité : `Groupe_01_Cas_01/cahier_des_charges.md` (produit par R2)

Contrôles faits en lecture seule, par un script Python exécuté hors du dépôt (citations, sources, termes techniques, Q-xx, matrice, valeurs de l'oracle), puis par lecture de l'IA.

| # | Constat | Preuve (fichier:ligne, B/C/CA) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|
| 1 | Dépôt synchronisé : `## main...origin/main` sans autre ligne ; tags `relais-1` et `relais-2` présents ; ETAT §8 « Aucun relais en cours. » | `git status -sb`, `git tag -l` | conforme | laissé |
| 2 | Empreinte SHA-256 du CSV conforme | `Get-FileHash` → `True` | conforme | laissé |
| 3 | A1 : les 5 rubriques de C-20 sont présentes (§1 à §3, §4 et §5, §6 et §7, §9, §10 et §10 bis, §11) ; table de correspondance au §12.2 | `cahier_des_charges.md` L287 | conforme | laissé |
| 4 | A2 : tirage au hasard (graine 20261018) EF-07, RM-01, EF-03, CT-01, ENF-01 : chaque source existe et dit bien cela (B-10, B-13, B-19 ; B-12 ; B-09 ; C-10 ; B-16). Les 19 exigences (8 EF, 2 ENF, 4 RM, 5 CT) ont une source valide ; chaque CT cite un C-xx | L66 à L121 | conforme | laissé |
| 5 | A3 : aucune exigence inventée. « export » n'apparaît que dans Q-10 (L206), « graphique » que dans le §10 bis, Q-11, Q-14 et la matrice. Lectures d'équipe déclarées par R2 : définitions du §4, EF-02 au rang 1, EF-06 « pour la période » | L58 à L60, L67, L71, L77, L206 | conforme | laissé ; prises en compte dans les CA |
| 6 | A4 : pas de solution technique. « HTML », « CSS » et « JavaScript » seulement dans CT-01 (texte de C-10) et au §12.2 ; « navigateur » dans CT-02 (C-11), Q-09 et H-05 | L117, L118, L283 | conforme | laissé |
| 7 | A5 : B-25 à B-27 mot pour mot au §10 ; B-21 à B-24 mot pour mot au §10 bis ; Q-01 à Q-17 présentes avec leur hypothèse, statuts identiques à `travail/decisions.md` | L170 à L213 | conforme | laissé |
| 8 | A5 (fiche) : la checklist de la fiche 02 cite encore « Q-01 à Q-14 », dépassée depuis Q-15 à Q-17 | `agents/02_product_owner.md` L31 | à corriger (mineur) | remonté ; fiche non modifiée (RG-10) |
| 9 | A6 : la matrice §12.1 relie chacun de B-06 à B-17 à une EF, une ENF ou une RM ; B-01 à B-27 tous présents | L238 à L271 | conforme | laissé |
| 10 | Relecture mot à mot (ETAT §6, étape 3) : les 39 passages cités entre guillemets ou en bloc (§3, RM-01, §8, §9, §10, §10 bis) sont identiques au brief (comparaison automatique). « Toute la période », « Aucun fonctionnement de la génératrice sur la période », « données au 16/10 » et les libellés de H-04 sont des textes de l'équipe (Q-xx, H-xx), correctement attribués | L47 à L49, L101, L127, L133 à L138, L148 à L162, L170 à L172, L182 à L185 | à faire (humain) | relecture humaine faite par Leddycia pendant la rédaction (résultat : voir section suivante) |
| 11 | Aucune valeur chiffrée de l'oracle dans le CDC, comme annoncé | L17 | conforme | laissé ; toutes les valeurs des CA viennent de `docs/oracle.md` |
| 12 | Points O-10 #1 et #2 : colonnes et ordre des lignes du tableau jour par jour non fixés par le client ; les fixer dans un CA serait trancher à la place du client (RG-02) | `travail/audits/R2_audit.md`, « Points remontés » ; B-11 | à corriger | remonté : Q-18 et Q-19 (validées par Leddycia, JP-16) |
| 13 | Point O-10 #11 : rappel, à côté du coût, que le prix est un prix de référence et non un prix officiel ; présentation non demandée par le client | B-12 ; esquisse CA-02.02 de la fiche 02 | à corriger | remonté : Q-20 (validée par Leddycia, JP-16) |
| 14 | Points O-10 #4 et #5 : « toute la période » = toutes les lignes du fichier chargé, et remplacement complet au rechargement ; couverts par la définition du CDC §4 (« tous les jours du fichier chargé ») et par B-26 (« le CSV reste la seule source ») | L60 ; B-26 | conforme | laissé ; CA-01.10 et CA-01.09 citent ces sources |
| 15 | O-9 (B-14 « peuvent avoir une décimale » contre R-04 « au plus une décimale ») : sans effet sur les CA, qui citent l'hypothèse Q-01 | ETAT §5, O-9 | à corriger (équipe) | laissé ouvert, à trancher avant le prompt de R4 |
| 16 | Esquisse de la fiche 02 : seul CA-01.05 teste le fuseau ; le bug fausse aussi le coût (23 100 au lieu de 21 300 gourdes en août) et le jour max (05/08/2026 au lieu de 06/08/2026) | `docs/oracle.md` §5 | amélioration | CA-02.04 et CA-03.04 ajoutés dans le backlog (numéros nouveaux, sans renuméroter) |
| 17 | Esquisse de la fiche 02 : le bénéfice de l'US-03 (« identifier les journées les plus dépendantes de la génératrice ») n'est pas dans le brief | fiche 02 L54 ; B-04 | amélioration | bénéfice rattaché à B-04 dans le backlog |
| 18 | Avec Q-18 à Q-20, le CDC §11.1 (Q-01 à Q-17), embarqué dans le prompt de R4, ne serait plus complet | L191 ; DoD `AGENTS.md` §12 | à corriger | ajout ciblé au CDC, accepté par Leddycia (JP-16) |
| 19 | ETAT §2 : outil d'IA de R3 « à compléter » | `ETAT_PROJET.md` L47 | à corriger | corrigé : donné par Leddycia (JP-16) |

## Ce qui a été seulement survolé ; résultats donnés par le membre

- Rien n'a été survolé : A1 à A6 contrôlés par script et par lecture.
- Relecture humaine mot à mot du CDC contre le brief : faite par Leddycia pendant la rédaction du backlog ; résultat : **conforme** (JP-17). Le reste de R2 (ETAT §4, point 1) est donc levé.
- Relecture humaine du product backlog par Leddycia : rien à changer (JP-17).

## Corrections apportées (une ligne par correction)

- `Groupe_01_Cas_01/cahier_des_charges.md` (livrable de R2), ajout ciblé validé par Leddycia (JP-16) : Q-18 à Q-20 au §11.1 (titre « Q-01 à Q-20 ») ; renvois au §4 « Points à confirmer liés » (EF-06 → Q-20 ; EF-08 → Q-18, Q-19), dans RM-01 (Q-20) et au §12.1 (B-08, B-12 → Q-20 ; B-11 → Q-18, Q-19 ; B-19 → Q-18) ; mention dans la ligne « Version ». Aucun autre texte du CDC modifié (RG-10).

## Points remontés à l'équipe (decisions.md, ETAT_PROJET.md)

- **Q-18 à Q-20** (provisoires, hypothèses proposées par l'IA, validées par Leddycia, JP-16) : colonnes du tableau jour par jour (les 4 colonnes de B-19), ordre de ses lignes (chronologique), rappel « prix de référence de l'intendance, pas un prix officiel » à côté du coût. Points O-10 #1, #2 et #11 de R2 résolus ainsi ; #4 et #5 traités par CA-01.10 et CA-01.09.
- **O-9** (B-14 contre `AGENTS.md` R-04) : toujours ouvert, à trancher par l'équipe avant le prompt de R4 ; les CA citent l'hypothèse Q-01.
- **Fiche 02** : la checklist A5 cite encore Q-01 à Q-14 (mineur ; ETAT §5, O-12).
- **Pour R4** : les CA du Sprint 01 citent cinq fichiers de test ; le cinquième (en-tête et 24 lignes d'août et de septembre, pour CA-01.09 et CA-01.10 : 54 h et 155,0 L) n'est pas encore décrit dans `docs/oracle.md` §8. Le relecteur du prompt RMTCEV est le membre de R3 (Leddycia).
- **O-2** : membre de R4 = Bradley, outil Antigravity (Gemini), modèle à préciser ; R5 et R6 à compléter.

## Ce que j'ai produit pendant mon relais

- `Groupe_01_Cas_01/product_backlog.md` v1 : 8 US au format exact, 34 CA (20 pour le Sprint 01, chiffrés avec l'oracle et contrôlés par un recalcul indépendant depuis le CSV), justification de l'ordre et du MoSCoW, souhaits « plus tard » avec compatibilité, section Sprint 01 (objectif, US-01 à US-03, hypothèses appliquées, fichiers de test nécessaires, DoD).
- `Groupe_01_Cas_01/cahier_des_charges.md` : ajout ciblé de Q-18 à Q-20 (voir « Corrections apportées »).
- `travail/decisions.md` : Q-18 à Q-20 et leur ligne au journal des changements.
- `travail/journal_prompts.md` : JP-15 à JP-17 ; `travail/journal_ecarts.md` : E-20 et E-21.
- `ETAT_PROJET.md` tenu à jour pendant le relais (§1, §2, §8), puis passation (§1 à §8).
- Ce rapport.

## Journal de bord du relais (copie intégrale d'ETAT §8, ajoutée à la passation)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

| Relais | Membre | Outil et modèle | Fiche | Porte visée | Début |
|---|---|---|---|---|---|
| R3 | Leddycia | Claude Code (application de bureau, Claude Opus 5.5) | `agents/02_product_owner.md` | G3 | 11:55 |

**Plan validé** (JP-16) : 1. R3 EN COURS, rapport d'audit créé, JP-15 et JP-16 ; 2. Q-18 à Q-20 dans `travail/decisions.md` (provisoires, validées par Leddycia) ; 3. ajout ciblé de Q-18 à Q-20 au cahier des charges (§4 « Points à confirmer liés », §11.1, §12.1), consigné en « Corrections apportées » ; 4. rédaction de `Groupe_01_Cas_01/product_backlog.md` selon la fiche 02 (8 US, CA du Sprint 01 chiffrés avec l'oracle, numérotation CA-01.01 à CA-01.08 conservée, ajouts CA-01.09, CA-01.10, CA-02.04, CA-03.04 ; pas de Sprint 02) ; 5. contrôle de la DoD par script, E-xx pour toute proposition de l'IA corrigée ou rejetée ; 6. relecture par Leddycia, puis « fin de notre relais ».

**Audit d'entrée (synthèse)** (détail : `travail/audits/R3_audit.md`) :
- A1 à A6 conformes : 5 rubriques de C-20 ; 5 exigences tirées au hasard (EF-07, RM-01, EF-03, CT-01, ENF-01) et les 19 exigences ont une source valide ; aucune exigence inventée ni solution technique ; B-21 à B-27 mot pour mot ; Q-01 à Q-17 identiques à `decisions.md` ; matrice B-06 à B-17 complète | script hors dépôt | conforme.
- Relecture mot à mot : 39 citations du CDC comparées automatiquement au brief, toutes identiques ; relecture humaine faite par Leddycia pendant la rédaction : conforme (JP-17) | CDC §3, RM-01, §8 à §10 bis | conforme.
- Points O-10 : colonnes et ordre du tableau jour par jour non fixés par le client (RG-02) ; rappel « pas un prix officiel » non demandé | `R2_audit.md` | à corriger : Q-18 à Q-20.
- Esquisse de la fiche 02 : le fuseau n'est testé que sur les totaux, alors que le bug fausse aussi le coût et le jour max (oracle §5) | fiche 02, oracle §5 | amélioration : CA-02.04, CA-03.04.
- Fiche 02 : la checklist A5 cite encore Q-01 à Q-14 | fiche 02 L31 | à corriger (mineur), remonté.
- Survolé : rien. Résultats du membre : relecture mot à mot du CDC conforme ; relecture du backlog sans correction (JP-17).

**Journal de bord**

| Heure | Étape | Ce qui a été fait | Fichiers | État |
|---|---|---|---|---|
| 11:52 | 1 | (JP-15) Synchronisation, contrôle de chargement (RG-08), audit d'entrée A1 à A6 en lecture seule, rapport et plan présentés | aucun fichier du dépôt | fait |
| 11:55 | 1 | (JP-16) Plan, audit et Q-18 à Q-20 validés ; R3 EN COURS ; rapport d'audit créé ; JP-15 et JP-16 | `ETAT_PROJET.md`, `travail/audits/R3_audit.md`, `travail/journal_prompts.md` | fait |
| 11:56 | 2 | Q-18 (colonnes du tableau), Q-19 (ordre du tableau), Q-20 (rappel du prix de référence) consignées, statut provisoire, ligne au journal des changements | `travail/decisions.md` | fait |
| 11:57 | 3 | Ajout ciblé de Q-18 à Q-20 au cahier des charges : version, §4 « Points à confirmer liés », RM-01, §11.1, §12.1 (B-08, B-11, B-12, B-19) | `Groupe_01_Cas_01/cahier_des_charges.md` | fait |
| 12:00 | 4 | Product backlog v1 : 8 US, 34 CA (Sprint 01 : CA-01.01 à CA-01.11, CA-02.01 à CA-02.05, CA-03.01 à CA-03.04 ; CA-01.11, valeur non numérique, ajouté en plus du plan), justification de l'ordre et du MoSCoW, souhaits « plus tard » avec compatibilité, Sprint 01 (objectif, US, hypothèses, fichiers de test, DoD) | `Groupe_01_Cas_01/product_backlog.md` | fait |
| 12:01 | 5 | Contrôle DoD par script : format des 8 US et des 34 CA, numérotation CA-01.01 à CA-01.08 conservée, identifiants cités existants, valeurs recalculées depuis le CSV (totaux, coûts, jours max, signature du fuseau, deux mois, tableau), aucun terme technique, Sprint 01 = US-01 à US-03 : conforme | aucun fichier modifié | fait |
| 12:02 | 5 | E-20 (citation de B-12 corrigée dans Q-20) et E-21 (esquisse de la fiche 02 corrigée : bénéfice de l'US-03, fuseau) | `travail/journal_ecarts.md` | fait |
| 12:03 | 6 | (JP-17) Relecture du backlog par Leddycia : rien à changer ; relecture mot à mot du CDC : conforme ; « fin de notre relais » : passation complète ; membre de R4 : Bradley (Antigravity, Gemini) | `ETAT_PROJET.md`, `travail/audits/R3_audit.md`, `travail/journal_prompts.md` | fait |

**Points ouverts du relais** :
- O-9 (B-14 contre R-04) reste à trancher par l'équipe avant le prompt de R4 ; les CA citent l'hypothèse Q-01.
- Relecture humaine mot à mot du cahier des charges par Leddycia : faite, conforme (JP-17).
- Relecture humaine du backlog par Leddycia : faite, aucune correction (JP-17).
- Pour R4 : les CA du Sprint 01 citent cinq fichiers de test à créer (lignes mélangées, colonne manquante, valeur `abc`, mois sans génératrice, août et septembre seuls) ; le dernier n'est pas encore dans `docs/oracle.md` §8.

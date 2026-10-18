# Audit d'entrée : relais R6 (Petiote, Claude [modèle non précisé], 2026-10-18 16:59)

## Livrables audités : `Groupe_01_Cas_01/` et résultats du relais R5

| # | Constat | Preuve (fichier, CA ou règle) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|
| A1 | Passe réduite sur `version_IA.html` : chargement du CSV local, valeurs de toute la période correctes (97 h, 280,0 L, 84 000 gourdes, 06/08/2026 (5 h)) ; puis septembre correct (30 h, 84,0 L, 25 200 gourdes, 08/09/2026 (5 h)). Après chargement, le contexte navigateur a été placé hors ligne ; le changement de période a continué à fonctionner. Fuseau observé : `America/Port-au-Prince`, décalage de 240 minutes le 01/09/2026. | CA-01.01, CA-01.02, CA-01.04, CA-02.01, CA-03.01 ; navigateur local | conforme | laissé |
| A2 | Le tag `version-ia` est présent et `git diff version-ia -- Groupe_01_Cas_01/prototype/version_IA.html` ne produit aucune différence. | RG-08, C-09 | conforme | laissé |
| A3 | 34 fichiers de capture sont présents. L'inventaire comprend une preuve nommée pour chaque CA du Sprint 01 ; CA-03.02 possède une capture par période. La lisibilité de chaque image n'a pas été inspectée individuellement. | C-15, `tests/plan_de_test.md` §3, `Groupe_01_Cas_01/captures/` | conforme | laissé |
| A4 | Les identifiants US/CA du backlog concordent avec le plan de test et le prompt RMTCEV : Sprint 01 = US-01 à US-03 et 20 CA. Les sections 2 à 4 de `prompts.md` restent à compléter. | `product_backlog.md`, `tests/plan_de_test.md` §1 et §3, `prompts.md` | à corriger | compléter dans le cadre de R6 |
| A5 | L'inventaire du dossier livrable ne montre aucun fichier parasite. `README.md` est absent et doit être produit par R6. `index.html` est absent ; R5 documente qu'aucun écart aux CA n'a justifié sa création (C-09). | C-01, C-09, RG-12 ; `ETAT_PROJET.md` §3 | à corriger | créer le README ; expliquer l'absence d'`index.html` |
| O-13a | Le brut commence directement par `<!DOCTYPE html>` et ne contient pas de bloc Markdown ```html ni de texte d'enrobage. Il est impossible d'établir si ces marqueurs ont été retirés lors de la sauvegarde ou absents de la réponse reçue. | `travail/brut/delegation_reponse_brute.md`, prompt de délégation dans `prompts.md` §1.2, DoD `AGENTS.md` §12 | à corriger | laissé ouvert ; Bradley n'a pas répondu |
| O-13b | Le brut décrit une « nouvelle conversation web temporaire » ; `prompts.md` §1.1 décrit une « Nouvelle conversation web ». Le membre R6 indique ne pas avoir reçu de réponse de Bradley sur le mode exact. | `travail/brut/delegation_reponse_brute.md`, `prompts.md` §1.1, D-09 | à corriger | ne pas harmoniser par supposition ; mentionner l'information vérifiable et la confirmation manquante |
| O-14 | R5 signale qu'une ligne vide au milieu du CSV est ignorée sans message et que les heures décimales seraient arrondies à l'entier. Aucun de ces comportements ne viole les CA testés ; aucun correctif ne doit être ajouté hors Sprint 01. | `travail/audits/R5_audit.md`, `travail/journal_ecarts.md`, RG-04, Q-04, Q-16 | conforme (hors CA) | laisser ; signaler comme comportement connu dans le README |

## Ce qui a été seulement survolé ; résultats donnés par le membre

- Les 34 captures ont été vérifiées par leur nom et leur présence, mais pas ouvertes une par une pour juger leur lisibilité.
- Le membre a répondu qu'il n'a pas reçu de réponse de Bradley sur O-13.
- Le membre indique « Leddycia » pour le téléversement Drive ; l'heure du téléversement, le testeur, l'ordinateur et le navigateur restent à obtenir.
- Le membre a indiqué « CLAUDE » sans préciser le modèle. Le modèle exact reste non documenté.
- La passe réduite est celle du navigateur intégré : `version_IA.html` local, puis coupure réseau simulée. Ce n'est pas le test depuis le Drive sur un autre ordinateur exigé par C-14.

## Reprise du relais (Leddycia, Claude Code, Claude Opus 5.5, 2026-10-18 : contrôles à 18:38, reprise inscrite à 18:40)

Reprise du même relais (`agents/00_protocole_relais.md` §2.1 et §3.7) : pas de nouvel audit d'entrée. Contrôles faits en lecture seule sur l'état poussé par Petiote, avant toute écriture ; plan complété validé par Leddycia à 18:40 (JP-31). Les étapes de ce plan sont notées a à g (ETAT §8), pour ne pas les confondre avec les relais.

| # | Constat | Preuve | Gravité | Action |
|---|---|---|---|---|
| K1 | Synchronisation : `git pull` en avance rapide jusqu'à `a3886ae` ; `## main...origin/main`, arbre propre | `git status -sb` | conforme | laissé |
| K2 | Fusion `a3886ae` de la sauvegarde `a88461d` avec les quatre commits distants `b797c0c`, `fef19bd`, `6f59584` et `a72170b`, sans marqueur de conflit ; aucun apport distant perdu : `git diff a72170b HEAD` ne touche que `ETAT_PROJET.md`, `README.md`, `prompts.md` et ce rapport. ETAT §1 attribuait l'ajout d'`index.html` au complément de R4 : il a été ajouté pendant R6, en parallèle, par Leddycia (D-16, `6f59584`) | `git log --graph a3886ae` ; `git diff --stat a72170b HEAD` | conforme (attribution du §1 : à corriger) | laissé ; §1 corrigé (étape e de la reprise) |
| K3 | Message du commit de fusion : « 1 », hors du format conventionnel | `a3886ae`, `AGENTS.md` §11 | à corriger | laissé : l'historique n'est jamais réécrit (`AGENTS.md` §11) |
| K4 | `version_IA.html` intact ; tag `relais-6` absent du dépôt distant | `git diff version-ia` vide ; `git ls-remote --tags origin relais-6` vide | conforme | laissé |
| K5 | Blocs de `travail/transmission_R6_index.md` non intégrés : D-16, E-29 à E-33, JP-28 à JP-30 absents des registres ; ni rectificatif ni §4 dans le plan de test. Numéros encore libres (dernier E-28, dernier JP-27, dernière décision D-15) | `travail/decisions.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `tests/plan_de_test.md` | à corriger | intégrés tels quels (étape b de la reprise) |
| K6 | Le README affirme que le livrable ne contient pas `prototype/index.html`, alors que le fichier y est depuis `6f59584` (D-16) | `Groupe_01_Cas_01/README.md` l. 7 et 66 (version de `a3886ae`) | bloquant (remise) | corrigé (étape c de la reprise) |
| K7 | README : BOM accepté (Q-10, E-28), captures communes à plusieurs CA et Firefox non testé sur `index.html` non mentionnés | ETAT §4 et §6 ; `travail/transmission_R6_index.md`, bloc 6 | à corriger | corrigé (étape c de la reprise) |
| K8 | README : « Éditeur du dépôt : Visual Studio Code » sans source dans le dépôt | `Groupe_01_Cas_01/README.md` l. 19 | à corriger | corrigé : « Antigravity », donné par Leddycia (JP-32) |
| K9 | RG-09 : prénoms de membres dans `prompts.md` (l. 15, note d'audit l. 18, §2 l. 520, 530 et 536) et dans `tests/plan_de_test.md` §3 (l. 73, 79, 81, 86, 88, 105 et 108) | RG-09 | à corriger | corrigé : `tests/plan_de_test.md` §3 à l'étape b (18:43), `prompts.md` à l'étape d (18:48) de la reprise |
| K10 | `prompts.md` §3 ne cite que E-16 ; §4 ne mentionne que `version_IA.html` | `Groupe_01_Cas_01/prompts.md` l. 540 à 553 | à corriger | complété (étape d de la reprise) |
| K11 | `fiche_contribution.pdf` absente de la racine du dépôt | `ls` | à corriger | corrigé (étape f de la reprise, 18:49) |
| K12 | ETAT §6 indique qu'aucune correction de la version de l'IA ne peut être montrée en démonstration ; E-29 et E-30 (corrigés dans `index.html`) le permettent désormais | `ETAT_PROJET.md` §6, étape 5 | à corriger | à la passation (ETAT §6 réécrit) |
| K13 | Audit d'entrée de Petiote : A1 et A3 faits sur `370abc6`, avant les compléments de R5 et de R4 et avant `index.html` ; le dépôt compte 51 captures à `a3886ae` (34 recensées par A3). Captures visées par E-25 ouvertes : données personnelles masquées ou recadrées ; captures `_index` ouvertes par la relecture : aucune donnée personnelle | `git ls-files Groupe_01_Cas_01/captures` ; relecture (étape e) | conforme | laissé : A1 sur `index.html` couvert par la revérification de D-16 (`tests/plan_de_test.md` §4) et par le test depuis le Drive |
| K14 | Textes d'aide propres à `index.html` (« Lecture seule · Fonctionne sans Internet », colonnes attendues, descriptions, rappel de la règle d'égalité) non listés par E-29 à E-31 ; le rappel de la règle d'égalité reste affiché quand la période n'a aucun fonctionnement (capture de CA-03.03) | `Groupe_01_Cas_01/prototype/index.html` l. 641 ; relecture (étape e) | à corriger | README complété (« Ce qui change », « Écarts connus ») ; prototype non modifié : texte fixe, sans effet sur le calcul ni sur les CA ; réponse à préparer pour la soutenance |
| K15 | Trois captures de `version_IA.html` absentes de l'arbre de travail : `US01_CA03_liste_periodes.png`, `US01_CA08_lecture_seule.png`, `US01_CA10_fichier_partiel.png` (suppression à 19:13, faite hors de cette session, non commitée) ; le README (colonne `version_IA.html`) et le plan de test §3 y renvoient | `git status --short` ; date de modification du dossier `captures/` | bloquant (preuves du README) si la suppression est commitée sans mise à jour | remonté à Leddycia : suppression voulue (JP-34) ; README et plan de test §3 mis à jour (E-35) |

## Corrections apportées (une ligne par correction)

- Aucune correction au prototype des relais précédents ; `version_IA.html` reste intact (RG-08).
- Le README absent et les sections finales vides de `prompts.md` sont des livrables R6 à compléter, pas des corrections au prototype.
- Reprise, `travail/journal_prompts.md` (JP-30, transmission de la session parallèle) : champ « Ce que l'humain a vérifié ou corrigé » complété (blocs intégrés à la reprise, JP-31).
- Reprise, `tests/plan_de_test.md` §3 (R5) : prénom du membre de R5 remplacé par son rôle, 7 occurrences (RG-09, K9) ; rectificatif D-16 ajouté sous la ligne « `index.html` : non créé », sans réécrire le tableau de R5.
- Reprise, `Groupe_01_Cas_01/prompts.md` §1.1 (R4) : relecteurs désignés par leur rôle (RG-09, K9) ; note d'audit O-13 de Petiote remplacée par une note de clôture (E-34).
- Reprise, `Groupe_01_Cas_01/prompts.md` §2 (Petiote) : prénoms remplacés par le rôle (RG-09, K9) ; §3 complété par E-29, E-30 et E-32, E-16 conservé ; §4 complété pour `index.html` (K10).
- Reprise, `Groupe_01_Cas_01/README.md` (Petiote) : absence d'`index.html` remplacée par la section « Prototype » (bloc 7, K6) ; tableau des CA fusionné avec le bloc 8 (preuves des deux versions, Test-P04) ; ajouts : captures communes, lecture de CA-02.02, E-24, conditions de test d'`index.html`, Q-10 et BOM (E-28), outils ; éditeur « Antigravity » donné par Leddycia (K7, K8).
- Reprise, relecture indépendante (étape e, 8 vérificateurs en lecture seule) : README (renvoi d'E-29 et E-30 vers `prompts.md` §3, textes d'aide d'`index.html`, Firefox et test depuis le Drive au futur, rappel d'égalité, K14) ; `prompts.md` (note O-13 précisée, §4 « selon la lecture retenue par R5 », E-16 rattaché à l'hypothèse provisoire Q-02 et à B-18) ; E-34 précisé ; ETAT §1 (attribution d'`index.html`, K2), heure de reprise et étapes notées a à g ; ligne de Delly de la fiche de contribution réduite à ce que Leddycia a indiqué (JP-32).
- Reprise, `Groupe_01_Cas_01/README.md` et `tests/plan_de_test.md` §3 : renvois aux trois photos retirées remplacés ou annotés (K15, E-35), sans réécrire les observations de R5.
- Reprise, seconde relecture indépendante (19:36) : README (captures de R5 « sauf trois photos », plan de test désigné « hors livrable »), `prompts.md` §4 (CA-02.02 et CA-02.05 décrits sans les confondre), E-35, JP-31, K9, K13 et ETAT §8 précisés.

## Points remontés à l'équipe (decisions.md, ETAT_PROJET.md)

- O-13 demeure non résolu jusqu'à confirmation de Bradley ; aucune décision n'est ajoutée au registre sur la base d'une supposition.
- Leddycia doit confirmer le téléversement Drive, puis les faits du test depuis le Drive et le remplacement du README ; ils conditionnent le statut REMIS.
- Les heures décimales arrondies et les lignes vides ignorées sont mentionnées comme comportements hors CA (O-14), sans changement de périmètre.
- Reprise : O-13 résolu à 18:44 par la confirmation du membre de R4, transmise par Leddycia (JP-32, E-34) ; seule la présence éventuelle de marques ```html autour du bloc reste non précisée, sans effet sur `version_IA.html`.
- Reprise : trois photos de l'écran de `version_IA.html` retirées du livrable hors de cette session ; suppression voulue, confirmée par Leddycia (K15, JP-34, E-35) : photos prises de biais, peu lisibles et peu professionnelles pour le livrable.

## Ce que j'ai produit pendant mon relais

- À compléter au fil des étapes R6.

## Journal de bord du relais (copie intégrale d'ETAT §8, ajoutée à la passation)

À compléter à la passation avec la copie intégrale d'ETAT §8.

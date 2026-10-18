# Audit d'entrée : relais R5 (Louis, Claude Code [Claude Opus 5.5], 2026-10-18 14:00)

## Livrable audité : `Groupe_01_Cas_01/prototype/version_IA.html`, `travail/brut/`, `Groupe_01_Cas_01/prompts.md`, `tests/` et `docs/oracle.md` §8 (produits par R4)

| # | Constat | Preuve (fichier:ligne, B/C/CA) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|
| A1 | `version_IA.html` brut et tagué : `version-ia` est un tag annoté sur `624003a` ; `git diff version-ia -- Groupe_01_Cas_01/prototype/version_IA.html` est vide | `git cat-file -t version-ia` = `tag` ; C-09, RG-08 | conforme | laissé |
| A2 | Extraction fidèle : le bloc HTML de la réponse brute (`travail/brut/delegation_reponse_brute.md` l. 9 à 1116), copié dans un fichier temporaire hors du dépôt, donne un `git diff --no-index --ignore-cr-at-eol` vide avec `version_IA.html` | C-09 | conforme | laissé |
| A2b | Le prompt exigeait « un seul bloc de code HTML (```html … ```) » ; le fichier brut ne contient ni les balises de ce bloc ni aucun texte autour : impossible de confirmer que la réponse est conservée « complète » (DoD `AGENTS.md` §12) ou si les balises ont été retirées | `prompts.md` §1.2, partie V ; `travail/brut/delegation_reponse_brute.md` l. 1-9 | à signaler | remonté (Bradley, ETAT §5) |
| A3 | Prompt RMTCEV complet : 6 parties (R, M, T, C, E, V), CDC intégral, Sprint 01 avec les 20 CA, outil, modèle, date et heure ; commité avant la délégation (`b170333` à 13:04, envoi à 13:12) | `prompts.md` §1.1, §1.2 ; C-08 | conforme | laissé |
| A3b | Mode de session décrit différemment : « conversation web temporaire » (brut) et « nouvelle conversation web » (`prompts.md` §1.1) | `travail/brut/delegation_reponse_brute.md` l. 6 ; `prompts.md` l. 14 ; D-09 | à corriger | remonté (Bradley confirme, R6 corrige `prompts.md`) |
| A4 | Plan de test et 6 fixtures présents ; fixtures recalculées par script Python : f01 permutation exacte des 36 lignes (ordre différent), f06 = 24 premières lignes (54 h, 155 L), f04 = 8 jours d'août à 0 h, f05 = 0.1 + 0.2 = 0.30000000000000004, f02 sans `litres_carburant`, f03 `abc` en ligne 3 | `tests/fixtures/` ; `docs/oracle.md` §8 | conforme | laissé |
| A4b | `tests/plan_de_test.md` n'a pas de tableau de résultats (observé, statut, capture) demandé par la fiche 05 | `agents/05_verificateur.md` « Tableau de résultats » | à compléter | corrigé par ajout d'un §3 (R5) |
| Env | Poste sous Kali Linux, pas sous Windows ; fuseau système `America/Port-au-Prince` (décalage de 240 min au 01/09/2026, négatif : le piège P-01 se manifesterait) ; empreinte du CSV vérifiée par `sha256sum` : `320155c7…a84b` | `timedatectl` ; Q-09 | écart de procédure | consigné (E-22) |
| Pré-test | `version_IA.html` sous Chromium headless (CDP), fuseau d'Haïti : les 20 CA et Test-P04 donnent exactement les valeurs de l'oracle ; aucune requête réseau ; aucune donnée du CSV dans le source ; aucun champ éditable | `docs/oracle.md` §2, §4, §5, §8 | conforme | passe formelle à l'étape 2 |
| Obs-1 | Une ligne vide au milieu du fichier est ignorée sans message (`version_IA.html` l. 787-792) ; cas non listé par Q-04 | Q-04 | hors CA | remonté (question pour le client) |
| Obs-2 | Les heures sont affichées arrondies à l'entier (`formaterNombre(…, 0)`) : une valeur décimale du fichier (ex. 2.5 h) serait affichée « 3 h » ; Q-16 prévoit « la valeur du fichier » ; aucun cas dans le CSV fourni | `version_IA.html` l. 1059-1060 ; Q-16 | hors CA | remonté (non corrigé, RG-04) |
| Obs-3 | Le BOM UTF-8 est retiré par `FileReader.readAsText` : le nom de la première colonne n'est pas altéré et le fichier est accepté, ce qui reste cohérent avec la formulation de Q-10 | Q-10 | conforme | laissé |

## Ce qui a été seulement survolé ; résultats donnés par le membre

- Les sections 2 à 4 de `prompts.md`, encore vides (à compléter par R5 et R6).
- Les métadonnées Git : l'auteur des commits et du tag de R4 utilise une adresse e-mail personnelle, et non l'adresse noreply recommandée (D-12, O-8). Risque déjà assumé ; l'historique n'est pas réécrit.

## Corrections apportées (une ligne par correction)

- `tests/plan_de_test.md` (livrable de R4) : ajout d'un §3 « Résultats d'exécution (R5) » (tableau par CA et contrôles transverses, demandé par la fiche 05) ; les §1 et §2 ne sont pas modifiés (RG-10).
- Aucune correction de `version_IA.html` (RG-08) et aucun `index.html` : aucun écart constaté sur les CA du Sprint 01 (C-09).

## Points remontés à l'équipe (decisions.md, ETAT_PROJET.md)

- A2b : complétude de la réponse brute (bloc ```html ou texte autour non conservés ?) : à confirmer par Bradley (ETAT §5, O-13).
- A3b : mode de session « temporaire » ou « nouvelle conversation » : Bradley confirme, R6 harmonise `prompts.md` §1.1 (ETAT §5, O-13).
- Obs-1 et Obs-2 (ligne vide au milieu du fichier ignorée ; heures décimales arrondies à l'affichage) : comportements hors des CA du Sprint 01, non corrigés (RG-04), à proposer au client avec Q-04 et Q-16 (ETAT §5, O-14).
- Pas de nouvelle décision ni de Q-xx dans `travail/decisions.md`.

## Ce que j'ai produit pendant mon relais

- Vérification complète de `version_IA.html` : 20 CA du Sprint 01 et Test-P04 respectés, sous le fuseau d'Haïti, dans Chromium (script CDP) et dans Firefox (Louis, réseau coupé) ; contrôles transverses conformes ; empreinte du CSV identique avant et après (`tests/plan_de_test.md` §3).
- 34 captures dans `Groupe_01_Cas_01/captures/` (29 automatiques, dont 3 montages « fuseau » ; 5 manuelles de Louis, dont 3 photos de l'écran).
- E-22 (environnement de test) ; JP-20 à JP-23.
- `index.html` non créé (C-09).

## Journal de bord du relais (copie intégrale d'ETAT §8, ajoutée à la passation)

## 8. Relais en cours (journal de bord, tenu par l'IA)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

| Relais | Membre | Outil et modèle | Fiche | Porte visée | Début |
|---|---|---|---|---|---|
| R5 | Louis | Claude Code (Claude Opus 5.5) | `agents/05_verificateur.md`, puis `agents/04_developpeur.md` | G5 | 14:00 |

**Plan validé** : 1. Démarrage (ETAT §1, §2, §8 ; `travail/audits/R5_audit.md`). 2. Passe formelle de `version_IA.html` sur les 20 CA et Test-P04 (Chromium headless piloté par CDP, fuseau America/Port-au-Prince ; Firefox pour le libellé du bouton et une période), résultats ajoutés en §3 de `tests/plan_de_test.md`. 3. Journal des écarts : E-22 (environnement Linux au lieu de Windows) ; A2b et A3b remontés en ETAT §5. 4. `index.html` seulement si un écart est constaté, sinon justification C-09. 5. Captures : automatiques (CDP) pour les CA à valeurs ; manuelles par Louis pour CA-01.03, CA-01.10 (liste ouverte), CA-01.01 hors ligne, fuseau (`timedatectl`), CA-01.08 (empreinte). 6. Contrôles transverses (hors ligne en fin de passe, empreinte du CSV, hors sprint). 7. Passation (« fin de notre relais »).

**Audit d'entrée (synthèse)** : A1 `version_IA.html` intact et tagué (`git diff version-ia` vide) | conforme ; A2 extraction fidèle (`git diff --no-index --ignore-cr-at-eol` vide) | conforme ; A2b le brut ne contient ni bloc ```html ni texte autour, alors que le prompt l'exigeait : complétude de la réponse brute à confirmer par Bradley | à signaler ; A3 prompt RMTCEV complet, commité avant l'envoi (`b170333` 13:04, envoi 13:12) | conforme ; A3b mode de session incohérent (« temporaire » dans le brut l.6, « nouvelle conversation » dans `prompts.md` §1.1) | à corriger (Bradley confirme, R6 corrige) ; A4 plan de test et 6 fixtures conformes à l'oracle §8 (recalcul Python) | conforme ; A4b pas de tableau de résultats dans le plan de test | à compléter (R5) ; environnement : Kali Linux, fuseau système America/Port-au-Prince (décalage 240 min), CSV `320155c7…a84b` vérifié | écart de procédure (E-22). Pré-test Chromium : les 20 CA et Test-P04 conformes à l'oracle, aucune requête réseau. Survolé : US hors sprint. Résultats du membre : aucun pour l'instant (détail : `travail/audits/R5_audit.md`).

**Journal de bord**

| Heure | Étape | Ce qui a été fait | Fichiers | État |
|---|---|---|---|---|
| 14:04 | étape 1 | R5 marqué EN COURS ; rapport d'audit créé ; JP-20 et JP-21 | `ETAT_PROJET.md`, `travail/audits/R5_audit.md`, `travail/journal_prompts.md` | fait |
| 14:06 | étape 2 | Passe formelle de `version_IA.html` (Chromium headless, fuseau d'Haïti) : 20 CA et Test-P04 conformes à l'oracle ; 0 requête réseau ; résultats ajoutés en §3 du plan de test ; Firefox et vues manuelles en attente (Louis) | `tests/plan_de_test.md` | partiel |
| 14:07 | étape 3 | E-22 (environnement Linux au lieu de Windows, accepté tel quel) ; aucun écart sur `version_IA.html` | `travail/journal_ecarts.md` | fait |
| 14:07 | étape 4 | `index.html` non créé : aucun écart sur les CA du Sprint 01 (C-09) | aucun | fait |
| 14:07 | étape 5 | 29 captures automatiques copiées (noms du plan de test ; CA-03.02 en 4 fichiers par période ; fuseau en montages des 3 mois) ; 4 captures manuelles en attente (CA-01.01, CA-01.03, CA-01.08, CA-01.10) | `Groupe_01_Cas_01/captures/` | partiel |
| 14:07 | étape 6 | Hors ligne émulé, aucune ressource externe, aucune donnée intégrée, lecture seule (empreinte identique après les tests), hors sprint, rechargement P-09 : conformes ; coupure réelle en attente | `tests/plan_de_test.md` | partiel |
| 14:14 | étape 5 | CA-01.01 vu par Louis dans Firefox, réseau coupé : respecté ; capture enregistrée ; libellé du bouton conforme dans Firefox | `Groupe_01_Cas_01/captures/US01_CA01_etat_initial.png`, `tests/plan_de_test.md` | fait |
| 14:16 | étape 5 | Firefox, hors ligne, `energie_college.csv` chargé : Toute la période = 97 h, 280,0 L, 84 000 gourdes, 06/08/2026 (5 h), conforme (second navigateur) ; capture enregistrée | `Groupe_01_Cas_01/captures/US01_CA02_firefox_toute_periode.png` | fait |
| 14:18 | étape 5 | CA-01.03 vu par Louis (Firefox, hors ligne) : liste ouverte avec exactement 4 choix, respecté ; photo de l'écran enregistrée | `Groupe_01_Cas_01/captures/US01_CA03_liste_periodes.png`, `tests/plan_de_test.md` | fait |
| 14:20 | étape 5 | CA-01.10 vu par Louis (Firefox, hors ligne, f06) : 3 choix sans Octobre, 54 h, 155,0 L, respecté ; photo enregistrée | `Groupe_01_Cas_01/captures/US01_CA10_fichier_partiel.png`, `tests/plan_de_test.md` | fait |
| 14:31 | étapes 5 et 6 | CA-01.08 vu par Louis : empreinte identique après les essais, aucun champ de saisie, respecté ; photo redressée et enregistrée ; hors ligne réel conforme. Les 20 CA et Test-P04 sont respectés ; 34 captures | `Groupe_01_Cas_01/captures/US01_CA08_lecture_seule.png`, `tests/plan_de_test.md` | fait |
| 14:35 | étape 7 | « fin de notre relais » (JP-23) : passation ; bilan : étapes 1 à 6 faites ; la capture « fuseau » prévue avec `timedatectl` est remplacée par les montages des 3 mois, où le fuseau est lu dans le navigateur (E-22) ; JP-22 et JP-23 ; R6 = Petiote | `ETAT_PROJET.md`, `travail/audits/R5_audit.md`, `travail/journal_prompts.md` | fait |

**Points ouverts du relais** : A2b et A3b à faire confirmer par Bradley (R4).

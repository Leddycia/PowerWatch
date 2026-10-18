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

## Complément (2026-10-18 15:04 → 15:53)

Complément fait par Leddycia avec Claude Code (application de bureau, Claude Opus 5.5), après le tag `relais-5` et avant le démarrage de R6 (JP-24). Contrôle préalable : dépôt distant inchangé depuis 370abc6, pas de tag `relais-6` ; Leddycia confirme que R6 n'a pas encore fait de `git pull`.

### Audit (relecture du dépôt après le push de R5)

| # | Constat | Preuve (fichier:ligne, B/C/CA) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|
| C1 | Tag `relais-5` annoté et poussé ; `version_IA.html` identique à `version-ia` ; originaux de `docs/` inchangés ; CSV `320155c7…a84b` | `git ls-remote --tags origin` ; `git diff version-ia` vide ; C-09, RG-08 | conforme | laissé |
| C2 | Q-01 porte le statut « provisoire (confirmé) », absent de la légende du registre ; « confirmé » laisse croire que le client a répondu ; ETAT O-9 et l'entrée R4 du §7 écrivent « Q-01 confirmé » | `travail/decisions.md` l. 52 et 105 ; ETAT §5 (O-9), §7 (R4) ; RG-02, `AGENTS.md` §4 | à corriger | voir « Corrections apportées » |
| C3 | f01 ne déplace que 5 lignes d'août : les 11 jours à 5 h restent dans l'ordre chronologique (06/08 avant 12/08, 08/09 avant 09/09 et 11/09, 02/10 avant les 5 autres). Un prototype qui se fierait à l'ordre du fichier réussirait CA-03.02. L'audit d'entrée de R5 (A4) l'a jugé conforme | `tests/fixtures/f01_lignes_melangees.csv` ; CA-03.02 ; B-13, P-03 | à corriger | voir « Corrections apportées » |
| C4 | 4 captures manuelles montrent le chemin personnel `/home/<utilisateur>`, l'invite du terminal (utilisateur et nom du poste) et des favoris du navigateur sans rapport avec le projet ; ces fichiers font partie du livrable remis | `captures/US01_CA01_etat_initial.png`, `US01_CA02_firefox_toute_periode.png`, `US01_CA03_liste_periodes.png`, `US01_CA08_lecture_seule.png` ; RG-09, C-01 | à corriger | voir « Corrections apportées » |
| C5 | Dans `prompts.md`, le bloc du prompt s'ouvre l. 20 avec trois accents graves : la ligne 384 le ferme trop tôt et la ligne 510 ouvre un bloc jamais fermé ; à l'affichage, la fin du prompt sort du bloc et les sections 2 à 4 apparaissent comme du code | `Groupe_01_Cas_01/prompts.md` l. 20, 384, 510 | à corriger | voir « Corrections apportées » |
| C6 | Captures identiques octet pour octet : un même écran sert de preuve à plusieurs CA (par exemple 7 fichiers pour « Toute la période », dont CA-01.09) | `Groupe_01_Cas_01/captures/` | conforme (à expliquer dans le README) | remonté (R6) |
| C7 | CA-02.02 : le prix de 300 gourdes par litre est affiché dans le bloc de chargement, pas dans la carte du coût ; R5 l'a jugé respecté (même écran) | `version_IA.html` l. 540-543, 594-604 ; CA-02.02 | conforme (lecture à assumer) | remonté (R6, README et soutenance) |
| C8 | Commit et tag de R5 signés d'une autre identité Git que celle de Louis, avec une adresse locale, alors que le membre de R5 est Louis | `git log -1 370abc6` ; `git cat-file -p relais-5` | non corrigeable (historique jamais réécrit, `AGENTS.md` §11) | remonté (R6, fiche de contribution) |
| C9 | O-13 (mode de session, complétude de la réponse brute) attend la réponse de Bradley | ETAT §5 | ouvert | laissé (R6) |

### Corrections apportées (une ligne par correction)

- C2 : `travail/decisions.md`, Q-01 « provisoire (confirmé) » → « provisoire » (hypothèse inchangée ; justification reformulée, « tranche le point O-9 » retiré), ligne ajoutée au journal des changements ; ETAT §5, O-9 reformulé (E-23).
- C3 : `tests/fixtures/f01_lignes_melangees.csv` refait (jours à égalité dans un ordre non chronologique) ; `docs/oracle.md` §8, ligne f01 (E-24).
- C3 : `Groupe_01_Cas_01/captures/US03_CA02_lignes_melangees_{aout,septembre,octobre,toute_periode}.png` refaites avec le nouveau f01 ; `tests/plan_de_test.md` §3, ligne CA-03.02 complétée (E-24).
- C4 : `Groupe_01_Cas_01/captures/US01_CA01_etat_initial.png`, `US01_CA02_firefox_toute_periode.png`, `US01_CA03_liste_periodes.png`, `US01_CA08_lecture_seule.png` : données personnelles masquées ou recadrées (E-25).
- C5 : `Groupe_01_Cas_01/prompts.md`, l. 20 et 510 : bloc du prompt clôturé par quatre accents graves ; texte du prompt inchangé (identique à `b170333`) (E-26).

### Points remontés à l'équipe (complément)

- C6 et C7 (captures identiques pour plusieurs CA ; lecture de CA-02.02) : à expliquer par R6 dans le README.
- C8 (identité Git de R5) : R6 attribue R5 à Louis dans la fiche de contribution.
- E-25 : les versions non masquées des 4 captures restent dans l'historique Git public (commit 370abc6), qui n'est jamais réécrit ; seule la remise sur le Drive est garantie propre.
- O-13 : inchangé (Bradley, puis R6).
- Relevé par la relecture indépendante, antérieur au complément (RG-09) : `Groupe_01_Cas_01/prompts.md` l. 15 nomme deux membres (livrable) et `tests/plan_de_test.md` §3 nomme le membre de R5 sept fois ; RG-09 ne permet les noms que dans ETAT, PLAN_CADRAGE, `travail/`, le README et la fiche de contribution. À R6 : remplacer les prénoms par les rôles (membre de R3, membre de R4 ; membre de R5 dans `tests/plan_de_test.md` §3), RG-09 étant une règle d'or non négociable.

### Ce que j'ai produit pendant le complément

- `travail/decisions.md` : Q-01 remise à « provisoire » et ligne au journal des changements (E-23).
- `tests/fixtures/f01_lignes_melangees.csv` v2 et `docs/oracle.md` §8 (E-24).
- 4 captures de CA-03.02 refaites (Windows 11, Chrome 155 sans interface, fuseau d'Haïti et coupure réseau émulés) et ligne CA-03.02 de `tests/plan_de_test.md` §3.
- 4 captures manuelles masquées ou recadrées (E-25) ; originaux gardés hors du dépôt.
- `Groupe_01_Cas_01/prompts.md` : affichage des blocs réparé, texte du prompt inchangé (E-26).
- JP-24, JP-25 ; E-23 à E-26 ; cette section.
- Relecture indépendante avant le commit : 5 vérificateurs en lecture seule (protocole, traçabilité, technique, confidentialité, intégrité) ; aucun point bloquant ; 2 points « à corriger » et 7 mineurs, tous traités avant le commit (environnement des captures de CA-03.02 précisé, E-26 ajoutée, auteur des vérifications précisé dans E-23 à E-26, formulation de l'oracle §8 sur `>=` précisée, « onglet » rectifié dans E-25, renvoi de JP-24 corrigé, note du §8 ajoutée à la copie ci-dessous, adresse noreply pour le commit, noms RG-09 remontés à R6). Seconde relecture (3 vérificateurs en lecture seule) sur l'état corrigé : aucun point bloquant ; 8 points traités (heure de fin, adresse noreply à passer au commit, portée du constat sur la livraison de R5, citation de B-13 et RM-02 dans E-24, « GitHub ou tout lecteur Markdown » dans E-26, justification de Q-01 reformulée signalée, phrase de détection d'E-24, option contraire à RG-09 retirée). Troisième relecture (2 vérificateurs en lecture seule) : corrections du tour 2 confirmées ; 1 point à corriger et 7 mineurs, traités (portée du constat d'ETAT §7 ramenée à C1, C3 et C4 ; relectures décrites de la même façon dans ETAT §3 ; « trois variantes fautives » dans l'oracle §8 ; RG-09 ajouté au reste à faire d'ETAT §4 ; heures de JP-24 et JP-25 et de la confirmation de Leddycia rectifiées ; référence d'E-26 ; gravité d'E-25 sans « remis »).

### Journal de bord du complément (copie intégrale d'ETAT §8, ajoutée à la clôture)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

| Relais | Membre | Outil et modèle | Fiche | Porte visée | Début |
|---|---|---|---|---|---|
| R5 (complément, après le tag `relais-5`) | Leddycia | Claude Code (application de bureau, Claude Opus 5.5) | `agents/05_verificateur.md`, `agents/00_protocole_relais.md` | G5 (corrections avant R6) | 15:04 |

**Plan validé** (demande de Leddycia, JP-24 ; uniquement si R6 n'a pas encore fait de `git pull` : confirmé par Leddycia à 15:04 ; dépôt distant inchangé depuis 370abc6, pas de tag `relais-6`) : 1. Ouvrir le complément (ETAT §1, §2, §8 ; section « Complément » de `travail/audits/R5_audit.md`). 2. Q-01 : retirer le statut « provisoire (confirmé) », qui n'existe pas et laisse croire à une réponse du client. 3. f01 : placer les jours à égalité dans un ordre non chronologique, puis mettre à jour `docs/oracle.md` §8. 4. Refaire les 4 captures de CA-03.02 avec le nouveau f01. 5. Masquer les données personnelles (chemin, nom d'utilisateur, nom du poste, favoris) des 4 captures manuelles. 6. `prompts.md` : réparer l'affichage des blocs de code, sans toucher au texte du prompt. 7. Journaux, contrôle final, puis passation du complément sur demande. Chaque étape est contrôlée trois fois (relecture du diff, contrôle par script, relecture indépendante ou visuelle).

**Audit d'entrée (synthèse)** : Q-01 « provisoire (confirmé) » (`travail/decisions.md` l. 52 et 105, ETAT §5 O-9, §7 R4) | à corriger (RG-02, `AGENTS.md` §4) ; f01 garde les 11 jours à 5 h dans l'ordre chronologique : CA-03.02 n'est pas prouvé par ce fichier (un prototype qui se fierait à l'ordre du fichier le réussirait) | à corriger ; 4 captures manuelles (CA-01.01, CA-01.02 Firefox, CA-01.03, CA-01.08) montrent le chemin personnel, le nom d'utilisateur et du poste et des favoris sans rapport avec le projet | à corriger (RG-09) ; `prompts.md` l. 384 et 510 : blocs de code mal fermés, les sections 2 à 4 s'affichent comme du code | à corriger ; non corrigeables ici : mode de session et complétude de la réponse brute (O-13, réponse de Bradley attendue), identité Git des commits de R5 (historique jamais réécrit). Détail : `travail/audits/R5_audit.md`, section « Complément ».

**Journal de bord**

| Heure | Étape | Ce qui a été fait | Fichiers | État |
|---|---|---|---|---|
| 15:04 | étape 1 | Complément ouvert : R5 « complément EN COURS » ; contrôle préalable (dépôt distant inchangé, pas de `relais-6`, Leddycia confirme que R6 n'a pas fait de `git pull`) | `ETAT_PROJET.md` | fait |
| 15:08 | étape 2 | Q-01 remise à « provisoire » (hypothèse inchangée, gardée par l'équipe pour le Sprint 01) ; ligne au journal des changements ; O-9 reformulé (E-23). Contrôles : diff relu, statuts du tableau Q relus par script (aucun « confirmé »), recherche dans tout le dépôt (restent seulement des traces historiques : ETAT §7 R4, `R4_audit.md`, JP-18) | `travail/decisions.md`, `ETAT_PROJET.md` | fait |
| 15:10 | étape 3 | f01 refait (mélange par script à graine fixe) : les jours à 5 h sont dans l'ordre 16/10, 02/10, 12/08, 13/10, 11/09, 05/10, 08/10, 06/08, 08/09, 15/10, 09/09 ; ligne f01 de l'oracle §8 mise à jour (E-24). Contrôles : 727 octets, 37 CRLF, sans BOM, mêmes 36 lignes et même en-tête que le CSV ; simulation des deux règles fautives (l'ancien f01 ne détectait que `>=`, le nouveau détecte aussi l'ordre du fichier) ; pré-contrôle de `version_IA.html` : valeurs de l'oracle | `tests/fixtures/f01_lignes_melangees.csv`, `docs/oracle.md` | fait |
| 15:11 | étape 4 | 4 captures de CA-03.02 refaites avec le nouveau f01 (Chrome 155 sans interface, protocole DevTools, vrai `<input type="file">`, fuseau `America/Port-au-Prince`, réseau coupé, 0 requête réseau), même format que celles de R5 (1200 × 1166) ; ligne CA-03.02 du plan de test (§3) complétée. Contrôles : valeurs lues dans la page = oracle ; 4 images relues (nom du fichier f01, période, jour max lisibles) ; copies identiques aux fichiers produits ; `version_IA.html` toujours identique à `version-ia` | `Groupe_01_Cas_01/captures/US03_CA02_*.png`, `tests/plan_de_test.md` | fait |
| 15:13 | étape 5 | Données personnelles masquées (E-25) : CA-01.01, barre des favoris remplie de sa couleur de fond et « home/<utilisateur> » masqué en gris dans l'adresse (`file:///…/Desktop/…/version_IA.html` reste lisible) ; CA-01.02 (Firefox) et CA-01.03, bandeau du haut recadré (18 et 50 px) ; CA-01.08, 10 masques gris (adresse, titre et invites du terminal, onglet, chemin du résultat de `sha256sum`), l'empreinte `320155c7…a84b` reste lisible. Contrôles : images relues en entier et agrandies ; script (recadrages exacts, aucun pixel modifié hors des masques prévus) ; copies identiques ; aucune métadonnée dans les 34 PNG. Originaux gardés hors du dépôt | `Groupe_01_Cas_01/captures/US01_CA01_etat_initial.png`, `US01_CA02_firefox_toute_periode.png`, `US01_CA03_liste_periodes.png`, `US01_CA08_lecture_seule.png` | fait |
| 15:15 | étape 6 | `prompts.md` : bloc du prompt ouvert et fermé par quatre accents graves (l. 20 et 510), pour que les trois accents graves internes (l. 75, 384, 390…) ne le ferment plus. Contrôles : diff (2 lignes, un accent grave ajouté à chacune) ; texte du prompt (l. 21 à 509) identique octet pour octet à celui commité avant l'envoi (`b170333`) ; analyse des blocs selon les règles CommonMark : avant, 5 blocs dont un jamais fermé et les sections 2 à 4 dans du code ; après, un seul bloc (l. 20 à 510) et les sections 2 à 4 affichées | `Groupe_01_Cas_01/prompts.md` | fait |
| 15:16 | étape 7 | JP-24 ; E-23 à E-25 ; « Corrections apportées » et « Points remontés » du complément dans `R5_audit.md`. Contrôle final : 17 fichiers modifiés, tous prévus par le plan ; aucun fichier interdit (contrôle du bloc A : OK) ; `version_IA.html` identique à `version-ia` ; originaux de `docs/`, `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` et fiches inchangés ; CSV `320155c7…a84b` ; aucun fichier non suivi ; 34 captures, rien d'autre dans `Groupe_01_Cas_01/` ; dépôt distant toujours sur 370abc6 ; seules les lignes prévues sont retirées. Passation du complément en attente de la demande de Leddycia | `travail/journal_prompts.md`, `travail/journal_ecarts.md`, `travail/audits/R5_audit.md` | fait |
| 15:17 | étape 7 | « fin de notre relais » (JP-25) : clôture du complément ; bilan : étapes 1 à 7 faites, aucune partielle ; relecture indépendante avant le commit ; commit et push sans tag | `ETAT_PROJET.md`, `travail/audits/R5_audit.md`, `travail/journal_prompts.md` | fait |

**Points ouverts du relais** : O-13 reste à Bradley et R6.

**Rectificatifs après la copie** (relectures indépendantes avant le commit ; la copie ci-dessus n'est pas modifiée) : 15:04 est l'heure du contrôle préalable ; la demande de Leddycia (JP-24) date de 15:03 et sa confirmation (pas de `git pull` de R6, complément à son nom) de 15:07 ; « fin de notre relais » (JP-25) date de 15:16 ; les relectures indépendantes et leurs corrections ont eu lieu de 15:18 à 15:53, avant le commit ; à 15:11, la coupure réseau et le fuseau du navigateur sont émulés, sur un poste Windows 11 (fuseau système « Haiti Standard Time »), et non sur le poste Linux de R5 ; à 15:13, « onglet » désigne en fait un fragment de la barre des favoris, et l'onglet « about:sessionrestore » (page interne du navigateur, sans donnée personnelle) est conservé ; la correction de 15:15 est consignée en E-26.

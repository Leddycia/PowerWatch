# Audit d'entrée : relais R4 (Bradley, Antigravity [Gemini 3.8 Flash High], 2026-10-18 12:47)

## Livrable audité : `Groupe_01_Cas_01/product_backlog.md` (produit par R3)

| # | Constat | Preuve (fichier:ligne, B/C/CA) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|
| A1 | 8 US au format exact (« En tant que… je veux… afin de… »), avec leurs sources complètes (B-xx, C-xx, EF/ENF/RM, CT-xx). | `product_backlog.md`: l. 39 (US-01), l. 60 (US-02), l. 75 (US-03), l. 89 (US-04), l. 104 (US-05), l. 117 (US-06), l. 129 (US-07), l. 141 (US-08) | conforme | laissé |
| A2 | Le Sprint 01 contient exactement US-01 à US-03 ; le chargement fait partie intégrante de l'US-01. | `product_backlog.md`: l. 21-28, 37-56 (C-07, D-01) ; US-04 en 4e priorité (D-07), US-05 à US-08 en souhaits ultérieurs classés (D-08). | conforme | laissé |
| A3 | Les 20 CA du Sprint 01 sont chiffrés et strictement conformes à l'oracle (`docs/oracle.md` §2, §4, §5) : totaux d'heures et de litres, coûts en gourdes sans décimale, jours max chronologiques à égalité (06/08, 08/09, 02/10 à 5 h), total partiel cumulé (54 h / 155,0 L pour août+septembre), et exclusions des artefacts de fuseau UTC-05. | `product_backlog.md`: l. 46-56 (CA-01.01 à CA-01.11), l. 67-71 (CA-02.01 à CA-02.05), l. 82-85 (CA-03.01 à CA-03.04) | conforme | laissé |
| A4 | Les CA sont vérifiables par un tiers, formulés en « Étant donné… quand… alors… » purement comportementaux et observables à l'écran, sans dicter d'implémentation technique. | `product_backlog.md`: ensemble des CA du Sprint 01 | conforme | laissé |
| A5 | Les critères d'acceptation couvrant les cas particuliers critiques existent : fuseau d'Haïti (CA-01.05, CA-02.04, CA-03.04), fichier mélangé (CA-03.02), mode hors ligne sans réseau (CA-01.01), empreinte SHA-256 du CSV (CA-01.08), rejet de fichier invalide (CA-01.07, CA-01.11). | `product_backlog.md`: CA cités | conforme | laissé |

## Ce qui a été seulement survolé ; résultats donnés par le membre

- Les US hors Sprint 01 (US-04 à US-08) ont été auditées quant à leur structure, leur format et leurs sources ; leurs critères ne fixant ni formule ni seuil (Q-11, Q-12, Q-13) ont été confirmés conformes à C-05.
- Contrôle d'intégrité SHA-256 du CSV `docs/energie_college.csv` exécuté dans PowerShell : hash identique `320155c76969aeb0e05779861b2520a150675f853318d2dfd6592eaf0107a84b` (`True`).
- Contrôle de lecture intégrale des 33,4 ko du CDC et 24,7 ko du backlog validé (dernière ligne du §12.3 du CDC et dernier point DoD du §5 du backlog).

## Corrections apportées (une ligne par correction)

- Aucune correction nécessaire sur le livrable `Groupe_01_Cas_01/product_backlog.md` (entièrement conforme).

## Points remontés à l'équipe (decisions.md, ETAT_PROJET.md)

- **D-10 tranché** : le prompt RMTCEV fournit toutes les règles et valeurs attendues de l'oracle, sans souffler les solutions d'implémentation des pièges techniques.
- **O-9 tranché** : confirmation de l'hypothèse Q-01 pour le format des litres (toujours 1 décimale avec virgule française, ex. « 71,0 L »).
- **Q-10 précisé** : rejet propre selon Q-04 si un fichier CSV présente un BOM UTF-8 altérant l'en-tête de colonne.

## Ce que j'ai produit pendant mon relais

- `Groupe_01_Cas_01/prompts.md` : livrable officiel contenant le prompt de délégation du Sprint 01 au format RMTCEV complet (incluant le cahier des charges intégral et la spécification complète du Sprint 01 avec ses 20 CA), relu par Leddycia (R3) et commité avant délégation (`b170333`, C-08).
- `travail/brut/delegation_reponse_brute.md` : sauvegarde intégrale et transparente de la réponse brute fournie par l'IA déléguée ChatGPT (GPT-4o) en session vierge (D-09).
- `Groupe_01_Cas_01/prototype/version_IA.html` : extraction brute 100% fidèle (`git diff --no-index` vide) du prototype HTML autonome, commité avec le tag annoté `version-ia` (commit `624003a`, C-09, RG-08).
- `tests/fixtures/` : création des 6 fixtures de test (`f01_lignes_melangees.csv`, `f02_colonne_manquante.csv`, `f03_valeur_non_numerique.csv`, `f04_mois_sans_generatrice.csv`, `f05_decimales.csv`, `f06_aout_septembre.csv`).
- `docs/oracle.md` §8 : complétion des résultats attendus déterministes pour chaque fixture de test.
- `tests/plan_de_test.md` : plan de test exhaustif couvrant les 20 CA du Sprint 01 et le test d'arrondi flottant, avec procédure pas à pas, fixtures associées et nommage exact des captures attendues.
- Arbitrages D-10 (validé), Q-01 (confirmé, résout O-9), Q-10 (précisé, BOM UTF-8) enregistrés dans `travail/decisions.md`.

## Journal de bord du relais (copie intégrale d'ETAT §8, ajoutée à la passation)

| Relais | Membre | Outil et modèle | Fiche | Porte visée | Début |
|---|---|---|---|---|---|
| R4 | Bradley | Antigravity (Gemini 3.8 Flash High) | `agents/03_prompt_engineer.md` | G4 | 12:47 |

**Plan validé** : 1. Initialisation d'ETAT §1/§2/§8, audit d'entrée et arbitrage D-10, Q-01, Q-10 ; 2. Rédaction du prompt RMTCEV intégrant CDC et Sprint 01 avec tous les CA, commit dans prompts.md §1 ; 3. Relecture du prompt par Leddycia (R3) ; 4. Délégation en session vierge (D-09) et sauvegarde brute ; 5. Extraction brute de version_IA.html, contrôle git diff --no-index vide, commit, tag annoté version-ia et push ; 6. Complétion de prompts.md v1 ; 7. Plan de test, fixtures f01 à f06 et mise à jour oracle.md §8 ; 8. Passation à « fin de notre relais » (relais-4).

**Audit d'entrée (synthèse)** : A1 conforme (8 US au format exact, sources B-xx/C-xx) ; A2 conforme (Sprint 01 = US-01 à US-03, chargement en US-01) ; A3 conforme (20 CA du Sprint 01 chiffrés avec oracle §2, §4 et §5, égalités et fuseau horaire) ; A4 conforme (CA vérifiables sans solution technique) ; A5 conforme (fuseau Haïti, fichier mélangé, mode hors ligne et hash SHA-256 présents). Détail : `travail/audits/R4_audit.md`.

**Journal de bord**

| Heure | Étape | Ce qui a été fait | Fichiers | État |
|---|---|---|---|---|
| 12:47 | - | Audit d'entrée A1-A5 et validation du plan avec Bradley (JP-18) | `agents/03_prompt_engineer.md`, `ETAT_PROJET.md` | fait |
| 12:51 | étape 1 | Initialisation d'ETAT §1/§2/§8, création du rapport d'audit R4, arbitrages D-10, Q-01 (O-9) et Q-10 | `ETAT_PROJET.md`, `travail/audits/R4_audit.md`, `travail/decisions.md` | fait |
| 12:59 | étape 2 | Rédaction du prompt RMTCEV (R, M, T, C avec CDC et Sprint 01 intégraux, E avec oracle, V) et assemblage du livrable | `Groupe_01_Cas_01/prompts.md` | fait |
| 13:03 | étape 3 | Relecture croisée du prompt RMTCEV validée avec Leddycia (R3) et Bradley (JP-19) | `Groupe_01_Cas_01/prompts.md`, `ETAT_PROJET.md` | fait |
| 13:17 | étape 4 | Délégation en session vierge ChatGPT (GPT-4o), sauvegarde brute complète (D-09) | `travail/brut/delegation_reponse_brute.md` | fait |
| 13:20 | étape 5 | Extraction brute de `version_IA.html`, contrôle `git diff --no-index` vide (conformité 100%) | `Groupe_01_Cas_01/prototype/version_IA.html` | fait |
| 13:21 | étape 6 | Commit et push de `version_IA.html`, `prompts.md` v1 et `travail/brut/` avec tag annoté `version-ia` (commit 624003a) | `Groupe_01_Cas_01/prototype/version_IA.html`, `Groupe_01_Cas_01/prompts.md` | fait |
| 13:24 | étape 7 | Création du plan de test complet (20 CA + Test-P04), des 6 fixtures de test (f01 à f06) et complétion d'oracle.md §8 | `tests/plan_de_test.md`, `tests/fixtures/*`, `docs/oracle.md` | fait |
| 13:42 | étape 8 | Clôture du relais R4, mise à jour des documents et passation complète vers R5 (relais-4) | `ETAT_PROJET.md`, `travail/audits/R4_audit.md` | fait |

**Points ouverts du relais** : D-10 validé (règles et oracle sans solutions d'implémentation) ; O-9 résolu (Q-01 confirmé, litres à 1 décimale systématique) ; Q-10 précisé (BOM traité comme rejet Q-04).

## Complément (2026-10-18 15:59 → 16:31)

Complément fait par Leddycia avec Claude Code (application de bureau, Claude Opus 5.5), après le complément de R5 et avant le démarrage de R6 (JP-26). Les points corrigés ici sont les points restants relevés sur le travail de R4 lors de la relecture du dépôt que Leddycia a demandée dans la session de son IA après le push de R4 (texte exact : « R4 done », 13:50 ; non consigné en JP à ce moment), puis rappelés à sa question « Les corrections de R4 ont ete faits? » (15:55). Les autres points de cette relecture (Q-01, f01), relevés aussi après le push de R5 (C2 et C3 de `travail/audits/R5_audit.md`), et les blocs de `prompts.md` ont été corrigés au complément de R5 (E-23, E-24, E-26).

### Audit (points restants sur le travail de R4)

| # | Constat | Preuve (fichier:ligne, B/C/CA) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|
| K0 | Contrôle préalable : tag `relais-4` sur le dépôt distant (commit ffee9e6) ; `version_IA.html` identique au tag `version-ia` ; originaux de `docs/` inchangés, CSV `320155c7…a84b` ; dépôt distant sur b797c0c, pas de tag `relais-6` | `git ls-remote --tags origin` ; `git diff version-ia` vide ; `Get-FileHash` | conforme | laissé |
| K1 | La précision de Q-10 est résumée par « BOM traité en rejet Q-04 » (ETAT O-10) et par « BOM UTF-8 traité en rejet Q-04 sans planter » (journal des changements du registre) ; or la formulation de Q-10 dans le registre ne rejette un BOM UTF-8 que s'il altère le nom de la première colonne, et `version_IA.html` accepte un fichier avec BOM (`FileReader.readAsText`, qu'il utilise, retire le BOM : Obs-3 de R5). Le cahier des charges §11.1 et le prompt envoyé gardent la formulation plus large « tout autre format est rejeté » | ETAT §5 (O-10) ; `travail/decisions.md` l. 61 (Q-10) et l. 106 (journal) ; `travail/audits/R5_audit.md` (Obs-3) ; `Groupe_01_Cas_01/cahier_des_charges.md` §11.1 (Q-10) | à corriger | corrigé (résumés) ; remonté (cahier des charges, R6) |
| K2 | ETAT §3 annonce `prompts.md` v1 « sections 1 à 4 complétées » ; les sections 2 à 4 sont des emplacements annoncés pour R5 et R6, non remplis par R5 | ETAT §3 l. 88 ; `Groupe_01_Cas_01/prompts.md` §2 à §4 | à corriger | corrigé |
| K3 | Le plan de test dit de créer `index.html` dans tous les cas, alors que la fiche 04 ne le prévoit qu'en cas d'écart (C-09) | `tests/plan_de_test.md` l. 63 ; `agents/04_developpeur.md` l. 8 et 10 ; `tests/plan_de_test.md` l. 75 | à corriger | corrigé |
| K4 | Le prompt RMTCEV reprend la bonne pratique de trois pièges, alors que D-10 exclut les solutions d'implémentation des pièges : l. 36 « à l'aide de l'API FileReader » (P-06), l. 40 réinitialisation de l'état (P-09), l. 69 « CSS et JavaScript natifs » (P-05) ; aucun E-xx ne le consigne | `Groupe_01_Cas_01/prompts.md` l. 36, 40, 69 ; `travail/decisions.md` (D-10) ; `AGENTS.md` §7 | à corriger | consigné (E-27) ; prompt laissé tel quel (texte envoyé : C-08 ; `AGENTS.md` §12, « tel qu'envoyé ») |
| K5 | O-13 (complétude de la réponse brute, mode de session) | ETAT §5 | ouvert | laissé (Bradley, puis R6) |
| K6 | Les commits de R4 portent une adresse e-mail personnelle | `git log` (b170333, 624003a, ffee9e6) | non corrigeable (historique jamais réécrit, `AGENTS.md` §11) | laissé |

### Ce qui a été seulement survolé ; résultats donnés par le membre

- Survolé : le reste du travail de R4, déjà audité par R5 (`travail/audits/R5_audit.md`) et par le complément de R5.
- Donné par Leddycia : à 15:58, R6 n'avait pas encore fait de `git pull`.

### Corrections apportées (une ligne par correction)

- K1 : ETAT §5, O-10 reformulé ; `travail/decisions.md`, ligne de rectificatif ajoutée au journal des changements (la ligne R4 n'est pas réécrite), après un essai réel sous Chrome 155 : CSV avec BOM accepté, CSV à `;` rejeté (E-28).
- K2 : ETAT §3, ligne `prompts.md` : « section 1 remplie (§1.1 encore à corriger par R6 : O-13, RG-09) ; sections 2 à 4 : emplacements créés, encore vides, à compléter par R6 » (E-28).
- K3 : `tests/plan_de_test.md` §2 : `index.html` seulement en cas d'écart sur les CA, les règles du client ou les consignes ; sinon, l'écrire dans ETAT et le README (fiche 04, C-09) (E-28).
- K4 : aucune correction du prompt (texte envoyé) ; E-27 ajoutée.

### Points remontés à l'équipe (complément)

- K1 : le cahier des charges §11.1 garde la formulation plus large de Q-10 ; le registre prime (`AGENTS.md` §2) ; à signaler par R6 dans le README (« écarts connus et points à confirmer »), ETAT §6.
- E-27 peut illustrer la précision des prompts (C-18) dans `prompts.md`, citée à part et signalée comme acceptée telle quelle (pas comme une proposition corrigée ou rejetée du §3, exigée par C-08) (ETAT §6).
- K5 (O-13) et K6 : inchangés.

### Ce que j'ai produit pendant le complément

- `ETAT_PROJET.md` (§3, §4, §5 O-10, §6) ; `travail/decisions.md` (journal des changements) ; `tests/plan_de_test.md` (§2).
- E-27, E-28 ; JP-26, JP-27 ; cette section.
- Relecture indépendante avant la clôture : 3 vérificateurs en lecture seule (exactitude, dont l'essai refait du BOM et du `;` ; traçabilité ; intégrité et protocole) ; aucun point bloquant ; 18 remarques (3 « à corriger », 15 mineures, dont plusieurs relevées en double), toutes traitées (E-27 complétée, l. 40 et 69 ; état de `prompts.md` ; citations exactes ; formulation sur le BOM ; cahier des charges signalé ; plan de test précisé ; E-27 hors des exemples de C-08 ; K0 et sous-section « survolé » ajoutés ; origine des points précisée).

### Journal de bord du complément (copie intégrale d'ETAT §8, ajoutée à la clôture)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

| Relais | Membre | Outil et modèle | Fiche | Porte visée | Début |
|---|---|---|---|---|---|
| R4 (complément, après le tag `relais-4`) | Leddycia | Claude Code (application de bureau, Claude Opus 5.5) | `agents/03_prompt_engineer.md`, `agents/00_protocole_relais.md` | G4 (corrections avant R6) | 15:59 |

**Plan validé** (demande de Leddycia, JP-26 ; uniquement si R6 n'a pas encore fait de `git pull` : dépôt distant inchangé depuis b797c0c, pas de tag `relais-6`, Leddycia confirme à 15:58 que R6 n'a pas fait de `git pull`) : 1. Ouvrir le complément (ETAT §1, §2, §8 ; section « Complément » de `travail/audits/R4_audit.md`). 2. Q-10 : corriger les deux résumés de sa précision, « BOM traité en rejet Q-04 » (ETAT §5, O-10) et « BOM UTF-8 traité en rejet Q-04 sans planter » (journal des changements du registre, par une ligne ajoutée), après un essai réel dans un navigateur. 3. ETAT §3 : `prompts.md` « sections 1 à 4 complétées » → état réel. 4. `tests/plan_de_test.md` §2 : création d'`index.html` seulement en cas d'écart (fiche 04). 5. Consigner en E-xx l'indication « API FileReader » du prompt (D-10). 6. Journaux, relecture indépendante, puis clôture sur demande. Chaque étape est contrôlée trois fois (diff relu, contrôle par script ou essai, relecture).

**Audit d'entrée (synthèse)** : ETAT O-10 (« BOM traité en rejet Q-04 ») et `travail/decisions.md` (journal des changements, ligne R4 de Q-10 : « BOM UTF-8 traité en rejet Q-04 sans planter ») résument mal la précision de Q-10, alors que la formulation de Q-10 ne rejette un BOM que s'il altère l'en-tête, et que `version_IA.html` accepte un fichier avec BOM (Obs-3 de R5) | à corriger ; ETAT §3 l. 88 : `prompts.md` « sections 1 à 4 complétées », alors que les sections 2 à 4 restent à compléter par R6 | à corriger ; `tests/plan_de_test.md` l. 63 : `index.html` à créer dans tous les cas, contraire à la fiche 04 (l. 10) et au §3 du même fichier (l. 75) | à corriger ; `prompts.md` l. 36 : « à l'aide de l'API FileReader », solution d'implémentation du piège P-06, contraire à D-10, sans E-xx | à consigner (le prompt envoyé ne se modifie pas) ; hors de portée : O-13 (Bradley), adresses e-mail des commits de R4 (historique jamais réécrit). Détail : `travail/audits/R4_audit.md`, section « Complément ».

**Journal de bord**

| Heure | Étape | Ce qui a été fait | Fichiers | État |
|---|---|---|---|---|
| 15:59 | étape 1 | Complément de R4 ouvert : R4 « complément EN COURS » ; contrôle préalable (dépôt distant inchangé, pas de `relais-6`, Leddycia confirme que R6 n'a pas fait de `git pull`) | `ETAT_PROJET.md`, `travail/audits/R4_audit.md` | fait |
| 16:00 | étape 2 | Q-10 : essai réel sous Chrome 155 sans interface (Windows 11) : `version_IA.html` accepte le CSV précédé d'un BOM UTF-8 (97 h, 280,0 L) et rejette le CSV à `;` (« Erreur à la ligne 1 (en-tête) … »), conformément à la formulation de Q-10 ; résumé d'O-10 corrigé ; ligne de rectificatif ajoutée au journal des changements du registre (la ligne R4 n'est pas réécrite) (E-28). Contrôles : diff relu ; formulation de Q-10 dans le tableau inchangée ; recherche dans tout le dépôt : seules restent des traces historiques, suivies du rectificatif | `ETAT_PROJET.md`, `travail/decisions.md` | fait |
| 16:00 | étapes 3 et 4 | ETAT §3 : `prompts.md` « section 1 complète ; sections 2 à 4 créées, encore à compléter par R5 et R6 » ; `tests/plan_de_test.md` §2 : `index.html` seulement en cas d'écart (fiche 04, C-09) (E-28). Contrôles : diff relu (une ligne par fichier) ; `prompts.md` contient toujours 3 emplacements « Section à compléter » ; plan de test cohérent avec la fiche 04 (l. 10) et avec son §3 (l. 75) | `ETAT_PROJET.md`, `tests/plan_de_test.md` | fait |
| 16:01 | étapes 5 et 6 | E-27 (indication « API FileReader » du prompt, laissée telle quelle : texte envoyé ; seule indication de ce type dans le prompt) ; E-28 ; JP-26 ; « Corrections apportées », « Points remontés » et « Ce que j'ai produit » dans `R4_audit.md` ; E-27 proposée à R6 pour `prompts.md` §3 (§6). Relecture indépendante à faire avant la clôture | `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `travail/audits/R4_audit.md`, `ETAT_PROJET.md` | fait |
| 16:18 | étape 6 | Relecture indépendante (3 vérificateurs en lecture seule, dont un a refait l'essai du BOM et du `;`) : aucun point bloquant ; 3 « à corriger » et 12 mineurs, traités. Rectificatifs des lignes précédentes : l'indication FileReader n'est pas la seule (l. 40, P-09, et l. 69, P-05, reprennent aussi une bonne pratique de piège : E-27 complétée et classée « accepté tel quel ») ; ETAT §3 : « section 1 remplie (§1.1 encore à corriger par R6) ; sections 2 à 4 encore vides, à compléter par R6 » ; l'entrée R4 du §7 garde le résumé inexact de Q-10 et sera signalée dans l'entrée du complément. Autres corrections : citations exactes des deux résumés de Q-10 ; « `FileReader.readAsText` retire le BOM » au lieu de « un navigateur » ; formulation plus large de Q-10 dans le cahier des charges signalée (E-28, ETAT §5 et §6 : à mentionner au README par R6, cahier des charges non modifié) ; plan de test §2 précisé (écarts sur les CA, règles ou consignes ; où l'écrire) ; E-27 retirée des exemples de propositions corrigées ou rejetées du §6 ; `R4_audit.md` complété (constat conforme K0, sous-section « survolé ») | `travail/journal_ecarts.md`, `travail/decisions.md`, `ETAT_PROJET.md`, `tests/plan_de_test.md`, `travail/audits/R4_audit.md`, `travail/journal_prompts.md` | fait |
| 16:20 | étape 6 | « fin de notre relais » (JP-27, 16:19) : clôture du complément ; bilan : étapes 1 à 6 faites, aucune partielle ; relecture indépendante finale, puis commit et push sans tag | `ETAT_PROJET.md`, `travail/audits/R4_audit.md`, `travail/journal_prompts.md` | fait |

**Points ouverts du relais** : O-13 reste à Bradley et R6.

**Rectificatifs après la copie** (relecture indépendante finale, avant le commit ; la copie ci-dessus n'est pas modifiée) : à 16:18, la première relecture a produit 18 remarques (3 « à corriger », 15 mineures, dont plusieurs en double), et non « 3 « à corriger » et 12 mineurs » ; le texte final d'ETAT §3 est celui cité en K2 (« section 1 remplie (§1.1 encore à corriger par R6 : O-13, RG-09) ; sections 2 à 4 : emplacements créés, encore vides, à compléter par R6 ») ; la relecture finale (2 vérificateurs en lecture seule) a relevé 7 points mineurs, traités avant le commit (JP-27 et §4 ajoutés à « Ce que j'ai produit » et à ETAT §3, complément de R4 attribué à Leddycia pour la fiche de contribution, place d'E-27 dans `prompts.md`, liste des autres lignes d'E-27 présentée comme non exhaustive, comptes ci-dessus).

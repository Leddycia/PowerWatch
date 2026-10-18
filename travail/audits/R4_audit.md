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

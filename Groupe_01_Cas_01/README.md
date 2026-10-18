# PowerWatch : Groupe 01, Cas 01

## Présentation
PowerWatch est un tableau de bord destiné au Collège Les Palmistes. Il aide la directrice à suivre la consommation de la génératrice et son coût à partir du CSV préparé par l'intendant. Le Sprint 01 couvre le chargement du fichier, les totaux par période, le coût estimé et le jour de fonctionnement maximal (US-01 à US-03).

## Comment ouvrir le prototype
1. Ouvrir `prototype/version_IA.html` par double-clic. Le livrable ne contient pas `prototype/index.html` : R5 n'a constaté aucun écart aux critères du Sprint 01, et C-09 interdit de créer une seconde version sans correction nécessaire.
2. Cliquer sur « Choisir un fichier » et sélectionner le fichier `energie_college.csv` fourni avec le cas par l'intendant. Le CSV n'est pas inclus dans ce dossier livrable.
3. Aucun serveur, compte ni accès Internet n'est requis.

## Outils utilisés

| Étape | Outil et modèle |
|---|---|
| Cadrage, cahier des charges et product backlog (R1 à R3) | Claude Code, Claude Opus 5.5 |
| Prompt et prototype délégué (R4) | Antigravity, Gemini 3.8 Flash High ; délégation vierge à ChatGPT, GPT-4o |
| Vérification et captures (R5) | Claude Code, Claude Opus 5.5 ; Chromium 150 et Firefox |
| Finalisation documentaire (R6) | Claude ; modèle non précisé |
| Éditeur du dépôt | Visual Studio Code |

## Contenu du dossier

| Élément | Contenu |
|---|---|
| `cahier_des_charges.md` | Besoin, exigences, règles métier, contraintes et traçabilité |
| `product_backlog.md` | 8 user stories, priorités, critères d'acceptation et Sprint 01 |
| `prompts.md` | Prompt RMTCEV, prompts significatifs et retour critique sur les propositions de l'IA |
| `prototype/version_IA.html` | Prototype HTML autonome produit par l'IA déléguée, non modifié |
| `captures/` | Preuves visuelles des critères du Sprint 01 |

## Vérification du Sprint 01

Les statuts ci-dessous reprennent les résultats documentés par R5 dans le plan de test du projet. Les liens ouvrent les captures du livrable.

| CA | Énoncé court | Statut | Preuve |
|---|---|---|---|
| CA-01.01 | État initial, bouton et hors ligne | respecté | [Capture](captures/US01_CA01_etat_initial.png) |
| CA-01.02 | Chargement et période par défaut | respecté | [Chromium](captures/US01_CA02_chargement_toute_periode.png), [Firefox](captures/US01_CA02_firefox_toute_periode.png) |
| CA-01.03 | Liste des périodes | respecté | [Capture](captures/US01_CA03_liste_periodes.png) |
| CA-01.04 | Totaux pour les quatre périodes | respecté | [Août](captures/US01_CA04_aout.png), [septembre](captures/US01_CA04_septembre.png), [octobre](captures/US01_CA04_octobre.png), [toute la période](captures/US01_CA04_toute_periode.png) |
| CA-01.05 | Totaux sous fuseau d'Haïti | respecté | [Montage des trois mois](captures/US01_CA05_fuseau_haiti.png) |
| CA-01.06 | Changement de période sans rechargement | respecté | [Capture](captures/US01_CA06_changement_octobre.png) |
| CA-01.07 | Rejet de colonne manquante | respecté | [Capture](captures/US01_CA07_colonne_manquante.png) |
| CA-01.08 | Fichier source inchangé et lecture seule | respecté | [Capture](captures/US01_CA08_lecture_seule.png) |
| CA-01.09 | Remplacement des données au second chargement | respecté | [Capture](captures/US01_CA09_reinitialisation_cumul.png) |
| CA-01.10 | Périodes déduites d'un fichier partiel | respecté | [Capture](captures/US01_CA10_fichier_partiel.png) |
| CA-01.11 | Rejet d'une valeur non numérique | respecté | [Capture](captures/US01_CA11_valeur_non_numerique.png) |
| CA-02.01 | Coût estimé pour les quatre périodes | respecté | [Août](captures/US02_CA01_cout_aout.png), [septembre](captures/US02_CA01_cout_septembre.png), [octobre](captures/US02_CA01_cout_octobre.png), [toute la période](captures/US02_CA01_cout_toute_periode.png) |
| CA-02.02 | Libellé du coût et prix de référence | respecté | [Capture](captures/US02_CA02_libelle_prix_reference.png) |
| CA-02.03 | Actualisation du coût au changement de période | respecté | [Capture](captures/US02_CA03_changement_cout.png) |
| CA-02.04 | Coût sous fuseau d'Haïti | respecté | [Montage des trois mois](captures/US02_CA04_fuseau_cout.png) |
| CA-02.05 | Mention que le prix n'est pas officiel | respecté | [Capture](captures/US02_CA05_mention_officielle.png) |
| CA-03.01 | Jour maximal pour les quatre périodes | respecté | [Août](captures/US03_CA01_jour_max_aout.png), [septembre](captures/US03_CA01_jour_max_septembre.png), [octobre](captures/US03_CA01_jour_max_octobre.png), [toute la période](captures/US03_CA01_jour_max_toute_periode.png) |
| CA-03.02 | Égalité chronologique avec lignes mélangées | respecté | [Août](captures/US03_CA02_lignes_melangees_aout.png), [septembre](captures/US03_CA02_lignes_melangees_septembre.png), [octobre](captures/US03_CA02_lignes_melangees_octobre.png), [toute la période](captures/US03_CA02_lignes_melangees_toute_periode.png) |
| CA-03.03 | Période sans fonctionnement | respecté | [Capture](captures/US03_CA03_sans_generatrice.png) |
| CA-03.04 | Jour maximal sous fuseau d'Haïti | respecté | [Montage des trois mois](captures/US03_CA04_fuseau_jour_max.png) |

## Conditions de test

R5 a testé `version_IA.html` sous Kali Linux avec le fuseau `America/Port-au-Prince`, Chromium 150 piloté en mode headless et Firefox (test manuel). Le hors-ligne a été émulé sous Chromium et réellement coupé pour les essais Firefox. L'écart avec la procédure Windows initialement prévue est consigné en E-22 ; les résultats détaillés figurent dans le plan de test interne du projet.

**Test depuis le Drive sur un autre ordinateur (C-14)** : à réaliser après le téléversement par Leddycia. Le nom du testeur, l'ordinateur, le navigateur, la date et l'heure ainsi que la valeur contrôlée avec l'oracle seront ajoutés après exécution. Ce test n'est pas déclaré effectué à ce stade.

## Écarts connus et points à confirmer avec le client

- Aucun écart aux critères du Sprint 01 n'a été constaté par R5. `index.html` n'a donc pas été créé ; `version_IA.html` est resté intact, conformément à C-09 et RG-08.
- O-14, hors critères d'acceptation : une ligne vide au milieu du CSV est ignorée sans message, et une valeur décimale d'heures serait affichée arrondie à l'entier. Ces comportements n'ont pas été corrigés, car ils ne sont pas couverts par le Sprint 01 (RG-04). Leur traitement reste à confirmer avec le client, en lien avec Q-04 et Q-16 du cahier des charges.
- Les autres hypothèses et questions encore ouvertes sont recensées au §11 du cahier des charges.

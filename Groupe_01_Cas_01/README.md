# PowerWatch : Groupe 01, Cas 01

## Présentation
PowerWatch est un tableau de bord destiné au Collège Les Palmistes. Il aide la directrice à suivre la consommation de la génératrice et son coût à partir du CSV préparé par l'intendant. Le Sprint 01 couvre le chargement du fichier, les totaux par période, le coût estimé et le jour de fonctionnement maximal (US-01 à US-03).

## Comment ouvrir le prototype
1. Ouvrir `prototype/index.html` par double-clic : c'est la version à utiliser (voir « Prototype » ci-dessous). `prototype/version_IA.html`, la sortie brute de l'IA déléguée, s'ouvre de la même façon.
2. Cliquer sur « Choisir un fichier » et sélectionner le fichier `energie_college.csv` fourni avec le cas par l'intendant. Le CSV n'est pas inclus dans ce dossier livrable.
3. Aucun serveur, compte ni accès Internet n'est requis.

## Prototype

Le dossier `prototype/` contient deux fichiers. Ils s'ouvrent par double-clic, sans Internet, sans serveur et sans compte.

| Fichier | Rôle |
|---|---|
| `prototype/index.html` | **Version à utiliser.** Même calcul que `version_IA.html`, présentation et textes revus. |
| `prototype/version_IA.html` | Première sortie brute de l'IA déléguée (ChatGPT, GPT-4o), jamais modifiée (C-09). |

**Pourquoi un `index.html` alors que `version_IA.html` respectait les CA ?** La vérification de R5 a trouvé les 20 CA respectés. Une relecture plus stricte a relevé deux points faibles : le prix de 300 gourdes par litre n'était pas dans la carte du coût (CA-02.02, E-29), et la mention « prix de référence de l'intendance, pas un prix officiel » était le plus petit texte de la page, en 11 px (CA-02.05, E-30). S'y ajoutent un contraste insuffisant, un tiret cadratin dans le titre et des pictogrammes peu clairs (E-31). L'équipe a donc décidé (D-16) de créer `index.html` pour la présentation seulement. E-29 et E-30 sont détaillés dans `prompts.md` §3.

**Ce qui ne change pas** : tout le code JavaScript. Le bloc `<script>` d'`index.html` est la copie exacte de celui de `version_IA.html` : mêmes calculs, mêmes messages, mêmes formats. Aucune fonction n'est ajoutée (pas de graphique, d'export ni de mode sombre).

**Ce qui change** : un logo PowerWatch dessiné en SVG dans la page ; le prix dans la carte du coût ; la mention du prix non officiel en phrase lisible ; deux étapes numérotées (« Charger le fichier du registre », « Choisir la période ») ; des textes d'aide revus, tirés du brief : « Lecture seule · Fonctionne sans Internet » dans l'en-tête, les colonnes attendues du fichier, la description de chaque indicateur et, sous le jour maximal, le rappel de la règle d'égalité du client (B-13) ; une aide après une erreur ; des couleurs plus contrastées ; des pictogrammes dessinés au lieu de caractères spéciaux ; un affichage adapté au téléphone.

**Vérification** : `index.html` a été revérifié entièrement (Chrome 155, fuseau d'Haïti et réseau coupé par émulation) : 20 CA, Test-P04 et contrôles transverses respectés (plan de test du projet, `tests/plan_de_test.md` §4, hors livrable). Les captures d'`index.html` portent le suffixe `_index` ; celles de `version_IA.html` (R5) sont conservées, sauf trois photos de l'écran retirées du livrable (voir « Vérification du Sprint 01 »).

## Outils utilisés

| Étape | Outil et modèle |
|---|---|
| Cadrage, cahier des charges et product backlog (R1 à R3) | Claude Code, Claude Opus 5.5 |
| Prompt et prototype délégué (R4) | Antigravity, Gemini 3.8 Flash High ; délégation vierge à ChatGPT, GPT-4o |
| Vérification et captures (R5) | Claude Code, Claude Opus 5.5 ; Chromium 150 et Firefox |
| Corrections avant R6 (compléments de R5 et de R4) | Claude Code (application de bureau), Claude Opus 5.5 ; Google Chrome 155 |
| `prototype/index.html` (habillage, D-16) et sa revérification | Claude Code (application de bureau), Claude Opus 5.5 ; Google Chrome 155 |
| Finalisation documentaire (R6) | Claude, modèle non précisé ; reprise et clôture : Claude Code (application de bureau), Claude Opus 5.5 |
| Éditeur du dépôt | Antigravity |

## Contenu du dossier

| Élément | Contenu |
|---|---|
| `cahier_des_charges.md` | Besoin, exigences, règles métier, contraintes et traçabilité |
| `product_backlog.md` | 8 user stories, priorités, critères d'acceptation et Sprint 01 |
| `prompts.md` | Prompt RMTCEV, prompts significatifs et retour critique sur les propositions de l'IA |
| `prototype/index.html` | Prototype à utiliser : même script que `version_IA.html`, présentation et textes revus (D-16) |
| `prototype/version_IA.html` | Prototype HTML autonome produit par l'IA déléguée, non modifié |
| `captures/` | Preuves visuelles des critères du Sprint 01 : captures de `version_IA.html` (R5) et captures d'`index.html` (suffixe `_index`) |

## Vérification du Sprint 01

Le statut vaut pour les deux versions du prototype : celui de `version_IA.html` vient de la vérification de R5, celui d'`index.html` de sa revérification complète (D-16). Le détail des résultats figure dans le plan de test du projet (`tests/plan_de_test.md` §3 et §4), conservé dans le dépôt Git du projet, hors livrable. Les liens ouvrent les captures du livrable.

| CA | Énoncé court | Statut | Preuve `index.html` | Preuve `version_IA.html` (R5) |
|---|---|---|---|---|
| CA-01.01 | État initial, bouton et hors ligne | respecté | [Capture](captures/US01_CA01_etat_initial_index.png) | [Capture](captures/US01_CA01_etat_initial.png) |
| CA-01.02 | Chargement et période par défaut | respecté | [Capture](captures/US01_CA02_toute_periode_index.png) | [Chromium](captures/US01_CA02_chargement_toute_periode.png), [Firefox](captures/US01_CA02_firefox_toute_periode.png) |
| CA-01.03 | Liste des périodes | respecté | [Capture](captures/US01_CA03_liste_periodes_index.png) | Aucune (photo retirée, voir sous le tableau) |
| CA-01.04 | Totaux pour les quatre périodes | respecté | [Août](captures/US01_CA04_aout_index.png), [septembre](captures/US01_CA04_septembre_index.png), [octobre](captures/US01_CA04_octobre_index.png), [toute la période](captures/US01_CA02_toute_periode_index.png) | [Août](captures/US01_CA04_aout.png), [septembre](captures/US01_CA04_septembre.png), [octobre](captures/US01_CA04_octobre.png), [toute la période](captures/US01_CA04_toute_periode.png) |
| CA-01.05 | Totaux sous fuseau d'Haïti | respecté | [Montage des trois mois](captures/US01_CA05_fuseau_haiti_index.png) | [Montage des trois mois](captures/US01_CA05_fuseau_haiti.png) |
| CA-01.06 | Changement de période sans rechargement | respecté | [Capture](captures/US01_CA06_changement_octobre_index.png) | [Capture](captures/US01_CA06_changement_octobre.png) |
| CA-01.07 | Rejet de colonne manquante | respecté | [Capture](captures/US01_CA07_colonne_manquante_index.png) | [Capture](captures/US01_CA07_colonne_manquante.png) |
| CA-01.08 | Fichier source inchangé et lecture seule | respecté | [Capture](captures/US01_CA08_lecture_seule_index.png) | Aucune (photo retirée, voir sous le tableau) |
| CA-01.09 | Remplacement des données au second chargement | respecté | [Capture](captures/US01_CA09_reinitialisation_index.png) | [Capture](captures/US01_CA09_reinitialisation_cumul.png) |
| CA-01.10 | Périodes déduites d'un fichier partiel | respecté | [Capture](captures/US01_CA10_fichier_partiel_index.png) | Aucune (photo retirée, voir sous le tableau) |
| CA-01.11 | Rejet d'une valeur non numérique | respecté | [Capture](captures/US01_CA11_valeur_non_numerique_index.png) | [Capture](captures/US01_CA11_valeur_non_numerique.png) |
| CA-02.01 | Coût estimé pour les quatre périodes | respecté | Captures de CA-01.04 | [Août](captures/US02_CA01_cout_aout.png), [septembre](captures/US02_CA01_cout_septembre.png), [octobre](captures/US02_CA01_cout_octobre.png), [toute la période](captures/US02_CA01_cout_toute_periode.png) |
| CA-02.02 | Libellé du coût et prix de référence | respecté | [Capture](captures/US02_CA02_libelle_prix_index.png) | [Capture](captures/US02_CA02_libelle_prix_reference.png) |
| CA-02.03 | Actualisation du coût au changement de période | respecté | [Septembre, juste après août](captures/US01_CA04_septembre_index.png) | [Capture](captures/US02_CA03_changement_cout.png) |
| CA-02.04 | Coût sous fuseau d'Haïti | respecté | [Montage des trois mois](captures/US01_CA05_fuseau_haiti_index.png) | [Montage des trois mois](captures/US02_CA04_fuseau_cout.png) |
| CA-02.05 | Mention que le prix n'est pas officiel | respecté | [Capture](captures/US02_CA02_libelle_prix_index.png) | [Capture](captures/US02_CA05_mention_officielle.png) |
| CA-03.01 | Jour maximal pour les quatre périodes | respecté | Captures de CA-01.04 | [Août](captures/US03_CA01_jour_max_aout.png), [septembre](captures/US03_CA01_jour_max_septembre.png), [octobre](captures/US03_CA01_jour_max_octobre.png), [toute la période](captures/US03_CA01_jour_max_toute_periode.png) |
| CA-03.02 | Égalité chronologique avec lignes mélangées | respecté | [Montage des quatre périodes](captures/US03_CA02_lignes_melangees_index.png) | [Août](captures/US03_CA02_lignes_melangees_aout.png), [septembre](captures/US03_CA02_lignes_melangees_septembre.png), [octobre](captures/US03_CA02_lignes_melangees_octobre.png), [toute la période](captures/US03_CA02_lignes_melangees_toute_periode.png) |
| CA-03.03 | Période sans fonctionnement | respecté | [Capture](captures/US03_CA03_sans_generatrice_index.png) | [Capture](captures/US03_CA03_sans_generatrice.png) |
| CA-03.04 | Jour maximal sous fuseau d'Haïti | respecté | [Montage des trois mois](captures/US01_CA05_fuseau_haiti_index.png) | [Montage des trois mois](captures/US03_CA04_fuseau_jour_max.png) |
| Test-P04 | Arrondi à l'affichage d'une somme décimale (piège P-04) | respecté | [Capture](captures/TEST_P04_arrondi_decimales_index.png) | [Capture](captures/TEST_P04_arrondi_decimales.png) |

**Une même capture prouve souvent plusieurs CA**, car un seul écran affiche à la fois les heures, les litres, le coût et le jour maximal. Pour `index.html`, chaque capture de CA-01.04 prouve aussi CA-02.01 et CA-03.01, et le montage `US01_CA05_fuseau_haiti_index.png` prouve CA-01.05, CA-02.04 et CA-03.04. Pour `version_IA.html`, R5 a enregistré le même écran sous le nom de chaque CA : par exemple, l'écran « Toute la période » est le même fichier sous sept noms (`US01_CA02_chargement_toute_periode.png`, `US01_CA04_toute_periode.png`, `US01_CA09_reinitialisation_cumul.png`, `US02_CA01_cout_toute_periode.png`, `US02_CA02_libelle_prix_reference.png`, `US02_CA05_mention_officielle.png` et `US03_CA01_jour_max_toute_periode.png`).

**Lecture de CA-02.02 sur `version_IA.html`** : le prix de référence de 300 gourdes par litre y est affiché dans le bloc de chargement, sur le même écran que le coût. R5 a retenu cette lecture, et le CA est respecté. Sous une lecture stricte (« son libellé »), le prix manque dans la carte du coût : `index.html` l'y ajoute (E-29).

**Trois preuves de `version_IA.html` retirées** : pour CA-01.03, CA-01.08 et CA-01.10, les seules preuves de `version_IA.html` étaient des photos de l'écran prises par R5 sous Firefox. L'équipe les a retirées du livrable le 2026-10-18, car ces photos, prises de biais, étaient peu lisibles. Les résultats observés par R5 restent consignés dans le plan de test du projet (§3, hors livrable), et ces trois CA sont prouvés par les captures d'`index.html`, qui exécute le même script.

## Conditions de test

R5 a testé `version_IA.html` sous Kali Linux avec le fuseau `America/Port-au-Prince`, Chromium 150 piloté en mode headless et Firefox (test manuel). Le hors-ligne a été émulé sous Chromium et réellement coupé pour les essais Firefox. L'écart avec la procédure Windows initialement prévue est consigné en E-22 ; les résultats détaillés figurent dans le plan de test du projet (hors livrable). Les 4 captures de CA-03.02 sur `version_IA.html` ont ensuite été refaites sous Windows 11, avec Chrome 155 sans interface, le fuseau d'Haïti et la coupure du réseau émulés, avec un fichier de test dont les jours à égalité sont dans le désordre (E-24).

`index.html` a été revérifié sous Windows 11 Pro avec Google Chrome 155 sans interface, piloté par script : fuseau `America/Port-au-Prince` et coupure du réseau émulés, chargement par le vrai champ de fichier de la page (`<input type="file">`). Firefox n'a pas encore été testé sur `index.html` : il le sera lors du test depuis le Drive.

**Test depuis le Drive sur un autre ordinateur (C-14)** : confié à Gervais, à réaliser après le téléversement par Leddycia, Firefox compris. L'ordinateur, les navigateurs, la date et l'heure ainsi que les valeurs contrôlées avec l'oracle seront ajoutés après exécution. Ce test n'est pas déclaré effectué à ce stade.

## Écarts connus et points à confirmer avec le client

- Aucun écart aux critères du Sprint 01 n'a été constaté par R5 sur `version_IA.html`. Une relecture plus stricte a relevé deux points faibles de présentation, sur CA-02.02 et CA-02.05 (E-29, E-30) : ils sont corrigés dans `index.html` sans toucher au calcul. `version_IA.html` est resté intact, conformément à C-09 et RG-08.
- O-14, hors critères d'acceptation : une ligne vide au milieu du CSV est ignorée sans message, et une valeur décimale d'heures serait affichée arrondie à l'entier. Ces comportements n'ont pas été corrigés, car ils ne sont pas couverts par le Sprint 01 (RG-04). Ils sont identiques dans les deux versions, qui partagent le même script. Leur traitement reste à confirmer avec le client, en lien avec Q-04 et Q-16 du cahier des charges.
- Dans `index.html`, le rappel de la règle d'égalité reste affiché sous le jour maximal même quand la période n'a aucun fonctionnement (capture de CA-03.03) : c'est un texte fixe, sans effet sur le calcul ni sur les CA.
- Q-10, format du fichier : un CSV précédé d'un BOM UTF-8 (marque d'ordre des octets) est accepté par les deux versions, car le navigateur retire cette marque à la lecture ; un CSV séparé par des points-virgules est bien rejeté avec un message. Ce comportement suit l'hypothèse provisoire du registre des décisions de l'équipe (seul un BOM qui altère le nom de la première colonne entraîne le rejet), alors que le cahier des charges (§11.1) écrit plus largement « tout autre format est rejeté » (E-28). Le format exact produit par l'intendant reste à confirmer avec le client (Q-10).
- Les autres hypothèses et questions encore ouvertes sont recensées au §11 du cahier des charges.

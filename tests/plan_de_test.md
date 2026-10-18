# Plan de test du Sprint 01 : PowerWatch

> **Objet** : définir le protocole pas à pas de validation des critères d'acceptation du Sprint 01 (US-01, US-02, US-03) sur le prototype.
> Ce document sert de guide d'exécution pour le relais R5 (développeur / vérificateur) et fournit la grille des preuves par captures d'écran pour le livrable final (C-15, README.md).
>
> **Règles de nommage des captures (AGENTS.md §11)** : `captures/USxx_CAyy_<detail>.png`.
> **Fichiers de données utilisés** :
> - `docs/energie_college.csv` : fichier original de référence (36 lignes, hash SHA-256 `320155c7…a84b`).
> - `tests/fixtures/f01_lignes_melangees.csv` : 36 lignes mélangées (égalité chronologique, CA-03.02).
> - `tests/fixtures/f02_colonne_manquante.csv` : en-tête sans `litres_carburant` (rejet Q-04, CA-01.07).
> - `tests/fixtures/f03_valeur_non_numerique.csv` : valeur `abc` dans les heures (rejet Q-04, CA-01.11).
> - `tests/fixtures/f04_mois_sans_generatrice.csv` : mois à 0 h de génératrice (message Q-05, CA-03.03).
> - `tests/fixtures/f05_decimales.csv` : contrôle de l'arrondi flottant IEEE 754 (B-14, P-04).
> - `tests/fixtures/f06_aout_septembre.csv` : en-tête et 24 lignes d'août et septembre (CA-01.09, CA-01.10).

---

## 1. Grille de test des critères d'acceptation (Sprint 01)

| CA | Intitulé court | Données d'entrée | Procédure pas à pas | Résultat attendu (Oracle §2, §4, §5, §8) | Nom de la capture d'écran |
|---|---|---|---|---|---|
| **CA-01.01** | État initial hors ligne | Aucun fichier | 1. Déconnecter le réseau / mode avion.<br>2. Double-cliquer sur le fichier HTML du prototype.<br>3. Observer la page d'accueil. | Page affichée sans erreur, bouton « Choisir un fichier » visible. Aucune donnée calculée ni total affiché avant chargement. Rappel fixe du prix de 300 gourdes/L permis. | `captures/US01_CA01_etat_initial.png` |
| **CA-01.02** | Chargement initial et période par défaut | `energie_college.csv` | 1. Cliquer sur « Choisir un fichier ».<br>2. Sélectionner `docs/energie_college.csv`.<br>3. Observer l'affichage immédiat. | Aucun message d'erreur. Période sélectionnée par défaut = « Toute la période ». Totaux affichés = 97 h et 280,0 L. | `captures/US01_CA02_chargement_toute_periode.png` |
| **CA-01.03** | Liste des périodes proposées | `energie_college.csv` | 1. Ouvrir le sélecteur / menu déroulant de période. | Exactement quatre choix disponibles : « Août 2026 », « Septembre 2026 », « Octobre 2026 » et « Toute la période » (H-04). | `captures/US01_CA03_liste_periodes.png` |
| **CA-01.04a** | Totaux Août 2026 | `energie_college.csv` | 1. Sélectionner « Août 2026 » dans la liste des périodes. | Heures de génératrice = **24 h** ; Litres de carburant = **71,0 L** (1 décimale, virgule). | `captures/US01_CA04_aout.png` |
| **CA-01.04b** | Totaux Septembre 2026 | `energie_college.csv` | 1. Sélectionner « Septembre 2026 ». | Heures de génératrice = **30 h** ; Litres de carburant = **84,0 L**. | `captures/US01_CA04_septembre.png` |
| **CA-01.04c** | Totaux Octobre 2026 | `energie_college.csv` | 1. Sélectionner « Octobre 2026 ». | Heures de génératrice = **43 h** ; Litres de carburant = **125,0 L**. | `captures/US01_CA04_octobre.png` |
| **CA-01.04d** | Totaux Toute la période | `energie_college.csv` | 1. Sélectionner « Toute la période ». | Heures de génératrice = **97 h** ; Litres de carburant = **280,0 L**. | `captures/US01_CA04_toute_periode.png` |
| **CA-01.05** | Insensibilité au fuseau horaire (Haïti UTC-05) | `energie_college.csv` | 1. Régler l'ordinateur sur le fuseau « (UTC-05:00) Haïti ».<br>2. Charger `energie_college.csv`.<br>3. Vérifier les totaux pour Août, Septembre et Octobre. | Totaux conformes à CA-01.04. Les valeurs erronées du piège P-01 (Août: 26 h, Septembre: 32 h, Octobre: 39 h) n'apparaissent pas. | `captures/US01_CA05_fuseau_haiti.png` |
| **CA-01.06** | Réactivité sans rechargement | `energie_college.csv` | 1. Sur « Toute la période » (97 h / 280,0 L), basculer sur « Octobre 2026 » sans cliquer sur recharger. | Les valeurs basculent instantanément à 43 h et 125,0 L. | `captures/US01_CA06_changement_octobre.png` |
| **CA-01.07** | Rejet de fichier avec colonne manquante | `tests/fixtures/f02_colonne_manquante.csv` | 1. Charger `f02_colonne_manquante.csv`. | Message d'erreur clair indiquant que la colonne `litres_carburant` est manquante et désignant l'en-tête (ligne 1). Aucun total affiché. | `captures/US01_CA07_colonne_manquante.png` |
| **CA-01.08** | Intégrité et lecture seule du fichier source | `energie_college.csv` | 1. Noter l'empreinte SHA-256 du fichier avant test.<br>2. Charger le fichier et naviguer sur les 4 périodes.<br>3. Recalculer l'empreinte SHA-256 avec PowerShell. | Empreinte strictement identique (`320155c7…a84b`). L'interface ne comporte aucun bouton ni champ de saisie permettant d'éditer ou de sauvegarder. | `captures/US01_CA08_lecture_seule.png` |
| **CA-01.09** | Réinitialisation et non-cumul entre fichiers | `f06_aout_septembre.csv` puis `energie_college.csv` | 1. Charger `f06_aout_septembre.csv` (affiche 54 h).<br>2. Charger ensuite `energie_college.csv` sans rafraîchir la page.<br>3. Observer « Toute la période ». | « Toute la période » affiche 97 h et 280,0 L (et non le cumul 54 + 97 = 151 h). | `captures/US01_CA09_reinitialisation_cumul.png` |
| **CA-01.10** | Déduction dynamique des périodes (fichier partiel) | `tests/fixtures/f06_aout_septembre.csv` | 1. Charger `f06_aout_septembre.csv`.<br>2. Ouvrir le sélecteur de périodes. | Exactement 3 choix : « Août 2026 », « Septembre 2026 » et « Toute la période » (Octobre absent). « Toute la période » affiche 54 h et 155,0 L. | `captures/US01_CA10_fichier_partiel.png` |
| **CA-01.11** | Rejet d'une valeur non numérique | `tests/fixtures/f03_valeur_non_numerique.csv` | 1. Charger `f03_valeur_non_numerique.csv`. | Message d'erreur clair indiquant une valeur invalide et désignant la ligne fautive (ligne 3). Aucun total affiché. | `captures/US01_CA11_valeur_non_numerique.png` |
| **CA-02.01a** | Coût estimé Août 2026 | `energie_college.csv` | 1. Sélectionner « Août 2026 ». | Coût affiché = **21 300 gourdes** (sans décimale, espace milliers, RM-01, RM-03, H-02). | `captures/US02_CA01_cout_aout.png` |
| **CA-02.01b** | Coût estimé Septembre 2026 | `energie_college.csv` | 1. Sélectionner « Septembre 2026 ». | Coût affiché = **25 200 gourdes**. | `captures/US02_CA01_cout_septembre.png` |
| **CA-02.01c** | Coût estimé Octobre 2026 | `energie_college.csv` | 1. Sélectionner « Octobre 2026 ». | Coût affiché = **37 500 gourdes**. | `captures/US02_CA01_cout_octobre.png` |
| **CA-02.01d** | Coût estimé Toute la période | `energie_college.csv` | 1. Sélectionner « Toute la période ». | Coût affiché = **84 000 gourdes**. | `captures/US02_CA01_cout_toute_periode.png` |
| **CA-02.02** | Libellé et prix de référence | `energie_college.csv` | 1. Examiner la zone d'affichage du coût. | Présence du libellé « coût estimé » et mention du prix de référence de « 300 gourdes par litre ». | `captures/US02_CA02_libelle_prix_reference.png` |
| **CA-02.03** | Réactivité du coût au changement de période | `energie_college.csv` | 1. Sur « Août 2026 » (21 300 gourdes), sélectionner « Septembre 2026 ». | Le coût passe immédiatement à 25 200 gourdes sans rechargement. | `captures/US02_CA03_changement_cout.png` |
| **CA-02.04** | Fuseau horaire et calcul du coût (Haïti UTC-05) | `energie_college.csv` | 1. Sous fuseau Haïti, vérifier les coûts d'août, septembre et octobre. | Coûts conformes à CA-02.01. Les valeurs fausses du piège P-01 (23 100, 27 000, 33 900 gourdes) n'apparaissent pas. | `captures/US02_CA04_fuseau_cout.png` |
| **CA-02.05** | Mention de prix non officiel | `energie_college.csv` | 1. Observer la mention à proximité du coût estimé. | Présence visible de la mention « prix de référence de l'intendance, pas un prix officiel » (Q-20). | `captures/US02_CA05_mention_officielle.png` |
| **CA-03.01a** | Jour max et égalité Août 2026 | `energie_college.csv` | 1. Sélectionner « Août 2026 ». | Affiche **06/08/2026 (5 h)**. Le 06/08 et le 12/08 sont à égalité à 5 h : le premier chronologiquement est affiché (B-13). | `captures/US03_CA01_jour_max_aout.png` |
| **CA-03.01b** | Jour max et égalité Septembre 2026 | `energie_college.csv` | 1. Sélectionner « Septembre 2026 ». | Affiche **08/09/2026 (5 h)** (égalité entre 08/09, 09/09 et 11/09). | `captures/US03_CA01_jour_max_septembre.png` |
| **CA-03.01c** | Jour max et égalité Octobre 2026 | `energie_college.csv` | 1. Sélectionner « Octobre 2026 ». | Affiche **02/10/2026 (5 h)** (égalité entre 02/10, 05/10, 08/10, 13/10, 15/10 et 16/10). | `captures/US03_CA01_jour_max_octobre.png` |
| **CA-03.01d** | Jour max Toute la période | `energie_college.csv` | 1. Sélectionner « Toute la période ». | Affiche **06/08/2026 (5 h)** (premier des 11 jours à 5 h sur toute la période). | `captures/US03_CA01_jour_max_toute_periode.png` |
| **CA-03.02** | Indépendance de l'ordre du fichier | `tests/fixtures/f01_lignes_melangees.csv` | 1. Charger `f01_lignes_melangees.csv`.<br>2. Vérifier les 4 périodes. | Jours maximaux strictement identiques à CA-03.01 (06/08, 08/09, 02/10, 06/08 à 5 h). Le tri chronologique s'applique. | `captures/US03_CA02_lignes_melangees.png` |
| **CA-03.03** | Période sans aucun fonctionnement | `tests/fixtures/f04_mois_sans_generatrice.csv` | 1. Charger `f04_mois_sans_generatrice.csv`.<br>2. Sélectionner « Août 2026 ». | Affiche le message exact **« Aucun fonctionnement de la génératrice sur la période »** à la place d'une date (Q-05). | `captures/US03_CA03_sans_generatrice.png` |
| **CA-03.04** | Fuseau Haïti et date du jour max | `energie_college.csv` | 1. Sous fuseau Haïti, vérifier les jours max pour chaque période. | Jours conformes à CA-03.01. Les dates décalées d'un jour (05/08, 07/09, 01/10) n'apparaissent pas. | `captures/US03_CA04_fuseau_jour_max.png` |
| **Test-P04** | Contrôle d'arrondi flottant IEEE 754 | `tests/fixtures/f05_decimales.csv` | 1. Charger `f05_decimales.csv`.<br>2. Observer le total des litres. | Affiche **0,3 L** (arrondi à 1 décimale, virgule). L'artefact `0.30000000000000004` n'apparaît pas à l'écran. | `captures/TEST_P04_arrondi_decimales.png` |

---

## 2. Consignes pour le relais R5 (Vérification et Captures)

1. **Environnement de test** :
   - Tester sous Windows, avec le fuseau horaire réglé sur **« (UTC-05:00) Haïti »** (Paramètres Windows > Heure et langue > Date et heure).
   - Tester successivement sous deux navigateurs distincts (par ex. Google Chrome / Edge et Mozilla Firefox), hors connexion Internet.
2. **Exécution des tests** :
   - Tester d'abord `Groupe_01_Cas_01/prototype/version_IA.html` (sans jamais modifier ce fichier).
   - Noter chaque écart constaté dans `travail/journal_ecarts.md`.
   - Seulement si des écarts sont constatés sur les CA du Sprint 01, les règles du client ou les consignes (fiche 04) : créer ensuite `Groupe_01_Cas_01/prototype/index.html` en appliquant les corrections nécessaires pour satisfaire 100% des critères du plan de test. Si `version_IA.html` est conforme (C-09), ne pas créer `index.html` : l'écrire dans `ETAT_PROJET.md`, et R6 le mentionne dans le README (fiche 04 ; rectifié au complément de R4, E-28).
3. **Prise des captures** :
   - Effectuer les captures d'écran de la page sous `index.html` (ou `version_IA.html` si conforme) en veillant à la lisibilité des chiffres et mentions attendus.
   - Enregistrer chaque capture au format PNG dans `Groupe_01_Cas_01/captures/` avec son nommage exact défini dans le tableau ci-dessus.

---

## 3. Résultats d'exécution (R5, 2026-10-18)

**Version testée** : `Groupe_01_Cas_01/prototype/version_IA.html`, intacte (`git diff version-ia` vide).
**Environnement** (écart de procédure E-22) : Kali Linux, fuseau système `America/Port-au-Prince` (décalage de 240 min au 01/09/2026, négatif comme celui d'Haïti : le piège P-01 se manifesterait) ; Chromium 150 en mode headless, piloté par le protocole DevTools (chargement par le vrai `<input type="file">`, choix de la période par l'événement `change`) ; Firefox pour le second navigateur (manuel, par le membre de R5). Script de pilotage conservé hors du dépôt.
**Empreinte du CSV** : `320155c7…a84b` avant et après les tests (`sha256sum`).
**`index.html`** : non créé, car aucun écart n'a été constaté sur les CA du Sprint 01 (C-09, fiche 04).
**Rectificatif (2026-10-18, D-16)** : `index.html` a été créé ensuite, pour l'habillage seulement (script identique à `version_IA.html`). Ses résultats sont au §4 ; ce tableau garde les résultats de R5 sur `version_IA.html`.
**Rectificatif (2026-10-18, R6, E-35)** : les trois photos de l'écran prises sous Firefox (`US01_CA03_liste_periodes.png`, `US01_CA08_lecture_seule.png`, `US01_CA10_fichier_partiel.png`) ont été retirées du livrable par décision de l'équipe (photos prises de biais, peu lisibles). Les observations du membre de R5 restent consignées dans ce tableau ; pour CA-01.03, CA-01.08 et CA-01.10, les captures du livrable sont celles d'`index.html` (§4). Les noms de captures du §1 restent ceux du plan.

| CA | Résultat attendu (oracle) | Observé sur `version_IA` | Statut `version_IA` | Observé sur `index` | Statut final | Capture |
|---|---|---|---|---|---|---|
| CA-01.01 | Page sans donnée, bouton « Choisir un fichier », hors ligne | Bouton visible « Choisir un fichier » ; indicateurs masqués ; seul le libellé fixe « 300 gourdes par litre » ; réseau coupé (émulé) : aucune requête, fonctionnement identique ; Firefox, réseau réellement coupé (membre de R5, 14:13) : page sans donnée, bouton « Choisir un fichier », barre `file:///` | respecté | sans objet | respecté | `US01_CA01_etat_initial.png` (manuelle) |
| CA-01.02 | Sans erreur ; « Toute la période » ; 97 h, 280,0 L | Message de succès ; « Toute la période » ; 97 h ; 280,0 L | respecté | sans objet | respecté | `US01_CA02_chargement_toute_periode.png`, `US01_CA02_firefox_toute_periode.png` (Firefox, hors ligne) |
| CA-01.03 | Exactement 4 choix | « Août 2026 », « Septembre 2026 », « Octobre 2026 », « Toute la période » ; Firefox, hors ligne (membre de R5, 14:18) : liste ouverte, mêmes 4 choix | respecté | sans objet | respecté | `US01_CA03_liste_periodes.png` (photo de l'écran, Firefox ; retirée du livrable, E-35) |
| CA-01.04 | 24 h / 71,0 L ; 30 h / 84,0 L ; 43 h / 125,0 L ; 97 h / 280,0 L | Identique pour les 4 périodes | respecté | sans objet | respecté | `US01_CA04_aout.png`, `_septembre`, `_octobre`, `_toute_periode` |
| CA-01.05 | Totaux de CA-01.04 sous fuseau d'Haïti ; ni 26 h, ni 32 h, ni 39 h | 24 h, 30 h, 43 h (fuseau du navigateur `America/Port-au-Prince`) | respecté | sans objet | respecté | `US01_CA05_fuseau_haiti.png` (montage des 3 mois) |
| CA-01.06 | Toute la période puis Octobre : 43 h, 125,0 L sans rechargement | 43 h ; 125,0 L | respecté | sans objet | respecté | `US01_CA06_changement_octobre.png` |
| CA-01.07 | Message clair, ligne d'en-tête, aucun total | « Erreur à la ligne 1 (en-tête) : la colonne obligatoire « litres_carburant » est absente. » ; indicateurs masqués | respecté | sans objet | respecté | `US01_CA07_colonne_manquante.png` |
| CA-01.08 | Empreinte identique ; aucun moyen de saisir ou d'enregistrer | Empreinte identique avant et après ; 0 champ éditable ; aucun bouton d'enregistrement ni d'export ; vu par le membre de R5 (14:31) : `sha256sum` = `320155c7…a84b` après les essais dans Firefox, page sans champ de saisie | respecté | sans objet | respecté | `US01_CA08_lecture_seule.png` (photo de l'écran, redressée ; retirée du livrable, E-35) |
| CA-01.09 | f06 puis original : 97 h, 280,0 L | 97 h ; 280,0 L (également f04 puis original : 97 h, 280,0 L) | respecté | sans objet | respecté | `US01_CA09_reinitialisation_cumul.png` |
| CA-01.10 | 3 choix ; 54 h et 155,0 L | « Août 2026 », « Septembre 2026 », « Toute la période » ; 54 h ; 155,0 L ; Firefox, hors ligne (membre de R5, 14:20) : liste ouverte avec 3 choix, 54 h, 155,0 L | respecté | sans objet | respecté | `US01_CA10_fichier_partiel.png` (photo de l'écran, Firefox ; retirée du livrable, E-35) |
| CA-01.11 | Message clair, ligne 3, aucun total | « Erreur à la ligne 3 : la valeur de « heures_generatrice » doit être un nombre valide positif ou nul. » ; indicateurs masqués | respecté | sans objet | respecté | `US01_CA11_valeur_non_numerique.png` |
| CA-02.01 | 21 300 ; 25 200 ; 37 500 ; 84 000 gourdes | Identique pour les 4 périodes | respecté | sans objet | respecté | `US02_CA01_cout_aout.png`, `_septembre`, `_octobre`, `_toute_periode` |
| CA-02.02 | Libellé « coût estimé » et 300 gourdes par litre | Carte « Coût estimé » ; « Prix de référence : 300 gourdes par litre » | respecté | sans objet | respecté | `US02_CA02_libelle_prix_reference.png` |
| CA-02.03 | Août puis Septembre : 25 200 gourdes | 25 200 gourdes | respecté | sans objet | respecté | `US02_CA03_changement_cout.png` |
| CA-02.04 | Coûts de CA-02.01 sous fuseau d'Haïti ; ni 23 100, ni 27 000, ni 33 900 | 21 300, 25 200, 37 500 gourdes | respecté | sans objet | respecté | `US02_CA04_fuseau_cout.png` (montage des 3 mois) |
| CA-02.05 | Mention « prix de référence de l'intendance, pas un prix officiel » à côté du coût | Mention présente sous le coût, dans la même carte | respecté | sans objet | respecté | `US02_CA05_mention_officielle.png` |
| CA-03.01 | 06/08/2026 (5 h) ; 08/09/2026 (5 h) ; 02/10/2026 (5 h) ; 06/08/2026 (5 h) | Identique pour les 4 périodes | respecté | sans objet | respecté | `US03_CA01_jour_max_aout.png`, `_septembre`, `_octobre`, `_toute_periode` |
| CA-03.02 | f01 : jours identiques à CA-03.01 | 06/08, 08/09, 02/10, 06/08 (5 h) ; totaux aussi identiques. **Refait au complément de R5 (15:11) avec le nouveau f01** (jours à 5 h dans un ordre non chronologique, E-24), sur un autre poste que celui de R5 : Windows 11 Pro, fuseau système « Haiti Standard Time », Google Chrome 155 sans interface piloté par le protocole DevTools (vrai `<input type="file">`), fuseau du navigateur fixé à `America/Port-au-Prince` par émulation, réseau coupé par émulation, 0 requête réseau ; mêmes valeurs ; les 4 captures sont remplacées | respecté | sans objet | respecté | `US03_CA02_lignes_melangees_aout.png`, `_septembre`, `_octobre`, `_toute_periode` |
| CA-03.03 | f04, Août : « Aucun fonctionnement de la génératrice sur la période » | Message exact (totaux 0 h, 0,0 L, 0 gourdes) | respecté | sans objet | respecté | `US03_CA03_sans_generatrice.png` |
| CA-03.04 | Jours de CA-03.01 sous fuseau d'Haïti ; ni 05/08, ni 07/09, ni 01/10 | 06/08, 08/09, 02/10 (5 h) | respecté | sans objet | respecté | `US03_CA04_fuseau_jour_max.png` (montage des 3 mois) |
| Test-P04 | f05 : 0,3 L (pas 0.30000000000000004) | 0,3 L ; 2 h ; 90 gourdes ; 03/08/2026 (1 h) | respecté | sans objet | respecté | `TEST_P04_arrondi_decimales.png` |

**Contrôles transverses**

| Contrôle | Observé | Statut |
|---|---|---|
| Hors ligne | Réseau coupé par émulation (Chromium) : aucune requête, Septembre = 30 h, 84,0 L, 25 200 gourdes, 08/09/2026 (5 h). Coupure réelle (membre de R5, Firefox, 14:13 à 14:29) : chargement, Toute la période conforme (97 h, 280,0 L, 84 000 gourdes, 06/08/2026 (5 h)), liste des périodes et fichier f06 conformes | respecté |
| Aucune ressource externe | Recherche des URL, `@import`, `fetch(`, `XMLHttpRequest`, `WebSocket`, `url(`, `src=`, `<link` : aucune occurrence ; 0 requête réseau pendant toute la passe | respecté |
| Aucune donnée intégrée | `2026-08-03` absent du source ; à l'ouverture, aucune valeur calculée | respecté |
| Bouton | « Choisir un fichier » dans Chromium et dans Firefox (membre de R5, 14:13) | respecté |
| Lecture seule | Empreinte identique ; aucun champ éditable, aucun export | respecté |
| Hors sprint | Aucune fonction au-delà d'US-01 à US-03 (pas de tableau, de graphique, de stockage local ni d'export) | respecté |
| Rechargement (P-09) | f04 puis original et f06 puis original : 97 h, 280,0 L, 84 000 gourdes | respecté |

---

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

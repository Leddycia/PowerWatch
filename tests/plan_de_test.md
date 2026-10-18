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
   - Créer ensuite `Groupe_01_Cas_01/prototype/index.html` en appliquant les corrections nécessaires pour satisfaire 100% des critères du plan de test.
3. **Prise des captures** :
   - Effectuer les captures d'écran de la page sous `index.html` (ou `version_IA.html` si conforme) en veillant à la lisibilité des chiffres et mentions attendus.
   - Enregistrer chaque capture au format PNG dans `Groupe_01_Cas_01/captures/` avec son nommage exact défini dans le tableau ci-dessus.

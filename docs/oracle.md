# Oracle : résultats attendus sur `energie_college.csv`

> **À quoi sert ce fichier ?** Il donne les valeurs **justes**, calculées par un script de l'IA assistante de R1 **indépendamment de l'IA déléguée et du prototype** (voir « Méthode »), auxquelles on compare la sortie du prototype. C'est la référence des critères d'acceptation, des tests (R5) et des preuves du README (R6).
>
> **Méthode** : valeurs calculées par un script Python déterministe, écrit et exécuté par l'IA assistante du relais R1 (Claude Code, Claude Opus 5.5), sur le fichier original, sans modification, indépendamment de l'IA déléguée et du prototype. Le script n'a pas été conservé dans le dépôt. Une relecture adversariale automatisée les a recalculées sans trouver d'erreur de valeur. Les règles appliquées sont B-12 (coût), B-13 (égalité) et B-14 (formats).
> **Contre-vérification humaine obligatoire** : le relais R2 recalcule **à la main**, à partir du CSV ouvert dans le Bloc-notes ou un tableur **sans enregistrer**, les totaux d'août **et** de septembre (septembre contient le 01/09 et les litres 12.5 et 2.5). Il ne compare à cet oracle qu'**après** son calcul, et le note dans son rapport d'audit.
>
> Empreinte SHA-256 du CSV original, pour vérifier qu'il n'a pas été modifié (B-15) :
> `320155c76969aeb0e05779861b2520a150675f853318d2dfd6592eaf0107a84b`
> Contrôle dans PowerShell, à la racine du dépôt : `(Get-FileHash .\docs\energie_college.csv -Algorithm SHA256).Hash -eq '320155c76969aeb0e05779861b2520a150675f853318d2dfd6592eaf0107a84b'` doit afficher `True` (Get-FileHash affiche l'empreinte en majuscules ; la comparaison `-eq` ignore la casse).
> Si `False` : `git restore docs/energie_college.csv`, puis recontrôler (ne jamais le restaurer depuis le commit initial 478570e, qui l'avait stocké en LF) ; vérifier aussi que `.gitattributes` est présent : il empêche Git de convertir les fins de ligne CRLF du fichier.

---

## 1. Format constaté du fichier

| Élément | Constat | Conséquence à tester |
|---|---|---|
| Lignes | 37 : 1 en-tête et 36 données | Les totaux du §2 portent sur ces 36 jours |
| En-tête | `date,heures_solaire,heures_generatrice,litres_carburant` | Conforme à B-19 |
| Séparateur | Virgule | Conforme à B-18 |
| Fins de ligne | **CRLF** (Windows) | Piège P-02 : l'en-tête se termine par `\r` |
| Fin de fichier | La dernière ligne se termine aussi par CRLF (37 CRLF, 727 octets) ; un découpage sur `/\r?\n/` donne un 38e élément vide | L'ignorer : ce n'est pas une ligne invalide au sens de Q-04 (P-02) |
| Encodage | ASCII pur, sans BOM | Conforme à B-18 |
| Dates | AAAA-MM-JJ, triées, sans doublon, toutes du lundi au vendredi | Ne **pas** se fier à l'ordre du fichier (P-03) |
| Heures | Entiers ; génératrice entre 0 et 5 h | |
| Litres | Entiers (32 lignes) ou décimales en `.5` (4 lignes : 08/09, 15/09, 02/10, 14/10), écrites avec un point dans le fichier | Affichage avec virgule française (Q-01) |
| Jours sans génératrice | 8 jours à 0 h et 0 L | Aucune incohérence entre heures et litres |
| Ratio litres/heure | Entre 2,5 et 3,0 | Normal, l'outil ne doit **rien corriger** (B-15) |

## 2. Valeurs attendues par période

### 2.1 Valeurs brutes

| Période | Jours | Heures génératrice | Litres | Coût (litres × 300) | Jour max (B-13) | Heures du jour max |
|---|---|---|---|---|---|---|
| Août 2026 | 12 | 24 | 71 | 21 300 | 2026-08-06 | 5 |
| Septembre 2026 | 12 | 30 | 84 | 25 200 | 2026-09-08 | 5 |
| Octobre 2026 | 12 | 43 | 125 | 37 500 | 2026-10-02 | 5 |
| **Toute la période** | **36** | **97** | **280** | **84 000** | **2026-08-06** | **5** |

### 2.2 Affichage attendu

Cet affichage suit `travail/decisions.md` : l'hypothèse provisoire Q-01 (litres avec 1 décimale) et les choix de présentation H-01 (dates JJ/MM/AAAA) et H-02 (montants avec espace des milliers).

| Période | Heures génératrice | Litres | Coût estimé | Jour max |
|---|---|---|---|---|
| Août 2026 | 24 h | 71,0 L | 21 300 gourdes | 06/08/2026 (5 h) |
| Septembre 2026 | 30 h | 84,0 L | 25 200 gourdes | 08/09/2026 (5 h) |
| Octobre 2026 | 43 h | 125,0 L | 37 500 gourdes | 02/10/2026 (5 h) |
| Toute la période | 97 h | 280,0 L | 84 000 gourdes | 06/08/2026 (5 h) |

> Si l'hypothèse Q-01 ou un choix H change dans `decisions.md`, seul le **format** de ce tableau change. Les valeurs du §2.1 restent vraies.

## 3. Couverture réelle de chaque période (point Q-08)

| Période | Premier jour | Dernier jour | Jours chargés | Jours à 0 h de génératrice |
|---|---|---|---|---|
| Août 2026 | 03/08/2026 | 18/08/2026 | 12 | 5 (04, 10, 11, 17, 18/08) |
| Septembre 2026 | 01/09/2026 | 16/09/2026 | 12 | 2 (14, 16/09) |
| Octobre 2026 | 01/10/2026 | 16/10/2026 | 12 | 1 (12/10) |
| Toute la période | 03/08/2026 | 16/10/2026 | 36 | 8 |

> Chaque « mois » n'est qu'un **échantillon** de 12 jours ouvrables (B-18), pas un mois complet.
> Hypothèse Q-08 : cette couverture n'est **pas affichée en V1** (non demandée par le client) ; elle est proposée au client dans les points à confirmer du CDC.

## 4. Égalités sur le maximum (règle B-13)

Le maximum vaut **5 h dans chaque période** et il est **toujours atteint par plusieurs jours**. La règle d'égalité est donc testée sur les données réelles.

| Période | Jours à 5 h, dans l'ordre chronologique | Jour à afficher |
|---|---|---|
| Août 2026 | 06/08, 12/08 | **06/08/2026** |
| Septembre 2026 | 08/09, 09/09, 11/09 | **08/09/2026** |
| Octobre 2026 | 02/10, 05/10, 08/10, 13/10, 15/10, 16/10 | **02/10/2026** |
| Toute la période | Les 11 jours ci-dessus | **06/08/2026** |

**Erreurs typiques à reconnaître :**

| Résultat affiché | Diagnostic |
|---|---|
| 12/08, 11/09, 16/10 | L'IA a pris le **dernier** maximum au lieu du premier (comparaison `>=`). |
| 16/10 pour toute la période | Même erreur, appliquée à toute la période. |

## 5. Signature du bug de fuseau horaire (piège P-01)

Si le prototype convertit les dates avec `new Date("AAAA-MM-JJ")` (interprétation en UTC) et qu'il tourne avec un fuseau négatif comme celui d'**Haïti** (UTC-5 ou UTC-4 ; fuseau supposé, car le brief ne nomme aucun pays : Q-09), chaque date recule d'un jour. Le 01/09 bascule alors en août et le 01/10 en septembre : août compte 13 jours, septembre 12 et octobre 11. Les dates affichées à partir de cet objet `Date` ont aussi un jour de moins (02/08/2026 pour 2026-08-03, 31/08/2026 pour 2026-09-01). **Le prototype affiche ces valeurs fausses :**

| Période | Heures (fausses) | Litres (faux) | Coût (faux) | Jour max affiché (faux) |
|---|---|---|---|---|
| Août 2026 | 26 h | 77 L | 23 100 gourdes | 05/08/2026 |
| Septembre 2026 | 32 h | 90 L | 27 000 gourdes | 07/09/2026 |
| Octobre 2026 | 39 h | 113 L | 33 900 gourdes | 01/10/2026 |
| Toute la période | 97 h (inchangé) | 280 L (inchangé) | 84 000 gourdes (inchangé) | 05/08/2026 |

> **Ce bug est invisible quand on teste depuis l'Europe** (fuseau positif). Les tests doivent être faits avec le fuseau Windows **« (UTC-05:00) Haïti »** (fuseau supposé : Q-09), via Paramètres, Heure et langue, Date et heure.

## 6. Détail jour par jour (référence pour l'US-04 ; pour R2, à consulter seulement après le recalcul manuel fait sur le CSV)

Les valeurs « telles que dans le fichier » ne doivent jamais être modifiées par l'outil (B-15). La colonne « Litres affichés » applique Q-01 (1 décimale, virgule).

### Août 2026

| # | Date (fichier) | Date affichée | Heures solaires | Heures génératrice | Litres (fichier) | Litres affichés |
|---|---|---|---|---|---|---|
| 1 | 2026-08-03 | 03/08/2026 | 4 | 3 | 9 | 9,0 |
| 2 | 2026-08-04 | 04/08/2026 | 6 | 0 | 0 | 0,0 |
| 3 | 2026-08-05 | 05/08/2026 | 6 | 4 | 12 | 12,0 |
| 4 | 2026-08-06 | 06/08/2026 | 6 | 5 | 15 | 15,0 |
| 5 | 2026-08-07 | 07/08/2026 | 6 | 2 | 5 | 5,0 |
| 6 | 2026-08-10 | 10/08/2026 | 6 | 0 | 0 | 0,0 |
| 7 | 2026-08-11 | 11/08/2026 | 5 | 0 | 0 | 0,0 |
| 8 | 2026-08-12 | 12/08/2026 | 4 | 5 | 15 | 15,0 |
| 9 | 2026-08-13 | 13/08/2026 | 5 | 2 | 6 | 6,0 |
| 10 | 2026-08-14 | 14/08/2026 | 5 | 3 | 9 | 9,0 |
| 11 | 2026-08-17 | 17/08/2026 | 6 | 0 | 0 | 0,0 |
| 12 | 2026-08-18 | 18/08/2026 | 5 | 0 | 0 | 0,0 |
| | **Total** | | **64** | **24** | **71** | **71,0** |

### Septembre 2026

| # | Date (fichier) | Date affichée | Heures solaires | Heures génératrice | Litres (fichier) | Litres affichés |
|---|---|---|---|---|---|---|
| 13 | 2026-09-01 | 01/09/2026 | 6 | 2 | 6 | 6,0 |
| 14 | 2026-09-02 | 02/09/2026 | 6 | 1 | 3 | 3,0 |
| 15 | 2026-09-03 | 03/09/2026 | 7 | 2 | 5 | 5,0 |
| 16 | 2026-09-04 | 04/09/2026 | 7 | 3 | 9 | 9,0 |
| 17 | 2026-09-07 | 07/09/2026 | 6 | 4 | 10 | 10,0 |
| 18 | 2026-09-08 | 08/09/2026 | 6 | 5 | 12.5 | 12,5 |
| 19 | 2026-09-09 | 09/09/2026 | 6 | 5 | 15 | 15,0 |
| 20 | 2026-09-10 | 10/09/2026 | 6 | 2 | 6 | 6,0 |
| 21 | 2026-09-11 | 11/09/2026 | 6 | 5 | 15 | 15,0 |
| 22 | 2026-09-14 | 14/09/2026 | 6 | 0 | 0 | 0,0 |
| 23 | 2026-09-15 | 15/09/2026 | 5 | 1 | 2.5 | 2,5 |
| 24 | 2026-09-16 | 16/09/2026 | 7 | 0 | 0 | 0,0 |
| | **Total** | | **74** | **30** | **84** | **84,0** |

### Octobre 2026

| # | Date (fichier) | Date affichée | Heures solaires | Heures génératrice | Litres (fichier) | Litres affichés |
|---|---|---|---|---|---|---|
| 25 | 2026-10-01 | 01/10/2026 | 6 | 4 | 12 | 12,0 |
| 26 | 2026-10-02 | 02/10/2026 | 5 | 5 | 12.5 | 12,5 |
| 27 | 2026-10-05 | 05/10/2026 | 4 | 5 | 15 | 15,0 |
| 28 | 2026-10-06 | 06/10/2026 | 6 | 2 | 6 | 6,0 |
| 29 | 2026-10-07 | 07/10/2026 | 6 | 2 | 6 | 6,0 |
| 30 | 2026-10-08 | 08/10/2026 | 7 | 5 | 15 | 15,0 |
| 31 | 2026-10-09 | 09/10/2026 | 6 | 2 | 6 | 6,0 |
| 32 | 2026-10-12 | 12/10/2026 | 5 | 0 | 0 | 0,0 |
| 33 | 2026-10-13 | 13/10/2026 | 5 | 5 | 15 | 15,0 |
| 34 | 2026-10-14 | 14/10/2026 | 6 | 3 | 7.5 | 7,5 |
| 35 | 2026-10-15 | 15/10/2026 | 5 | 5 | 15 | 15,0 |
| 36 | 2026-10-16 | 16/10/2026 | 6 | 5 | 15 | 15,0 |
| | **Total** | | **67** | **43** | **125** | **125,0** |

**Toute la période** : 205 heures solaires, 97 heures de génératrice, 280 litres.

## 7. Informations pour le backlog (non exigées en V1)

- **Graphique par mois (US-05, B-21)** : barres attendues août 24 h, septembre 30 h, octobre 43 h. Octobre s'arrête au 16/10 (Q-14).
- **Part solaire (US-07, B-23)** : **aucune valeur de référence** tant que la formule n'est pas fixée par le client (Q-11). Il ne faut pas en inventer une.

## 8. Fixtures de test (complété par R4)

Le relais R4 a créé les fichiers fictifs de `tests/fixtures/` et consigne ci-dessous, pour chacun, les résultats attendus calculés indépendamment de l'IA déléguée et du prototype (vérifications par calcul exact et script déterministe).

| Fixture | Objet | Résultat attendu | Méthode de calcul |
|---|---|---|---|
| `f01_lignes_melangees.csv` | Mêmes 36 lignes que `energie_college.csv`, dans un ordre aléatoire (B-13, P-03, CA-03.02) | Strictement identique aux §2 et §4 (Août: 24 h / 71,0 L / 21 300 gourdes / 06/08/2026 (5 h) ; Septembre: 30 h / 84,0 L / 25 200 gourdes / 08/09/2026 (5 h) ; Octobre: 43 h / 125,0 L / 37 500 gourdes / 02/10/2026 (5 h) ; Toute la période: 97 h / 280,0 L / 84 000 gourdes / 06/08/2026 (5 h)). | Permutation déterministe des lignes de l'oracle de référence. |
| `f02_colonne_manquante.csv` | En-tête sans `litres_carburant` (Q-04, CA-01.07) | Rejet complet du fichier avec message d'erreur clair désignant la ligne d'en-tête (ligne 1) comme fautive ; aucun total ni indicateur affiché. | Déduction directe de la règle Q-04 et du critère CA-01.07. |
| `f03_valeur_non_numerique.csv` | Valeur non numérique `abc` dans `heures_generatrice` à la ligne 3 (Q-04, CA-01.11) | Rejet complet du fichier avec message d'erreur clair indiquant le numéro de la ligne fautive (ligne 3) ; aucun total affiché. | Déduction directe de la règle Q-04 et du critère CA-01.11. |
| `f04_mois_sans_generatrice.csv` | 8 jours en août 2026 avec 0 h partout (Q-05, CA-03.03) | Totaux : 0 h et 0,0 L ; Coût : 0 gourdes ; Jour max : affichage du message exact « Aucun fonctionnement de la génératrice sur la période ». | Déduction directe de Q-05 et calcul trivial (8 × 0 = 0). |
| `f05_decimales.csv` | 2 jours (0.1 L et 0.2 L) générant un artefact de calcul flottant IEEE 754 (B-14, P-04, Q-01) | Somme brute flottante vérifiée par script : `0.30000000000000004` ; Affichage attendu à l'écran : « 0,3 L » (arrondi à 1 décimale, virgule française) ; Heures : 2 h ; Coût estimé : 0,3 × 300 = 90 gourdes ; Jour max : 03/08/2026 (1 h). | Calcul arithmétique et contrôle d'artefact flottant par script déterministe. |
| `f06_aout_septembre.csv` | En-tête et les 24 lignes d'août et septembre seules (CA-01.09, CA-01.10) | Périodes proposées : exactement « Août 2026 », « Septembre 2026 » et « Toute la période » (Octobre absent) ; « Toute la période » affiche 54 h (24+30) et 155,0 L (71+84) ; Coût estimé : 155 × 300 = 46 500 gourdes ; Jour max : 06/08/2026 (5 h). | Somme exacte des valeurs des §2.1 et §2.2 pour les mois d'août et septembre. |

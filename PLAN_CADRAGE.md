# PowerWatch : plan de cadrage

> **Statut : v1, relais R1 (cadrage).** Les choix structurants sont validés (§11). Aucun livrable n'est encore rédigé et aucune ligne de code n'est écrite.
> Sources analysées : `docs/Consignes_Projet_Final_IA_L3.pdf`, `docs/01_Demande_client.docx`, `docs/energie_college.csv`.
> En cas d'écart, `AGENTS.md`, `docs/` (`brief_client.md`, `consignes.md`, `oracle.md`) et `travail/decisions.md` priment.

---

## 0. Alerte calendrier

L'échéance indiquée dans les consignes est le **dimanche 18 octobre 2026 à 23 h 59** (jour même du relais R1). Le plan est donc découpé en portes de validation courtes (§9). Si une autre date a été annoncée en cours, il faut la confirmer.

---

## 1. Ce que disent les sources

### 1.1 Consignes du projet (identifiants C-xx)

| ID | Consigne |
|---|---|
| C-01 | Livrables : `README.md`, `cahier_des_charges.md`, `product_backlog.md`, `prompts.md`, `prototype/version_IA.html`, `prototype/index.html`, `captures/`, regroupés dans `Groupe_01_Cas_01/`. La fiche `fiche_contribution.pdf` est placée **à côté** de ce dossier, pas dedans. |
| C-02 | Chaque exigence du cahier des charges doit être reliée au brief. **Aucune exigence sans justification dans le brief.** |
| C-03 | La rubrique « Ce qui ne fait pas partie de la première version » contient des décisions du client : on les respecte. |
| C-04 | Les souhaits « plus tard » doivent être classés dans le backlog, avec une justification et une vérification de compatibilité avec les règles du client. |
| C-05 | Si un souhait dépend d'une règle non fixée, on ne l'invente pas : on le signale comme **point à décider**. |
| C-06 | User stories au format « En tant que… je veux… afin de… », avec des critères d'acceptation **observables et vérifiables**, une priorité MoSCoW, un ordre justifié et une section « Sprint 01 » (objectif et US retenues). |
| C-07 | Taille du Sprint 01 : 2 US pour un groupe de 4, 3 US pour un groupe de 5 ou 6. Le sprint livre un incrément utilisable. Le chargement des données ou l'affichage de base fait partie de la **première US**, pas d'une US séparée. |
| C-08 | `prompts.md` contient le prompt de délégation au format **RMTCEV**, avec le CDC et le Sprint 01 en contexte, 2 ou 3 autres prompts importants, et **au moins une proposition de l'IA corrigée ou rejetée**, avec sa raison. |
| C-09 | `version_IA.html` est la première sortie de l'IA, **sans aucune modification**. `index.html` est la version corrigée ; il devient facultatif si `version_IA.html` respecte déjà tous les CA, ce qu'il faut alors indiquer dans le README. |
| C-10 | Le prototype est un fichier HTML autonome : CSS, JS (et données) inclus. |
| C-11 | Il s'ouvre par double-clic, sans Internet, sans serveur et sans compte. |
| C-12 | Pour les cas avec CSV, les données sont chargées par un bouton **« Choisir un fichier »**. Intégrer les données dans la page est un écart qu'il faut signaler et justifier dans `prompts.md`. |
| C-13 | On n'utilise que des données fictives, dans les prompts comme dans le prototype. |
| C-14 | Avant la remise, un membre télécharge le dossier depuis le Drive et teste la page **sur un autre ordinateur**. |
| C-15 | Le README explique comment ouvrir le prototype et quels outils ont été utilisés. Il donne, **pour chaque CA du Sprint 01**, un statut (respecté, non respecté ou partiel) et une capture dans `captures/` comme preuve. |
| C-16 | Soutenance d'environ 15 min : démonstration, puis questions individuelles. **Chaque membre doit comprendre tout le projet.** |
| C-17 | Un Sprint 02 est facultatif. Il doit figurer dans le backlog, être vérifié dans le README et ne compense pas un manque ailleurs. |
| C-18 | Critères de notation : fidélité au besoin, qualité des CA, pertinence des arbitrages, précision des prompts, capacité à vérifier et corriger l'IA. La taille du prototype ne compte pas. |
| C-19 | Remise sur le Drive partagé, au plus tard le dimanche 18 octobre 2026 à 23 h 59. |
| C-20 | Contenu obligatoire du cahier des charges : 5 rubriques (contexte, objectifs et acteurs ; exigences fonctionnelles et non fonctionnelles ; règles métier et contraintes ; périmètre de la V1 et hors périmètre ; points à confirmer ou à décider). |
| C-21 | Objectif : cadrer, confier une tâche précise à l'IA et contrôler son résultat ; il ne s'agit pas de produire l'application la plus complète. |
| C-22 | Travail en groupe, un cas par groupe ; outils d'IA et éditeur au choix. |

> **Tension relevée entre C-10 et C-12.** C-10 dit que « le CSS, le JavaScript et les données sont inclus dans le fichier », tandis que C-12 impose le bouton « Choisir un fichier » pour les cas avec CSV. Lecture retenue : notre cas a un CSV, donc **C-12 prime**. Le CSS et le JS sont dans le fichier, les données sont chargées par l'utilisateur et aucune donnée n'est intégrée dans la page.

### 1.2 Brief client, cas 01 (identifiants B-xx)

| ID | Élément du brief |
|---|---|
| B-01 | Collège Les Palmistes, environ 600 élèves. Le réseau public est irrégulier : l'établissement utilise des panneaux solaires, puis une génératrice diesel en complément. |
| B-02 | Chaque jour ouvrable, le gardien note sur un registre papier les heures solaires, les heures de génératrice et le carburant consommé. |
| B-03 | Chaque semaine, l'intendant recopie le registre dans un CSV. |
| B-04 | La directrice veut un petit tableau de bord pour suivre la consommation de la génératrice et son coût, afin de **préparer le budget** et de **discuter avec le conseil d'administration** de nouveaux panneaux. |
| B-05a | Acteur : la **directrice** consulte le tableau de bord pour suivre la consommation et le coût. |
| B-05b | Acteur : l'**intendant** charge le fichier CSV dans l'outil et vérifie les chiffres. |
| B-05c | Acteur : le **gardien** tient le registre papier ; il n'utilise pas l'outil. |
| B-06 | Attente : charger le CSV fourni par l'intendant. |
| B-07 | Attente : afficher, pour la période choisie, le total des heures de génératrice et le total des litres. |
| B-08 | Attente : afficher le coût estimé du carburant pour la période. |
| B-09 | Attente : choisir un mois (août, septembre ou octobre 2026) ou toute la période. |
| B-10 | Attente : afficher le jour où la génératrice a fonctionné le plus longtemps sur la période choisie. |
| B-11 | Attente : afficher les données dans un tableau, jour par jour. |
| B-12 | Règle : coût estimé = litres × **300 gourdes**. C'est un prix de référence fixé par l'intendance, pas un prix officiel. |
| B-13 | Règle : en cas d'égalité sur le maximum d'heures, on affiche **le premier jour dans l'ordre chronologique**. |
| B-14 | Règle : les montants sont en gourdes, **sans décimale** ; les litres peuvent avoir **une décimale**. |
| B-15 | Règle : l'outil **ne modifie pas** les données du fichier. |
| B-16 | Contrainte : l'outil fonctionne **sans Internet**, sur le PC du bureau de l'intendance. |
| B-17 | Contrainte : aucun compte utilisateur dans la V1. |
| B-18 | Données : 36 jours ouvrables (12 par mois), du 3 août au 16 octobre 2026, séparateur virgule, valeurs sans accents. |
| B-19 | Colonnes : `date` (AAAA-MM-JJ), `heures_solaire`, `heures_generatrice`, `litres_carburant`. |
| B-20.1 | Priorité V1 n° 1 : voir le total des heures de génératrice et des litres consommés pour un mois donné. |
| B-20.2 | Priorité V1 n° 2 : connaître le coût estimé du carburant pour ce mois. |
| B-20.3 | Priorité V1 n° 3 : repérer le jour où la génératrice a le plus fonctionné. |
| B-20.4 | Priorité V1 n° 4 : consulter le détail jour par jour. |
| B-21 | Plus tard : graphique en barres des heures de génératrice par mois. |
| B-22 | Plus tard : comparaison de deux mois côte à côte. |
| B-23 | Plus tard : part des heures solaires par rapport aux heures de génératrice. |
| B-24 | Plus tard : alerte SMS quand la consommation du mois dépasse un seuil. |
| B-25 | Hors V1 : connexion directe à la génératrice ou à un compteur. |
| B-26 | Hors V1 : saisie des données dans l'outil, le CSV restant la seule source. |
| B-27 | Hors V1 : gestion de comptes et de mots de passe. |

### 1.3 Analyse du CSV et résultats de référence (oracle)

**Format constaté** : 37 lignes (1 en-tête et 36 données). Fins de ligne **CRLF**, pas de BOM, ASCII pur, séparateur virgule. Dates triées, sans doublon, toutes des jours de semaine. Les heures sont des entiers. Les litres ont parfois une décimale : 4 lignes en `.5` (08/09, 15/09, 02/10, 14/10 ; point décimal dans le fichier, la virgule n'apparaît qu'à l'affichage : Q-01). Huit jours affichent 0 h de génératrice et 0 L. Aucune incohérence entre heures et litres. Le ratio varie de 2,5 à 3 L/h, ce qui est normal et ne doit pas être « corrigé ».

**Observation importante** : chaque mois n'est **qu'un échantillon** de 12 jours. Août va du 3 au 18, septembre du 1er au 16, octobre du 1er au 16. Les totaux « du mois » ne couvrent donc pas des mois complets. Voir le point Q-08.

**Valeurs attendues** : valeurs calculées par un script Python déterministe, écrit et exécuté par l'IA assistante du relais R1 (Claude Code, Claude Opus 5.5), indépendamment de l'IA déléguée et du prototype ; le script n'a pas été conservé dans le dépôt ; une relecture adversariale automatisée les a recalculées sans trouver d'erreur de valeur ; contre-vérification humaine obligatoire par R2. La référence est `docs/oracle.md` §2.

| Période | Jours | Heures génératrice | Litres | Coût estimé | Jour max (règle B-13) | Ex-aequo à 5 h |
|---|---|---|---|---|---|---|
| Août 2026 | 12 | **24 h** | **71,0 L** | **21 300 gourdes** | **06/08/2026** (5 h) | 06/08, 12/08 |
| Septembre 2026 | 12 | **30 h** | **84,0 L** | **25 200 gourdes** | **08/09/2026** (5 h) | 08/09, 09/09, 11/09 |
| Octobre 2026 | 12 | **43 h** | **125,0 L** | **37 500 gourdes** | **02/10/2026** (5 h) | 02, 05, 08, 13, 15, 16/10 |
| Toute la période | 36 | **97 h** | **280,0 L** | **84 000 gourdes** | **06/08/2026** (5 h) | 11 jours |

Pour référence future (US-07) : il y a 205 heures solaires au total. Le maximum de 5 h est **toujours à égalité** : la règle B-13 sera testée sur les données réelles.

### 1.4 Pièges techniques identifiés (à vérifier dans la sortie de l'IA)

| ID | Piège | Conséquence si l'IA se trompe | Comment le détecter |
|---|---|---|---|
| P-01 | **Fuseau horaire** : `new Date("2026-09-01")` est interprété en UTC. En Haïti (UTC-4/-5 ; fuseau supposé, Q-09), cela donne le 31/08. | Le 01/09 et le 01/10 basculent dans le mois précédent (août 26 h au lieu de 24, septembre 32 h au lieu de 30, octobre 39 h au lieu de 43 ; voir `docs/oracle.md` §5) et les dates affichées sont décalées d'un jour. **Le bug est invisible si l'on teste depuis l'Europe.** | Passer le fuseau Windows sur « (UTC-05:00) Haïti », puis recontrôler l'oracle. |
| P-02 | Fins de ligne CRLF : l'en-tête devient `litres_carburant\r`. La dernière ligne se termine aussi par CRLF (37 CRLF, 727 octets) : un découpage sur `/\r?\n/` donne un 38e élément vide qu'il faut ignorer (ce n'est pas une ligne invalide au sens de Q-04). | La colonne litres est introuvable ou vaut NaN. | Charger le fichier original. |
| P-03 | Égalités : l'IA prend le dernier maximum (`>=`) ou se fie à l'ordre du fichier. | Mauvais jour max. | Charger un CSV aux lignes mélangées (fixture). |
| P-04 | Flottants : une somme de décimales donne `0.30000000000000004`. | Affichage incorrect des litres. | Fixture avec des décimales variées. |
| P-05 | Bibliothèque chargée depuis un CDN (Chart.js, PapaParse, Tailwind…). | Page cassée hors ligne. | Tester hors ligne et rechercher les ressources externes dans le source (voir §6). |
| P-06 | Données CSV intégrées dans la page. | Écart C-12. | Relire le source, puis ouvrir sans charger de fichier : aucune valeur calculée ni donnée du fichier ne doit s'afficher. |
| P-07 | Libellé natif `<input type=file>` (« Choose File » ou « Parcourir… » selon le navigateur). | Le libellé « Choisir un fichier » n'est pas garanti. | Tester sur Chrome ou Edge et sur Firefox. |
| P-08 | Fonctions hors sprint ajoutées spontanément : graphique, export, édition, stockage local, etc. | Périmètre non respecté (C-03, B-15, B-26). | Relecture contre le Sprint 01. **Matière pour le journal des corrections (C-08).** |
| P-09 | Un second chargement ne réinitialise pas l'état. | Données cumulées ou mélangées. | Charger d'abord une fixture aux totaux différents (f04 ou f05), puis le fichier original : les valeurs doivent être exactement celles de l'oracle (toute la période : 97 h, 280,0 L, 84 000 gourdes), sans cumul ni reste de la fixture. |
| P-10 | Cellules éditables ou bouton d'enregistrement. | Violation de B-15 et B-26. | Relecture et test d'intégrité (hash du CSV avant et après). |

---

## 2. Arbitrages proposés

- **A-01 : découpage en user stories.** On suit l'ordre de priorité du client (B-20.1 à B-20.4). Le chargement, le choix de période et l'affichage des totaux forment l'US-01, conformément à C-07.
- **A-02 : contenu du Sprint 01 (validé : groupe de 6, donc 3 US).** Le Sprint 01 comprend US-01 (chargement et totaux), US-02 (coût) et US-03 (jour max), dans l'ordre exact des priorités 1 à 3 du client.
  - Alternative écartée : intégrer le tableau jour par jour dans l'US-01 au titre de « l'affichage de base ». C'est défendable, mais le client classe explicitement le tableau en **4e priorité** ; le remonter contredirait B-20.4.
- **A-03 : MoSCoW.** Les quatre priorités V1 (B-20.1 à B-20.4) sont toutes **Must** pour la release V1, même si le Sprint 01 n'en prend que 3 (groupe de 6, C-07, D-01). L'ordre interne suit le client.
- **A-04 : souhaits « plus tard ».**

| Souhait | MoSCoW proposé | Justification et compatibilité |
|---|---|---|
| B-21 Graphique en barres | **Should** | Sert directement l'objectif « discuter avec le CA » (B-04). Compatible hors ligne s'il est dessiné en SVG ou CSS, **sans bibliothèque externe**. Candidat naturel pour un Sprint 02. |
| B-22 Comparer deux mois | **Could** | Partiellement couvert en changeant de période. Les indicateurs à comparer ne sont pas définis (Q-13). |
| B-23 Part solaire / génératrice | **Could, bloquée** | **La formule n'est pas fixée par le client** (Q-11). Selon C-05, on ne l'invente pas. |
| B-24 Alerte SMS | **Won't (V1)** | **Incompatible** avec B-16 (sans Internet) et C-11 (sans serveur). Elle exige aussi un service tiers, et le seuil n'est pas défini (valeur, unité, destinataire : Q-12). |

---

## 3. Registre des points à décider

**Q = question pour le client** : on ne tranche pas seul, mais on propose un comportement provisoire, marqué comme hypothèse dans le prototype.
**H = choix de présentation de l'équipe** : ce n'est pas une règle métier ; on le documente.

| ID | Question | Recommandation (hypothèse de travail) | Bloquant pour |
|---|---|---|---|
| Q-01 | Format des litres : toujours une décimale (« 71,0 L ») ou au plus une (« 71 L », « 12,5 L ») ? | Toujours 1 décimale, virgule française. C'est non ambigu et facile à vérifier. | US-01, US-04 |
| Q-02 | Liste des mois : figée sur août à octobre 2026 ou déduite du fichier (les CSV sont hebdomadaires) ? | Déduite du fichier. Sur le CSV fourni, elle donne exactement les 3 mois du brief. | US-01 |
| Q-03 | Période affichée par défaut après chargement ? | « Toute la période » : un résultat est visible immédiatement. | US-01 |
| Q-04 | Fichier invalide (colonne manquante, valeur non numérique ou négative, date invalide, doublon) : rejet complet ou lignes ignorées ? | **Rejet complet**, avec un message qui cite la ligne fautive. Ignorer des lignes reviendrait à modifier silencieusement les données (B-15). | US-01 |
| Q-05 | Période sans aucune heure de génératrice : quel « jour max » afficher ? | Message « Aucun fonctionnement de la génératrice sur la période ». Le cas n'existe pas dans le CSV fourni. | US-03 |
| Q-06 | Prix de 300 gourdes : constante, ou modifiable par l'intendance ? | Constante en V1 (B-12). Le rendre modifiable n'est pas demandé : à poser comme question pour plus tard. | US-02 |
| Q-07 | Arrondi du coût si des litres avaient plus d'une décimale ? | Arrondi à la gourde la plus proche. Le cas ne se présente pas avec une seule décimale, car ×300 donne toujours un entier. | US-02 |
| Q-08 | Faut-il rappeler la couverture réelle de la période (« 12 jours, du 03/08 au 18/08 ») ? | Non en V1 (non demandé par le client) ; à proposer au client dans les points à confirmer du CDC (statut provisoire). | US-01 |
| Q-09 | Dans quel pays est le collège ? Quels navigateur, système et fuseau sur le PC de l'intendance ? | Tester Edge/Chrome et Firefox, avec le fuseau Haïti (le brief ne nomme aucun pays ; Haïti est supposé d'après les gourdes). | Tests |
| Q-10 | Outil qui produit le CSV : un Excel français exporte avec `;` et un BOM ? | En V1, seul le format décrit (virgule) est accepté ; tout autre format produit un message clair. | US-01 |
| Q-11 | Formule de la « part solaire » : hs/(hs+hg) ? hs/hg ? Par jour ou en cumul ? En % ou en graphique ? | Aucune : décision du client. | US-07 |
| Q-12 | Alerte : seuil (valeur, unité en litres, heures ou gourdes), destinataire, canal possible sans Internet ? | Aucune : Won't en V1. | US-08 |
| Q-13 | Comparaison de deux mois : quels indicateurs ? | Aucune. | US-06 |
| Q-14 | Graphique : afficher octobre, partiel, tel quel ? | Oui, avec une mention « données au 16/10 ». À confirmer. | US-05 |
| H-01 | Format des dates | JJ/MM/AAAA | Tout |
| H-02 | Format des montants | « 21 300 gourdes » (espace comme séparateur des milliers) | US-02 |
| H-03 | Langue de l'interface | Français | Tout |
| H-04 | Libellés des périodes | « Août 2026 », « Septembre 2026 », « Octobre 2026 », « Toute la période » | US-01 |
| H-05 | Bouton de chargement | Libellé personnalisé, exactement « Choisir un fichier » (P-07) | US-01 |
| H-06 | Acteur de l'US-01 | La directrice (B-05a, B-20.1) ; le chargement par l'intendant figure dans les CA (C-07) | US-01 |

H-01 à H-06 : proposition de l'IA (R1), validée par Leddycia à la relecture humaine du 2026-10-18 (`travail/decisions.md` §3). Les Q-xx restent provisoires.

---

## 4. Ébauche du Product Backlog

> Ce n'est pas encore `product_backlog.md`. Cette ébauche sert à valider la structure. Les CA définitifs seront rédigés à l'étape 2.

| Ordre | ID | User story (résumé) | Acteur | MoSCoW | Sources |
|---|---|---|---|---|---|
| 1 | US-01 | Charger le CSV et voir, pour un mois ou toute la période, le total des heures de génératrice et des litres | Directrice (chargement fait par l'intendant) | Must | B-04 à B-07, B-09, B-14 à B-19, B-20.1 |
| 2 | US-02 | Voir le coût estimé du carburant pour la période choisie | Directrice | Must | B-04, B-08, B-12, B-14, B-20.2 |
| 3 | US-03 | Repérer le jour où la génératrice a le plus fonctionné sur la période | Directrice | Must | B-10, B-13, B-20.3 |
| 4 | US-04 | Consulter le tableau jour par jour pour vérifier les chiffres | Intendant | Must | B-05b, B-11, B-14, B-15, B-20.4 |
| 5 | US-05 | Graphique en barres des heures de génératrice par mois | Directrice | Should | B-04, B-21 |
| 6 | US-06 | Comparer deux mois côte à côte | Directrice | Could | B-22 (Q-13) |
| 7 | US-07 | Part des heures solaires et de génératrice | Directrice | Could, bloquée | B-23 (Q-11) |
| 8 | US-08 | Alerte SMS au-delà d'un seuil | Directrice | Won't (V1) | B-24, en conflit avec B-16 et C-11 |

**Sprint 01 retenu : US-01, US-02 et US-03.** US-04 à US-08 restent au backlog. US-04 et US-05 sont les candidates d'un éventuel Sprint 02, facultatif.

**Esquisse des CA du Sprint 01** (à affiner) :

- **US-01** (même numérotation que `agents/02_product_owner.md`)
  - CA-01.01 : Double-clic sur le fichier, hors ligne : la page s'ouvre avec un bouton « Choisir un fichier » ; aucune valeur calculée ni donnée du fichier n'est affichée avant le chargement (les libellés fixes, comme le prix de référence de 300 gourdes/L, sont permis).
  - CA-01.02 : Après le chargement d'`energie_college.csv`, aucun message d'erreur n'apparaît et les totaux de la période par défaut, « Toute la période » (Q-03), s'affichent.
  - CA-01.03 : Le sélecteur propose exactement « Août 2026 », « Septembre 2026 », « Octobre 2026 » et « Toute la période » (B-09, H-04 ; liste déduite du fichier : Q-02).
  - CA-01.04 (format des litres : hypothèse Q-01) : Août : 24 h et 71,0 L ; septembre : 30 h et 84,0 L ; octobre : 43 h et 125,0 L ; toute la période : 97 h et 280,0 L.
  - CA-01.05 (fuseau supposé : Q-09) : avec le fuseau Windows « (UTC-05:00) Haïti », les valeurs de CA-01.04 sont identiques (le 01/09 est compté en septembre).
  - CA-01.06 : Changer de période met à jour les totaux sans recharger le fichier.
  - CA-01.07 (hypothèse Q-04) : un fichier à l'en-tête incorrect affiche un message d'erreur clair, et aucun total.
  - CA-01.08 : l'empreinte SHA-256 du CSV est identique avant et après utilisation ; aucune fonction ne permet de modifier une valeur.
- **US-02**
  - CA-02.01 : Le coût est affiché sans décimale : 21 300, 25 200, 37 500 et 84 000 gourdes.
  - CA-02.02 : Le libellé indique « coût estimé » et le prix de référence de 300 gourdes/L.
  - CA-02.03 : Le coût suit la période choisie.
- **US-03**
  - CA-03.01 : Le jour affiché est le 06/08, le 08/09, le 02/10, ou le 06/08 pour toute la période, avec 5 h.
  - CA-03.02 : Le résultat est identique avec le fichier aux lignes mélangées.
  - CA-03.03 : Sur une période sans heure de génératrice, le message « Aucun fonctionnement de la génératrice sur la période » s'affiche (Q-05, fixture f04).

**Objectif du Sprint 01, en une phrase :** « L'intendant charge le CSV et la directrice voit immédiatement, pour un mois ou pour toute la période, combien d'heures la génératrice a tourné, combien de litres elle a consommés, ce que cela coûte et quel jour elle a le plus fonctionné. »

---

## 5. Stratégie de délégation à l'IA (étapes 3 et 4)

1. **Deux usages de l'IA, à ne pas mélanger.**
   - L'**IA assistante** aide au cadrage (CDC, backlog, tests). Elle utilise les fichiers d'agents (§8).
   - L'**IA déléguée** produit `version_IA.html`. Elle doit tourner dans une **session neuve et vierge**, qui ne reçoit que le prompt RMTCEV avec le CDC et le Sprint 01. Sinon, `prompts.md` ne refléterait pas réellement ce qui a produit la sortie. Par exemple, Claude Code ou Codex lancés dans le dépôt liraient automatiquement `AGENTS.md`.
   - Concrètement, le relais 4 lance cette session **hors du dépôt** (D-09) : de préférence une IA web dans une conversation temporaire (ou nouvelle), mémoire et instructions personnalisées du compte désactivées, hors de tout Projet, Gem ou GPT personnalisé, sans autre pièce jointe que le prompt. En ligne de commande, uniquement `claude --safe-mode` lancé dans un dossier temporaire vide hors du dépôt (il désactive CLAUDE.md, règles, skills, plugins et hooks). Codex, Gemini CLI ou Antigravity CLI seulement si aucun fichier d'instructions global n'existe (`~/.codex/AGENTS.md`, `~/.gemini/GEMINI.md`). Raison : une CLI ouverte dans un dossier vide charge quand même les instructions globales de l'utilisateur (`~/.claude/CLAUDE.md`, `~/.claude/rules/`, `~/.codex/AGENTS.md`). Noter le mode exact dans `prompts.md` §1. Si la CLI écrit elle-même le fichier, le copier tel quel vers `version_IA.html` et garder la transcription dans `travail/brut/`. Si l'IA pose une question au lieu de livrer, répondre uniquement « Applique les hypothèses du cahier des charges et livre le fichier complet. » et consigner l'échange dans `prompts.md` §1.
2. **Exécution unique et traçable.** Le prompt final est écrit dans `Groupe_01_Cas_01/prompts.md` §1 et commité **avant** la délégation ; c'est ce texte, et lui seul, qui est collé. On enregistre la réponse brute complète dans `travail/brut/`. On extrait le HTML **tel quel** dans `prototype/version_IA.html`. Avant le commit, on contrôle que le fichier est identique au bloc HTML de la réponse brute : `git diff --no-index --ignore-cr-at-eol <bloc extrait dans un fichier temporaire hors dépôt> <version_IA.html>` doit être vide (l'extraction est fidèle). Puis on **commite immédiatement** et on pose le tag annoté `version-ia` : le tag prouve l'absence de modification après le commit. On note l'outil, le modèle, la date et l'heure. Commandes (Git Bash) :
   ```
   git add <version_IA.html> <prompts.md> travail/brut/ && git commit -m "feat(proto): version_IA brute produite par <outil/modèle>" && git tag -a version-ia -m "version_IA brute (C-09)" && git push origin main --follow-tags
   git ls-remote --tags origin
   ```
3. **Structure RMTCEV.** Hypothèse retenue par l'équipe : **R**ôle, **M**ission, **T**âches, **C**ontexte/Contraintes, **E**xemples, **V**alidation. Si un membre retrouve la définition exacte dans le support de cours, elle remplace l'hypothèse avant le relais 4.
4. **Ce que le prompt de délégation doit verrouiller :**
   - fichier HTML unique et hors ligne, sans CDN ;
   - bouton « Choisir un fichier », aucune donnée intégrée ;
   - règles B-12 à B-15 ;
   - frontière de périmètre : implémenter **uniquement** les US du Sprint 01 ;
   - format de sortie : un seul bloc HTML complet ;
   - « Exemples » : l'en-tête et 4 lignes représentatives du CSV (point décimal dans le fichier, virgule à l'affichage : Q-01 ; fins de ligne CRLF), données comme exemples de format (« Ces lignes illustrent le format : n'écris aucune donnée dans la page, les données viennent uniquement du fichier choisi par l'utilisateur (C-12). »), et les valeurs attendues de `docs/oracle.md` §2, qui servent à l'auto-vérification.
5. **Choix à trancher (D-10) : signaler ou non les pièges P-01 à P-10 dans le prompt.** Recommandation : y mettre **les règles et les valeurs attendues**, pas les solutions d'implémentation. Le prompt reste précis, et les vrais écarts de l'IA alimentent honnêtement le journal des corrections.
6. **Journaux tenus au fil de l'eau, hors livrable :**
   - `travail/journal_prompts.md` : tous les prompts significatifs, sauf le prompt RMTCEV, qui reste dans `prompts.md` §1 (pas de JP-xx) ; on en sélectionnera 2 ou 3 pour `prompts.md` ;
   - `travail/journal_ecarts.md` : pour chaque proposition de l'IA, ce qui a été observé, le CA concerné, la décision (corrigé ou rejeté), la raison et le commit.

---

## 6. Plan de vérification

- **Matrice CA → test → preuve.** Chaque CA a une procédure, un résultat attendu (issu de l'oracle) et une capture nommée selon la convention (par exemple `captures/US01_CA04_aout.png`).
- **Fixtures fictives** dans `tests/fixtures/` :
  - `f01_lignes_melangees.csv` : mêmes données, ordre aléatoire. Teste B-13 et P-03.
  - `f02_colonne_manquante.csv` : teste Q-04.
  - `f03_valeur_non_numerique.csv` : teste Q-04.
  - `f04_mois_sans_generatrice.csv` : teste Q-05.
  - `f05_decimales.csv` : petit fichier (en-tête et quelques lignes) dont un même mois contient des litres `0.1` et `0.2` écrits avec un point décimal, comme dans le CSV original (la virgule n'apparaît qu'à l'affichage, Q-01). R4 vérifie par script que la somme brute présente un artefact de flottant (par exemple `0.30000000000000004`) ; attendu à l'écran : valeur arrondie à 1 décimale. Teste B-14 et P-04.
- **Contrôles systématiques :**
  - fuseau Windows « (UTC-05:00) Haïti » (P-01) ;
  - hors ligne (B-16, C-11) : débrancher le câble Ethernet ET activer le mode avion, vérifier dans le panneau rapide (Win+A) que le Wi-Fi est coupé ; contrôle : https://example.com doit afficher une erreur dans chaque navigateur de test. Le hors-ligne se fait en fin de passe (les IA de test ont besoin d'Internet) : couper le réseau, rouvrir la page par double-clic, charger le CSV, vérifier une période, capturer, rétablir le réseau ;
  - empreinte du CSV avant et après (B-15), en PowerShell à la racine du dépôt : `(Get-FileHash .\docs\energie_college.csv -Algorithm SHA256).Hash -eq '320155c76969aeb0e05779861b2520a150675f853318d2dfd6592eaf0107a84b'` doit afficher `True` (Get-FileHash affiche en majuscules ; la comparaison `-eq` ignore la casse). Si `False` : `git restore docs/energie_college.csv` puis recontrôler ; vérifier que `.gitattributes` est présent ;
  - double-clic depuis l'Explorateur (`file://`) ;
  - au moins deux navigateurs (Q-09) ;
  - recherche des ressources externes dans le source : tolérer tout espace de noms `http://www.w3.org/…` (svg, xlink, xhtml) ; rechercher aussi `//`, `@import`, `url(`, `fetch(`, `XMLHttpRequest`, `src=`. En PowerShell : `Select-String -Path <fichier> -Pattern '(https?:)?//(?!www\.w3\.org/)[a-z0-9.-]+\.[a-z]{2,}|@import|fetch\(|XMLHttpRequest|WebSocket'`.
- **Test final sur un autre PC**, après téléchargement depuis le Drive (C-14).

---

## 7. Organisation de l'équipe : course de relais (6 personnes × 1 h)

**Principe validé par l'équipe :**

- les membres travaillent **l'un après l'autre**, avec **1 h chacun** ;
- chacun commence par **auditer** le travail du relais précédent, avec son IA, puis le **poursuit ou l'améliore** sans dépasser les consignes ;
- à la fin, il **passe la main** au suivant de façon formalisée.

Chaque membre audite ainsi au moins un livrable qu'il n'a pas écrit, ce qui prépare la soutenance (C-16).

### 7.1 Répartition des relais

| Relais | Porte | Audit d'entrée (travail du relais précédent) | Mission du relais | Fiche d'agent |
|---|---|---|---|---|
| **R1** (cadrage, fait) | G0 et G1 | Aucun | Plan, registre des décisions, `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, fiches `agents/`, transcriptions B-xx et C-xx, oracle, `ETAT_PROJET.md`, journaux | Aucune |
| **R2** | G2 | Socle : les transcriptions sont-elles fidèles au docx et au pdf ? Les totaux d'août ET de septembre sont-ils recalculés à la main à partir du CSV (ouvert sans enregistrer), avant toute comparaison avec l'oracle ? | `cahier_des_charges.md` et sa matrice de traçabilité | `01_analyste_cdc.md` |
| **R3** | G3 | CDC : chaque exigence est-elle reliée à un B-xx ? Rien n'est-il inventé ? Les points à décider sont-ils reportés ? | `product_backlog.md` : 8 US avec leurs CA (chiffrés pour le Sprint 01), MoSCoW, ordre, Sprint 01 | `02_product_owner.md` |
| **R4** | G4 | Backlog : les CA sont-ils vérifiables ? Le Sprint 01 compte-t-il bien 3 US ? | Prompt RMTCEV, écrit dans `prompts.md` §1 et commité avant la délégation ; exécution unique **en session vierge** ; `version_IA.html` commité et tagué (tag annoté `version-ia`) ; `tests/plan_de_test.md` et fixtures | `03_prompt_engineer.md` |
| **R5** | G5 | `version_IA.html` : passe complète de la matrice de tests (oracle, fuseau Haïti, hors ligne, hash) | `journal_ecarts.md`, corrections dans `index.html`, nouvelle passe de tests, **captures** de la version finale | `04_developpeur.md` et `05_verificateur.md` |
| **R6** | G6 et G7 | `index.html` : nouvelle passe rapide des CA ; cohérence globale des livrables | README (statuts et preuves), finalisation de `prompts.md` (2 ou 3 prompts et corrections), `fiche_contribution.pdf`, remise prête dans le dépôt, téléversée sur le Drive par Leddycia (D-13), **test sur un autre PC**, fiche de soutenance | `06_finalisation_soutenance.md` |

> Si un relais déborde, il **passe quand même la main à l'heure prévue** : il indique dans `ETAT_PROJET.md` ce qui reste à faire, et le relais suivant le reprend en priorité. Le Sprint 02, facultatif, n'est envisagé que si G7 est assuré.
>
> **Budgets horaires.** Par défaut, 10 min de démarrage, 40 min de mission et 10 min de passation (`AGENTS.md` §8). Les fiches fixent les exceptions : R2 consacre 0 à 15 min au démarrage et à l'audit (fiche 01) ; R5 enchaîne les fiches 05 et 04 sur 60 min, avec 5 min de démarrage (fiche 05) ; R6 suit la « Procédure (1 h) » de la fiche 06. **R6 démarre au plus tard à 22 h 00.**

### 7.2 Protocole de démarrage (chaque relais, environ 10 min)

0. Prérequis, une seule fois avant son premier créneau : voir `ETAT_PROJET.md` §0 (invitation GitHub, Git for Windows, identité Git avec adresse noreply, `git clone https://github.com/Leddycia/PowerWatch.git`).
1. **L'humain** lance `git pull`, puis `git fetch --tags` et `git tag -l`, avant d'ouvrir son IA : les tags des relais précédents doivent apparaître.
2. Ouvrir son IA :
   - **dans le dépôt** pour Claude Code, Codex, Gemini CLI ou Antigravity CLI, qui chargent automatiquement `AGENTS.md`, `CLAUDE.md` ou `GEMINI.md` (pour un compte Google personnel, Gemini CLI est remplacé par Antigravity CLI : voir §8.1 et `GEMINI.md`). Contrôle commun de chargement : demander « Cite mot pour mot la règle RG-08 d'AGENTS.md » ;
   - **pour une IA web**, téléverser le kit décrit dans `AGENTS.md` §13, qui fait foi.
3. Lancer le **prompt d'amorçage standard** d'`AGENTS.md` §14, copié tel quel.
4. **Le membre valide** l'audit et le plan de l'IA. C'est lui qui est responsable : le critère C-18 évalue la capacité humaine à vérifier. Avant cette validation, les commandes en lecture seule de l'audit (`git log`, `git status`, `git diff`, `git show`, `git tag -l`, `Get-FileHash`) sont autorisées ; seules les écritures (fichiers, `git add`, `commit`, `tag`, `push`) attendent la validation.

### 7.3 Protocole de passation (chaque relais, environ 10 min)

> **Mise à jour (D-14)** : la passation est automatisée ; **seul `agents/00_protocole_relais.md` §4 fait foi** (ordre des étapes, blocs Git A et B, tag, push). Le membre dit « fin de notre relais » ; pendant le relais, l'IA tient le journal de bord de `ETAT_PROJET.md` §8. Les points ci-dessous n'en donnent que le principe.

1. Mettre à jour **`ETAT_PROJET.md`**, le témoin du relais : porte atteinte, ce qui est fait, ce qui reste, points ouverts, décisions prises, mission du relais suivant.
2. Compléter le rapport d'audit `travail/audits/RX_audit.md`, créé au démarrage : constats, corrections, points remontés, copie du journal de bord.
3. Commit, tag **annoté** `relais-X` et push : blocs A (contrôle) et B (commit, tag, push), lancés séparément (protocole §4, étape 7). Les tags sont toujours annotés : un tag léger n'est pas envoyé par `--follow-tags`.
4. Envoyer au sous-groupe le message de passation (modèle : `agents/00_protocole_relais.md` §5.4 ; l'IA le prépare à « fin de notre relais ») : « Relais X terminé, porte GX atteinte, à toi : [mission], points d'attention : […] ».

### 7.4 Règles d'audit (anti-dérive)

- **On améliore, on ne réécrit pas.** Un relais ne refait pas le livrable précédent. Il corrige des points précis et consigne chaque correction dans son rapport d'audit.
- **Désaccord avec une décision antérieure** : on l'inscrit dans `travail/decisions.md` (statut « contesté », avec la raison) au lieu de la changer en silence.
- **`version_IA.html` n'est jamais modifié** par aucun relais. Un audit qui y trouve un défaut l'inscrit dans `journal_ecarts.md`.
- **Aucun relais n'ajoute** de fonctionnalité, d'exigence ou de fichier livrable que les consignes ou le brief ne justifient pas.

---

## 8. Fichiers d'agents multi-IA

### 8.1 Principe : une seule source de vérité

- **`AGENTS.md`** est la référence complète. Codex le lit nativement ; Copilot, Cursor et d'autres le reconnaissent aussi.
- **`CLAUDE.md`** importe `@AGENTS.md` et n'ajoute que les spécificités de Claude Code.
- **`GEMINI.md`** importe `@./AGENTS.md` (syntaxe d'import de Gemini CLI) et n'ajoute que les spécificités de Gemini. Depuis le 18/06/2026, Gemini CLI n'est plus servi aux comptes personnels (gratuit, Google One, Google AI Pro et Ultra) : il est remplacé par Antigravity CLI, qui lit directement `AGENTS.md` et `GEMINI.md` à la racine (limite de 24 000 octets par fichier) ; la syntaxe `@fichier` n'y insère pas le contenu, et `/memory show` et `context.fileName` ne s'y appliquent pas. Gemini CLI reste utilisable avec une clé API payante ou Code Assist Standard/Enterprise : l'import `@./AGENTS.md`, `/memory show` et `context.fileName` restent alors valables (`.gemini/settings.json` est ignoré dans un dossier non approuvé). Détails et sources : `GEMINI.md`.
- **Membres qui utilisent une IA web** (ChatGPT ou Gemini dans le navigateur) : un « kit copier-coller », décrit dans `AGENTS.md` §13.
- On évite ainsi trois copies qui divergent.

### 8.2 Arborescence cible

```
powerwatch/                         dépôt Git = espace de travail
├── AGENTS.md                       référence unique pour toutes les IA
├── CLAUDE.md                       @AGENTS.md + spécificités Claude
├── GEMINI.md                       @./AGENTS.md + spécificités Gemini
├── ETAT_PROJET.md                  témoin du relais : où on en est, qui suit, quoi faire
├── PLAN_CADRAGE.md                 ce document
├── agents/                         fiches de rôle, indépendantes de l'outil
│   ├── 00_protocole_relais.md      protocole de relais : journal de bord, « fin de notre relais » (D-14)
│   ├── 01_analyste_cdc.md
│   ├── 02_product_owner.md
│   ├── 03_prompt_engineer.md
│   ├── 04_developpeur.md
│   ├── 05_verificateur.md
│   └── 06_finalisation_soutenance.md
├── docs/
│   ├── 01_Demande_client.docx      original (lecture seule)
│   ├── Consignes_Projet_Final_IA_L3.pdf
│   ├── energie_college.csv         original (lecture seule)
│   ├── brief_client.md             transcription fidèle, numérotée B-xx
│   ├── consignes.md                transcription fidèle, numérotée C-xx
│   └── oracle.md                   valeurs attendues (son §2)
├── travail/                        hors livrable
│   ├── decisions.md                registre Q/H/D avec statut
│   ├── journal_prompts.md
│   ├── journal_ecarts.md
│   ├── brut/                       réponse brute de l'IA déléguée (preuve)
│   └── audits/                     R2_audit.md … R6_audit.md
├── tests/
│   ├── plan_de_test.md
│   └── fixtures/*.csv
└── Groupe_01_Cas_01/               LIVRABLE exact, copié tel quel sur le Drive
    ├── README.md
    ├── cahier_des_charges.md
    ├── product_backlog.md
    ├── prompts.md
    ├── prototype/
    │   ├── version_IA.html
    │   └── index.html
    └── captures/
```

**Pourquoi ces transcriptions `.md` ?** Plusieurs IA en ligne de commande lisent mal les `.docx` et les `.pdf`. Avec des transcriptions numérotées, **toutes les IA citent les mêmes identifiants B-xx et C-xx**, ce qui sert directement la traçabilité exigée par C-02.

### 8.3 Contenu prévu d'`AGENTS.md`

1. Mission, cas 01 et échéance.
2. Hiérarchie des sources : consignes et brief, puis registre des décisions, puis CDC, puis backlog, puis prototype.
3. **Règles d'or non négociables :**
   - ne rien inventer : toute exigence (EF, ENF, RM) et toute US cite au moins un B-xx ; une obligation qui ne vient que des consignes est une contrainte du projet (CT-xx) qui cite son C-xx ; un CA se rattache à son US et, s'il dépend d'une hypothèse, cite la Q-xx ; sans source, on ne l'écrit pas ;
   - respecter le hors périmètre (B-25 à B-27) ;
   - données du cas fictives uniquement, dans les prompts et dans le prototype (C-13) ; les prénoms et noms des membres sont permis dans `ETAT_PROJET.md`, les journaux, le README et la fiche de contribution (C-01) ; aucune autre donnée personnelle réelle ;
   - ne jamais modifier les originaux de `docs/` (.docx, .pdf, CSV) ; les transcriptions ne se corrigent que pour une erreur de transcription, signalée dans l'audit ;
   - **ne jamais toucher `version_IA.html` après son commit** ;
   - prototype en un seul fichier, hors ligne, sans données intégrées ;
   - n'implémenter aucune US hors du sprint courant ;
   - consigner chaque écart de l'IA et chaque prompt significatif.
4. Glossaire : période, jour ouvrable, coût estimé, jour max, gourdes, etc.
5. Règles métier R-xx, chacune avec sa source B-xx.
6. Oracle (valeurs attendues).
7. Arborescence et propriétaire de chaque fichier.
8. Workflow, portes de validation (§9), **protocoles de démarrage et de passation** (§7.2 et §7.3), prompt d'amorçage standard, modèle de message de passation, kit web par relais.
9. Definition of Done par livrable.
10. Conventions : identifiants, nommage des captures, commits au format conventionnel en français.
11. Pièges connus P-01 à P-10.
12. Ce qu'une IA ne doit **jamais** faire dans ce dépôt.

### 8.4 Gabarit commun des fiches de rôle

Chaque fiche contient :

- rôle, objectif et relais concerné ;
- **checklist d'audit d'entrée** du livrable précédent ;
- entrées (fichiers à lire) ;
- sorties (fichier, format, emplacement) ;
- règles propres au rôle ;
- procédure pas à pas, découpée pour tenir dans 1 h ;
- checklist de sortie (DoD) ;
- interdits ;
- prompt d'amorçage prêt à copier ;
- ce qu'il faut écrire dans `ETAT_PROJET.md` au moment de passer la main.

`04_developpeur.md` précise qu'il sert **uniquement aux corrections d'`index.html`**, jamais à produire `version_IA.html`. Les fiches 04 et 05 forment ensemble la fiche de R5 : l'audit et la section `ETAT_PROJET.md` sont dans la fiche 05.

---

## 9. Workflow et portes de validation

| Porte | Contenu | Critère de passage |
|---|---|---|
| G0 Cadrage | Ce plan, réponses aux questions bloquantes, registre des décisions | Équipe d'accord sur A-01 à A-04 et sur les hypothèses Q/H |
| G1 Socle | `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `agents/*`, transcriptions, oracle, `ETAT_PROJET.md` | L'IA de R2 cite correctement B-xx et C-xx dès l'amorçage |
| G2 CDC | `cahier_des_charges.md` | 100 % des exigences (EF, ENF, RM) tracées vers un B-xx, contraintes CT-xx vers leur C-xx ; points à décider reportés |
| G3 Backlog | `product_backlog.md` avec le Sprint 01 | Chaque US a des CA observables et vérifiables ; ceux du Sprint 01 sont chiffrés grâce à l'oracle ; ceux d'US-07 et US-08 renvoient à Q-11 ou Q-12 (« valeurs à compléter après réponse du client ») |
| G4 Délégation | Prompt RMTCEV écrit dans `prompts.md` §1 et commité avant la délégation, relu par le membre de R3 (joignable par message entre la 20e et la 30e minute de R4 ; sans réponse en 5 min, R4 délègue quand même et écrit « relu par un seul membre » dans `prompts.md` §1 et `ETAT_PROJET.md`) ; exécution unique | `version_IA.html` commité brut, tag annoté `version-ia` poussé |
| G5 Vérification | Tests, `journal_ecarts.md`, `index.html` | Tous les CA du Sprint 01 « respectés », ou statut justifié |
| G6 Documentation | README, captures, `prompts.md` final | Un statut et une preuve pour chaque CA |
| G7 Remise | Copie sur le Drive, test sur un autre PC, `fiche_contribution.pdf` | Déposé **avant 23 h 59** |
| G8 Soutenance | Questions-réponses croisées (agent coach) | Chaque membre explique toutes les parties |

Les portes sont franchies **séquentiellement**, un relais à la fois (§7.1). Avec 6 relais d'une heure, il faut environ 6 h de travail effectif plus les transitions. Le relais 1 doit donc démarrer au plus tôt, et chaque relais garde une marge de 10 min pour la passation.

---

## 10. Risques

| Risque | Impact | Parade |
|---|---|---|
| Échéance le 18/10/2026 à 23 h 59 | Critique | Portes courtes ; Sprint 02 uniquement si G7 est assuré |
| Relais séquentiels : un retard se propage | Critique | Passation à l'heure même si c'est incomplet ; reste à faire noté dans `ETAT_PROJET.md` |
| Un relais réécrit le travail précédent | Élevé | Règles anti-dérive (§7.4) et rapport d'audit obligatoire |
| Membre indisponible au moment de son relais | Élevé | Ordre de remplacement défini dans `ETAT_PROJET.md` |
| Définition de RMTCEV seulement supposée | Moyen | Hypothèse retenue ; à remplacer si la définition du cours est retrouvée avant R4 |
| Bug de fuseau invisible depuis l'Europe | Élevé (totaux faux chez le client) | Test obligatoire avec le fuseau Haïti (supposé, Q-09) |
| `version_IA` influencée par les fichiers d'agents ou les instructions globales de l'utilisateur | Moyen (honnêteté de `prompts.md`) | Session vierge selon §5 (conversation web temporaire sans mémoire, ou `claude --safe-mode`) |
| L'IA ajoute des fonctions hors sprint | Moyen | Frontière explicite dans le prompt et journal des écarts |
| Membres ne maîtrisant qu'une partie | Élevé à l'oral | Revue croisée et agent coach |

---

## 11. Prochaines étapes (fin du relais R1)

> **Mise à jour** : le socle R1 est rédigé (voir `ETAT_PROJET.md` §3). La suite se pilote désormais depuis `ETAT_PROJET.md`.

**Décidé (G0, puis relecture humaine du 2026-10-18) :**

- groupe de 6, Sprint 01 = US-01, US-02 et US-03 ;
- RMTCEV selon l'hypothèse ;
- `AGENTS.md` comme source unique ;
- dépôt organisé en espace de travail plus un sous-dossier livrable ;
- organisation en relais 6 × 1 h ;
- D-06 à D-09 et H-01 à H-06 : proposition de l'IA (R1), validée par Leddycia à la relecture humaine du 2026-10-18 ;
- D-11 : le groupe est le **Groupe 01** (numéro confirmé par l'équipe le 2026-10-18) ; le dossier `Groupe_01_Cas_01/` n'existe pas encore, R2 le crée directement sous ce nom ; aucun renommage n'est prévu ;
- D-13 : remise sur le Drive par Leddycia ; `fiche_contribution.pdf` à la racine du dépôt (R6) ;
- D-14 : protocole de relais automatisé ; « fin de notre relais » déclenche la passation complète (`agents/00_protocole_relais.md`) ;
- D-12 : dépôt GitHub **laissé public**, décision de Leddycia prise en connaissance de cause (la proposition de le passer en privé a été écartée) ; membres invités comme collaborateurs pour pouvoir pousser ; adresse e-mail noreply GitHub fortement recommandée pour les commits. Tout ce qui est poussé est public, y compris le commit initial `478570e` (documents du cours, e-mail de l'auteur).

**Reste à fournir :**

- l'**ordre des relais**, avec le nom de chaque membre et l'outil d'IA qu'il utilise ;
- l'acceptation par chaque membre de l'invitation comme collaborateur du dépôt (public, D-12) et son premier clone (`git clone https://github.com/Leddycia/PowerWatch.git`), selon les prérequis d'`ETAT_PROJET.md` §0, pour que tout le monde puisse faire `pull` et `push`.

**À produire par R1, après validation de ce plan :**

1. `travail/decisions.md`, avec les hypothèses Q marquées « provisoire » et les choix H proposés (validés ensuite à la relecture humaine du 2026-10-18).
2. Les transcriptions `docs/brief_client.md`, `docs/consignes.md` et `docs/oracle.md`.
3. `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` et les 6 fiches `agents/`.
4. `ETAT_PROJET.md` et les journaux `travail/journal_prompts.md` et `travail/journal_ecarts.md`. Le dossier `Groupe_01_Cas_01/` sera créé par R2 avec son premier livrable.
5. Vérification de la visibilité du dépôt (laissé public par décision de Leddycia, D-12), puis commit, tag annoté `relais-1`, push avec `--follow-tags` (commandes d'origine de R1) et message de passation à R2. Ce commit rétablit volontairement les octets CRLF d'origine de `docs/energie_college.csv` (stocké en LF par le commit initial `478570e`) grâce à `.gitattributes` : `git log --stat` le montre donc modifié par R1, c'est voulu, les données ne changent pas (empreinte `320155c7…a84b`). Ne jamais le restaurer depuis `478570e`.

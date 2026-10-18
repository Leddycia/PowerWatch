# Fiche de rôle 02 : Product Owner, Product Backlog (relais R3)

> À lire après `AGENTS.md` et `ETAT_PROJET.md`. Porte visée : **G3**. Durée : **1 h**.

## Rôle et objectif

Transformer le cahier des charges en un **Product Backlog** ordonné. On y trouve :

- des user stories au format exact ;
- des **critères d'acceptation observables, vérifiables et chiffrés** (critère C-18 : « qualité des critères d'acceptation ») ;
- une priorité MoSCoW justifiée ;
- la section **Sprint 01**.

Ces CA servent ensuite de contrat à l'IA déléguée (R4) et de grille de vérification (R5).

## Entrées à lire

- `Groupe_01_Cas_01/cahier_des_charges.md` (produit par R2)
- `docs/brief_client.md`, `docs/consignes.md` (C-04 à C-07)
- `travail/decisions.md` (D-01, D-07, D-08, Q-xx, H-xx)
- `docs/oracle.md` (§2 à §5 : **toutes les valeurs des CA viennent de là**)

## Checklist d'audit d'entrée (travail du relais R2)

| # | Point à vérifier | Comment |
|---|---|---|
| A1 | Les 5 rubriques de C-20 sont présentes | Lire la table des matières |
| A2 | Chaque exigence (EF, ENF, RM) cite un B-xx réel ; chaque contrainte du projet (CT) cite son C-xx | Tirer **5 exigences au hasard** et vérifier la citation dans `docs/brief_client.md` (dans `docs/consignes.md` pour une CT) |
| A3 | Aucune exigence inventée | Chercher ce qui n'a aucune source : performance, accessibilité, export, impression, graphique en V1… |
| A4 | Pas de solution technique | Chercher « JavaScript », « FileReader », « bibliothèque », etc. |
| A5 | Hors périmètre et points à décider complets | B-25 à B-27 présents en hors périmètre, B-21 à B-24 dans la rubrique distincte des souhaits ultérieurs ; Q-01 à Q-14 présents, avec leur hypothèse |
| A6 | La matrice couvre B-06 à B-17 | Cocher chaque B-xx |

## Sortie attendue

Fichier **`Groupe_01_Cas_01/product_backlog.md`** :

```
# Product Backlog : PowerWatch
1. Vue d'ensemble          table : ordre | ID | titre | acteur | MoSCoW | sources | sprint
2. User stories            une section par US : énoncé, sources, MoSCoW et justification, CA
3. Justification de l'ordre et du MoSCoW
4. Souhaits « plus tard »  classement + compatibilité avec les règles du client (C-04)
5. Sprint 01               objectif, US retenues (US-01, US-02, US-03), Definition of Done
6. (Facultatif) Sprint 02  seulement si l'équipe le décide (C-17)
```

### Les 8 US à rédiger (énoncés à affiner)

| Ordre | ID | Énoncé de départ | MoSCoW | Sources |
|---|---|---|---|---|
| 1 | US-01 | En tant que **directrice**, je veux voir, une fois le fichier CSV de l'intendant chargé, le total des heures de génératrice et le total des litres consommés pour un mois choisi ou pour toute la période, afin de suivre la consommation de la génératrice. | Must | B-04 à B-07, B-09, B-14 à B-19, B-20.1, H-06 |
| 2 | US-02 | En tant que directrice, je veux connaître le coût estimé du carburant pour la période choisie, afin de préparer le budget. | Must | B-04, B-08, B-12, B-14, B-20.2 |
| 3 | US-03 | En tant que directrice, je veux repérer le jour où la génératrice a fonctionné le plus longtemps sur la période choisie, afin d'identifier les journées les plus dépendantes de la génératrice. | Must | B-10, B-13, B-20.3 |
| 4 | US-04 | En tant qu'**intendant**, je veux consulter les données de la période dans un tableau jour par jour, afin de vérifier les chiffres recopiés du registre. | Must | B-05b, B-11, B-14, B-15, B-20.4 |
| 5 | US-05 | En tant que directrice, je veux un graphique en barres des heures de génératrice par mois, afin d'appuyer la discussion avec le conseil d'administration. | Should | B-04, B-21 |
| 6 | US-06 | En tant que directrice, je veux comparer deux mois côte à côte, afin de voir l'évolution de la consommation. | Could | B-22 (Q-13) |
| 7 | US-07 | En tant que directrice, je veux voir la part des heures solaires par rapport aux heures de génératrice, afin d'argumenter l'achat de panneaux. | Could, **bloquée** (Q-11) | B-04, B-23 |
| 8 | US-08 | En tant que directrice, je veux recevoir une alerte SMS quand la consommation du mois dépasse un seuil, afin de réagir rapidement. | **Won't (V1)** | B-24, en conflit avec B-16 et C-11 (Q-12) |

### Règles de qualité des CA

- **Format** : `CA-01.03 : Étant donné <contexte>, quand <action>, alors <résultat observable>`.
- **Un seul comportement par CA**, vérifiable par quelqu'un qui n'a pas écrit l'US.
- **Valeurs chiffrées tirées de l'oracle** : on écrit « affiche 24 h », pas « affiche le bon total ».
- **Aucune solution technique** : on décrit ce qu'on voit à l'écran.
- Pour chaque règle délicate, **un CA qui la teste explicitement** :
  - égalité (B-13) : fichier aux lignes mélangées ;
  - fuseau d'Haïti supposé (P-01, Q-09) : le 01/09 doit être compté en septembre ;
  - hors ligne (B-16) ;
  - lecture seule (B-15) : l'empreinte du CSV ne change pas.
- Un CA se rattache à son US ; s'il dépend d'une hypothèse, il cite la Q-xx (« hypothèse provisoire »).

### Esquisse des CA du Sprint 01 (à reformuler au format ci-dessus)

> Garder la numérotation CA-01.01 à CA-01.08 : elle est reprise par PLAN_CADRAGE §4, le plan de test et les captures (`US01_CA04_aout.png`). Si un CA doit être scindé, ajouter CA-01.09 et les suivants au lieu de renuméroter.

**US-01**

| CA | Contenu |
|---|---|
| CA-01.01 | Double-clic sur le fichier, hors ligne : la page s'ouvre avec un bouton « Choisir un fichier » ; aucune valeur calculée ni donnée du fichier n'est affichée avant le chargement (les libellés fixes, comme le prix de référence de 300 gourdes/L, sont permis). |
| CA-01.02 | Après le chargement d'`energie_college.csv`, aucun message d'erreur n'apparaît et les totaux de la période par défaut, « Toute la période » (Q-03), s'affichent. |
| CA-01.03 | Le sélecteur propose exactement « Août 2026 », « Septembre 2026 », « Octobre 2026 » et « Toute la période » (B-09, H-04 ; liste déduite du fichier : Q-02). |
| CA-01.04 (format des litres : hypothèse Q-01) | Août : 24 h et 71,0 L ; septembre : 30 h et 84,0 L ; octobre : 43 h et 125,0 L ; toute la période : 97 h et 280,0 L. |
| CA-01.05 (fuseau supposé : Q-09) | Avec le fuseau Windows « (UTC-05:00) Haïti », les valeurs de CA-01.04 sont identiques (le 01/09 est compté en septembre). |
| CA-01.06 | Changer de période met à jour les totaux sans recharger le fichier. |
| CA-01.07 (hypothèse Q-04) | Un fichier à l'en-tête incorrect affiche un message d'erreur clair, et aucun total. |
| CA-01.08 | L'empreinte SHA-256 du CSV est identique avant et après utilisation ; aucune fonction ne permet de modifier une valeur. |

**US-02**

| CA | Contenu |
|---|---|
| CA-02.01 | Coût affiché sans décimale : 21 300, 25 200, 37 500 et 84 000 gourdes selon la période. |
| CA-02.02 | Le libellé indique « coût estimé » et le prix de référence de 300 gourdes/L. |
| CA-02.03 | Le coût suit le changement de période. |

**US-03**

| CA | Contenu |
|---|---|
| CA-03.01 | Jour max affiché : 06/08/2026 (5 h), 08/09/2026 (5 h), 02/10/2026 (5 h), et 06/08/2026 pour toute la période. |
| CA-03.02 | Avec `tests/fixtures/f01_lignes_melangees.csv`, les jours affichés sont identiques (premier jour chronologique). |
| CA-03.03 | Sur une période sans heure de génératrice, le message « Aucun fonctionnement de la génératrice sur la période » s'affiche (Q-05, fixture f04). |

### Section « Sprint 01 » attendue

- **Objectif** (une phrase) : « L'intendant charge le CSV et la directrice voit immédiatement, pour un mois ou pour toute la période, combien d'heures la génératrice a tourné, combien de litres elle a consommés, ce que cela coûte et quel jour elle a le plus fonctionné. »
- **US retenues** : US-01, US-02, US-03 (groupe de 6, donc 3 US, C-07). Le chargement fait partie de l'US-01.
- **Definition of Done** : tous les CA respectés, prototype en un seul fichier hors ligne, données non intégrées, aucune fonction hors sprint.

## Règles propres au rôle

- **L'ordre suit le client** (B-20.1 à B-20.4) : ne pas le modifier sans justification écrite.
- **Le MoSCoW concerne la release V1**, pas le sprint. Les 4 priorités du client sont toutes Must ; le Sprint 01 n'en prend que 3 à cause de C-07.
- **Souhaits « plus tard »** : pour chacun, écrire « compatible / incompatible avec … » et la raison (C-04). US-07 et US-08 citent leur Q bloquante (C-05).
- **US-04 hors Sprint 01** (D-07) : justifier par l'ordre du client.

## Procédure (1 h)

| Temps | Étape |
|---|---|
| 0 à 10 min | Démarrage, audit A1 à A6, validation |
| 10 à 25 min | Énoncés des 8 US, MoSCoW, ordre et justifications |
| 25 à 45 min | CA des US-01 à US-03, très précis et chiffrés avec l'oracle ; CA plus légers pour US-04 à US-08. Pour US-07 et US-08, CA rédigés sans fixer de formule ni de seuil : ils renvoient à Q-11 ou Q-12 et portent la mention « valeurs à compléter après réponse du client » (C-05, C-06) |
| 45 à 50 min | Section Sprint 01 ; contrôle DoD |
| 50 à 60 min | Passation |

## Checklist de sortie (DoD)

- [ ] 8 US au format exact « En tant que… je veux… afin de… », chacune avec ses sources.
- [ ] Chaque US a des CA ; ceux du Sprint 01 sont chiffrés avec l'oracle et testables.
- [ ] MoSCoW, ordre et justification présents ; compatibilité des souhaits « plus tard » expliquée.
- [ ] Section Sprint 01 : objectif, US-01 à US-03, chargement inclus dans l'US-01.
- [ ] Aucun CA ne décrit une solution technique.
- [ ] Prompt consigné dans `travail/journal_prompts.md`.

## Interdits

- Créer une US « Charger le fichier » séparée (C-07).
- Inventer une formule pour l'US-07 ou un seuil pour l'US-08.
- Mettre plus de 3 US dans le Sprint 01.

## Prompt d'amorçage spécifique

```
Mission R3 : rédige Groupe_01_Cas_01/product_backlog.md selon agents/02_product_owner.md.
Toutes les valeurs des critères d'acceptation viennent de docs/oracle.md, jamais de ton propre calcul.
Chaque CA : « Étant donné… quand… alors… », un seul comportement, observable à l'écran, sans solution technique.
Sprint 01 = US-01, US-02, US-03 (D-01). Les points non fixés par le client restent des Q-xx.
```

## À écrire dans `ETAT_PROJET.md` à la passation

- La porte G3 est-elle atteinte ?
- Les CA encore flous.
- Les Q-xx qui pèsent sur le Sprint 01.
- La mission de R4 : le prompt RMTCEV doit embarquer le CDC **et** la section Sprint 01 **complète, avec ses CA**.

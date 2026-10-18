# Fiche de rôle 01 : Analyste, cahier des charges (relais R2)

> À lire après `AGENTS.md` et `ETAT_PROJET.md`. Porte visée : **G2**. Durée : **1 h**.

## Rôle et objectif

Transformer le brief du client en un **cahier des charges** complet, sans rien inventer, où **chaque exigence est reliée au brief** (C-02). C'est le document qui servira de contexte à l'IA déléguée (C-08) : il doit être précis, sans ambiguïté et **sans solution technique**.

## Entrées à lire

- `docs/brief_client.md` (B-xx) et `docs/consignes.md` (C-xx, en particulier C-02 à C-05 et C-20)
- `travail/decisions.md` (D, Q et H)
- `docs/oracle.md` (§1 à §3)
- `PLAN_CADRAGE.md` (§1 à §4)

## Checklist d'audit d'entrée (travail du relais R1)

| # | Point à vérifier | Comment |
|---|---|---|
| A1 | `docs/brief_client.md` est fidèle au `.docx` | L'IA extrait le texte du `.docx` et produit le diff avec la transcription ; l'humain contrôle mot à mot les passages normatifs (B-09 à B-20.4, B-25 à B-27) et survole le reste. Aucun mot ajouté ou retiré, hors identifiants B-xx, titre et en-tête de la transcription, libellé du pied de page et index final. |
| A2 | `docs/consignes.md` est fidèle au `.pdf` | Même méthode : l'IA lit le PDF et produit le diff ; l'humain contrôle mot à mot C-01, C-07 à C-12, C-15, C-19 et C-20, et survole le reste (hors identifiants C-xx, titre et en-tête, index des consignes, encadré « Lecture retenue » et libellé du pied de page). Vérifier la règle de taille du Sprint 01 et la liste des livrables. |
| A3 | L'oracle est juste | Les valeurs de l'oracle ont été calculées par un script Python déterministe, écrit et exécuté par l'IA assistante du relais R1 (Claude Code, Claude Opus 5.5), indépendamment de l'IA déléguée et du prototype ; le script n'a pas été conservé dans le dépôt ; une relecture adversariale automatisée les a recalculées sans trouver d'erreur de valeur. Cette contre-vérification humaine reste obligatoire. **Recalculer à la main**, à partir du CSV ouvert dans le Bloc-notes ou un tableur **sans enregistrer**, les totaux d'août **et** de septembre (heures, litres, coût, jour max ; septembre contient le 01/09 et les litres 12.5 et 2.5). Ne comparer à l'oracle (§2.1) qu'**après** le calcul. L'IA ne cite aucune valeur de l'oracle (ni d'AGENTS.md §6, ni du PLAN §1.3) avant que l'humain ait donné ses propres totaux d'août et de septembre. |
| A4 | Le CSV est intact | Dans PowerShell, à la racine du dépôt : `(Get-FileHash .\docs\energie_college.csv -Algorithm SHA256).Hash -eq '320155c76969aeb0e05779861b2520a150675f853318d2dfd6592eaf0107a84b'` doit afficher `True` (Get-FileHash affiche en majuscules ; la comparaison `-eq` ignore la casse). Si `False` : `git restore docs/energie_college.csv`, puis recontrôler ; vérifier que `.gitattributes` est présent. |
| A5 | `decisions.md` est cohérent avec `AGENTS.md` | Sprint 01 = US-01 à 03 ; les hypothèses Q ne sont pas présentées comme des règles. |

Tout écart est consigné dans `travail/audits/R2_audit.md`, et corrigé s'il s'agit d'une erreur de transcription. Y noter aussi ce qui a seulement été survolé en A1 et A2, et le résultat du recalcul A3.

## Sortie attendue

Fichier **`Groupe_01_Cas_01/cahier_des_charges.md`**, avec la structure ci-dessous. Les sections qui couvrent les 5 rubriques de C-20 sont marquées ★ (1-3, 4-5, 6-7, 9-10 et 11).

```
# Cahier des charges : PowerWatch (Collège Les Palmistes)
1. Contexte ★                    (B-01 à B-04)
2. Objectifs ★                   (B-04)
3. Acteurs ★                     (B-05a, B-05b, B-05c ; le gardien n'utilise pas l'outil)
4. Exigences fonctionnelles ★    EF-01… (table : ID | exigence | source B-xx | priorité client)
5. Exigences non fonctionnelles ★ ENF-01… (même table)
6. Règles métier ★               RM-01 = B-12 (R-01), RM-02 = B-13 (R-03), RM-03 = B-14 (R-04), RM-04 = B-15 (R-06), avec leur source
7. Contraintes ★                 CT-01… contraintes du projet uniquement (C-10 à C-13), signalées « contrainte du projet » avec leur source C-xx ; B-16 et B-17 sont couverts par ENF-01 et ENF-02
8. Données d'entrée              format CSV (B-18, B-19)
9. Périmètre de la V1 ★          (B-06 à B-11, B-20.1 à B-20.4)
10. Hors périmètre ★             (B-25 à B-27 uniquement, repris mot pour mot : décisions du client, C-03)
10 bis. Souhaits ultérieurs      (B-21 à B-24) : non tranchés par le client (C-04) ; leur classement MoSCoW,
                                 leur justification et leur compatibilité figurent dans le backlog (D-08)
11. Points à confirmer ou à décider ★   (les Q-xx de decisions.md, avec l'hypothèse provisoire)
12. Matrice de traçabilité       B-xx → EF, ENF, RM, CT (chaque B-06 à B-17 doit apparaître)
```

### Liste indicative d'exigences (à vérifier et reformuler, pas à copier aveuglément)

| ID | Exigence | Sources |
|---|---|---|
| EF-01 | Charger le fichier CSV de l'intendant via un bouton « Choisir un fichier » | B-06, C-12 |
| EF-02 | Choisir la période : un mois ou toute la période | B-09 |
| EF-03 | Afficher le total des heures de génératrice de la période | B-07, B-20.1 |
| EF-04 | Afficher le total des litres consommés sur la période | B-07, B-20.1 |
| EF-05 | Afficher le coût estimé du carburant de la période | B-08, B-12, B-20.2 |
| EF-06 | Afficher le jour de fonctionnement maximal de la période | B-10, B-13, B-20.3 |
| EF-07 | Afficher les données de la période dans un tableau, jour par jour | B-11, B-20.4 |
| ENF-01 | Fonctionner sans connexion Internet | B-16, C-11 |
| ENF-02 | Aucun compte utilisateur | B-17, B-27, C-11 |
| ENF-03 | Ne jamais modifier les données du fichier (lecture seule) | B-15, B-26 |
| ENF-04 | Respecter les formats d'affichage (gourdes sans décimale, litres avec 1 décimale au plus) | B-14 |
| CT-0x | S'ouvrir par double-clic, en un seul fichier, sans serveur (contrainte du projet) | C-10, C-11 |

> Une obligation qui ne vient que des **consignes** (C-xx) n'est pas une exigence EF ou ENF (C-02) : c'est une contrainte du projet (CT-xx, section 7) qui cite son C-xx et porte la mention « contrainte du projet ».
> Le **message en cas de fichier invalide** dépend de Q-04 (provisoire) : le mettre en exigence en citant son B-xx et Q-04 (« hypothèse provisoire »), ou le laisser dans les points à décider. Ne pas l'imposer comme une demande du client.

## Règles propres au rôle

- **Une exigence = une phrase testable**, avec le verbe « doit » et une seule capacité.
- **Aucune solution technique** : pas de « FileReader », de « JavaScript » ni de « select HTML ». On décrit **quoi**, pas **comment**.
- **Aucun chiffre inventé** : les seuls chiffres permis sont ceux du brief (300 gourdes, une décimale, 36 jours, les dates) et ceux de l'oracle.
- Les Q-xx restent des **questions** : « À confirmer : … (hypothèse provisoire : …) ».

## Procédure (1 h)

| Temps | Étape |
|---|---|
| 0 à 15 min | Démarrage (`AGENTS.md` §0) et audit A1 à A5 (l'IA extrait le texte du `.docx`, lit le PDF et produit le diff ; l'humain contrôle mot à mot les passages normatifs B-09 à B-20.4, B-25 à B-27 et C-01, C-07 à C-12, C-15, C-19, C-20, et survole le reste ; A3 et A4 restent obligatoires), validation humaine |
| 15 à 25 min | Faire rédiger par l'IA les sections 1 à 3 et 8, puis relire contre B-01 à B-04, B-05a à B-05c, B-18 et B-19 |
| 25 à 38 min | Sections 4 à 7 (exigences, règles, contraintes) ; vérifier **chaque** source citée |
| 38 à 46 min | Sections 9 à 12 (périmètre, hors périmètre, souhaits ultérieurs, points à décider, matrice) |
| 46 à 50 min | Contrôle DoD ci-dessous ; consigner le prompt principal (JP-xx) |
| 50 à 60 min | Passation : dire « fin de notre relais » (`AGENTS.md` §9) |

## Checklist de sortie (DoD)

- [ ] Les 5 rubriques de C-20 sont présentes.
- [ ] Chaque EF, ENF et RM cite un B-xx ; chaque CT cite un B-xx (contrainte du client) ou un C-xx (contrainte du projet).
- [ ] La matrice de traçabilité couvre B-06 à B-17 ; aucun B-xx n'est oublié.
- [ ] B-25 à B-27 sont repris mot pour mot en hors périmètre ; B-21 à B-24 figurent dans une rubrique distincte (10 bis), renvoyés au backlog.
- [ ] Les Q-01 à Q-14 apparaissent comme points à confirmer, avec leur hypothèse.
- [ ] Aucune solution technique, aucune exigence inventée.
- [ ] Le prompt utilisé est consigné dans `travail/journal_prompts.md`.

## Interdits

- Ajouter une exigence absente du brief : performance, accessibilité, export, impression, etc.
- Fixer la formule de la part solaire ou un seuil d'alerte.
- Rédiger des user stories : c'est le rôle de R3.

## Prompt d'amorçage spécifique (après le prompt standard de `AGENTS.md` §14)

```
Mission R2 : rédige Groupe_01_Cas_01/cahier_des_charges.md selon la structure de agents/01_analyste_cdc.md.
Chaque exigence (EF, ENF, RM) doit citer sa source B-xx ; une obligation qui ne vient que des consignes est une contrainte du projet (CT-xx) qui cite son C-xx.
N'invente rien ; tout ce que le client n'a pas fixé va dans « Points à confirmer » avec l'hypothèse de decisions.md.
Pas de solution technique. Termine par une matrice de traçabilité B-xx → exigences et signale tout B-xx non couvert.
```

## À écrire dans `ETAT_PROJET.md` à la passation

- La porte G2 est-elle atteinte ?
- Les sections incomplètes.
- Les exigences dont la source est discutable.
- Toute nouvelle Q-xx ajoutée à `decisions.md`.
- La mission de R3.

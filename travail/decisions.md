# Registre des décisions

> **Règle** : une décision n'est jamais changée en silence. Pour la contester, on passe son statut à « contesté » et on ajoute une ligne au journal des changements (§4) avec la raison. L'équipe tranche ensuite.
>
> **Statuts possibles :**
>
> | Statut | Signification |
> |---|---|
> | **validé** | Décidé ou validé par l'équipe ; qui et quand sont indiqués pour chaque décision. |
> | **provisoire** | Hypothèse de travail, en attente d'une confirmation du client. |
> | **ouvert** | Question au client sans hypothèse applicable : l'US concernée reste bloquée ou en Won't. |
> | **à trancher** | Pas encore décidé, avec le relais qui doit trancher. |
> | **contesté** | Remis en cause par un relais. |
> | **remplacé** | Remplacé par une autre décision. |
>
> **Familles d'identifiants :**
>
> | Préfixe | Signification |
> |---|---|
> | **D-xx** | Décision d'organisation ou de méthode, prise par l'équipe. |
> | **Q-xx** | Question au client. Une hypothèse est appliquée dans le prototype, mais **on ne la présente jamais comme une règle du client**. |
> | **H-xx** | Choix de présentation de l'équipe (pas une règle métier). |

---

## 1. Décisions d'équipe (D-xx)

| ID | Décision | Statut | Justification et source | Décidé par | Date |
|---|---|---|---|---|---|
| D-01 | **Sprint 01 = US-01 (chargement et totaux), US-02 (coût estimé), US-03 (jour max).** | validé | Groupe de 6, donc 3 US (C-07). Suit l'ordre de priorité 1 à 3 du client (B-20.1 à B-20.3). | Équipe (R1) | 2026-10-18 |
| D-02 | Structure RMTCEV : **R**ôle, **M**ission, **T**âches, **C**ontexte/Contraintes, **E**xemples, **V**alidation. | validé | Hypothèse : la définition exacte du cours n'est pas disponible. Si un membre la retrouve avant R4, elle remplace celle-ci (statut « remplacé »). | Équipe (R1) | 2026-10-18 |
| D-03 | **`AGENTS.md` est la source unique** des instructions d'IA. `CLAUDE.md` et `GEMINI.md` l'importent ; les fiches de rôle sont dans `agents/`. | validé | Évite la divergence entre plusieurs copies. Codex et Antigravity CLI lisent `AGENTS.md` nativement. | Équipe (R1) | 2026-10-18 |
| D-04 | La racine du dépôt est l'espace de travail ; le sous-dossier `Groupe_01_Cas_01/` contient le **livrable exact** copié sur le Drive. | validé | Les fichiers d'agents, les journaux et les tests ne doivent pas encombrer le livrable (C-01). | Équipe (R1) | 2026-10-18 |
| D-05 | Organisation en **relais séquentiels de 6 × 1 h**, avec audit d'entrée et passation formalisée (`ETAT_PROJET.md`). | validé | Disponibilité de chaque membre : 1 h. L'audit croisé prépare la soutenance (C-16). | Équipe (R1) | 2026-10-18 |
| D-06 | C-12 prime sur C-10 : **aucune donnée CSV intégrée** dans le HTML ; chargement par le bouton « Choisir un fichier ». | validé | Notre cas fournit un CSV. Intégrer les données serait un écart (C-12). | Proposition de l'IA (R1), validée par Leddycia à la relecture humaine du 2026-10-18 | 2026-10-18 |
| D-07 | Le tableau jour par jour reste une US à part (US-04, Must, 4e), hors Sprint 01. | validé | Le client le classe en 4e priorité (B-20.4). Le fondre dans l'US-01 contredirait cet ordre. | Proposition de l'IA (R1), validée par Leddycia à la relecture humaine du 2026-10-18 | 2026-10-18 |
| D-08 | Souhaits « plus tard » : B-21 graphique = **Should** ; B-22 comparaison = **Could** ; B-23 part solaire = **Could, bloquée** (Q-11) ; B-24 SMS = **Won't (V1)**. | validé | C-04 et C-05. Le SMS est incompatible avec B-16 et C-11. La formule de la part solaire n'est pas fixée. | Proposition de l'IA (R1), validée par Leddycia à la relecture humaine du 2026-10-18 | 2026-10-18 |
| D-09 | `version_IA.html` est produit dans une **session d'IA vierge, hors du dépôt**, qui ne reçoit que le prompt RMTCEV (avec le CDC et le Sprint 01). Session vierge : de préférence une IA web dans une conversation temporaire (ou nouvelle), mémoire et instructions personnalisées du compte désactivées, hors de tout Projet, Gem ou GPT personnalisé, sans autre pièce jointe que le prompt. En ligne de commande, uniquement `claude --safe-mode` lancé dans un dossier temporaire vide hors du dépôt (il désactive `CLAUDE.md`, règles, skills, plugins et hooks). Codex, Gemini CLI ou Antigravity CLI seulement si aucun fichier d'instructions global n'existe (`~/.codex/AGENTS.md`, `~/.gemini/GEMINI.md`). Noter le mode exact dans `prompts.md` §1. Si la CLI écrit elle-même le fichier, le copier tel quel vers `version_IA.html` et garder la transcription dans `travail/brut/`. Si l'IA pose une question au lieu de livrer, répondre uniquement « Applique les hypothèses du cahier des charges et livre le fichier complet. » et consigner l'échange dans `prompts.md` §1. Avant le commit de `version_IA.html`, contrôler qu'il est identique au bloc HTML de la réponse brute : `git diff --no-index --ignore-cr-at-eol <bloc extrait dans un fichier temporaire hors dépôt> <version_IA.html>` doit être vide. Il est commité brut et tagué `version-ia` (tag annoté : `git tag -a`). | validé | Sincérité de `prompts.md` (C-08) et preuve de non-modification (C-09). Raison des précautions : une CLI ouverte dans un dossier vide charge quand même les instructions globales de l'utilisateur (`~/.claude/CLAUDE.md`, `~/.claude/rules/`, `~/.codex/AGENTS.md`). | Proposition de l'IA (R1), validée par Leddycia à la relecture humaine du 2026-10-18 | 2026-10-18 |
| D-10 | Le prompt de délégation contient les **règles et les valeurs attendues** (oracle), mais **pas les solutions d'implémentation** des pièges P-01 à P-10. | validé | Décision de méthode : le prompt reste précis (C-18), sans induire les solutions techniques à l'avance ; les écarts réels de l'IA alimentent le journal des corrections (C-08). | Bradley (R4) | 2026-10-18 |
| D-11 | Numéro de groupe : **Groupe 01**. Livrable : `Groupe_01_Cas_01/` ; dossier Drive : `Groupe_01/`. | validé | Numéro 01 confirmé par l'équipe le 2026-10-18. Le dossier n'existe pas encore : R2 le crée directement sous ce nom. Plus aucun renommage n'est prévu. | Équipe (R1) | 2026-10-18 |
| D-12 | **Dépôt GitHub laissé public**, décision de Leddycia prise en connaissance de cause ; membres invités comme collaborateurs pour pouvoir pousser ; adresse e-mail noreply GitHub fortement recommandée pour les commits. | validé | La proposition initiale (passer en privé avant le premier push) a été écartée par Leddycia après vérification du 2026-10-18 (accès anonyme toujours possible). Conséquence assumée : tout ce qui est poussé est public, y compris le commit initial 478570e (documents du cours, e-mail de l'auteur), les noms des membres et les journaux. L'historique n'est jamais réécrit. | Leddycia (propriétaire du dépôt), JP-07 | 2026-10-18 |
| D-13 | **Remise sur le Drive par Leddycia** : R6 prépare la remise dans le dépôt (`Groupe_01_Cas_01/` et `fiche_contribution.pdf` à la racine, au même niveau, comme sur le Drive), puis Leddycia téléverse les deux dans `Groupe_01/` et remplace le README après le test sur un autre PC. | validé | Leddycia a l'accès au Drive et s'en charge elle-même ; la fiche de contribution est versionnée pour lui être transmise. | Leddycia, JP-08 | 2026-10-18 |
| D-14 | **Protocole de relais automatisé** (`agents/00_protocole_relais.md`) : l'IA du relais tient `ETAT_PROJET.md` à jour pendant le travail (relais EN COURS au démarrage, journal de bord §8 après chaque étape). La phrase **« fin de notre relais »** déclenche la passation complète (ETAT, audit, journaux, commit, tag annoté, push, message de passation) et vaut demande explicite de commit et de push ; « sauvegarde du relais » commite et pousse sans tag. | validé | Demande de Leddycia : que tout se mette à jour sans procédure manuelle. L'IA s'arrête si un contrôle échoue (original de `docs/` ou `version_IA.html` indexé, conflit Git). | Leddycia, JP-08 | 2026-10-18 |
| D-15 | **Contre-vérification A3 de l'oracle** (fiche 01) : le recalcul à la main par un humain n'est **pas** fait ; il est remplacé par **trois recalculs automatiques indépendants** (Python en décimal exact, awk, PowerShell) et une comparaison automatique avec chaque tableau de `docs/oracle.md`, faits par l'IA assistante de R2. Résultat : aucun écart. Les deux scripts sont conservés en annexe de `travail/audits/R2_audit.md`. | validé | Décision de Leddycia (« Je ne fais pas de recalcul. Assure-toi que le calcul est le bon »). Limite assumée : le contrôle n'est pas humain, et il est fait par le même outil et le même modèle que l'oracle (Claude Code, Claude Opus 5.5), avec d'autres méthodes ; R2 étant tenu par le membre de R1, un recalcul humain n'aurait pas été indépendant non plus. Les scripts conservés rendent le contrôle refaisable par tout membre. | Leddycia, JP-12 | 2026-10-18 |

## 2. Questions au client et hypothèses provisoires (Q-xx)

> Dans le prototype, on applique l'hypothèse. Dans le cahier des charges, on liste ces points dans « Points à confirmer ou à décider » (C-20), **sans les présenter comme des règles du client**.

| ID | Question | Hypothèse appliquée | Statut | US touchée | Pourquoi cette hypothèse |
|---|---|---|---|---|---|
| Q-01 | Format des litres affichés ? | Toujours **1 décimale**, virgule française : « 71,0 L », « 12,5 L ». | provisoire | US-01, US-04 | B-14 autorise une décimale ; un format fixe est non ambigu et vérifiable. Point O-9 : l'équipe garde cette hypothèse pour le Sprint 01 ; le client n'a pas répondu, ce n'est donc pas une règle du client. |
| Q-02 | Liste des mois : figée (août à octobre 2026) ou déduite du fichier ? | **Déduite du fichier**. Sur le CSV fourni, elle donne exactement les 3 mois de B-09. | provisoire | US-01 | L'intendant met le CSV à jour chaque semaine (B-03) : un futur fichier peut couvrir d'autres mois ; la liste reste conforme à B-09 sur les données fournies. |
| Q-03 | Période sélectionnée par défaut après chargement ? | « Toute la période ». | provisoire | US-01 | Un résultat utile est visible immédiatement (C-07). |
| Q-04 | Que faire d'un fichier invalide (colonne manquante, valeur non numérique ou négative, date invalide, date en double) ? | **Rejet complet** avec un message clair qui indique la ligne fautive ; aucun total affiché. | provisoire | US-01 | Ignorer des lignes reviendrait à modifier silencieusement les données (B-15). |
| Q-05 | Période sans aucune heure de génératrice : quel « jour max » afficher ? | Message « Aucun fonctionnement de la génératrice sur la période ». | provisoire | US-03 | Afficher un jour à 0 h serait trompeur. Le cas n'existe pas dans le CSV fourni. |
| Q-06 | Le prix de 300 gourdes est-il modifiable par l'intendance ? | **Constante** de 300 gourdes/L en V1. | provisoire | US-02 | B-12 fixe ce prix « pour ce suivi ». Le rendre modifiable n'est pas demandé. |
| Q-07 | Comment arrondir le coût si des litres avaient plus d'une décimale ? | Arrondi à la gourde la plus proche. | provisoire | US-02 | B-14 impose des montants sans décimale. Avec au plus 1 décimale, × 300 donne toujours un entier. |
| Q-08 | Faut-il rappeler la couverture réelle de la période (nombre de jours, premier et dernier jour) ? | **Non en V1** (non demandé par le client) ; à proposer au client dans les points à confirmer du CDC. | provisoire | US-01 | Aucun élément du brief ne demande cet affichage (C-02). Il éviterait pourtant de lire un échantillon comme un mois complet pour le budget (B-04, B-18) : d'où la question au client. |
| Q-09 | Dans quel pays est le collège ? Quels navigateur, système et fuseau sur le PC de l'intendance ? | Collège supposé en **Haïti**. Tests sur Edge ou Chrome et sur Firefox, sous Windows, fuseau « (UTC-05:00) Haïti ». | provisoire | Tests | Le brief ne nomme aucun pays : « Haïti » est déduit des gourdes. Le piège P-01 impose de tester dans ce fuseau. |
| Q-10 | Avec quel outil le CSV est-il produit ? Un Excel français pourrait exporter avec `;` et un BOM. | Seul le format décrit (virgule, B-18) est accepté ; un fichier avec `;` ou avec un BOM UTF-8 altérant le nom de la première colonne est rejeté avec un message d'en-tête invalide (Q-04). | provisoire | US-01 | Le brief fixe la virgule. On n'invente pas de support d'autres formats (point O-10 #10 précisé). |
| Q-11 | Formule de la « part solaire » ? hs/(hs+hg) ? hs/hg ? Par jour ou en cumul ? En % ou en graphique ? | **Aucune hypothèse.** US-07 bloquée. | ouvert | US-07 | C-05 : on n'invente pas une règle non fixée. |
| Q-12 | Alerte : seuil (valeur, unité en litres, heures ou gourdes), destinataire, canal possible sans Internet ? | **Aucune.** US-08 en Won't (V1). | ouvert | US-08 | Incompatible avec B-16 et C-11 ; seuil non fixé (C-05). |
| Q-13 | Comparaison de deux mois : quels indicateurs ? | Aucune. | ouvert | US-06 | Non précisé par le client. |
| Q-14 | Graphique : afficher octobre, partiel, tel quel ? | Oui, avec la mention « données au 16/10 ». | provisoire | US-05 | B-18 précise que les données d'octobre s'arrêtent au 16. |
| Q-15 | Le tableau jour par jour montre-t-il les jours de la période choisie, ou toutes les données chargées ? | Les jours de la **période choisie**. | provisoire | US-04 | B-11 ne cite pas la période, contrairement à B-07 et B-10. La liste indicative de la fiche 01 (« données de la période ») l'entendait ainsi. Hypothèse proposée par l'IA (R2), validée par Leddycia (JP-13). |
| Q-16 | Quel format d'affichage pour les heures de génératrice (totaux, jour maximal, tableau) ? | La valeur du fichier, suivie de l'unité « h » (par exemple « 5 h »). | provisoire | US-01, US-03, US-04 | B-14 ne fixe que le format des montants et des litres. Affichage déjà retenu par `docs/oracle.md` §2.2. Hypothèse proposée par l'IA (R2), validée par Leddycia (JP-13). |
| Q-17 | Pour le jour de fonctionnement maximal, faut-il afficher la date seule, ou aussi le nombre d'heures de génératrice de ce jour ? | La date (H-01) **et** le nombre d'heures de génératrice de ce jour. | provisoire | US-03 | B-10 demande le jour ; ses heures permettent à l'intendant de vérifier les chiffres (B-05b). Affichage déjà retenu par `docs/oracle.md` §2.2. Hypothèse proposée par l'IA (R2), validée par Leddycia (JP-13). |
| Q-18 | Quelles colonnes le tableau jour par jour affiche-t-il ? | Les **4 colonnes du fichier** (B-19) : date, heures solaires, heures de génératrice, litres de carburant. | provisoire | US-04 | B-11 demande « les données » jour par jour sans préciser les colonnes ; afficher toutes celles du fichier permet à l'intendant de vérifier les chiffres recopiés (B-05b). Point renvoyé par R2 (O-10 #1). Hypothèse proposée par l'IA (R3), validée par Leddycia (JP-16). |
| Q-19 | Dans quel ordre les lignes du tableau jour par jour sont-elles affichées ? | **Ordre chronologique** des dates, quel que soit l'ordre des lignes dans le fichier. | provisoire | US-04 | B-11 ne fixe pas l'ordre ; le client raisonne déjà en ordre chronologique pour l'égalité (B-13) et le registre papier suit les jours (B-02). Point renvoyé par R2 (O-10 #2). Hypothèse proposée par l'IA (R3), validée par Leddycia (JP-16). |
| Q-20 | Faut-il rappeler, à côté du coût estimé, que les 300 gourdes par litre sont un prix de référence de l'intendance et non un prix officiel ? | **Oui** : mention « prix de référence de l'intendance, pas un prix officiel ». | provisoire | US-02 | B-12 précise : « il ne s'agit pas d'un prix officiel » ; le rappeler évite de lire le coût comme une dépense réelle (B-04, budget). Le client ne demande pas cet affichage. Point renvoyé par R2 (O-10 #11). Hypothèse proposée par l'IA (R3), validée par Leddycia (JP-16). |

## 3. Choix de présentation de l'équipe (H-xx)

> H-01 à H-06 : proposition de l'IA (R1), validée par Leddycia à la relecture humaine du 2026-10-18.

| ID | Choix | Statut | Justification |
|---|---|---|---|
| H-01 | Dates affichées au format **JJ/MM/AAAA** (le fichier reste en AAAA-MM-JJ). | validé | Usage francophone. Il s'agit d'affichage, pas de modification des données (B-15). |
| H-02 | Montants : « 21 300 gourdes » (espace comme séparateur des milliers, pas de décimale). | validé | B-14 ; lisibilité. |
| H-03 | Interface et livrables entièrement en **français**. | validé | Brief et client francophones. |
| H-04 | Libellés des périodes : « Août 2026 », « Septembre 2026 », « Octobre 2026 », « Toute la période ». | validé | B-09. |
| H-05 | Bouton de chargement personnalisé, au libellé exact **« Choisir un fichier »**, quel que soit le navigateur. | validé | C-12 ; le libellé natif varie selon le navigateur (P-07). |
| H-06 | L'acteur de l'US-01 est **la directrice**. Le chargement par l'intendant figure dans les CA. | validé | B-20.1 est un besoin de suivi de la directrice (B-05a) ; C-07 impose le chargement dans la 1re US. |

## 4. Journal des changements de décision

| Date | Relais | ID | Ancien → nouveau statut | Raison |
|---|---|---|---|---|
| 2026-10-18 | R1 | D-01 à D-05 | création → validé | Réponses de l'équipe aux questions de cadrage (JP-02) |
| 2026-10-18 | R1 | D-06 à D-09, H-01 à H-06 | création → validé | Statut écrit par l'IA de R1 avant toute validation de l'équipe (écart E-12) |
| 2026-10-18 | R1 | Q-01 à Q-14 | création → provisoire ou ouvert | Hypothèses de travail en attente du client |
| 2026-10-18 | R1 | D-10, D-11 | création → à trancher | D-10 par R4 ; D-11 dès que le numéro du groupe est connu |
| 2026-10-18 | R1 | D-02, D-06 à D-09, H-01 à H-06 | validé → validé (confirmé) | Validation humaine par Leddycia à la relecture du socle du 2026-10-18 (JP-05) ; colonne « Décidé par » de D-06 à D-09 corrigée, note ajoutée sous le titre du §3 pour H-01 à H-06. D-02 : « validé (hypothèse) » → « validé », la mention « hypothèse » passe dans la justification |
| 2026-10-18 | R1 | D-11 | à trancher → validé | Numéro 01 confirmé par l'équipe (JP-06) : livrable `Groupe_01_Cas_01/`, dossier Drive `Groupe_01/` ; aucun renommage prévu |
| 2026-10-18 | R1 | D-12 | création → validé | Dépôt GitHub passé en privé avant le premier push du socle (proposition de l'IA, validée par Leddycia, JP-05) |
| 2026-10-18 | R1 | D-12 | validé (privé) → validé (laissé public) | Vérification avant le push : dépôt toujours public. Leddycia décide de le laisser public en connaissance de cause (JP-07) ; O-8 résolu. |
| 2026-10-18 | R1 | D-13 | création → validé | Leddycia téléverse elle-même la remise sur le Drive (JP-08) ; O-7 résolu |
| 2026-10-18 | R1 | D-14 | création → validé | Protocole de relais automatisé et phrase « fin de notre relais » (JP-08) |
| 2026-10-18 | R1 | Q-08 | provisoire (« Oui ») → provisoire (« Non en V1 ») | Affichage de la couverture non demandé par le client (C-02, RG-01) : à proposer dans les points à confirmer du CDC ; le CA « 36 jours chargés » est retiré (écart E-06) |
| 2026-10-18 | R2 | D-15 | création → validé | Leddycia ne fait pas le recalcul humain A3 ; recalcul automatique indépendant, aucun écart avec l'oracle (JP-12) |
| 2026-10-18 | R2 | Q-15 à Q-17 | création → provisoire | Points non fixés par le client, relevés par les vérificateurs du cahier des charges ; hypothèses validées par Leddycia (JP-13). Les 12 autres points relevés sont renvoyés à R3 et R4 (`travail/audits/R2_audit.md`) |
| 2026-10-18 | R3 | Q-18 à Q-20 | création → provisoire | Points O-10 #1, #2 et #11 renvoyés par R2 : colonnes et ordre du tableau jour par jour, rappel du prix de référence ; ils ne peuvent pas être fixés dans un CA sans trancher à la place du client (RG-02). Hypothèses validées par Leddycia (JP-16) ; ajoutées au cahier des charges (§4, §11.1, §12.1) |
| 2026-10-18 | R4 | D-10 | à trancher → validé | Décision de Bradley : règles et oracle dans le prompt, sans solutions d'implémentation |
| 2026-10-18 | R4 | Q-01 | provisoire → provisoire (confirmé) | Point O-9 tranché pour le Sprint 01 : 1 décimale systématique avec virgule |
| 2026-10-18 | R4 | Q-10 | provisoire → provisoire (précisé) | Point O-10 #10 précisé : BOM UTF-8 traité en rejet Q-04 sans planter |
| 2026-10-18 | R5 (complément) | Q-01 | provisoire (confirmé) → provisoire | « confirmé » n'est pas un statut du registre et laisse croire que le client a répondu (RG-02, `AGENTS.md` §4, écart E-23). L'hypothèse ne change pas : l'équipe la garde pour le Sprint 01 (point O-9). Justification reformulée dans le même sens (« tranche le point O-9 » retiré). Correction demandée par Leddycia (JP-24) |

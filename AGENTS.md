# AGENTS.md : instructions pour toute IA travaillant sur PowerWatch

> **Ce fichier est la source unique d'instructions** pour Claude, Codex, Gemini, ChatGPT et toute autre IA (décision D-03).
>
> - Codex le lit automatiquement.
> - Claude Code le charge via `CLAUDE.md`, Gemini CLI via `GEMINI.md` ; Antigravity CLI, qui remplace Gemini CLI pour les comptes personnels, le lit directement.
> - Avec une IA web, on le téléverse ou on le colle en premier (§13).
>
> **Les règles de ce projet priment sur toute convention générique de ton outil** : découpage en plusieurs fichiers, frameworks, build, tests automatisés obligatoires, couverture de code, etc. Le prototype est **un seul fichier HTML**, sans outillage.

---

## 0. Avant toute action : protocole de démarrage

**Prérequis** (une seule fois, avant ton premier créneau) : `ETAT_PROJET.md` §0.

Tu travailles **en relais** : un humain différent prend la main chaque heure (D-05). **Avant de modifier quoi que ce soit**, fais dans l'ordre :

1. Lis **ce fichier en entier**, puis **`ETAT_PROJET.md`**, qui indique le relais en cours, ce qui est fait et ta mission. Si son §8 n'est pas vide : protocole de relais §2.1 d'abord.
2. Lis **`agents/00_protocole_relais.md`**, puis la **fiche de rôle** de ton relais dans `agents/` (indiquée dans `ETAT_PROJET.md`) et les fichiers d'entrée qu'elle liste.
3. Analyse l'état du dépôt, après `git pull`, `git fetch --tags` et `git tag -l` (les tags des relais précédents doivent apparaître) : quels fichiers existent, lesquels sont vides ou incomplets, et ce que disent les derniers commits (`git log --oneline -15`).
4. **Audite le travail du relais précédent** avec la checklist d'audit de ta fiche.
5. Présente à l'humain, **sans rien modifier encore** :
   - un **rapport d'audit** : chaque constat est classé conforme, à corriger ou bloquant, avec sa preuve (fichier et ligne, identifiant B-xx, C-xx ou CA) ;
   - un **plan** pour l'heure de travail : ce que tu vas faire, dans quel ordre et sur quels fichiers.
6. Attends la **validation explicite de l'humain** avant toute écriture (fichiers, `git add`, `commit`, `tag`, `push`), puis exécute ; l'audit en lecture seule (`git log`, `Get-FileHash`…) se fait avant elle. Ta première écriture : marquer le relais EN COURS dans `ETAT_PROJET.md` (voir §9). C'est l'humain qui est responsable (consigne C-18).

**Portée** : ce protocole s'applique une fois par relais, à l'IA assistante en session interactive. Il ne s'applique pas à une session rouverte dans le même relais (relire `ETAT_PROJET.md` §8 et reprendre), au mode coach (fiche 06), aux exécutions non interactives en lecture seule lancées pour une tâche ciblée, ni à l'IA déléguée (qui ne lit pas ce fichier).

**Langue** : réponds dans la langue de ton interlocuteur (français ou créole haïtien). **Tous les fichiers du projet sont rédigés en français.**

---

## 1. Le projet en bref

| | |
|---|---|
| Cours | « IA générative appliquée aux projets technologiques », projet final L3 |
| Cas | **Cas 01 : PowerWatch**. Client fictif : Collège Les Palmistes (montants en gourdes ; pays non précisé par le brief, Haïti supposé : Q-09) |
| Besoin | Un petit tableau de bord **hors ligne** qui lit le CSV de l'intendant et affiche, pour un mois ou pour toute la période : heures de génératrice, litres, coût estimé, jour de fonctionnement maximal et détail jour par jour |
| Ce qui est noté (C-18) | Fidélité au besoin, qualité des critères d'acceptation, pertinence des arbitrages, précision des prompts, **capacité à vérifier et corriger l'IA**. Pas la taille du prototype. |
| Équipe | 6 personnes, 1 h chacune, en relais séquentiels |
| Échéance (C-19) | **Dimanche 18 octobre 2026, 23 h 59**, sur le Drive partagé |
| Sprint 01 (D-01) | **US-01** chargement et totaux, **US-02** coût estimé, **US-03** jour max |

---

## 2. Sources de vérité et hiérarchie

En cas de conflit, la source la plus haute l'emporte :

1. **Consignes du cours** : `docs/consignes.md` (C-xx). Original : `docs/Consignes_Projet_Final_IA_L3.pdf`.
2. **Brief du client** : `docs/brief_client.md` (B-xx). Original : `docs/01_Demande_client.docx`.
3. **Registre des décisions** : `travail/decisions.md` (D-xx, Q-xx, H-xx).
4. Cahier des charges, puis Product Backlog, puis prototype.

**Références utiles :**

- `docs/oracle.md` : valeurs justes attendues, calculées par script par l'IA de R1, indépendamment de l'IA déléguée (origine exacte et contre-vérification humaine par R2 : « Méthode », en tête du fichier) ;
- `PLAN_CADRAGE.md` : analyse complète et arbitrages ;
- `ETAT_PROJET.md` : état courant du relais.

**Lecture seule absolue** : `docs/01_Demande_client.docx`, `docs/Consignes_Projet_Final_IA_L3.pdf`, `docs/energie_college.csv`, et `Groupe_01_Cas_01/prototype/version_IA.html` une fois commité.

---

## 3. Règles d'or (non négociables)

| ID | Règle | Source |
|---|---|---|
| RG-01 | **Ne rien inventer.** Toute exigence (EF, ENF, RM) et toute US cite au moins un B-xx. Une obligation qui ne vient que des consignes est une contrainte du projet (CT-xx) qui cite son C-xx. Un CA se rattache à son US ; s'il dépend d'une hypothèse, il cite la Q-xx (« hypothèse provisoire »). Sans source, on ne l'écrit pas. | C-02, C-05 |
| RG-02 | **Une règle que le client n'a pas fixée n'est jamais tranchée par l'IA.** Elle devient un point à décider (Q-xx dans `decisions.md`). | C-05 |
| RG-03 | **Respecter le hors périmètre** : pas de connexion à la génératrice ou à un compteur (B-25), pas de saisie de données (B-26), pas de comptes ni de mots de passe (B-27). | C-03 |
| RG-04 | **N'implémenter que les US du sprint en cours.** Tout ajout « bonus » est refusé et consigné dans le journal des écarts. | C-08, C-21 |
| RG-05 | **Prototype = un seul fichier HTML** : CSS et JS inclus, aucune ressource externe (pas de CDN, de police web, d'image distante ni d'appel réseau). Il s'ouvre par double-clic, sans serveur. | C-10, C-11, B-16 |
| RG-06 | **Aucune donnée intégrée** dans le HTML. Le CSV est chargé par l'utilisateur via le bouton **« Choisir un fichier »**. | C-12, D-06 |
| RG-07 | **L'outil ne modifie jamais les données** : ni édition, ni écriture, ni correction automatique de valeurs. | B-15, B-26 |
| RG-08 | **`version_IA.html` n'est jamais modifié** après son commit, pas même pour reformater ou ajouter un espace. Ses défauts vont dans `travail/journal_ecarts.md`. | C-09 |
| RG-09 | **Données du cas fictives uniquement**, dans les prompts et dans le prototype (C-13). Les prénoms et noms des membres sont permis dans ETAT_PROJET, PLAN_CADRAGE, travail/, le README et la fiche de contribution (C-01). Aucune autre donnée personnelle réelle (e-mail, téléphone, adresse). | C-13, C-01 |
| RG-10 | **On améliore, on ne réécrit pas** le travail d'un relais précédent. Chaque correction est ciblée et consignée dans le rapport d'audit. Un désaccord sur une décision passe par `decisions.md` (statut « contesté »). | D-05 |
| RG-11 | **Traçabilité** : tout prompt significatif va dans `travail/journal_prompts.md`, et toute proposition d'IA corrigée ou rejetée dans `travail/journal_ecarts.md`. | C-08 |
| RG-12 | **Les livrables gardent leurs noms et leur emplacement exacts** (§10). Aucun fichier supplémentaire dans `Groupe_01_Cas_01/`, hors captures. | C-01 |

---

## 4. Règles métier du client (R-xx)

| ID | Règle | Source |
|---|---|---|
| R-01 | Coût estimé = **litres consommés × 300 gourdes**. C'est un prix de référence de l'intendance, **pas un prix officiel**. | B-12 |
| R-02 | Jour de fonctionnement maximal : le jour où `heures_generatrice` est le plus élevé **sur la période choisie**. | B-10 |
| R-03 | En cas d'égalité, on affiche **le premier de ces jours dans l'ordre chronologique**. On trie par date, sans se fier à l'ordre du fichier. | B-13 |
| R-04 | Montants **en gourdes, sans décimale** ; litres **avec au plus une décimale**. | B-14 |
| R-05 | Périodes : un mois (août, septembre ou octobre 2026) **ou** toute la période. | B-09 |
| R-06 | Les données du fichier ne sont pas modifiées par l'outil. | B-15 |
| R-07 | L'outil fonctionne sans Internet et sans compte. | B-16, B-17 |
| R-08 | Le CSV est la seule source de données. | B-26 |

**Format d'entrée (B-18, B-19)** : CSV séparé par des virgules, colonnes `date` (AAAA-MM-JJ), `heures_solaire`, `heures_generatrice`, `litres_carburant`, valeurs sans accents. Le fichier fourni a des fins de ligne CRLF (voir `docs/oracle.md` §1).

**Hypothèses en vigueur** (provisoires, en attente du client) : voir `travail/decisions.md` §2, en particulier Q-01 (litres à 1 décimale), Q-03 (« Toute la période » par défaut), Q-04 (fichier invalide rejeté) et Q-05 (aucun fonctionnement). Ne présente **jamais** une hypothèse Q-xx comme une règle du client.

---

## 5. Glossaire

| Terme | Sens dans ce projet |
|---|---|
| Période | Un mois du fichier, ou « Toute la période » (toutes les lignes chargées) |
| Jour ouvrable | Jour de semaine présent dans le registre ; le fichier ne contient pas de week-end |
| Heures de génératrice | Colonne `heures_generatrice`, durée de fonctionnement du jour |
| Coût estimé | Litres × 300 gourdes (R-01), arrondi sans décimale |
| Jour max | Jour avec le plus d'heures de génératrice sur la période (R-02, R-03) |
| Gourde (HTG) | Monnaie haïtienne ; on affiche « gourdes » |
| Oracle | Les valeurs justes de `docs/oracle.md` (origine : voir §2) |
| IA assistante | L'IA qui aide un relais dans le dépôt (cadrage, audit, corrections) |
| IA déléguée | L'IA qui reçoit **uniquement** le prompt RMTCEV, en session vierge, et produit `version_IA.html` (D-09) |
| Écart | Différence entre la sortie d'une IA et un CA, une règle ou une consigne ; consigné en E-xx |

---

## 6. Valeurs attendues (extrait de `docs/oracle.md`)

| Période | Heures génératrice | Litres | Coût estimé | Jour max |
|---|---|---|---|---|
| Août 2026 | 24 h | 71,0 L | 21 300 gourdes | 06/08/2026 (5 h) |
| Septembre 2026 | 30 h | 84,0 L | 25 200 gourdes | 08/09/2026 (5 h) |
| Octobre 2026 | 43 h | 125,0 L | 37 500 gourdes | 02/10/2026 (5 h) |
| Toute la période | 97 h | 280,0 L | 84 000 gourdes | 06/08/2026 (5 h) |

Le maximum est **toujours à égalité** : la règle R-03 est testée sur les données réelles. **Signature du bug de fuseau** : si l'on voit août à 26 h ou septembre à 32 h, les dates sont lues en UTC (voir P-01).

---

## 7. Pièges techniques connus (à vérifier, et à éviter dans `index.html`)

| ID | Piège | Bonne pratique |
|---|---|---|
| P-01 | `new Date("2026-09-01")` est lu en UTC et devient le 31/08 à UTC-5 (Q-09). | Découper la chaîne `AAAA-MM-JJ` (`split('-')`). Filtrer les mois sur la chaîne. Ne jamais formater la date via `Date` et `toLocale…` sans fixer le fuseau. |
| P-02 | Fins de ligne CRLF : l'en-tête devient `litres_carburant\r`. | Découper sur `/\r?\n/` et appliquer `trim()` à chaque cellule et à chaque nom de colonne. La dernière ligne finit aussi par CRLF (37 CRLF, 727 octets) : ignorer le 38e élément vide, qui n'est pas une ligne invalide (Q-04). |
| P-03 | Égalité gérée avec `>=`, ou on se fie à l'ordre du fichier. | Trier une **copie** par date, puis comparer en `>` strict. |
| P-04 | Somme de flottants (`0.30000000000000004`). | Arrondir **à l'affichage** (1 décimale pour les litres, 0 pour les gourdes). |
| P-05 | Bibliothèque via CDN (Chart.js, PapaParse, Tailwind, polices Google). | JS et CSS natifs uniquement. |
| P-06 | CSV intégré dans la page. | Ne charger que par `FileReader` depuis le bouton. |
| P-07 | Libellé natif `<input type="file">` variable selon le navigateur. | Masquer l'input et utiliser un bouton ou label personnalisé « Choisir un fichier ». |
| P-08 | Fonctions hors sprint (graphique, export, édition, `localStorage`, mode sombre…). | Les refuser et les consigner (E-xx). |
| P-09 | Un second chargement ne réinitialise pas l'état. | Remplacer entièrement les données à chaque chargement. |
| P-10 | Cellules éditables ou bouton « enregistrer ». | Interface en lecture seule ; aucun téléchargement de fichier modifié. |

**Ressources externes** (P-05, RG-05), en PowerShell : `Select-String -Path <fichier> -Pattern '(https?:)?//(?!www\.w3\.org/)[a-z0-9.-]+\.[a-z]{2,}|@import|fetch\(|XMLHttpRequest|WebSocket'` ; chercher aussi `url(` et `src=`. Les espaces de noms `http://www.w3.org/…` sont tolérés.

---

## 8. Organisation en relais

| Relais | Porte | Mission | Fiche |
|---|---|---|---|
| R1 | G0 et G1 | Cadrage et socle (ce fichier, décisions, transcriptions, oracle, fiches) | Aucune |
| R2 | G2 | `cahier_des_charges.md` | `agents/01_analyste_cdc.md` |
| R3 | G3 | `product_backlog.md` | `agents/02_product_owner.md` |
| R4 | G4 | Prompt RMTCEV, délégation, `version_IA.html`, plan de test et fixtures | `agents/03_prompt_engineer.md` |
| R5 | G5 | Vérification, journal des écarts, `index.html`, captures | `agents/04_developpeur.md` et `agents/05_verificateur.md` |
| R6 | G6 et G7 | README, `prompts.md` final, fiche de contribution, test depuis le Drive sur un autre PC (téléversement : Leddycia, D-13) | `agents/06_finalisation_soutenance.md` |

**Après la remise**, chaque membre se prépare à la soutenance avec le « mode coach » de `agents/06_finalisation_soutenance.md`.

**Budget d'une heure** : 10 min de démarrage et d'audit, 40 min de mission, 10 min de passation. R2, R5 et R6 suivent le découpage minuté de leur fiche (**R6 démarre au plus tard à 22 h 00**). **À l'heure prévue, on passe la main même si c'est incomplet** : le reste à faire est écrit dans `ETAT_PROJET.md`.

---

## 9. Journal de bord et passation (D-14)

`ETAT_PROJET.md` est tenu à jour **par l'IA pendant le relais**, selon `agents/00_protocole_relais.md` :

1. **Démarrage** (après validation du plan) : relais **EN COURS** dans `ETAT_PROJET.md` §1, §2 et §8, avec le plan validé et la synthèse de l'audit.
2. **Pendant** : une ligne au journal de bord (§8) après chaque étape ; JP-xx et E-xx consignés au fil de l'eau (RG-11).
3. **« fin de notre relais »** (ou « fin du relais », « fen relè nou an ») : passation complète, après relecture du protocole §4 et §5. L'IA met à jour tout `ETAT_PROJET.md` (§1 à §8), écrit `travail/audits/RX_audit.md`, complète les journaux et `decisions.md`, puis commite, pose le tag annoté `relais-X` et pousse (`git ls-remote --tags origin` doit lister `relais-X`). Elle donne enfin le message de passation prêt à envoyer. **Cette phrase vaut demande explicite de commit et de push.** L'IA s'arrête si un original de `docs/` ou `version_IA.html` (après son tag) apparaît dans les fichiers indexés.
4. **« sauvegarde du relais »** : `ETAT_PROJET.md` à jour, commit et push, sans tag.

Commandes, contrôles, cas particuliers (tag existant, push refusé) et modèles : `agents/00_protocole_relais.md` §4 et §5. Une IA web fournit les contenus à coller et les commandes à lancer.

---

## 10. Arborescence et propriétaires

```
powerwatch/
├── AGENTS.md, CLAUDE.md, GEMINI.md        R1 (instructions d'IA)
├── ETAT_PROJET.md                         tous (témoin du relais)
├── PLAN_CADRAGE.md                        R1 (analyse de référence)
├── agents/                                R1 (fiches de rôle)
├── docs/                                  originaux (lecture seule) + transcriptions et oracle (R1)
├── travail/                               HORS LIVRABLE
│   ├── decisions.md                       tous (via statuts)
│   ├── journal_prompts.md                 tous
│   ├── journal_ecarts.md                  tous (surtout R5)
│   ├── brut/                              R4 (réponse brute de l'IA déléguée)
│   └── audits/RX_audit.md                 un fichier par relais
├── tests/                                 R4 (plan de test, fixtures), R5 (résultats)
└── Groupe_01_Cas_01/                      LIVRABLE (copié tel quel sur le Drive)
    ├── README.md                          R6
    ├── cahier_des_charges.md              R2
    ├── product_backlog.md                 R3
    ├── prompts.md                         R4 (prompt RMTCEV), complété par R6
    ├── prototype/version_IA.html          R4 (brut, intouchable)
    ├── prototype/index.html               R5
    └── captures/                          R5
```

`fiche_contribution.pdf` est créé par R6 **à la racine du dépôt**, au même niveau que `Groupe_01_Cas_01/`, comme sur le Drive (C-01). **Leddycia téléverse les deux sur le Drive** (D-13) ; rien d'autre n'est déposé.

---

## 11. Conventions

| Objet | Convention |
|---|---|
| Identifiants | B-xx brief ; C-xx consignes ; D/Q/H-xx décisions ; RG-xx règles d'or ; R-xx règles métier internes (§4) ; RM-xx règles métier et CT-xx contraintes du CDC (livrable) ; EF-xx et ENF-xx exigences ; US-xx user stories ; CA-xx.yy critères (CA-01.03 = 3e critère de l'US-01) ; P-xx pièges ; E-xx écarts ; JP-xx journal des prompts |
| Captures | `captures/USxx_CAyy_<detail>.png`, par exemple `US01_CA04_aout.png` |
| Commits | Format conventionnel, en français : `docs(r2): cahier des charges v1`, `fix(proto): E-13 tri chronologique du jour max` |
| Tags | `relais-1` … `relais-6` ; `version-ia` sur le commit de `version_IA.html`. Toujours annotés (`git tag -a`) : `--follow-tags` ne pousse pas un tag léger |
| Branche | `main` uniquement (les relais sont séquentiels). Jamais de `push --force`, jamais de réécriture d'historique ni de suppression de tag. |
| Dates dans les documents | Absolues (2026-10-18), jamais « hier » ni « demain » |

---

## 12. Definition of Done par livrable

| Livrable | Terminé quand… |
|---|---|
| `cahier_des_charges.md` | Les 5 rubriques de C-20 sont présentes. Chaque EF, ENF et RM cite un B-xx, chaque contrainte du projet (CT-xx) son C-xx (RG-01) ; la matrice de traçabilité est complète. Le hors périmètre reprend mot pour mot B-25 à B-27 (C-03) ; les souhaits B-21 à B-24, non tranchés (C-04), sont en rubrique 10 bis. Les points à décider reprennent les Q-xx ouvertes et provisoires. Aucune solution technique. |
| `product_backlog.md` | 8 US au format exact « En tant que… je veux… afin de… ». Chaque US a des CA observables et vérifiables, chiffrés avec l'oracle quand il le permet (toujours pour le Sprint 01) ; ceux d'US-07 et US-08 ne fixent ni formule ni seuil (Q-11, Q-12). MoSCoW, ordre et justification sont donnés. Les souhaits « plus tard » sont classés avec leur compatibilité. La section « Sprint 01 » donne l'objectif et US-01 à US-03. |
| `prompts.md` | Il contient le prompt RMTCEV **tel qu'envoyé** (écrit dans §1 et commité avant la délégation), avec le CDC et le Sprint 01 en contexte, l'outil, le modèle, la date et le mode exact de la session vierge. Il ajoute 2 ou 3 autres prompts importants avec ce qu'ils ont produit, et au moins une proposition de l'IA corrigée ou rejetée, avec sa raison. Tout écart C-12 éventuel y est signalé. |
| `version_IA.html` | Première sortie brute, identique au bloc HTML de la réponse brute, commitée avec le tag annoté `version-ia`, poussé (`git ls-remote --tags origin`). Réponse complète conservée dans `travail/brut/`. |
| `index.html` | Tous les CA du Sprint 01 sont respectés (ou le statut est justifié). RG-04 à RG-07 sont respectées. Aucune fonction hors sprint (C-23, C-09). |
| `captures/` | Au moins une capture par CA du Sprint 01, nommée selon la convention. La valeur attendue y est lisible. |
| `README.md` | Il explique comment ouvrir le prototype et liste les outils (IA et éditeur). Un tableau donne, pour chaque CA, le statut (respecté, non respecté ou partiel) et le lien vers la capture. Il mentionne `index.html` ou explique son absence (C-09), ainsi que le test sur un autre PC. |
| Remise | Dossier `Groupe_01_Cas_01/` et `fiche_contribution.pdf` au même niveau sur le Drive (téléversés par Leddycia, D-13), testés depuis le Drive sur un autre PC avant 23 h 59. |

---

## 13. Kit pour les IA web (ChatGPT, Gemini, Claude.ai)

Téléverse ou colle, **dans cet ordre** :

1. `AGENTS.md` ;
2. `ETAT_PROJET.md` ;
3. `agents/00_protocole_relais.md`, ta fiche `agents/0X_….md` et celle du relais suivant (pour ETAT §6) ;
4. `travail/decisions.md`, `travail/journal_prompts.md` et `travail/journal_ecarts.md` ;
5. les fichiers d'entrée listés dans ta fiche ;
6. la sortie copiée-collée de `git log --oneline -15`, `git status` et `git tag -l` ;
7. pour R2 : `docs/01_Demande_client.docx` et le PDF des consignes.

Puis envoie le prompt d'amorçage (§14). L'IA web ne voit pas le dépôt : demande-lui des modifications ciblées (« remplace la section X par… »), pas des fichiers entiers ; **c'est toi qui les reportes** dans les fichiers et relis `git diff --cached` après le bloc A (protocole, variante web).

## 14. Prompt d'amorçage standard (à copier au début de chaque relais)

```
Tu es l'IA assistante du relais R<X> du projet PowerWatch (cas 01).
1. Lis AGENTS.md en entier, puis ETAT_PROJET.md, agents/00_protocole_relais.md, la fiche agents/<fiche>.md
   et ses fichiers d'entrée. Tiens ETAT_PROJET.md à jour selon le protocole ; à « fin de notre relais »,
   fais la passation complète.
2. Analyse l'état actuel du dépôt (fichiers, contenu, derniers commits).
3. Audite le travail du relais précédent avec la checklist d'audit de ma fiche.
4. Présente-moi : (a) ton rapport d'audit (constat, preuve, gravité, action proposée),
   (b) ton plan pour mon heure de travail.
Ne modifie aucun fichier avant ma validation. Ne va jamais au-delà des consignes (docs/consignes.md)
ni du brief (docs/brief_client.md) ; tout point non fixé par le client devient une question Q-xx.
```

## 15. Ce que tu ne dois JAMAIS faire

- Modifier un fichier original de `docs/`, le CSV ou `version_IA.html` après son commit.
- Ajouter une exigence, une US, un CA ou une fonctionnalité sans la source exigée par RG-01.
- Trancher à la place du client une règle non fixée (part solaire, seuil d'alerte, etc.).
- Implémenter une US hors du sprint en cours, même « en bonus ».
- Utiliser une bibliothèque, un CDN, une police ou une ressource en ligne dans le prototype.
- Intégrer les données du CSV dans le HTML.
- Réécrire en bloc le livrable d'un relais précédent.
- Produire `version_IA.html` hors d'une session vierge (D-09 ; voir `CLAUDE.md` et la fiche 03) : ni session qui a lu ce dépôt, ni CLI qui charge des instructions globales (`~/.claude/`, `~/.codex/`).
- `git push --force`, réécrire l'historique, supprimer un tag.
- Terminer un relais sans mettre à jour `ETAT_PROJET.md`.

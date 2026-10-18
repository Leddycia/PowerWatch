# ÉTAT DU PROJET : le témoin du relais

> **Premier fichier à lire après `AGENTS.md`, au début de chaque relais.** Il est **tenu à jour par l'IA du relais en cours** (`agents/00_protocole_relais.md`, D-14) : au démarrage, après chaque étape (journal de bord, §8), et en entier quand le membre dit **« fin de notre relais »**.
> On **complète** ce fichier, on n'efface pas l'historique : le journal des passations (§7) se remplit uniquement par ajout.

---

## 0. Prérequis (une seule fois, avant ton premier créneau)

1. Accepter l'invitation GitHub comme collaborateur (nécessaire pour pousser ; le dépôt est public, D-12).
2. Installer Git for Windows (il fournit Git Bash).
3. Configurer ton identité Git avec ton adresse noreply (GitHub › Settings › Emails › « Keep my email addresses private ») :

   ```bash
   git config --global user.name "Prénom Nom"
   git config --global user.email "<id>+<login>@users.noreply.github.com"
   ```

4. Cloner le dépôt (connexion GitHub dans le navigateur ; SSH possible si une clé est enregistrée) :

   ```bash
   git clone https://github.com/Leddycia/PowerWatch.git
   ```

5. Vérifier, dans Git Bash et dans le dossier cloné : `git fetch --tags && git tag -l`.
6. Préparer ton IA (pour Gemini : voir `GEMINI.md`, Antigravity CLI pour un compte personnel).
7. Ne modifie pas ce fichier sur l'interface web de GitHub pendant le relais d'un autre membre (risque de conflit à sa passation) : demande-le à l'IA du relais en cours, ou fais-le entre deux relais.

## 1. Tableau de bord

| | |
|---|---|
| **Porte atteinte** | G3 (product backlog v1, Sprint 01 = US-01 à US-03 avec 20 CA chiffrés) ; G2 confirmée par l'audit de R3 (relecture humaine mot à mot du CDC : conforme) |
| **Relais terminé** | R3 (product backlog) |
| **Relais en cours** | Aucun (voir §8) |
| **Prochain relais** | **R4 : prompt RMTCEV, délégation, `version_IA.html`, plan de test et fixtures** (fiche `agents/03_prompt_engineer.md`) |
| **Échéance de remise** | **Dimanche 18/10/2026, 23 h 59**, sur le Drive (C-19) |
| **Sprint 01** | US-01 (chargement et totaux), US-02 (coût), US-03 (jour max) (D-01) |
| **Dépôt** | `https://github.com/Leddycia/PowerWatch.git` (HTTPS, pour cloner : §0) ou `git@github.com:Leddycia/PowerWatch.git` (SSH, si ta clé est enregistrée), branche `main` ; dépôt **public**, laissé public par décision de Leddycia (D-12, O-8) |

## 2. Tableau des relais

| Relais | Membre | Outil d'IA | Créneau prévu | Porte | Statut | Tag |
|---|---|---|---|---|---|---|
| R1 | Leddycia | Claude Code (Claude Opus 5.5) | 18/10, matin | G0 et G1 | **FAIT** (commit tagué `relais-1`) ; complément FAIT (10:40 → 11:37, non tagué) | `relais-1` |
| R2 | Leddycia | Claude Code (Claude Opus 5.5) | 18/10, matin | G2 | **FAIT** (10:49 → 11:48) | `relais-2` |
| R3 | Leddycia | Claude Code (application de bureau, Claude Opus 5.5) | *à compléter* | G3 | **FAIT** (11:55 → 12:06) | `relais-3` |
| R4 | Bradley | Antigravity (Gemini), modèle à préciser au démarrage | *à compléter* | G4 | À FAIRE | `relais-4`, `version-ia` |
| R5 | *à compléter* | *à compléter* | *à compléter* | G5 | À FAIRE | `relais-5` |
| R6 | *à compléter* | *à compléter* | *à compléter* | G6 et G7 | À FAIRE | `relais-6` |

**Statuts** : À FAIRE / EN COURS (début HH:MM) / FAIT (HH:MM → HH:MM) / FAIT (partiel) / FAIT (remise à confirmer) / REMIS. La colonne « Créneau prévu » ne change pas pendant le relais.

**R6 démarre au plus tard à 22 h 00.**

**Ordre de remplacement** : si le membre de RX est indisponible, le membre prévu pour R(X+1) prend la fiche de RX et les relais suivants glissent d'un cran ; aucune porte n'est sautée ; celui qui reprend une fiche inscrit son nom au §2 et dans le journal.

**Relecteur du prompt RMTCEV** : le membre de R3, joignable par message entre la 20e et la 30e minute de R4. Sans réponse en 5 min, R4 délègue quand même et écrit « relu par un seul membre » dans `prompts.md` §1 et dans ce fichier.

## 3. Ce qui est fait

| Élément | Fichier | Relais |
|---|---|---|
| Analyse complète des consignes, du brief et du CSV ; arbitrages ; risques | `PLAN_CADRAGE.md` | R1 |
| Registre des décisions (D-01 à D-14, Q-01 à Q-14, H-01 à H-06) | `travail/decisions.md` | R1 |
| Transcription fidèle et numérotée du brief (B-01 à B-27) | `docs/brief_client.md` | R1 |
| Transcription fidèle et numérotée des consignes (C-01 à C-23) | `docs/consignes.md` | R1 |
| Oracle : valeurs justes, égalités, signature du bug de fuseau, détail jour par jour, empreinte SHA-256 (valeurs calculées par un script Python déterministe, écrit et exécuté par l'IA assistante de R1, indépendamment de l'IA déléguée et du prototype : voir « Méthode » en tête de l'oracle et le journal R1 au §7 ; contre-vérification humaine obligatoire par R2 : §6) | `docs/oracle.md` | R1 |
| Instructions d'IA, source unique | `AGENTS.md` | R1 |
| Points d'entrée Claude et Gemini | `CLAUDE.md`, `GEMINI.md` | R1 |
| 6 fiches de rôle (R2 à R6, plus le mode coach) | `agents/*.md` | R1 |
| Journaux de travail initialisés | `travail/journal_prompts.md`, `travail/journal_ecarts.md` | R1 |
| Conservation des octets exacts du CSV et de `version_IA.html` (aucune conversion de fins de ligne par Git) | `.gitattributes` | R1 |
| CSV rétabli dans ses octets d'origine CRLF : le commit initial 478570e l'avait stocké en LF (conversion `core.autocrlf`). Le commit de R1 rétablit ces octets grâce à `.gitattributes` : `git log --stat` le montre donc modifié par R1. C'est voulu, les données ne changent pas (empreinte `320155c7…a84b`). **Ne jamais le restaurer depuis 478570e.** | `docs/energie_college.csv` | R1 |
| Relecture adversariale automatisée du socle (workflow Claude Code, 18 agents ; 142 constats, dont 103 confirmés après tentative de réfutation), puis application des corrections validées par Leddycia ; erreurs de l'IA de R1 consignées en E-01 à E-12 | tous les fichiers du socle ; `travail/journal_ecarts.md` | R1 |
| Protocole de relais (D-14) : `ETAT_PROJET.md` tenu à jour par l'IA pendant le relais (journal de bord §8) ; « fin de notre relais » déclenche la passation complète ; « sauvegarde du relais » et « reprise du relais » ; variante IA web ; vérifié par deux passes de simulation (Claude Code, Codex, Antigravity, IA web) et commandes Git testées | `agents/00_protocole_relais.md`, `AGENTS.md` §0, §9, §13, §14, `CLAUDE.md`, `GEMINI.md`, `ETAT_PROJET.md` §0 et §8 | R1 (complément) |
| Remise sur le Drive par Leddycia (D-13) : R6 prépare dans le dépôt (`fiche_contribution.pdf` à la racine), Leddycia fait `git pull`, vérifie le hash et téléverse | `agents/06_finalisation_soutenance.md`, `AGENTS.md` §8, §10, §12 | R1 (complément) |
| Journal de bord de R1 conservé ; erreurs du protocole v1 consignées en E-13 ; JP-08 et JP-09 | `travail/audits/R1_audit.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md` | R1 (complément) |
| Cahier des charges v1 : 8 EF, 2 ENF, 4 RM, 5 contraintes du projet (CT), hors périmètre et souhaits ultérieurs repris mot pour mot, Q-01 à Q-17 et H-01 à H-06 au §11, matrices B-01 à B-27 et C-xx ; rédigé par un workflow Claude Code de 9 agents (2 brouillons, synthèse, 5 vérificateurs adverses : 35 constats, 29 appliqués, 6 rejetés), puis contrôlé par script (DoD conforme) | `Groupe_01_Cas_01/cahier_des_charges.md` | R2 |
| Audit d'entrée du socle de R1 (A1, A2 : diffs mot à mot `.docx` et PDF conformes ; A4, A5 conformes) et relecture du protocole v2 (3 manques mineurs) | `travail/audits/R2_audit.md` | R2 |
| Oracle recalculé par trois méthodes indépendantes (Python, awk, PowerShell) et comparé automatiquement à tous ses tableaux : aucun écart ; remplace le recalcul humain A3 (D-15) ; scripts en annexe de l'audit | `travail/audits/R2_audit.md`, `travail/decisions.md` | R2 |
| Registre complété : D-15, Q-15 à Q-17 ; 12 points non fixés par le client renvoyés à R3 et R4 | `travail/decisions.md`, `travail/audits/R2_audit.md` | R2 |
| Journaux : JP-10 à JP-14 (JP-11 : instructions exactes de rédaction du CDC, candidat pour `prompts.md`), E-14 à E-19 | `travail/journal_prompts.md`, `travail/journal_ecarts.md` | R2 |
| Product backlog v1 : 8 US au format exact, 34 CA (Sprint 01 : CA-01.01 à CA-01.11, CA-02.01 à CA-02.05, CA-03.01 à CA-03.04, chiffrés avec l'oracle), ordre et MoSCoW justifiés, souhaits « plus tard » avec compatibilité, section Sprint 01 (objectif, hypothèses appliquées, fichiers de test nécessaires, DoD) ; contrôlé par script (valeurs recalculées depuis le CSV) et relu par Leddycia | `Groupe_01_Cas_01/product_backlog.md` | R3 |
| Audit d'entrée du CDC (A1 à A6 conformes ; relecture humaine mot à mot conforme) | `travail/audits/R3_audit.md` | R3 |
| Q-18 (colonnes du tableau jour par jour), Q-19 (ordre chronologique du tableau), Q-20 (rappel du prix de référence), dans le registre et ajoutées de façon ciblée au CDC (§4, RM-01, §11.1, §12.1) | `travail/decisions.md`, `Groupe_01_Cas_01/cahier_des_charges.md` | R3 |
| Journaux : JP-15 à JP-17, E-20 et E-21 | `travail/journal_prompts.md`, `travail/journal_ecarts.md` | R3 |

## 4. Ce qui reste (par ordre de priorité)

1. **Reste de R3, à reprendre par R4** : rien de partiel. À traiter avant le prompt : O-9 (format des litres, §5) ; fichier de test « août et septembre seuls » (CA-01.09, CA-01.10) à ajouter à `docs/oracle.md` §8.
2. **R4** : prompt RMTCEV, délégation en session vierge, `version_IA.html`, plan de test et fixtures (G4).
3. **R5** : vérification, journal des écarts, `index.html`, captures (G5).
4. **R6** : README, `prompts.md` final, `fiche_contribution.pdf` (à la racine du dépôt), test depuis le Drive sur un autre PC (G6 et G7). **Téléversement sur le Drive : Leddycia** (D-13).
5. **Tous** : préparation de la soutenance (mode coach, fiche 06).

## 5. Points ouverts et bloquants

| # | Point | Bloque | Qui |
|---|---|---|---|
| O-1 | **Numéro du groupe** (D-11) : **résolu**, Groupe 01. Livrable `Groupe_01_Cas_01/`, dossier Drive `Groupe_01/`. | Plus rien | Équipe |
| O-2 | **Noms, ordre des relais et outil d'IA de chaque membre** (§2) : R2 et R3 = Leddycia (Claude Code) ; R4 = Bradley (Antigravity, Gemini ; modèle à préciser au démarrage) ; **R5 et R6 à compléter** avant leur créneau | Organisation ; message de passation de R4 | Équipe |
| O-3 | **Accès au dépôt GitHub** : invitations **envoyées** par Leddycia le 2026-10-18. Chaque membre doit les **accepter** avant son créneau (§0, étape 1). | `push` de chaque relais | Chaque membre |
| O-4 | Définition exacte de RMTCEV dans le cours (hypothèse D-02 en vigueur) | Rien (hypothèse en place) ; à remplacer avant R4 si elle est retrouvée | Tout membre |
| O-5 | **Résolu par R2** : questions au client Q-01 à Q-17 listées au §11.1 du CDC avec leur hypothèse provisoire (Q-15 à Q-17 ajoutées par R2, JP-13) | Rien (résolu) | R2 |
| O-6 | Décision D-10 (pièges dans le prompt ou non) | Prompt RMTCEV | R4 |
| O-7 | **Résolu le 2026-10-18 : Leddycia téléverse elle-même sur le Drive** (D-13) le dossier `Groupe_01_Cas_01/` et `fiche_contribution.pdf`, pris dans le dépôt. Elle doit être **joignable pendant le créneau de R6** (vers la 35e minute, puis pour le README final). | Rien (résolu) | Leddycia |
| O-8 | **Résolu le 2026-10-18 : dépôt laissé public, décision de Leddycia** (D-12), prise en connaissance de cause après vérification (accès anonyme possible). Tout ce qui est poussé est public : noms des membres, journaux, e-mail de l'auteur de chaque commit. Adresse noreply fortement recommandée pour chaque membre (§0). | Rien (résolu) | Leddycia (propriétaire du dépôt) ; chaque membre pour son adresse |
| O-9 | **B-14 contre R-04** : le brief dit « les litres peuvent avoir une décimale » ; `AGENTS.md` R-04 et la fiche 01 écrivent « au plus une décimale ». Le CDC garde le texte du client (RM-03) et renvoie le format exact à Q-01 ; les CA du backlog citent l'hypothèse Q-01 (toujours une décimale). | À trancher dans `decisions.md` avant le prompt de R4 | Équipe, R4 |
| O-10 | **12 points non fixés par le client, renvoyés à R3 et R4** (liste : `travail/audits/R2_audit.md`, « Points remontés ») : **part de R3 résolue** (#1, #2 et #11 → Q-18 à Q-20 ; #4 et #5 → CA-01.10 et CA-01.09) ; reste pour R4 : fixtures (#3, #6 à #9), précision de Q-10 (fichier avec BOM, #10), poste de la directrice (#12, avec R5) | Fixtures, prompt | R4 |
| O-11 | **Fiche 01** : sa DoD admet une CT citant un B-xx, sa structure (§7) les réserve aux consignes ; le CDC suit la structure | Rien | Équipe |
| O-12 | **Fiche 02** : sa checklist d'audit A5 cite encore « Q-01 à Q-14 » ; le registre en compte désormais Q-01 à Q-20 | Rien | Équipe |

## 6. Mission du prochain relais : R4

1. Après les prérequis du §0 : `git pull`, puis `git fetch --tags` et `git tag -l` (`relais-1`, `relais-2` et `relais-3` doivent apparaître), puis ouvrir ton IA (Antigravity dans le dépôt : voir `GEMINI.md` ; ou le kit web de `AGENTS.md` §13) et vérifier le chargement : lui demander « Cite mot pour mot la règle RG-08 d'AGENTS.md ».
2. Lancer le prompt d'amorçage de `AGENTS.md` §14, en remplaçant `<X>` par `4` et `<fiche>` par `03_prompt_engineer`. Une fois le plan validé, l'IA marque R4 « EN COURS » ici (§1, §2 et §8), crée `travail/audits/R4_audit.md` et tient le journal de bord de §8 pendant tout le relais. Donne-lui le modèle exact de ton outil (§2, « modèle à préciser »).
3. **Audit du product backlog de R3** (checklist A1 à A5 de ta fiche ; démarrage et audit : 10 min). En particulier :
   - vérifie d'abord que ton IA a lu en entier `Groupe_01_Cas_01/cahier_des_charges.md` (33 ko) et `Groupe_01_Cas_01/product_backlog.md` (24,5 ko) : la limite de 24 000 octets d'Antigravity vaut pour ses fichiers de règles ; demande-lui de citer la dernière ligne du §12.3 du CDC et le dernier point de la DoD du §5 du backlog ;
   - A3 : comparer chaque valeur des CA du Sprint 01 à `docs/oracle.md` §2 et §4, ainsi qu'au §5 pour les CA du fuseau ; CA-01.10 (54 h et 155,0 L) est la somme des valeurs d'août et de septembre de l'oracle §2.1 ;
   - A5 : fuseau d'Haïti (CA-01.05, CA-02.04, CA-03.04), fichier mélangé (CA-03.02), hors ligne (CA-01.01), empreinte du CSV (CA-01.08).
4. Mission selon la fiche 03 :
   - avant le prompt : trancher D-10 et, avec l'équipe, O-9 (format des litres) ; préciser Q-10 pour un fichier avec BOM (O-10 #10) dans `travail/decisions.md` ;
   - rédiger le prompt RMTCEV : il embarque le cahier des charges **intégral** et la section Sprint 01 **complète**, avec US-01 à US-03 et **tous leurs CA** (CA-01.01 à CA-01.11, CA-02.01 à CA-02.05, CA-03.01 à CA-03.04) ; relecture par Leddycia (membre de R3) entre la 20e et la 30e minute ; prompt commité dans `prompts.md` §1 **avant** la délégation ;
   - déléguer **une seule fois** en session vierge (D-09) : de préférence une IA web en conversation temporaire ; Antigravity CLI seulement dans un dossier vide hors du dépôt et si `~/.gemini/GEMINI.md` n'existe pas ; jamais la session qui a lu ce dépôt. `version_IA.html` brut, contrôle `git diff --no-index` vide, commit, tag annoté `version-ia` et push ;
   - `prompts.md` v1 (sections 1 à 4) ; plan de test et fichiers de test : les cinq cités par les CA du Sprint 01 (lignes mélangées, colonne manquante, valeur `abc`, mois sans génératrice, et un nouveau : l'en-tête et les 24 lignes d'août et de septembre, pour CA-01.09 et CA-01.10), plus f05 (décimales) ; leurs résultats attendus dans `docs/oracle.md` §8, calculés hors de l'IA déléguée.
   - Points d'attention : les hypothèses Q-01 à Q-06, Q-09, Q-16, Q-17 et Q-20 sont appliquées par le Sprint 01, jamais présentées comme des règles du client ; Q-18 et Q-19 ne concernent que l'US-04, hors sprint ; aucune fonction hors Sprint 01 (ni tableau jour par jour, ni graphique, ni stockage local).
5. Passation : dire **« fin de notre relais »** à ton IA. Elle met à jour ce fichier, complète `travail/audits/R4_audit.md` et les journaux, commite, pose le tag annoté `relais-4`, pousse (`git ls-remote --tags origin` doit afficher `relais-4` et `version-ia`) et te donne le message à envoyer au groupe (`agents/00_protocole_relais.md` §4). Relis son compte rendu avant d'envoyer le message. Avec une IA web, c'est toi qui colles les contenus et lances les commandes qu'elle te donne, en deux blocs (protocole, « Variante pour une IA web »).

---

## 7. Journal des passations (une entrée par relais, plus une par complément, ajoutée à la fin de cette section, juste avant le §8)

### R1 : cadrage et socle (18/10/2026)

- **Membre et outil** : Leddycia, Claude Code (Claude Opus 5.5).
- **Audit d'entrée** : sans objet, premier relais. **Auto-contrôle** :
  - oracle : valeurs calculées par un script Python déterministe, écrit et exécuté par l'IA assistante du relais R1 (Claude Code, Claude Opus 5.5), indépendamment de l'IA déléguée et du prototype, puis contrôlées une seconde fois (simulation du bug de fuseau) ; le script n'a pas été conservé dans le dépôt ; une relecture adversariale automatisée les a recalculées sans trouver d'erreur de valeur ; contre-vérification humaine obligatoire par R2 (§6) ;
  - texte du brief extrait directement du `.docx` (y compris la numérotation 1 à 4 des priorités) ;
  - consignes transcrites depuis le PDF.
- **Relecture adversariale** : automatisée, sur tout le socle (workflow Claude Code, 18 agents) ; 142 constats, dont 103 confirmés après tentative de réfutation. Corrections validées par Leddycia (JP-05), puis appliquées. Les erreurs de l'IA de R1 sont consignées en E-01 à E-12 (`travail/journal_ecarts.md`).
- **CSV** : le commit initial 478570e avait stocké `docs/energie_college.csv` en LF (conversion `core.autocrlf`). Le commit de R1 rétablit ses octets d'origine CRLF grâce à `.gitattributes` : `git log --stat` le montre donc modifié par R1. C'est voulu, les données ne changent pas (empreinte `320155c7…a84b`). Ne jamais le restaurer depuis 478570e.
- **Fait** : voir §3.
- **Décisions** : D-01 à D-05 validées par l'équipe ; D-06 à D-09 et H-01 à H-06 proposées par l'IA (R1), validées par Leddycia à la relecture humaine du 2026-10-18 ; D-11 validée (Groupe 01) ; D-12 validée (dépôt laissé public, décision de Leddycia) ; D-10 à trancher par R4 ; Q-01 à Q-14 provisoires ou ouvertes (Q-08 : « Non en V1 »).
- **Points d'attention pour R2** :
  - **ne pas présenter les Q-xx comme des règles du client** ;
  - toute exigence (EF, ENF, RM) cite un B-xx ; une obligation qui ne vient que des consignes est une contrainte du projet (CT-xx), placée en section 7 « Contraintes » avec son C-xx, et non en EF ou ENF ;
  - aucune solution technique dans le CDC ;
  - `docs/energie_college.csv` apparaît modifié par le commit de R1 : c'est voulu (voir ci-dessus).
- **Porte** : G0 atteinte ; G1 atteinte sous réserve de l'audit de R2.

### R1 (complément) : protocole de relais et remise par Leddycia (2026-10-18, 10:40 → 11:37)

- **Membre et outil** : Leddycia, Claude Code (Claude Opus 5.5).
- **Audit d'entrée** : sans objet (complément de R1). Détail : `travail/audits/R1_audit.md`.
- **Fait** : protocole de relais `agents/00_protocole_relais.md` (D-14) et son branchement (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, ETAT §0 et §8, fiches) ; remise sur le Drive par Leddycia (D-13, fiche 06) ; invitations GitHub envoyées (O-3) ; deux passes de simulation multi-outils (87 puis 28 constats confirmés, corrigés : E-13) ; commit distant a468c31 intégré (R2 attribué à Leddycia).
- **Reste** : O-2 (membres de R3 à R6) ; relecture humaine du protocole par R2 lors de son audit.
- **Décisions** : D-13 et D-14 validées (JP-08) ; le plan a été déduit de JP-08 et exécuté sans validation préalable, la clôture demandée par Leddycia (JP-09) vaut acceptation.
- **Points d'attention pour R2** :
  - au démarrage, ton IA lit `agents/00_protocole_relais.md` puis marque R2 « EN COURS » ici ; garde ce journal de bord à jour et termine par « fin de notre relais » ;
  - ne modifie pas ce fichier sur le web pendant un relais (ETAT §0, étape 7) : c'est ce qui a causé le conflit de ce complément ;
  - audite aussi le protocole (lisibilité, cohérence avec ta fiche) et note tes constats dans `travail/audits/R2_audit.md`.
- **Porte** : G1 inchangée (socle prêt, sous réserve de l'audit de R2).
- **Tag** : complément, commit non tagué (le tag `relais-1` reste sur le commit du socle). Le hash du commit figure dans le compte rendu et le message de passation.

### R2 : cahier des charges (2026-10-18, 10:49 → 11:48)

- **Membre et outil** : Leddycia, Claude Code (application de bureau, Claude Opus 5.5) ; rédaction confiée à un workflow Claude Code de 9 agents (même modèle).
- **Audit d'entrée** : socle de R1 conforme sur A1 et A2 (diffs mot à mot de l'IA ; contrôle humain annoncé, résultat non communiqué), A4 et A5 ; A3 : recalcul humain non fait, remplacé par un recalcul automatique indépendant, sans écart (D-15) ; démarrage alors que le complément de R1 était encore ouvert dans une autre session : écritures différées jusqu'à son push (11:37) ; protocole v2 relu (3 manques mineurs) (détail : `travail/audits/R2_audit.md`).
- **Fait** : `Groupe_01_Cas_01/cahier_des_charges.md` v1 (§3) ; D-15 ; Q-15 à Q-17 ; JP-10 à JP-14 ; E-14 à E-19.
- **Reste** : relecture humaine mot à mot du CDC (à reprendre par R3, dans son audit) ; O-9 et O-11 à trancher par l'équipe ; points O-10 à traiter par R3 et R4.
- **Décisions** : D-15 validée (Leddycia, JP-12) ; Q-15 à Q-17 provisoires, hypothèses proposées par l'IA et validées par Leddycia (JP-13) ; arbitrages de rédaction validés à l'audit (constat 9) : EF-01 sur B-06 seul, libellé « Choisir un fichier » en contrainte du projet CT-03, B-14 et B-15 seulement en RM, Q-04 seulement au §11, aucune valeur de l'oracle dans le CDC.
- **Points d'attention pour R3** :
  - porte G2 : atteinte (DoD de la fiche 01 et d'`AGENTS.md` §12 contrôlée par script) ;
  - sections incomplètes : aucune ; la relecture humaine mot à mot reste à faire ;
  - exigences dont la source est discutable : EF-02 au rang 1 (lecture de « pour un mois donné », B-20.1) ; EF-06 « pour la période » lu comme la période choisie (B-08, avec B-07 et B-09) ; définitions du §4 « jour = une ligne du fichier » et « toute la période = tous les jours du fichier chargé » (lectures de l'équipe) ; CT-01 garde « CSS » et « JavaScript », termes de C-10 ;
  - nouvelles Q-xx : Q-15 à Q-17 ;
  - mission de R3 : backlog à partir du CDC, CA du Sprint 01 chiffrés avec l'oracle, Q-15 à Q-17 et points O-10 traités dans les CA.
- **Porte** : G2 atteinte.
- **Tag** : `relais-2`. Le hash du commit figure dans le compte rendu et le message de passation.

### R3 : product backlog (2026-10-18, 11:55 → 12:06)

- **Membre et outil** : Leddycia, Claude Code (application de bureau, Claude Opus 5.5).
- **Audit d'entrée** : cahier des charges de R2 conforme sur A1 à A6 (contrôles par script hors du dépôt) ; relecture humaine mot à mot par Leddycia : conforme ; points O-10 de R3 traités par Q-18 à Q-20 ; esquisse de la fiche 02 complétée (fuseau testé aussi sur le coût et le jour max, E-21) (détail : `travail/audits/R3_audit.md`).
- **Fait** : `Groupe_01_Cas_01/product_backlog.md` v1 (8 US, 34 CA, dont 20 pour le Sprint 01, contrôlés par un recalcul indépendant depuis le CSV, relus par Leddycia) ; Q-18 à Q-20 dans le registre et dans le CDC ; JP-15 à JP-17 ; E-20 et E-21.
- **Reste** : rien de partiel. À traiter par R4 avant le prompt : O-9 ; fichier de test « août et septembre seuls » à décrire dans `docs/oracle.md` §8.
- **Décisions** : Q-18 à Q-20 provisoires, hypothèses proposées par l'IA et validées par Leddycia (JP-16) ; ajout ciblé au CDC validé (JP-16) ; CA-01.11 (valeur non numérique, Q-04) ajouté en plus du plan.
- **Points d'attention pour R4** :
  - porte G3 : atteinte (DoD de la fiche 02 contrôlée par script) ;
  - CA encore flous : aucun pour le Sprint 01 ; ceux d'US-06 à US-08 attendent la réponse du client (Q-11 à Q-13) ; CA-03.03 dépend du fichier de test « mois sans génératrice », à créer ;
  - Q-xx qui pèsent sur le Sprint 01 : Q-01 (litres, lié à O-9), Q-02 (liste des mois), Q-03 (période par défaut), Q-04 (fichier invalide), Q-05 (période sans fonctionnement), Q-06 (prix constant), Q-09 (fuseau d'Haïti), Q-16 (heures en « h »), Q-17 (jour max avec ses heures), Q-20 (rappel du prix de référence) ;
  - le prompt RMTCEV doit embarquer le CDC **et** la section Sprint 01 **complète, avec US-01 à US-03 et tous leurs CA** ;
  - outil de R4 : Antigravity ; la délégation ne se fait jamais depuis la session qui a lu le dépôt (D-09).
- **Porte** : G3 atteinte.
- **Tag** : `relais-3`. Le hash du commit figure dans le compte rendu et le message de passation.

---

## 8. Relais en cours (journal de bord, tenu par l'IA)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

**Aucun relais en cours.** Prochain relais : voir §1.

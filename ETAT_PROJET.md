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
| **Porte atteinte** | G2 (cahier des charges v1) ; G1 confirmée par l'audit de R2, le recalcul humain A3 étant remplacé par un recalcul automatique (D-15) |
| **Relais terminé** | R2 (cahier des charges) |
| **Relais en cours** | Aucun (voir §8) |
| **Prochain relais** | **R3 : product backlog** (fiche `agents/02_product_owner.md`) |
| **Échéance de remise** | **Dimanche 18/10/2026, 23 h 59**, sur le Drive (C-19) |
| **Sprint 01** | US-01 (chargement et totaux), US-02 (coût), US-03 (jour max) (D-01) |
| **Dépôt** | `https://github.com/Leddycia/PowerWatch.git` (HTTPS, pour cloner : §0) ou `git@github.com:Leddycia/PowerWatch.git` (SSH, si ta clé est enregistrée), branche `main` ; dépôt **public**, laissé public par décision de Leddycia (D-12, O-8) |

## 2. Tableau des relais

| Relais | Membre | Outil d'IA | Créneau prévu | Porte | Statut | Tag |
|---|---|---|---|---|---|---|
| R1 | Leddycia | Claude Code (Claude Opus 5.5) | 18/10, matin | G0 et G1 | **FAIT** (commit tagué `relais-1`) ; complément FAIT (10:40 → 11:37, non tagué) | `relais-1` |
| R2 | Leddycia | Claude Code (Claude Opus 5.5) | 18/10, matin | G2 | **FAIT** (10:49 → 11:48) | `relais-2` |
| R3 | Leddycia | *à compléter* | *à compléter* | G3 | À FAIRE | `relais-3` |
| R4 | *à compléter* | *à compléter* | *à compléter* | G4 | À FAIRE | `relais-4`, `version-ia` |
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

## 4. Ce qui reste (par ordre de priorité)

1. **Reste de R2, à reprendre par R3** : relecture humaine mot à mot du cahier des charges (annoncée, non confirmée) ; points O-9 à O-11 (§5).
2. **R3** : `Groupe_01_Cas_01/product_backlog.md` (G3).
3. **R4** : prompt RMTCEV, délégation en session vierge, `version_IA.html`, plan de test et fixtures (G4).
4. **R5** : vérification, journal des écarts, `index.html`, captures (G5).
5. **R6** : README, `prompts.md` final, `fiche_contribution.pdf` (à la racine du dépôt), test depuis le Drive sur un autre PC (G6 et G7). **Téléversement sur le Drive : Leddycia** (D-13).
6. **Tous** : préparation de la soutenance (mode coach, fiche 06).

## 5. Points ouverts et bloquants

| # | Point | Bloque | Qui |
|---|---|---|---|
| O-1 | **Numéro du groupe** (D-11) : **résolu**, Groupe 01. Livrable `Groupe_01_Cas_01/`, dossier Drive `Groupe_01/`. | Plus rien | Équipe |
| O-2 | **Noms, ordre des relais et outil d'IA de chaque membre** (§2) : R2 = Leddycia (Claude Code) ; R3 = Leddycia (outil à compléter au démarrage) ; **R4 à R6 à compléter** avant leur créneau | Organisation ; message de passation de R3 | Équipe |
| O-3 | **Accès au dépôt GitHub** : invitations **envoyées** par Leddycia le 2026-10-18. Chaque membre doit les **accepter** avant son créneau (§0, étape 1). | `push` de chaque relais | Chaque membre |
| O-4 | Définition exacte de RMTCEV dans le cours (hypothèse D-02 en vigueur) | Rien (hypothèse en place) ; à remplacer avant R4 si elle est retrouvée | Tout membre |
| O-5 | **Résolu par R2** : questions au client Q-01 à Q-17 listées au §11.1 du CDC avec leur hypothèse provisoire (Q-15 à Q-17 ajoutées par R2, JP-13) | Rien (résolu) | R2 |
| O-6 | Décision D-10 (pièges dans le prompt ou non) | Prompt RMTCEV | R4 |
| O-7 | **Résolu le 2026-10-18 : Leddycia téléverse elle-même sur le Drive** (D-13) le dossier `Groupe_01_Cas_01/` et `fiche_contribution.pdf`, pris dans le dépôt. Elle doit être **joignable pendant le créneau de R6** (vers la 35e minute, puis pour le README final). | Rien (résolu) | Leddycia |
| O-8 | **Résolu le 2026-10-18 : dépôt laissé public, décision de Leddycia** (D-12), prise en connaissance de cause après vérification (accès anonyme possible). Tout ce qui est poussé est public : noms des membres, journaux, e-mail de l'auteur de chaque commit. Adresse noreply fortement recommandée pour chaque membre (§0). | Rien (résolu) | Leddycia (propriétaire du dépôt) ; chaque membre pour son adresse |
| O-9 | **B-14 contre R-04** : le brief dit « les litres peuvent avoir une décimale » ; `AGENTS.md` R-04 et la fiche 01 écrivent « au plus une décimale ». Le CDC garde le texte du client (RM-03) et renvoie le format exact à Q-01. | Rien pour R3 ; à trancher dans `decisions.md` avant le prompt de R4 | Équipe |
| O-10 | **12 points non fixés par le client, renvoyés à R3 et R4** (liste : `travail/audits/R2_audit.md`, « Points remontés ») : CA des US-01, US-02 et US-04 pour R3 ; fixtures et précision de Q-10 (fichier avec BOM) pour R4 | CA du backlog, fixtures | R3, R4 |
| O-11 | **Fiche 01** : sa DoD admet une CT citant un B-xx, sa structure (§7) les réserve aux consignes ; le CDC suit la structure | Rien | Équipe |

## 6. Mission du prochain relais : R3

1. Après les prérequis du §0 : `git pull`, puis `git fetch --tags` et `git tag -l` (`relais-1` et `relais-2` doivent apparaître), puis ouvrir ton IA (dans le dépôt, ou avec le kit web de `AGENTS.md` §13) et vérifier le chargement : lui demander « Cite mot pour mot la règle RG-08 d'AGENTS.md ».
2. Lancer le prompt d'amorçage de `AGENTS.md` §14, en remplaçant `<X>` par `3` et `<fiche>` par `02_product_owner`. Une fois le plan validé, l'IA marque R3 « EN COURS » ici (§1, §2 et §8), crée `travail/audits/R3_audit.md` et tient le journal de bord de §8 pendant tout le relais. Donne-lui ton outil d'IA et son modèle (§2, « à compléter »).
3. **Audit du cahier des charges de R2** (checklist A1 à A6 de ta fiche ; démarrage et audit : 10 min). En particulier :
   - **relire toi-même mot à mot** les passages du CDC cités entre guillemets (§3, RM-01, §8, §9, §10, §10 bis) contre `docs/brief_client.md` : la relecture humaine de R2 n'a pas été confirmée ;
   - tirer 5 exigences au hasard et vérifier leur B-xx ou C-xx (A2) ;
   - A5 : le CDC liste désormais **Q-01 à Q-17** (Q-15 à Q-17 ajoutées par R2).
4. Rédiger `Groupe_01_Cas_01/product_backlog.md` selon la fiche 02 : 8 US au format exact, CA « Étant donné… quand… alors… » chiffrés avec `docs/oracle.md` pour le Sprint 01 (l'oracle a été recalculé sans écart par R2 : D-15), MoSCoW et ordre justifiés, souhaits « plus tard » avec leur compatibilité, section Sprint 01 (US-01 à US-03, D-01). Points d'attention :
   - la numérotation des EF du CDC diffère de la liste indicative de la fiche 01 : EF-02 (choisir un mois) et EF-03 (toute la période) sont séparées, le tableau jour par jour est EF-08 ;
   - nouvelles hypothèses à citer dans les CA : Q-15 (tableau de la période choisie, US-04), Q-16 (heures suivies de « h », US-01, US-03, US-04), Q-17 (jour max avec ses heures, US-03) ;
   - points renvoyés à R3 (O-10, liste dans `travail/audits/R2_audit.md`) : colonnes et ordre du tableau (US-04), « toute la période » = toutes les lignes chargées et remplacement complet au rechargement (US-01), rappel du prix de référence (US-02) ;
   - le CDC ne contient aucune valeur chiffrée : toutes les valeurs des CA viennent de l'oracle.
5. Passation : dire **« fin de notre relais »** à ton IA. Elle met à jour ce fichier, complète `travail/audits/R3_audit.md` et les journaux, commite, pose le tag annoté `relais-3`, pousse (`git ls-remote --tags origin` doit afficher `relais-3`) et te donne le message à envoyer au groupe (`agents/00_protocole_relais.md` §4). Relis son compte rendu avant d'envoyer le message. Avec une IA web, c'est toi qui colles les contenus et lances les commandes qu'elle te donne, en deux blocs (protocole, « Variante pour une IA web »).

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

---

## 8. Relais en cours (journal de bord, tenu par l'IA)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

**Aucun relais en cours.** Prochain relais : voir §1.

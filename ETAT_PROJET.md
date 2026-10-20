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
| **Porte atteinte** | G5 (`version_IA.html` vérifié : 20 CA du Sprint 01 et Test-P04 respectés ; captures conformes aux compléments R5) ; G4 confirmée par l'audit de R5 ; `index.html` de présentation ajouté pendant R6, en parallèle, par Leddycia (D-16, `6f59584`), avec captures suffixées `_index` |
| **Relais terminé** | R5 (vérification, captures), puis son complément (corrections avant R6), puis un complément de R4 (quatre points mineurs) |
| **Relais en cours** | **R6 (finalisation, G6 et G7)** |
| **Prochain relais** | **Aucun (dernier relais ; préparation de la soutenance après remise)** |
| **Échéance de remise** | **Dimanche 18/10/2026, 23 h 59**, sur le Drive (C-19) |
| **Sprint 01** | US-01 (chargement et totaux), US-02 (coût), US-03 (jour max) (D-01) |
| **Dépôt** | `https://github.com/Leddycia/PowerWatch.git` (HTTPS, pour cloner : §0) ou `git@github.com:Leddycia/PowerWatch.git` (SSH, si ta clé est enregistrée), branche `main` ; dépôt **public**, laissé public par décision de Leddycia (D-12, O-8) |

## 2. Tableau des relais

| Relais | Membre | Outil d'IA | Créneau prévu | Porte | Statut | Tag |
|---|---|---|---|---|---|---|
| R1 | Leddycia | Claude Code (Claude Opus 5.5) | 18/10, matin | G0 et G1 | **FAIT** (commit tagué `relais-1`) ; complément FAIT (10:40 → 11:37, non tagué) | `relais-1` |
| R2 | Leddycia | Claude Code (Claude Opus 5.5) | 18/10, matin | G2 | **FAIT** (10:49 → 11:48) | `relais-2` |
| R3 | Leddycia | Claude Code (application de bureau, Claude Opus 5.5) | *à compléter* | G3 | **FAIT** (11:55 → 12:06) | `relais-3` |
| R4 | Bradley | Antigravity (Gemini 3.8 Flash High) | *à compléter* | G4 | **FAIT** (12:47 → 13:42) ; complément FAIT (15:59 → 16:31, non tagué) | `relais-4`, `version-ia` |
| R5 | Louis | Claude Code (Claude Opus 5.5) | *à compléter* | G5 | **FAIT** (14:00 → 14:37) ; complément FAIT (15:04 → 15:53, non tagué) | `relais-5` |
| R6 | Petiote, puis Leddycia (reprise à 18:40) | Claude (modèle non précisé) ; reprise : Claude Code (application de bureau, Claude Opus 5.5) | *à compléter* | G6 et G7 | **EN COURS** (début 16:59 ; reprise 18:40, §8) | `relais-6` |

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
| Livrable `prompts.md` v1 : prompt de délégation RMTCEV intégrant le CDC intégral et la spécification Sprint 01 complète avec ses 20 CA chiffrés, relu par Leddycia (R3) et commité avant délégation (`b170333`, C-08) ; section 1 remplie (§1.1 encore à corriger par R6 : O-13, RG-09) ; sections 2 à 4 : emplacements créés, encore vides, à compléter par R6 (rectifié au complément de R4, E-28) | `Groupe_01_Cas_01/prompts.md` | R4 |
| Réponse brute intégrale de la délégation ChatGPT (GPT-4o) en session vierge (D-09) | `travail/brut/delegation_reponse_brute.md` | R4 |
| Prototype brut `version_IA.html` extrait sans altération (`git diff --no-index` vide), commité avec tag annoté `version-ia` (`624003a`, C-09, RG-08) | `Groupe_01_Cas_01/prototype/version_IA.html` | R4 |
| Plan de test exhaustif des 20 CA du Sprint 01 et Test-P04 avec procédure pas à pas, fixtures associées et nommage exact des captures PNG attendues | `tests/plan_de_test.md` | R4 |
| 6 fixtures de test CSV (`f01` à `f06`) couvrant l'ensemble des cas limites (ordre mélangé, colonne manquante, valeur non numérique, mois sans génératrice, décimales, sous-ensemble août-septembre) | `tests/fixtures/f01_*.csv` à `f06_*.csv` | R4 |
| Oracle §8 complété avec les résultats attendus déterministes pour les 6 fixtures de test | `docs/oracle.md` | R4 |
| Rapport d'audit d'entrée R4, journal de bord intégral et traçabilité des arbitrages D-10, Q-01, Q-10 | `travail/audits/R4_audit.md` | R4 |
| Vérification de `version_IA.html` : 20 CA du Sprint 01 et Test-P04 respectés (fuseau d'Haïti, Chromium piloté par script et Firefox manuel, réseau coupé), contrôles transverses conformes, empreinte du CSV identique avant et après ; tableau de résultats ajouté au plan de test | `tests/plan_de_test.md` §3 | R5 |
| `index.html` **non créé** : aucun écart sur les CA du Sprint 01 (C-09, fiche 04) | — | R5 |
| 34 captures (29 automatiques dont 3 montages « fuseau », 5 manuelles de Louis dont 3 photos de l'écran) | `Groupe_01_Cas_01/captures/` | R5 |
| Audit d'entrée de R4 (A1 à A4 conformes ; A2b et A3b remontés) ; E-22 (environnement Linux) ; JP-20 à JP-23 | `travail/audits/R5_audit.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md` | R5 |
| Q-01 remise au statut « provisoire » (l'hypothèse ne change pas ; ce n'est pas une réponse du client) | `travail/decisions.md` | R5 (complément) |
| f01 refait : les jours à égalité y sont dans un ordre non chronologique, ce qui rend CA-03.02 vérifiable ; résultat attendu inchangé | `tests/fixtures/f01_lignes_melangees.csv`, `docs/oracle.md` §8 | R5 (complément) |
| 4 captures de CA-03.02 refaites avec le nouveau f01 (Windows 11, Chrome 155 sans interface, fuseau d'Haïti et coupure réseau émulés) | `Groupe_01_Cas_01/captures/US03_CA02_*.png`, `tests/plan_de_test.md` §3 | R5 (complément) |
| Données personnelles masquées ou recadrées dans 4 captures manuelles (CA-01.01, CA-01.02 Firefox, CA-01.03, CA-01.08) | `Groupe_01_Cas_01/captures/` | R5 (complément) |
| Affichage des blocs de `prompts.md` réparé (texte du prompt inchangé, identique à `b170333`) | `Groupe_01_Cas_01/prompts.md` | R5 (complément) |
| Audit de la livraison de R5 et corrections ; E-23 à E-26 ; JP-24 et JP-25 ; relectures indépendantes avant le commit (vérificateurs en lecture seule ; détail : `travail/audits/R5_audit.md`, section « Complément ») | `travail/audits/R5_audit.md` (section « Complément »), `travail/journal_ecarts.md`, `travail/journal_prompts.md` | R5 (complément) |
| Résumés de la précision de Q-10 corrigés après un essai réel (CSV avec BOM accepté, CSV à `;` rejeté par `version_IA.html`) ; formulation plus large du cahier des charges signalée | `travail/decisions.md` (journal des changements), ETAT §4, §5 (O-10) et §6 | R4 (complément) |
| État réel de `prompts.md` (ETAT §3) et création d'`index.html` seulement en cas d'écart (plan de test §2) | `ETAT_PROJET.md` §3, `tests/plan_de_test.md` §2 | R4 (complément) |
| Bonnes pratiques de trois pièges reprises dans le prompt envoyé (P-05, P-06, P-09), consignées et acceptées telles quelles | `travail/journal_ecarts.md` (E-27) | R4 (complément) |
| Audit des points restants sur le travail de R4 et corrections ; E-27, E-28 ; JP-26 et JP-27 ; relecture indépendante avant le commit | `travail/audits/R4_audit.md` (section « Complément »), `travail/journal_ecarts.md`, `travail/journal_prompts.md` | R4 (complément) |

## 4. Ce qui reste (par ordre de priorité)

1. **Reste de R5 et des compléments de R5 et de R4, à reprendre par R6** : rien de partiel. Dans le README, signaler que `version_IA.html` accepte un CSV précédé d'un BOM UTF-8, conformément au registre (Q-10), alors que le cahier des charges §11.1 écrit « tout autre format est rejeté » (E-28). Faire confirmer par Bradley les points A2b et A3b (O-13) et harmoniser `prompts.md` §1.1 ; dans le README, expliquer qu'une même capture prouve plusieurs CA et la lecture retenue pour CA-02.02 ; dans la fiche de contribution, attribuer R5 à Louis, et les compléments de R5 et de R4 à Leddycia (`travail/audits/R5_audit.md`, section « Complément », C6 à C8) ; RG-09 : remplacer les prénoms par les rôles dans `prompts.md` l. 15 et dans `tests/plan_de_test.md` §3 (point antérieur au complément).
2. **R6** : README, `prompts.md` final, `fiche_contribution.pdf` (à la racine du dépôt), test depuis le Drive sur un autre PC (G6 et G7). **Téléversement sur le Drive : Leddycia** (D-13).
3. **Tous** : préparation de la soutenance (mode coach, fiche 06).

## 5. Points ouverts et bloquants

| # | Point | Bloque | Qui |
|---|---|---|---|
| O-1 | **Numéro du groupe** (D-11) : **résolu**, Groupe 01. Livrable `Groupe_01_Cas_01/`, dossier Drive `Groupe_01/`. | Plus rien | Équipe |
| O-2 | **Noms, ordre des relais et outil d'IA de chaque membre** (§2) : R2 et R3 = Leddycia (Claude Code) ; R4 = Bradley (Antigravity, Gemini 3.8 Flash High) ; R5 = Louis (Claude Code, Claude Opus 5.5) ; R6 = Petiote (**outil à compléter**) | Rien (outil de R6 inscrit à son démarrage) | Petiote |
| O-3 | **Accès au dépôt GitHub** : invitations **envoyées** par Leddycia le 2026-10-18. Chaque membre doit les **accepter** avant son créneau (§0, étape 1). | `push` de chaque relais | Chaque membre |
| O-4 | Définition exacte de RMTCEV dans le cours (hypothèse D-02 en vigueur) | Rien (hypothèse en place) ; à remplacer avant R4 si elle est retrouvée | Tout membre |
| O-5 | **Résolu par R2** : questions au client Q-01 à Q-17 listées au §11.1 du CDC avec leur hypothèse provisoire (Q-15 à Q-17 ajoutées par R2, JP-13) | Rien (résolu) | R2 |
| O-6 | **Résolu par R4** : D-10 validé (règles et valeurs de l'oracle fournies sans dicter les solutions d'implémentation des pièges techniques) | Rien (résolu) | R4 |
| O-7 | **Résolu le 2026-10-18 : Leddycia téléverse elle-même sur le Drive** (D-13) le dossier `Groupe_01_Cas_01/` et `fiche_contribution.pdf`, pris dans le dépôt. Elle doit être **joignable pendant le créneau de R6** (vers la 35e minute, puis pour le README final). | Rien (résolu) | Leddycia |
| O-8 | **Résolu le 2026-10-18 : dépôt laissé public, décision de Leddycia** (D-12), prise en connaissance de cause après vérification (accès anonyme possible). Tout ce qui est poussé est public : noms des membres, journaux, e-mail de l'auteur de chaque commit. Adresse noreply fortement recommandée pour chaque membre (§0). | Rien (résolu) | Leddycia (propriétaire du dépôt) ; chaque membre pour son adresse |
| O-9 | **Résolu par R4** : l'équipe garde l'hypothèse provisoire Q-01 pour le Sprint 01 (format des litres toujours à une décimale avec virgule française, ex. « 71,0 L »), ce qui règle l'ambiguïté B-14 / R-04 ; ce n'est pas une réponse du client (statut corrigé au complément de R5, E-23) | Rien (résolu) | R4 |
| O-10 | **Résolu par R3 et R4** : points de R3 résolus par Q-18 à Q-20 ; points de R4 résolus par la création des fixtures f01 à f06, la complétion d'oracle §8, la précision de Q-10 (fichier rejeté selon Q-04 s'il est séparé par des `;` ou si un BOM UTF-8 altère le nom de la première colonne ; `FileReader.readAsText`, utilisé par `version_IA.html`, retire le BOM UTF-8, et le fichier est alors accepté : essai du complément de R4, E-28 ; le cahier des charges §11.1 garde la formulation plus large « tout autre format est rejeté », à signaler par R6 dans le README) ; poste de la directrice renvoyé à R5/R6. | Rien (résolu) | R3, R4 |
| O-11 | **Fiche 01** : sa DoD admet une CT citant un B-xx, sa structure (§7) les réserve aux consignes ; le CDC suit la structure | Rien | Équipe |
| O-12 | **Fiche 02** : sa checklist d'audit A5 cite encore « Q-01 à Q-14 » ; le registre en compte désormais Q-01 à Q-20 | Rien | Équipe |
| O-13 | **Délégation (audit R5, A2b et A3b)** : (a) le brut ne contient ni le bloc ```html exigé par le prompt ni aucun texte autour : la réponse est-elle conservée complète ? (b) mode de session « temporaire » (brut, l. 6) ou « nouvelle conversation » (`prompts.md` §1.1) ? | `prompts.md` final (R6) | Bradley confirme, R6 corrige `prompts.md` §1.1 |
| O-14 | **Comportements hors CA de `version_IA.html`** (non corrigés, RG-04) : une ligne vide au milieu du fichier est ignorée sans message (lien avec Q-04) ; des heures décimales seraient affichées arrondies à l'entier (lien avec Q-16) ; aucun cas dans le CSV fourni | Rien ; à mentionner au README (« Écarts connus et points à confirmer ») | R6 |
| O-15 | **Captures masquées au complément de R5 (E-25)** : les versions non masquées des 4 captures manuelles restent dans l'historique public du dépôt (commit 370abc6), qui n'est jamais réécrit (`AGENTS.md` §11, D-12) ; seule la remise sur le Drive est garantie sans ces données | Rien | Leddycia (propriétaire du dépôt) |

## 6. Mission du prochain relais : R6

1. Après les prérequis du §0 : `git pull`, puis `git fetch --tags` et `git tag -l` (`relais-1` à `relais-5` et `version-ia` doivent apparaître), puis ouvrir ton IA dans le dépôt et vérifier le chargement : lui demander « Cite mot pour mot la règle RG-08 d'AGENTS.md ».
2. Lancer le prompt d'amorçage de `AGENTS.md` §14, en remplaçant `<X>` par `6` et `<fiche>` par `06_finalisation_soutenance`. Une fois le plan validé, l'IA marque R6 « EN COURS » ici (§1, §2 et §8), crée `travail/audits/R6_audit.md` et tient le journal de bord du §8. Complète ton outil d'IA au §2. **R6 démarre au plus tard à 22 h 00.**
3. **Audit d'entrée (fiche 06, A1 à A5)** :
   - A1 : passe réduite sur **`version_IA.html`** (`index.html` est absent) : « Toute la période » plus un mois, fuseau d'Haïti, hors ligne en fin de passe ; résultats de R5 dans `tests/plan_de_test.md` §3 ;
   - A2 : `git diff version-ia -- Groupe_01_Cas_01/prototype/version_IA.html` vide ;
   - A3 : 34 captures dans `captures/`, au moins une par CA ; **aucune capture manquante** ; CA-03.02 est prouvé par 4 fichiers `US03_CA02_lignes_melangees_<période>.png`, refaits au complément de R5 avec un f01 dont les jours à égalité sont dans un ordre non chronologique (E-24) ; CA-01.05, CA-02.04 et CA-03.04 par des montages des 3 mois ; 4 captures manuelles masquées ou recadrées (E-25) : vérifier qu'aucune donnée personnelle n'y reste lisible ;
   - A4 et A5 : cohérence des ID entre livrables ; aucun fichier parasite dans `Groupe_01_Cas_01/`.
4. **Livrables (fiche 06)** :
   - `Groupe_01_Cas_01/README.md` : tableau des statuts par CA (tous « respecté », repris de `tests/plan_de_test.md` §3, avec le lien vers chaque capture) ; **expliquer l'absence d'`index.html`** (aucun écart sur les CA, C-09) ; conditions de test (Linux, fuseau America/Port-au-Prince, Chromium et Firefox, E-22 ; les 4 captures de CA-03.02 ont été refaites au complément de R5 sous Windows 11, Chrome 155 sans interface, fuseau et coupure réseau émulés, E-24) ; écarts connus et points à confirmer (O-14 ; Q-10 : `version_IA.html` accepte un CSV précédé d'un BOM UTF-8, conformément au registre, alors que le cahier des charges §11.1 écrit « tout autre format est rejeté », E-28) ; dire qu'une même capture sert de preuve à plusieurs CA (fichiers identiques, par exemple l'écran « Toute la période ») ; pour CA-02.02, le prix de référence de 300 gourdes par litre est affiché dans le bloc de chargement, sur le même écran que le coût (lecture retenue par R5) ;
   - `prompts.md` final : §2 à partir de `travail/journal_prompts.md` ; §3 au moins une proposition de l'IA corrigée ou rejetée (`travail/journal_ecarts.md`, par exemple E-23 ou E-24, corrigées au complément de R5, ou E-16, E-21 : aucune correction n'a été nécessaire sur `version_IA.html`) ; E-27 (bonnes pratiques de pièges reprises dans le prompt envoyé, acceptées telles quelles) peut illustrer la précision des prompts (C-18), citée à part et signalée comme acceptée telle quelle, sans tenir lieu de cette proposition corrigée ou rejetée ; §4 : aucun écart du prototype par rapport à la demande du client ; corriger §1.1 selon la réponse de Bradley (O-13) ; l'affichage des blocs du §1 est déjà réparé (complément de R5, E-26) : ne pas toucher au texte du prompt ; RG-09 (règle d'or) : au §1.1 (l. 15), remplacer les prénoms des relecteurs par leur rôle (membre de R3, membre de R4), et de même pour le prénom du membre de R5 dans `tests/plan_de_test.md` §3 ;
   - `fiche_contribution.pdf` à la racine du dépôt (R1 à R4 : Leddycia et Bradley ; R5 : Louis, même si le commit et le tag de R5 portent une autre identité Git ; complément de R5 : Leddycia ; complément de R4 : Leddycia ; R6 : Petiote).
5. **Remise et test sur un autre PC (fiche 06, tâches 4 et 5)** : « sauvegarde du relais », hash donné à **Leddycia**, qui téléverse sur le Drive ; test depuis le Drive sur un **PC différent de celui de R5** (idéalement sous Windows, fuseau « (UTC-05:00) Haïti ») ; README complété puis remplacé sur le Drive par Leddycia. Échéance : **23 h 59**.
   - Point d'attention pour la démonstration (fiche 06, étape 5 « Montrer une correction faite sur la version de l'IA ») : il n'y a pas de correction du prototype ; montrer à la place une proposition de l'IA rejetée ou corrigée (journal des écarts) et la vérification par l'oracle.
6. **Passation** : dire **« fin de notre relais »** à ton IA (passation complète, tag `relais-6`, `agents/00_protocole_relais.md` §4, cas du dernier relais).

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

### R4 : prompt RMTCEV, délégation, version_IA.html, plan de test et fixtures (2026-10-18, 12:47 → 13:42)

- **Membre et outil** : Bradley, Antigravity (Gemini 3.8 Flash High) ; délégation confiée à ChatGPT (GPT-4o) en session vierge (D-09).
- **Audit d'entrée** : product backlog de R3 conforme sur A1 à A5 (8 US, 20 CA du Sprint 01 chiffrés avec l'oracle §2, §4, §5, fuseau Haïti et égalités) ; CDC (33,4 ko) et backlog (24,7 ko) lus intégralement ; SHA-256 du CSV vérifié `320155c7…a84b` (`True`) (détail : `travail/audits/R4_audit.md`).
- **Fait** : prompt RMTCEV complet intégrant CDC et Sprint 01 intégraux, relu et validé par Leddycia (R3) et Bradley (JP-19), commité avant délégation (`b170333`, C-08) ; délégation en session vierge ChatGPT (GPT-4o), réponse brute archivée dans `travail/brut/delegation_reponse_brute.md` ; extraction 100% fidèle de `Groupe_01_Cas_01/prototype/version_IA.html` (`git diff --no-index` vide), commité avec tag annoté `version-ia` (`624003a`, C-09, RG-08) ; `prompts.md` v1 (sections 1 à 4) ; 6 fixtures de test CSV créées dans `tests/fixtures/` (`f01` à `f06`) ; résultats attendus déterministes ajoutés à `docs/oracle.md` §8 ; plan de test exhaustif des 20 CA et Test-P04 dans `tests/plan_de_test.md` ; arbitrages D-10, Q-01, Q-10 consignés dans `travail/decisions.md` ; JP-18 et JP-19.
- **Reste** : rien de partiel pour R4. R5 prend la suite pour vérification, journal des écarts, `index.html` et captures.
- **Décisions** : D-10 validé (prompt fournissant toutes les règles sans souffler le code des pièges techniques) ; Q-01 confirmé (résout O-9, 1 décimale avec virgule française ex. « 71,0 L ») ; Q-10 précisé (rejet propre Q-04 en cas de BOM UTF-8).
- **Points d'attention pour R5** :
  - `version_IA.html` est intouchable (RG-08, tag `version-ia`) ;
  - `version_IA.html` donne des résultats exacts sur le CSV nominal et gère déjà l'égalité chronologique, le fuseau horaire par split de chaîne, l'absence de génératrice et le rejet des colonnes/valeurs invalides ;
  - Point d'attention ergonomique mineur : dans le sélecteur, l'option « Toute la période » est insérée après les mois individuels (bien que sélectionnée par défaut) ;
  - Appliquer la fiche 05 pour l'audit et les tests, puis fiche 04 pour `index.html` si des écarts sont consignés, puis captures dans `Groupe_01_Cas_01/captures/`.
- **Porte** : G4 atteinte.
- **Tag** : `relais-4` (plus `version-ia` déjà posé et poussé). Le hash du commit figure dans le compte rendu et le message de passation.

### R5 : vérification de `version_IA.html` et captures (2026-10-18, 14:00 → 14:37)

- **Membre et outil** : Louis, Claude Code (Claude Opus 5.5).
- **Audit d'entrée** : travail de R4 conforme sur A1 (`version_IA.html` intact, tag `version-ia`), A2 (extraction fidèle, diff vide), A3 (prompt RMTCEV complet, commité avant l'envoi) et A4 (fixtures recalculées) ; A2b et A3b remontés à Bradley (O-13) ; tableau de résultats ajouté au plan de test ; poste sous Kali Linux, fuseau système America/Port-au-Prince (E-22) (détail : `travail/audits/R5_audit.md`).
- **Fait** : vérification complète de `version_IA.html` (Chromium piloté par script et Firefox manuel par Louis, réseau réellement coupé) ; **statuts finaux : les 20 CA du Sprint 01 (CA-01.01 à CA-01.11, CA-02.01 à CA-02.05, CA-03.01 à CA-03.04) et Test-P04 sont respectés** (tableau : `tests/plan_de_test.md` §3) ; contrôles transverses conformes (hors ligne, aucune ressource externe, aucune donnée intégrée, lecture seule avec empreinte identique avant et après, rien hors sprint, rechargement P-09) ; 34 captures ; E-22 ; JP-20 à JP-23.
- **Écarts restants** : aucun sur les CA. Comportements hors CA non corrigés (RG-04) : ligne vide ignorée, heures décimales arrondies (O-14).
- **Captures** : 34 dans `Groupe_01_Cas_01/captures/`, aucune manquante ; 3 sont des photos de l'écran (CA-01.03, CA-01.08, CA-01.10).
- **`index.html`** : non créé (aucun écart, C-09) ; R6 l'explique dans le README.
- **Reste** : rien de partiel ; O-13 à faire confirmer par Bradley (à reprendre par R6).
- **Décisions** : aucune nouvelle décision ni Q-xx ; E-22 accepté tel quel.
- **Points d'attention pour R6** : la démonstration ne peut pas montrer de correction du prototype (aucune n'a été nécessaire) : montrer une proposition de l'IA rejetée (journal des écarts) ; refaire le test sur un autre PC, idéalement sous Windows avec le fuseau « (UTC-05:00) Haïti » ; R6 démarre au plus tard à 22 h 00.
- **Porte** : G5 atteinte.
- **Tag** : `relais-5`. Le hash du commit figure dans le compte rendu et le message de passation.

### R5 (complément) : corrections avant R6 (2026-10-18, 15:04 → 15:53)

- **Membre et outil** : Leddycia, Claude Code (application de bureau, Claude Opus 5.5) ; fait avant le démarrage de R6 (Leddycia a confirmé que R6 n'avait pas encore fait de `git pull`).
- **Audit d'entrée** : relecture du dépôt après le push de R5 : livraison de R5 conforme sur le tag `relais-5`, l'intégrité de `version_IA.html`, les originaux de `docs/` et le CSV (C1) ; preuve de CA-03.02 non probante (C3) et 4 captures à masquer (C4) ; 4 points à corriger (C2 à C5) : statut de Q-01, f01 qui ne départageait pas les égalités, données personnelles dans 4 captures, blocs mal fermés dans `prompts.md` (détail : `travail/audits/R5_audit.md`, section « Complément »).
- **Fait** : Q-01 remise à « provisoire » (E-23) ; f01 refait et oracle §8 mis à jour (E-24) ; 4 captures de CA-03.02 refaites, statut de CA-03.02 inchangé (respecté) ; données personnelles masquées ou recadrées dans 4 captures (E-25) ; affichage des blocs de `prompts.md` réparé, texte du prompt inchangé (E-26) ; JP-24, JP-25. Chaque étape a été contrôlée trois fois (diff relu, contrôle par script, relecture indépendante ou visuelle), puis l'ensemble a été relu par des vérificateurs indépendants avant le commit.
- **Reste** : O-13 (Bradley, puis R6) ; README : captures communes à plusieurs CA et lecture de CA-02.02 ; fiche de contribution : R5 attribué à Louis (à reprendre par R6).
- **Décisions** : aucune nouvelle décision ; Q-01 : statut corrigé, hypothèse inchangée. L'entrée de R4 ci-dessus écrit encore « Q-01 confirmé » : ce journal ne se réécrit pas ; le bon statut est celui du registre (« provisoire »).
- **Points d'attention pour R6** : les versions non masquées des 4 captures restent dans l'historique public du dépôt (O-15) ; seule la remise sur le Drive en est garantie exempte ; vérifier les captures à l'audit A3 ; les 4 captures de CA-03.02 viennent d'un autre poste que celles de R5 (Windows 11, Chrome 155, fuseau et coupure réseau émulés) ; RG-09 : `prompts.md` l. 15 et `tests/plan_de_test.md` §3 nomment des membres (point antérieur au complément).
- **Porte** : G5 confirmée.
- **Tag** : complément, commit non tagué (le tag `relais-5` reste sur le commit de R5). Le hash du commit figure dans le compte rendu et le message de passation.

### R4 (complément) : quatre points mineurs avant R6 (2026-10-18, 15:59 → 16:31)

- **Membre et outil** : Leddycia, Claude Code (application de bureau, Claude Opus 5.5) ; fait après le complément de R5 et avant le démarrage de R6 (Leddycia a confirmé à 15:58 que R6 n'avait pas encore fait de `git pull`).
- **Audit d'entrée** : points restants sur le travail de R4, relevés à la relecture du dépôt après le push de R4 : résumés inexacts de Q-10, état de `prompts.md` au §3, création systématique d'`index.html` dans le plan de test, bonnes pratiques de pièges reprises dans le prompt sans E-xx ; tag `relais-4`, `version_IA.html` et originaux conformes (détail : `travail/audits/R4_audit.md`, section « Complément »).
- **Fait** : essai réel sous Chrome 155 (CSV avec BOM accepté, CSV à `;` rejeté) et résumés de Q-10 corrigés (O-10, ligne de rectificatif au registre) ; ETAT §3 et `tests/plan_de_test.md` §2 rectifiés (E-28) ; E-27 (l. 36, 40 et 69 du prompt, acceptées telles quelles : texte envoyé) ; JP-26, JP-27 ; chaque étape contrôlée trois fois, puis relecture indépendante (vérificateurs en lecture seule) avant le commit.
- **Reste** : README (R6) : Q-10, formulation plus large du cahier des charges ; O-13 (Bradley, puis R6).
- **Décisions** : aucune nouvelle décision ; Q-10 inchangée (seuls ses résumés sont corrigés). L'entrée de R4 ci-dessus écrit encore « Q-10 précisé (rejet propre Q-04 en cas de BOM UTF-8) » : ce journal ne se réécrit pas ; voir E-28 et le rectificatif du registre.
- **Points d'attention pour R6** : E-27 illustre la précision des prompts (C-18), sans tenir lieu de la proposition corrigée ou rejetée exigée par C-08 (prendre E-23 ou E-24) ; le cahier des charges n'a pas été modifié, car il a servi tel quel de contexte au prompt.
- **Porte** : G4 confirmée.
- **Tag** : complément, commit non tagué (le tag `relais-4` reste sur le commit de R4). Le hash du commit figure dans le compte rendu et le message de passation.

---

## 8. Relais en cours (journal de bord, tenu par l'IA)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

| Relais | Membre | Outil et modèle | Fiche | Porte visée | Début |
|---|---|---|---|---|---|
| R6 | Petiote | Claude (modèle non précisé) | `agents/06_finalisation_soutenance.md` | G6 et G7 | 16:59 |
| R6 (reprise) | Leddycia | Claude Code (application de bureau, Claude Opus 5.5) | `agents/06_finalisation_soutenance.md` | G6 et G7 | 18:40 |

**Plan validé** : 1. Finaliser le README avec les preuves pour chaque CA, les conditions et les limites vérifiées. 2. Compléter `prompts.md` §2 à §4 en gardant O-13 non résolu tant que Bradley n'a pas répondu. 3. Préparer `fiche_contribution.pdf` à la racine. 4. Faire téléverser le dossier par Leddycia, puis tester depuis le Drive sur un autre PC et compléter le README avec les faits réels. 5. Clôturer R6 avec le tag `relais-6` après la vérification Git ; indiquer « remise à confirmer » si le téléversement ou le test manque.

**Plan complété à la reprise** (validé par Leddycia à 18:40, JP-31 ; étapes notées a à g pour ne pas les confondre avec les relais) : a. Inscrire la reprise (§2, §8, `travail/audits/R6_audit.md`). b. Intégrer les blocs 1 à 6 de `travail/transmission_R6_index.md` (D-16, E-29 à E-33, JP-28 à JP-30, rectificatif et §4 du plan de test). c. README : `index.html` comme version à utiliser (blocs 7 et 8), BOM accepté (Q-10, E-28), captures communes à plusieurs CA, outils. d. `prompts.md` : rôles au lieu des prénoms (RG-09), E-29, E-30 et E-32 au §3, `index.html` au §4, texte du prompt envoyé inchangé ; rôles aussi dans `tests/plan_de_test.md` §3. e. Relecture indépendante des changements (vérificateurs en lecture seule). f. `fiche_contribution.pdf` (noms et contributions donnés par Leddycia). g. Étapes 4 et 5 du plan ci-dessus, puis « fin de notre relais ».

**Contrôles de reprise (synthèse)** : fusion `a3886ae` propre, aucun apport distant perdu (conforme) ; message de ce commit « 1 », non conventionnel (`AGENTS.md` §11 ; historique non réécrit) ; `version_IA.html` intact (conforme) ; textes D-16 non intégrés (à corriger) ; README affirmant l'absence d'`index.html` (bloquant pour la remise) ; prénoms dans `prompts.md` et `tests/plan_de_test.md` §3 (RG-09, à corriger) ; « Visual Studio Code » sans source (à corriger) ; README muet sur le BOM, les captures communes et Firefox sur `index.html` (à corriger) ; `prompts.md` §3 et §4 incomplets (à corriger) ; ETAT §6 à réécrire à la passation (démonstration des corrections E-29 et E-30) ; `fiche_contribution.pdf` absente. Relecture (étape e) : audit d'entrée A1 et A3 faits sur `370abc6`, avant `index.html` (couvert par la revérification de D-16 et le test depuis le Drive) ; textes d'aide d'`index.html` non listés (README complété) ; trois photos de l'écran retirées du livrable (K15, suppression voulue, E-35) (détail : `travail/audits/R6_audit.md`, section « Reprise », K1 à K15).

**Audit d'entrée (synthèse)** : A1 passe réduite sur `version_IA.html` conforme en local : 97 h / 280,0 L / 84 000 gourdes / 06/08/2026, puis septembre 30 h / 84,0 L / 25 200 gourdes / 08/09/2026 après coupure réseau simulée ; fuseau navigateur `America/Port-au-Prince`. A2 tags et diff vérifiés : `version-ia` présent, diff vide. A3 34 noms de captures recensés, couverture des CA conforme ; lisibilité non vérifiée image par image. A4 cohérence des US et CA conforme au backlog, au plan de test et au prompt. A5 aucun fichier parasite dans l'inventaire du livrable ; README absent, à produire par R6. O-13 non résolu : Bradley n'a pas répondu ; le mode exact et l'absence des clôtures de code du brut ne peuvent pas être confirmés. O-14 : ligne vide ignorée et heures décimales arrondies, hors CA, non corrigés (RG-04). Synchronisation initiale : `main` propre, tags `relais-1` à `relais-5` et `version-ia` présents, historique à `370abc6` ; `git fetch --tags origin` effectué.

**Journal de bord**

| Heure | Étape | Ce qui a été fait | Fichiers | État |
|---|---|---|---|---|
| 16:59 | étape 1 | R6 marqué EN COURS après validation du plan ; contrôles Git et audit d'entrée A1 à A5 réalisés ; O-13 déclaré non résolu | `ETAT_PROJET.md` | fait |
| 17:58 | étape 2 | Reprise synchronisée par fetch ; `main` est en retard de 4 commits distants et l'arbre contient les travaux R6 non commités. Le JavaScript de l'`index.html` distant est identique à celui de `version_IA.html` ; sauvegarde intermédiaire demandée, sans tag | `ETAT_PROJET.md`, `Groupe_01_Cas_01/prompts.md`, `Groupe_01_Cas_01/README.md`, `travail/audits/R6_audit.md` | partiel |
| 18:40 | reprise a | Reprise de R6 par Leddycia après le push de Petiote (sauvegarde `a88461d`, fusion `a3886ae`) ; contrôles de reprise faits en lecture seule ; plan complété validé (JP-31) ; reprise inscrite au §2, au §8 et dans l'audit R6 | `ETAT_PROJET.md`, `travail/audits/R6_audit.md`, `travail/journal_prompts.md` | fait |
| 18:43 | reprise b | Blocs 1 à 6 de la transmission copiés tels quels (script de copie hors du dépôt) : D-16 et sa ligne au journal des changements, E-29 à E-33, JP-28 à JP-30 (JP-30 complété), rectificatif et §4 du plan de test ; prénoms remplacés par le rôle dans le plan de test §3 (RG-09, 7 occurrences) | `travail/decisions.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `tests/plan_de_test.md` | fait |
| 18:44 | reprise | Réponses de Leddycia (JP-32) : O-13 résolu (le membre de R4 confirme une nouvelle conversation et le bloc HTML) ; éditeur : Antigravity ; test depuis le Drive : Gervais ; vérifications complètes du projet : Gervais et Delly ; noms complets des 6 membres pour la fiche de contribution | `travail/journal_prompts.md` | fait |
| 18:47 | reprise c | README mis à jour : `index.html` comme version à utiliser (blocs 7 et 8), tableau des CA avec preuves des deux versions et Test-P04, captures communes à plusieurs CA (empreintes SHA-256 comparées), lecture de CA-02.02, conditions de test (E-24, `index.html`, Firefox au test Drive par Gervais), Q-10 et BOM (E-28), outils et éditeur Antigravity. Leddycia signale le prompt d'audit complet de Gervais (session « Prompt d'audit projet complet ») : relu pour aligner les livrables sur ses contrôles (JP-33) | `Groupe_01_Cas_01/README.md` | fait |
| 18:48 | reprise d | `prompts.md` : relecteurs et §2 désignés par leur rôle (RG-09) ; O-13 clos au §1.1 (E-34, archive brute non modifiée ; extraction recontrôlée : identique) ; §3 complété par E-29, E-30 (corrigés) et E-32 (rejeté) ; §4 complété pour `index.html` ; texte du prompt envoyé inchangé | `Groupe_01_Cas_01/prompts.md`, `travail/journal_ecarts.md`, `travail/audits/R6_audit.md` | fait |
| 18:49 | reprise f | `fiche_contribution.pdf` créé à la racine : un tableau unique, une ligne par membre (6), noms complets tels que donnés par Leddycia (JP-32), attributions tirées des §2 et §7, et de JP-32 pour Delly et Gervais ; source HTML et conversion PDF par Chrome hors du dépôt ; PDF d'une page relu à l'écran | `fiche_contribution.pdf` | fait |
| 19:15 | reprise e | Relecture indépendante des changements de la reprise (8 vérificateurs en lecture seule) ; constats confirmés appliqués : README (renvoi vers `prompts.md` §3, textes d'aide d'`index.html`, Firefox et test depuis le Drive au futur, rappel d'égalité), `prompts.md` (note O-13 précisée, §4, E-16), E-34, JP-33, §1 (attribution d'`index.html`), heure de reprise, étapes notées a à g, audit R6 (K2, K8, K11, K13 à K15), `fiche_contribution.pdf` (ligne de Delly réduite à ce que Leddycia a indiqué, JP-32) ; constats réfutés laissés. Trois captures de `version_IA.html` trouvées supprimées hors de cette session (K15), remonté à Leddycia | `Groupe_01_Cas_01/README.md`, `Groupe_01_Cas_01/prompts.md`, `ETAT_PROJET.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `travail/audits/R6_audit.md`, `fiche_contribution.pdf` | partiel |
| 19:21 | reprise | Suppression voulue des trois photos de l'écran de `version_IA.html` confirmée par Leddycia (JP-34) : README (colonne `version_IA.html` de CA-01.03, CA-01.08 et CA-01.10, paragraphe d'explication), plan de test §3 (rectificatif et colonne « Capture »), E-35, K15 ; 53 liens du README vérifiés, 48 captures toutes liées | `Groupe_01_Cas_01/README.md`, `tests/plan_de_test.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `travail/audits/R6_audit.md` | partiel (motif à compléter) |
| 19:36 | reprise | Seconde relecture indépendante (16 agents en lecture seule : 3 lentilles, chaque constat contre-vérifié) : 12 constats confirmés (9 distincts), 1 réfuté. Appliqués : README (captures de R5 « sauf trois photos », plan de test désigné « hors livrable »), `prompts.md` §4 (CA-02.02 et CA-02.05 décrits sans les confondre), E-35 (recadrée ou masquée), JP-31 (étapes 1 à 4 = a à d), audit R6 (K9, K13), synthèse et ligne 19:15 du §8 | `Groupe_01_Cas_01/README.md`, `Groupe_01_Cas_01/prompts.md`, `ETAT_PROJET.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `travail/audits/R6_audit.md` | fait |
| 19:38 | reprise | Motif de la suppression donné par Leddycia (JP-34) : photos de l'écran prises de biais, peu lisibles et peu professionnelles pour le livrable ; reporté dans E-35, le README, le plan de test §3 et l'audit R6 | `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `Groupe_01_Cas_01/README.md`, `tests/plan_de_test.md`, `travail/audits/R6_audit.md`, `ETAT_PROJET.md` | fait |
| 19:39 | sauvegarde | « sauvegarde du relais » demandée par Leddycia : commit et push sans tag (protocole §3.6), avant l'audit complet de Gervais (JP-33) et le téléversement sur le Drive | tous les fichiers modifiés de la reprise, suppression des trois photos (E-35), `fiche_contribution.pdf` | fait |
| 19:45 | reprise | Réponse de Leddycia sur O-13 (JP-36) : un texte entourait le bloc HTML reçu par le membre de R4, contre le format demandé ; l'archive n'en garde que le code HTML. E-36 ajouté, E-34 précisé, `prompts.md` §1.1 et §3 complétés, K16 | `Groupe_01_Cas_01/prompts.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `travail/audits/R6_audit.md` | fait |
| 19:57 | reprise | Feuille de route de Gervais rédigée (JP-35) : état du projet, étapes, complément au prompt de contre-audit (JP-33), modèle de compte rendu du test depuis le Drive ; contre-vérifiée en lecture seule (17 constats confirmés, appliqués) ; publiée après la prochaine sauvegarde, avec son hash | hors dépôt (page privée claude.ai) | partiel |
| 19:58 | sauvegarde | « sauvegarde du relais » demandée par Leddycia : commit et push sans tag (protocole §3.6), pour que Gervais audite une version qui contient E-36 ; hash reporté dans la feuille de route de Gervais (JP-35) | `ETAT_PROJET.md`, `Groupe_01_Cas_01/prompts.md`, `travail/journal_ecarts.md`, `travail/journal_prompts.md`, `travail/audits/R6_audit.md` | fait |
| 19:59 | reprise | Feuille de route de Gervais publiée (page privée claude.ai, JP-35), avec le hash de la sauvegarde de 19:58 ; à partager à Gervais par Leddycia, avec le prompt de contre-audit | hors dépôt | fait |
| 20:01 | reprise | Leddycia (JP-37) : le membre de R4 ne pourra pas retrouver la réponse complète, E-36 laissé ; Gervais commence son contre-audit. E-36, `prompts.md` §3, K16 et point 5 du complément de la feuille de route mis à jour (page republiée) | `travail/journal_ecarts.md`, `Groupe_01_Cas_01/prompts.md`, `travail/audits/R6_audit.md`, `travail/journal_prompts.md`, `ETAT_PROJET.md` | fait |
| 20:04 | reprise | Leddycia (JP-38) : Delly prépare le document de soutenance pour la présentation du 2026-10-19 ; point ouvert ajouté (hors livrable, fiche 06 « Mode coach », C-16) | `travail/journal_prompts.md`, `ETAT_PROJET.md` | fait |

**Points ouverts du relais** : O-13 résolu à 18:44 (JP-32), puis précisé à 19:45 : un texte entourait le bloc HTML reçu, et la réponse complète n'est pas conservée (E-36, JP-36) ; ETAT §5 à mettre à jour à la passation. Le membre de R4 ne pourra pas retrouver la réponse complète (JP-37, 20:01) : écart laissé, consigné en E-36. Gervais commence son contre-audit (JP-37) : corrections éventuelles à appliquer dans cette session. Trois photos de l'écran de `version_IA.html` (`US01_CA03_liste_periodes.png`, `US01_CA08_lecture_seule.png`, `US01_CA10_fichier_partiel.png`) retirées du livrable à 19:13 : suppression voulue (JP-34, E-35, K15), car ces photos prises de biais étaient peu lisibles ; README et plan de test §3 mis à jour. Leddycia doit confirmer les heures de téléversement et de remplacement du README ; le test depuis le Drive sera fait par Gervais, Firefox compris (ordinateur, navigateur et heure à reporter dans le README). Vérifications complètes du projet par Gervais (prompt d'audit complet, JP-33) et Delly : corrections éventuelles appliquées dans cette session et consignées. À la passation : rectificatifs au §3 pour `index.html` (D-16, `6f59584`) et pour les 34 captures de R5 « dont 3 photos de l'écran » (E-35), sans effacer les lignes de R5 ; §6 réécrit « Après la remise » (K12) ; `travail/transmission_R6_index.md` supprimé dans le commit de passation, suppression notée dans l'audit R6 ; avant REMIS, vérifier que le test depuis le Drive et les vérifications ont bien eu lieu, sinon corriger la fiche de contribution et la remplacer sur le Drive. Le modèle Claude utilisé par Petiote n'a pas été précisé. Soutenance le 2026-10-19 : Delly prépare un document d'aide à la présentation (JP-38), hors livrable : rien de plus dans `Groupe_01_Cas_01/` (RG-12), ni sur le Drive ; s'appuyer sur la fiche 06, « Mode coach » (12 questions, démonstration d'environ 3 min) et sur les valeurs de l'oracle (`AGENTS.md` §6) ; la fiche de contribution ne cite pour Delly que les vérifications : à compléter avant le téléversement si l'équipe veut y mentionner ce document.

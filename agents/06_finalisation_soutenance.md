# Fiche de rôle 06 : Finalisation, remise et soutenance (relais R6, puis tous les membres)

> À lire après `AGENTS.md` et `ETAT_PROJET.md`. Portes visées : **G6** (documentation) et **G7** (remise). Durée : **1 h**.
> La partie « Mode coach » (en fin de fiche) sert à **chaque membre** après la remise, pour la porte G8.

## Rôle et objectif

Rendre le projet **complet, cohérent et remis à temps** :

- README avec les preuves ;
- `prompts.md` finalisé ;
- fiche de contribution ;
- remise prête dans le dépôt, **téléversée sur le Drive par Leddycia** (D-13) ;
- **test sur un autre ordinateur**, depuis le Drive (C-14).

## Entrées à lire

- Tout `Groupe_01_Cas_01/` ; `tests/plan_de_test.md` (statuts) ; `travail/journal_prompts.md` ; `travail/journal_ecarts.md`
- `ETAT_PROJET.md` (journal des passations : il sert à la fiche de contribution)

## Checklist d'audit d'entrée (travail du relais R5 et cohérence globale)

| # | Point à vérifier | Comment |
|---|---|---|
| A1 | Le prototype final passe les CA | Passe réduite (fiche 05) sur `index.html`, ou sur `version_IA.html` si `index.html` est absent : « Toute la période » plus un mois, fuseau Haïti, hors ligne en fin de passe (fiche 05, contrôles transverses) |
| A2 | `version_IA.html` est intact | Après `git pull` puis `git fetch --tags`, `git tag -l` liste `version-ia` ; `git diff version-ia -- Groupe_01_Cas_01/prototype/version_IA.html` est vide |
| A3 | Au moins une capture par CA (une capture peut en prouver plusieurs), nommée correctement | Comparer `captures/` à la liste des CA ; faire d'abord les captures manquantes notées par R5 dans `ETAT_PROJET.md` |
| A4 | Cohérence entre livrables | Mêmes ID d'US et de CA dans le backlog, `prompts.md`, le plan de test et les captures ; Sprint 01 = US-01 à US-03 partout |
| A5 | Rien d'interdit dans le livrable | Pas de fichier parasite (`.gitkeep`, brouillons) dans `Groupe_01_Cas_01/` ; pas de donnée réelle autre que les noms des membres |

## Tâches

### 1. `Groupe_01_Cas_01/README.md` (C-15)

```
# PowerWatch : Groupe 01, Cas 01
## Présentation (2 ou 3 phrases : client, besoin, Sprint 01)
## Comment ouvrir le prototype
   - Double-cliquer sur prototype/index.html (ou version_IA.html si index.html est absent : le dire, C-09)
   - Cliquer sur « Choisir un fichier » et sélectionner energie_college.csv (fourni par l'intendant)
   - Aucun Internet, serveur ni compte nécessaire
## Outils utilisés (IA : outil et modèle pour chaque étape ; éditeur ; navigateurs de test)
## Contenu du dossier (une ligne par fichier)
## Vérification du Sprint 01
   | CA | Énoncé court | Statut (respecté / non respecté / partiel) | Preuve (lien vers captures/…) |
## Conditions de test (fuseau Haïti, hors ligne, navigateurs, test sur un autre PC : qui, quand)
## Écarts connus et points à confirmer avec le client (renvoi au CDC)
```

> Le CSV n'est pas un livrable listé par C-01. Le README indique simplement d'utiliser le fichier `energie_college.csv` fourni avec le cas.

### 2. Finaliser `Groupe_01_Cas_01/prompts.md` (C-08)

- **§2 Autres prompts importants** : en choisir **2 ou 3** dans `travail/journal_prompts.md`, ceux qui ont produit un travail important (cadrage, CDC, backlog, correction clé). Pour chacun : le texte exact, l'outil, ce qu'il a produit et ce que l'équipe a vérifié.
- **§3 Propositions corrigées ou rejetées** : au moins une (souvent plusieurs), tirées de `travail/journal_ecarts.md`. Pour chacune : ce que l'IA a proposé ou produit, pourquoi c'était faux ou hors périmètre (CA, règle ou consigne violés), ce qu'on a fait.
- **§4 Écarts** : signaler et justifier tout écart à C-12 (données intégrées), ou écrire « aucun ».

### 3. `fiche_contribution.pdf` (à la racine du dépôt, C-01, D-13)

- **Un tableau unique** : nom du membre | partie principale | contribution en une phrase.
- Sources : le tableau des relais et le journal des passations d'`ETAT_PROJET.md`.
- Rédiger dans Word ou Google Docs, exporter en PDF, puis l'enregistrer à la **racine du dépôt**, au même niveau que `Groupe_01_Cas_01/`, comme sur le Drive.

### 4. Remise sur le Drive : préparer, puis passer la main à Leddycia (C-01, C-19, D-13)

1. Dire **« sauvegarde du relais »** à l'IA : le README, `prompts.md` et `fiche_contribution.pdf` sont commités et poussés (sans tag).
2. Prévenir **Leddycia** en lui donnant le hash court du commit de sauvegarde (`git log -1 --format=%h`), **seulement après** la vérification de la sauvegarde (`git status -sb` sans `ahead` ni `behind`). Dans son clone, elle fait `git pull`, vérifie que `git log -1 --format=%h` affiche ce hash et que `git status --short` n'affiche rien, puis téléverse elle-même dans le dossier du groupe sur le Drive (`Groupe_01/`), **au même niveau** :
   - le dossier `Groupe_01_Cas_01/`, pris dans le dépôt **tel quel** ;
   - `fiche_contribution.pdf`.
3. Rien d'autre n'est déposé : ni `AGENTS.md`, ni `travail/`, ni `tests/`, ni aucun autre fichier de l'espace de travail (D-04).
4. Attendre la confirmation de Leddycia (heure du téléversement), à noter dans le journal de bord.

### 5. Test sur un autre ordinateur (C-14)

1. **Sur un PC différent de celui de R5**, télécharger le dossier **depuis le Drive**, une fois le téléversement de Leddycia confirmé.
2. Récupérer `energie_college.csv` dans le dossier du cas fourni par l'enseignant, ou dans `docs/` du dépôt, et le placer **hors** du dossier livrable.
3. Double-cliquer sur le prototype, hors ligne (fiche 05, contrôles transverses), et charger ce CSV.
4. Vérifier une valeur par période avec l'oracle.
5. Compléter la section « Conditions de test » du README (qui, quand, sur quel PC et quel navigateur), dire **« sauvegarde du relais »**, puis, une fois la sauvegarde vérifiée, donner le nouveau hash à **Leddycia** : elle fait `git pull`, vérifie le hash et remplace le README sur le Drive (choisir « Remplacer le fichier existant », jamais « Conserver les deux »). Noter l'heure de sa confirmation au journal de bord.
6. Si quelque chose casse : corriger dans le dépôt, retester, dire « sauvegarde du relais », puis Leddycia fait `git pull`, supprime l'ancien dossier `Groupe_01_Cas_01` du Drive (Drive ne fusionne pas deux dossiers du même nom) et téléverse le nouveau, ou remplace un à un les fichiers modifiés. Un seul dossier `Groupe_01_Cas_01` doit rester dans `Groupe_01/`.

## Procédure (1 h)

**R6 démarre au plus tard à 22 h 00.**

| Temps | Étape |
|---|---|
| 0 à 10 min | Démarrage, audit A2 à A5 et A1 réduit (« Toute la période » plus un mois) |
| 10 à 25 min | README (tâche 1) |
| 25 à 30 min | `prompts.md` §2 à §4 (tâche 2) |
| 30 à 35 min | `fiche_contribution.pdf` à la racine du dépôt (tâche 3) |
| 35 à 45 min | « sauvegarde du relais », puis téléversement par Leddycia (tâche 4), **au plus tard à la 45e minute**, même si le README reste perfectible |
| 45 à 55 min | Test depuis le Drive sur un autre PC (tâche 5) |
| 55 à 60 min | Conditions de test dans le README, « sauvegarde du relais », remplacement du README sur le Drive par Leddycia, puis **« fin de notre relais »** (commit, tag annoté `relais-6`, push : `AGENTS.md` §9) |

## Checklist de sortie (DoD)

- [ ] Le README contient un statut et une preuve pour **chaque** CA du Sprint 01 ; il mentionne `index.html`, ou explique son absence.
- [ ] `prompts.md` : RMTCEV, 2 ou 3 autres prompts, au moins une correction ou un rejet avec sa raison, section écarts.
- [ ] `fiche_contribution.pdf` : un tableau unique, une ligne par membre ; à la racine du dépôt.
- [ ] Drive (téléversé par Leddycia) : `Groupe_01/fiche_contribution.pdf` et `Groupe_01/Groupe_01_Cas_01/`, rien d'autre.
- [ ] Test depuis le Drive sur un autre PC fait et noté dans le README, et ce README remplacé sur le Drive par Leddycia. **Tout est remis avant le 18/10/2026 à 23 h 59.**
- [ ] Commit, tag annoté `relais-6` et push (`AGENTS.md` §9) ; `relais-6` apparaît dans `git ls-remote --tags origin` ; R6 passé à « REMIS » dans `ETAT_PROJET.md` selon le critère du protocole (« Cas du dernier relais »), sinon « FAIT (remise à confirmer) » puis complément.

## Interdits

- Mettre dans le livrable autre chose que ce que prévoit C-01 (qui inclut le dossier `captures/` exigé par C-15) : ni CSV, ni brouillon, ni fichier de `travail/` ou de `tests/`.
- Modifier `version_IA.html`.
- Ajouter une fonction nouvelle dans `index.html`, même lors d'une correction de dernière minute.

## Prompt d'amorçage spécifique

```
Mission R6 (finalisation) : à partir de tests/plan_de_test.md, travail/journal_prompts.md,
travail/journal_ecarts.md et ETAT_PROJET.md, rédige Groupe_01_Cas_01/README.md selon le gabarit
de la fiche agents/06_finalisation_soutenance.md, puis propose les §2 à §4 de prompts.md.
N'ajoute rien au livrable hors C-01, ne touche jamais version_IA.html, n'ajoute aucune fonction à index.html.
```

## À écrire dans `ETAT_PROJET.md` à la passation

- R6 passé à « REMIS » (téléversement et remplacement du README confirmés par Leddycia, test noté dans le README), sinon « FAIT (remise à confirmer : … ») ; porte G7 atteinte ou non.
- Date et heure du téléversement sur le Drive par Leddycia, et du remplacement du README.
- Test sur un autre PC : qui, quand, sur quel PC et quel navigateur.
- Les écarts et les captures restants, s'il y en a.

---

## Mode coach : préparation de la soutenance (chaque membre, après la remise)

La soutenance dure environ 15 min : une démonstration courte, puis des **questions individuelles à tous, y compris sur les parties qu'on n'a pas faites** (C-16).

### Prompt coach (à utiliser avec n'importe quelle IA, après avoir chargé `AGENTS.md`)

```
Mode coach de soutenance PowerWatch. Lis AGENTS.md, ETAT_PROJET.md, docs/brief_client.md,
Groupe_01_Cas_01/cahier_des_charges.md, product_backlog.md, prompts.md et README.md.
Pose-moi 10 questions, une à la fois, comme un jury exigeant, en couvrant TOUTES les parties
(besoin, CDC, backlog et MoSCoW, prompt RMTCEV, vérification, corrections de l'IA, limites).
Après chacune de mes réponses : note sur 5, correction précise avec la référence (B-xx, C-xx, CA, E-xx).
À la fin : mes 3 points faibles et quoi relire.
```

### Questions que chacun doit savoir traiter

1. Qui sont les acteurs ? Pourquoi le gardien n'est-il pas un utilisateur ?
2. Pourquoi ces 3 US dans le Sprint 01, et pas le tableau jour par jour ?
3. Que dit exactement la règle d'égalité ? Montrez-la sur les données d'août.
4. Pourquoi l'alerte SMS est-elle en Won't ? Pourquoi la part solaire est-elle bloquée ?
5. Qu'est-ce qu'un CA « observable et vérifiable » ? Donnez-en un du Sprint 01.
6. Détaillez les 6 parties de votre prompt RMTCEV.
7. Citez une proposition de l'IA que vous avez rejetée, et pourquoi.
8. Comment avez-vous prouvé que l'outil ne modifie pas les données ?
9. Pourquoi tester avec le fuseau horaire d'Haïti (supposé, Q-09) ?
10. Pourquoi les données ne sont-elles pas intégrées dans la page ?
11. Que reste-t-il à confirmer avec le client ?
12. Quelle est la différence entre `version_IA.html` et `index.html` ?

### Démonstration (environ 3 min, à répéter une fois)

1. Ouvrir par double-clic, hors ligne.
2. Cliquer sur « Choisir un fichier » et charger le CSV.
3. « Toute la période » : 97 h, 280,0 L, 84 000 gourdes, 06/08/2026.
4. Passer à septembre : 30 h, 84,0 L, 25 200 gourdes, 08/09/2026, et expliquer l'égalité.
5. Montrer une correction faite sur la version de l'IA.

# Protocole du relais : journal de bord et « fin de notre relais »

> **Pour l'IA assistante de chaque relais, quel que soit l'outil.** À lire au démarrage, avec `AGENTS.md` et `ETAT_PROJET.md` (décision D-14).
> But : `ETAT_PROJET.md` se met à jour **pendant** que le membre travaille. À la fin, le membre dit simplement **« fin de notre relais »** et l'IA fait toute la passation.
> Les règles d'`AGENTS.md` restent en vigueur ; ce protocole ne fait que les appliquer.
> **Notation** : « ETAT §n » désigne une section d'`ETAT_PROJET.md` ; « §n » seul, une section de ce protocole.

---

## 1. Phrases de commande

L'IA reconnaît ces phrases sans tenir compte de la casse, des accents ni de la ponctuation, en français comme en créole :

| Phrase dite par le membre | Variantes acceptées | Effet |
|---|---|---|
| **« fin de notre relais »** | « fin du relais », « fin de relais », « fen relè nou an » | Passation complète (§4), **y compris commit, tag annoté `relais-X` et push**. La phrase vaut demande explicite de l'humain (`AGENTS.md` §9). |
| **« sauvegarde du relais »** | « sauvegarde intermédiaire » | Sauvegarde (§3.6) : ETAT à jour, commit et push, **sans tag**. |
| **« reprise du relais »** | aucune | Session rouverte dans le même relais (§3.7). |

Les mots courants seuls (« sauvegarde », « on reprend », « fin ») ne déclenchent rien. En cas de doute sur l'intention, l'IA pose une seule question : « Tu veux que je fasse maintenant la passation complète, ou seulement la sauvegarde (commit et push sans tag) ? ».

Avant d'exécuter une phrase de commande, l'IA **relit ce protocole** (§3.6 pour la sauvegarde, §4 et §5 pour la passation) : après une longue session, le détail a pu quitter son contexte.

---

## 2. Démarrage

### 2.1 Dès la lecture d'ETAT (avant tout audit)

Si ETAT §8 ne contient pas « **Aucun relais en cours.** » :

- **§8 concerne le relais RX que le membre annonce** (même numéro de relais, quel que soit le membre) : c'est une **reprise** (§3.7) ; pas de nouvel audit.
- **§8 concerne un autre relais** : ce relais n'a pas été clôturé. L'IA le signale **en tête de son rapport**, avant tout audit. Le membre décide :
  - **clôturer ce relais** : il dit « fin de notre relais » en précisant lequel, et l'IA applique le §4 pour ce relais. Si l'IA n'a pas suivi ce relais, elle ne reconstruit rien : pour une étape sans JP, elle demande au membre le texte exact ou écrit « texte exact non consigné pendant le relais » ; à l'étape 1, elle ne termine rien elle-même, montre `git status --short` et demande quoi garder ; l'heure de fin est celle de la dernière ligne du journal de bord ;
  - **ou l'archiver** : ajouter à la fin d'ETAT §7, juste avant le `---`, une entrée « ### RX (non clôturé, journal archivé par R(X+1) le AAAA-MM-JJ) » contenant le contenu du §8 **sans** son titre « ## 8. … » ni sa note ; dans la ligne RX d'ETAT §2, remplacer la mention « EN COURS … » par « non clôturé (journal archivé au §7) » ; puis remettre le §8 vide (§5.1).

### 2.2 Synchronisation

Le membre a lancé `git pull` avant d'ouvrir l'IA (ETAT §6, étape 1). L'IA lance `git fetch origin` (sans effet sur les fichiers), puis `git status -sb` : la première ligne doit être `## main...origin/main`, sans `behind` ni `ahead`, et **aucune autre ligne** ne doit suivre. Sinon, elle le signale en tête de son rapport d'audit, avec, pour chaque fichier modifié ou non suivi, le relais d'où il vient : ces fichiers seraient pris par le `git add -A` de la passation, et ne sont commités qu'avec l'accord du membre.

### 2.3 Après la validation de l'audit et du plan (`AGENTS.md` §0, étape 6)

Ces écritures sont les **premières** du relais ; la validation du plan les couvre.

1. **ETAT §2**, ligne RX : membre, outil d'IA et modèle (s'ils sont « à compléter », les demander au membre ; ne jamais les déduire) ; colonne Statut = « **EN COURS** (début HH:MM) ». Ne jamais modifier la colonne « Créneau prévu ».
   **Complément** d'un relais déjà tagué (tag `relais-X` sur le dépôt distant : `git ls-remote --tags origin relais-X`) : garder « FAIT … » et le tag, et ajouter seulement « ; complément EN COURS (début HH:MM, §8) » ; au §1, « Relais en cours » = « RX (complément) » ; au §8, colonne Relais = « RX (complément, après le tag `relais-X`) ».
2. **ETAT §1** : « Relais en cours » = RX ; « Prochain relais » = R(X+1) avec sa fiche.
3. **ETAT §8** : remplir le modèle du §5.2 : en-tête, **plan validé** (étapes numérotées), **synthèse de l'audit** (un constat bloquant ou à corriger par ligne, ce qui a été seulement survolé, les résultats donnés par le membre lui-même, par exemple ses totaux du recalcul A3 pour R2).
4. **Rapport d'audit complet** : créer tout de suite `travail/audits/RX_audit.md` (modèle §5.3), avec le tableau complet de l'audit validé, conformes compris. Il ne reste ainsi pas dans la seule conversation.

**Heure** : jamais inventée. En ligne de commande, la lire avec `date +%H:%M` (Git Bash) ou `Get-Date -Format HH:mm` (PowerShell). Une IA web la demande au membre.

---

## 3. Pendant le relais

1. **Journal de bord** : après chaque étape du plan terminée ou abandonnée, et après toute création ou modification importante d'un fichier, l'IA ajoute **une ligne** au tableau « Journal de bord » d'ETAT §8 :
   `| HH:MM | étape n | ce qui a été fait | fichiers | fait / partiel / abandonné |`
2. **Point ouvert** (question au client, blocage, décision à prendre) : une ligne dans « Points ouverts du relais » d'ETAT §8. Une décision suit aussi les règles de `travail/decisions.md`, tout de suite.
3. **Correction d'un livrable d'un relais précédent** : une ligne aussi dans « Corrections apportées » de `travail/audits/RX_audit.md` (RG-10).
4. **Prompt significatif** du membre : entrée JP-xx dans `travail/journal_prompts.md` au moment où il est envoyé, texte exact (RG-11). **Proposition de l'IA corrigée ou rejetée** : entrée E-xx dans `travail/journal_ecarts.md`, en continuant la numérotation. La ligne du journal de bord cite le JP ou l'E.
5. **Fichiers temporaires** (texte extrait du .docx, script de recalcul, diff, brouillon) : **toujours hors du dépôt** (dossier temporaire du système, par exemple `%TEMP%`). Le dépôt est public : tout ce qui y entre est publié.
6. **« sauvegarde du relais »** : terminer ou annuler la modification en cours, mettre ETAT §8 à jour, puis faire l'étape Git du §4.7 **sans aucun tag**, avec le message `docs(rX): sauvegarde intermédiaire`. Vérification : `git status -sb` affiche `## main...origin/main` sans `ahead`. Ne jamais créer `relais-X` lors d'une sauvegarde.
7. **Reprise** (« reprise du relais », ou cas du §2.1) : `git fetch origin` puis `git status -sb` ; si l'arbre est propre et `behind`, `git pull --no-rebase --no-edit` ; sinon, le signaler au membre. Relire `AGENTS.md`, ce protocole, puis ETAT §8, et reprendre à la dernière ligne du journal de bord. Ni nouvel audit, ni nouvelle validation, sauf si le membre change le plan.

Ces mises à jour touchent seulement ETAT §1, §2 et §8, `travail/audits/RX_audit.md`, `travail/decisions.md` et les journaux de `travail/`. Elles sont couvertes par la validation du plan : l'IA ne redemande pas l'accord à chaque ligne.

---

## 4. « Fin de notre relais » : passation complète

L'IA exécute **toutes** les étapes, **dans cet ordre**, puis rend compte. Elle ne s'arrête que si un contrôle de l'étape 7 échoue, si un conflit Git touche un autre fichier qu'ETAT ou un journal, ou si une commande lui est impossible.

1. **Arrêter proprement** : terminer ou annuler la modification en cours ; aucun fichier ne reste à moitié modifié.
2. **Bilan** : comparer le plan validé au journal de bord ; classer chaque étape : fait, partiel, non fait.
3. **Journaux et décisions** : chaque prompt significatif a son JP-xx, chaque correction ou rejet son E-xx ; toute décision prise pendant le relais figure dans `travail/decisions.md`, avec son statut et une ligne au journal des changements. Compléter ce qui manque.
4. **Rapport d'audit** `travail/audits/RX_audit.md` : compléter, à partir du journal de bord, « Corrections apportées », « Points remontés à l'équipe » et « Ce que j'ai produit pendant mon relais » ; puis coller la copie **intégrale** d'ETAT §8 tel qu'il figure dans le fichier (en-tête, plan, synthèse, journal, points ouverts), sans résumé, **sous le titre existant** « Journal de bord du relais » (ne pas le dupliquer). Ne jamais écraser un rapport existant : pour un complément, ajouter à la fin une section « ## Complément (AAAA-MM-JJ HH:MM → HH:MM) ». Si le rapport n'existe pas (relais sans audit d'entrée, comme R1), le créer avec le titre « # Relais RX : journal de bord (pas d'audit d'entrée) » et la seule section « Journal de bord du relais ».
5. **ETAT §1 à §7** (d'abord, `git ls-remote --tags origin relais-X` : si le tag est déjà sur le dépôt distant, c'est un **complément** ; appliquer le paragraphe « Complément » ci-dessous au lieu des règles §2 et §7) :
   - **§2** : ligne RX → Statut « **FAIT** (HH:MM → HH:MM) », ou « FAIT (partiel, HH:MM → HH:MM) » s'il reste du travail ; colonne Tag : `relais-X`. Si le prénom du membre suivant est encore « à compléter », le demander au membre et l'inscrire ; ne jamais l'inventer.
   - **§1** : porte atteinte, relais terminé RX, « Relais en cours : aucun », prochain relais R(X+1) avec sa fiche.
   - **§3** : une ligne par élément produit (élément, fichier, relais).
   - **§4** : retirer ce qui est fait ; placer en tête ce qui reste du relais RX, marqué « à reprendre par R(X+1) ».
   - **§5** : résoudre ou ajouter les points ouverts.
   - **§6** : réécrire « Mission du prochain relais : R(X+1) » **en gardant sa structure** : étape 1 (prérequis ETAT §0, `git pull`, `git fetch --tags`, `git tag -l` où `relais-X` doit apparaître, contrôle de chargement par la règle RG-08) ; étape 2 (prompt d'amorçage d'`AGENTS.md` §14 avec le bon numéro et la bonne fiche) ; étapes de mission tirées de la fiche de R(X+1) (audit, entrées, livrable), plus le reste à faire de RX et les points d'attention ; dernière étape : « fin de notre relais ».
   - **§7** : ajouter l'entrée de RX (modèle §5.2) **à la fin de la section, juste avant le `---` qui précède le §8** ; elle reprend la section « À écrire dans `ETAT_PROJET.md` à la passation » de la fiche du relais.
6. **ETAT §8** : seulement maintenant, remettre le modèle vide (§5.1).
7. **Git**, en deux blocs **lancés séparément** (jamais dans la même commande) :

   **Bloc A, contrôle** (Git Bash, à la racine du dépôt) :

   ```bash
   git fetch origin
   git status -sb
   git add -A
   git diff --cached --no-renames --name-status
   git diff --cached --no-renames --name-only | grep -E '^docs/.*\.(docx|pdf|csv)$|version_IA\.html$' && echo "STOP : fichier interdit indexé" || echo "CONTROLE OK"
   ```

   **Contrôle bloquant**, avant tout bloc B :
   - « STOP » : un original de `docs/` ou `version_IA.html` est indexé (toujours écrire le nom entre apostrophes : `'<fichier>'`). S'il est suivi par Git (`git ls-files --error-unmatch '<fichier>'` réussit) : `git restore --staged '<fichier>'`, puis `git restore '<fichier>'`. Sinon (fichier nouveau, par exemple `docs/~$_Demande_client.docx`, verrou créé par Word quand le .docx est ouvert) : seulement `git restore --staged '<fichier>'`, puis demander au membre de fermer Word. Dans tous les cas, prévenir le membre. Ne jamais restaurer le CSV depuis 478570e. Seule exception : le **premier** commit de `version_IA.html`, que R4 fait à part, selon la fiche 03 (tag `version-ia`), jamais par ce bloc.
   - **Fichier non prévu** dans la liste (ni livrable de C-01, ni ETAT, ni journal, ni audit, ni fichier du plan validé ; par exemple un brouillon, `~$…`, `desktop.ini`, un script ou un texte extrait) : `git restore --staged <fichier>`, ne pas le supprimer, demander au membre de le déplacer hors du dépôt. Dans `Groupe_01_Cas_01/`, rien d'autre que ce que prévoit C-01 (RG-12).
   - Si `AGENTS.md` ou `GEMINI.md` est indexé : `wc -c <fichier>` doit rester sous 23 500 octets sur le disque (Antigravity lit au plus 24 000 octets par fichier ; sous Windows, les fins de ligne CRLF ajoutent un octet par ligne).

   **Bloc B, commit, tag et push**, seulement après « CONTROLE OK » et la liste relue :
   1. `git commit -m "docs(rX): <résumé du relais>"` (sauvegarde : `docs(rX): sauvegarde intermédiaire`).
   2. Si le bloc A a montré `behind` ou `diverged` : `git pull --no-rebase --no-edit`. Si le conflit ne touche qu'`ETAT_PROJET.md` ou un journal de `travail/`, l'IA le résout **en gardant les deux apports** (sections réécrites par la passation et lignes modifiées à distance, par exemple l'affectation d'un membre au §2), montre `git diff HEAD -- <fichier>` au membre, puis `git add <fichier>` et `git commit --no-edit`. Autre fichier en conflit : s'arrêter et demander.
   3. **Tag** (passation seulement, jamais pour une sauvegarde) : vérifier `git tag -l relais-X` et `git ls-remote --tags origin relais-X`.
      - Absent partout : `git tag -a relais-X -m "Relais RX"`.
      - Présent en local seulement (push précédent échoué) : ne pas le recréer ; le push le publie.
      - Présent sur le dépôt distant : c'est un **complément** (déjà traité à l'étape 5). Ne pas toucher au tag.
   4. `git push --atomic origin main --follow-tags`.
   5. **Vérification** : `git status -sb` affiche `## main...origin/main` sans `ahead` ni `behind`, et sans fichier modifié ; pour une passation, `git ls-remote --tags origin relais-X` liste le tag.

   **Cas particuliers**
   - **Push refusé parce que le dépôt distant a avancé** (`rejected`, `fetch first`, `non-fast-forward`) : appliquer le point 2 du bloc B, puis relancer seulement le point 4.
   - **Push refusé pour droits ou identification** (403, `Permission denied`, `Authentication failed`, demande d'identifiants) : s'arrêter sans rien changer (ni remote, ni identifiants). Le membre accepte l'invitation GitHub (ETAT §0, étape 1) ou se connecte, puis lance lui-même le point 4 ; l'IA fait ensuite la vérification.
   - **Commande impossible pour l'IA** (sandbox, réseau coupé, approbation refusée ; par exemple `Permission denied` sur `.git/index.lock` ou `Could not resolve host` avec Codex) : ce n'est pas un push refusé. Les deux blocs restent séparés, comme dans la variante web : (1) l'IA donne le bloc A seul ; le membre le lance dans Git Bash, à la racine du dépôt, et colle la sortie ; (2) l'IA fait le contrôle bloquant sur cette sortie (elle peut relancer elle-même `git status -sb` et `git diff --cached --name-status`, qui ne font que lire) ; (3) seulement ensuite, elle donne le commit, puis, d'après la sortie collée de `git tag -l relais-X` et `git ls-remote --tags origin relais-X`, la ligne du tag qui convient, puis le push ; (4) elle fait la vérification avec le membre.
   - **Shell PowerShell** (Windows PowerShell 5.1) : `&&` y est une erreur. Lancer chaque commande séparément et ne passer à la suivante que si `$LASTEXITCODE` vaut 0. Lancer les commandes `git` directement dans PowerShell (git est dans le PATH). À la place de la ligne `grep` du bloc A : `$l = git diff --cached --no-renames --name-only | Select-String -Pattern '^docs/.*\.(docx|pdf|csv)$|version_IA\.html$'; if ($l) { "STOP : $l" } else { 'CONTROLE OK' }`. Ne pas lancer `bash` seul (il peut ouvrir WSL), et éviter d'appeler Git Bash depuis PowerShell : Windows PowerShell 5.1 supprime les guillemets doubles internes et tronque la commande sans erreur. Écrire dans les fichiers uniquement avec l'outil d'édition de l'IA (par exemple apply_patch pour Codex), jamais avec `Add-Content`, `Set-Content`, `Out-File` ou `>` : ils écrivent en ANSI ou en UTF-16 et abîment les accents.
   - Les avertissements « LF will be replaced by CRLF » sont normaux.

   **Complément d'un relais déjà clôturé** (tag `relais-X` déjà sur le dépôt distant). **Ouverture** : quand un membre reprend un relais déjà tagué (par exemple R6 pour passer à REMIS), l'IA applique le §2.3 avec la règle « Complément ». **Clôture** : ETAT §2 garde « FAIT » et le tag, en remplaçant « ; complément EN COURS (…) » par « ; complément FAIT (HH:MM → HH:MM, non tagué) » (exception R6 : le complément de remise remplace « FAIT (remise à confirmer : …) » par « REMIS (complément HH:MM, non tagué) ») ; §6 n'est modifié que si le complément change la mission ; §7 : **nouvelle entrée** « ### RX (complément) : … » à la fin de la section, sans toucher à l'entrée d'origine ; rapport d'audit : section ajoutée (étape 4).

8. **Rendre compte** au membre en quelques lignes : fait, reste, hash court du commit (`git rev-parse --short HEAD` ; dans `git ls-remote`, la première ligne d'un tag annoté désigne l'objet tag, pas le commit), tag. Le hash n'est jamais écrit dans ETAT (le fichier fait partie du commit). Puis donner le **message de passation prêt à envoyer** (§5.4).

### Cas du dernier relais (R6)

- **ETAT §2** : R6 passe à **REMIS** seulement quand Leddycia a confirmé le téléversement **et** le remplacement du README sur le Drive (heures notées au journal de bord), et que le test depuis le Drive figure dans le README. Sinon : « FAIT (remise à confirmer : <ce qui manque>) ». Le passage à REMIS se fera ensuite par un complément (tag `relais-6` déjà posé).
- **ETAT §1** : « Prochain relais : aucun (soutenance : mode coach, fiche 06) ».
- **ETAT §6** devient « Après la remise : préparation de la soutenance » (prompt coach et démonstration de la fiche 06).
- Le message de passation s'adresse à tout le groupe : heure de la remise, test sur un autre PC (qui, quand), préparation avec le mode coach. Il ne nomme aucun R7.

### Variante pour une IA web

Une IA web ne voit pas le dépôt et ne lance aucune commande. **C'est le membre qui reporte et qui exécute.**

- **Au démarrage** (§2.3) : les blocs à coller : les lignes « Relais en cours » et « Prochain relais » d'ETAT §1, la ligne RX d'ETAT §2, la section ETAT §8 complète ; puis le contenu de `travail/audits/RX_audit.md`.
- **Pendant le relais** : après chaque étape, la ligne à coller dans le journal de bord d'ETAT §8 (heure donnée par le membre) ; pour un point ouvert, la ligne à ajouter aux « Points ouverts du relais » ; les entrées JP-xx, E-xx et les lignes de `decisions.md` au moment où elles naissent.
- **« sauvegarde du relais »** : la ligne de §8, puis le bloc A ; après que le membre a collé la sortie du bloc A, le bloc B sans tag. Le membre colle ensuite la sortie du bloc B, de `git status -sb` et de `git log -1 --format=%h` : l'IA confirme qu'il n'y a ni `ahead` ni `behind` avant que ce hash soit donné à quiconque (fiche 06, tâche 4). Push refusé : cas particuliers ci-dessus.
- **« fin de notre relais »** : l'IA demande d'abord au membre de coller l'`ETAT_PROJET.md` **actuel** (il a pu changer depuis le téléversement). Elle fournit ensuite, éventuellement en plusieurs réponses :
  1. pour ETAT, **chaque section à remplacer** en entier (§1, §2, §4, §5, §6, §8), précédée de son titre exact ; les lignes à **ajouter** au §3 ; l'entrée à **ajouter** à la fin du §7. Jamais le fichier entier ;
  2. pour `travail/audits/RX_audit.md`, le contenu de chacune des sections à compléter (« Corrections apportées », « Points remontés à l'équipe », « Ce que j'ai produit pendant mon relais », « Journal de bord du relais »), précédé de son titre exact ;
  3. les entrées JP-xx, E-xx et les lignes de `decisions.md` manquantes, ou « aucune » ;
  4. le bloc A ; après que le membre a collé sa sortie et que l'IA a fait le contrôle bloquant, le bloc B **en deux collages** :
     - **B1** : le commit, puis, seulement si le bloc A a montré `behind` ou `diverged`, `git pull --no-rebase --no-edit`. Le membre colle la sortie. Si elle contient `CONFLICT` sur ETAT ou sur un journal : le membre colle `grep -n -A20 '^<<<<<<<' <fichier>` ; l'IA rend la zone fusionnée (les deux apports) ; le membre la reporte ; `grep -c '^<<<<<<<\|^>>>>>>>' <fichier>` doit afficher 0 ; puis `git add <fichier>` et `git commit --no-edit`. Conflit sur un autre fichier : s'arrêter ;
     - **B2**, seulement quand `git status -sb` ne montre plus `behind` : la vérification du tag (sortie collée), la ligne du tag qui convient, puis le push ;
  5. le message de passation, **seulement après** que le membre a collé la sortie de `git ls-remote --tags origin`, de `git status -sb` et de `git rev-parse --short HEAD`, et que l'IA a confirmé que le push est fait. Le hash du message vient de `git rev-parse` seulement ; sans sortie collée, l'IA écrit « hash à compléter » et le demande.
- **Entre le bloc A et le bloc B**, le membre lance `git --no-pager diff --cached -U0 -- ETAT_PROJET.md` et colle la sortie (après `git add -A`, `git diff` sans `--cached` n'affiche plus rien). L'IA vérifie qu'aucune ligne commençant par « - » ne vient du §3 ni du §7.

---

## 5. Modèles

### 5.1 ETAT §8 vide (à remettre à la fin de chaque relais)

```markdown
## 8. Relais en cours (journal de bord, tenu par l'IA)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

**Aucun relais en cours.** Prochain relais : voir §1.
```

### 5.2 ETAT §8 rempli (pendant le relais) et entrée ETAT §7

```markdown
## 8. Relais en cours (journal de bord, tenu par l'IA)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

| Relais | Membre | Outil et modèle | Fiche | Porte visée | Début |
|---|---|---|---|---|---|
| RX | <prénom> | <outil, modèle> | `agents/0X_….md` | GX | HH:MM |

**Plan validé** : 1. … 2. … 3. …

**Audit d'entrée (synthèse)** : <constat | preuve | gravité>, un par ligne ; survolé : … ; résultats du membre : … (détail : `travail/audits/RX_audit.md`).

**Journal de bord**

| Heure | Étape | Ce qui a été fait | Fichiers | État |
|---|---|---|---|---|

**Points ouverts du relais** : …
```

Entrée ETAT §7 (journal des passations) :

```markdown
### RX : <titre de la mission> (AAAA-MM-JJ, HH:MM → HH:MM)

- **Membre et outil** : …
- **Audit d'entrée** : <synthèse> (détail : `travail/audits/RX_audit.md`).
- **Fait** : …
- **Reste** : … (à reprendre par R(X+1))
- **Décisions** : …
- **Points d'attention pour R(X+1)** : …
- **Porte** : GX atteinte / partielle.
- **Tag** : `relais-X` (ou « complément, commit non tagué »). Le hash du commit figure dans le compte rendu et le message de passation.
```

### 5.3 Rapport d'audit `travail/audits/RX_audit.md`

```markdown
# Audit d'entrée : relais RX (<prénom>, <outil d'IA>, AAAA-MM-JJ HH:MM)

## Livrable audité : <fichier(s)> (produit par R<X-1>)

| # | Constat | Preuve (fichier:ligne, B/C/CA) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|

## Ce qui a été seulement survolé ; résultats donnés par le membre

## Corrections apportées (une ligne par correction)

## Points remontés à l'équipe (decisions.md, ETAT_PROJET.md)

## Ce que j'ai produit pendant mon relais

## Journal de bord du relais (copie intégrale d'ETAT §8, ajoutée à la passation)
```

### 5.4 Message de passation

```
Relais RX terminé (porte GX : atteinte / partielle).
Fait : …
Reste : …
Commit : <hash court> ; tag relais-X (vérifié avec git ls-remote).
À toi, R(X+1) [prénom] : <mission> (fiche agents/<fiche>.md).
Points d'attention : …
git pull puis lis ETAT_PROJET.md (§6 : ta mission).
```

# Fiche de rôle 03 : Prompt engineer, délégation du Sprint 01 (relais R4)

> À lire après `AGENTS.md` et `ETAT_PROJET.md`. Porte visée : **G4**. Durée : **1 h**.

## Rôle et objectif

Ce relais a quatre tâches :

1. **Rédiger le prompt de délégation** du Sprint 01, au format **RMTCEV** (critère C-18 : « précision des prompts »).
2. **Le faire exécuter une seule fois** par une **IA déléguée en session vierge** (D-09).
3. **Conserver la sortie brute** dans `version_IA.html` (C-09).
4. Préparer le plan de test et les fixtures pour R5.

## Entrées à lire

- `Groupe_01_Cas_01/cahier_des_charges.md` et `Groupe_01_Cas_01/product_backlog.md`
- `docs/consignes.md` (C-08 à C-13), `travail/decisions.md` (D-02, D-09, D-10), `docs/oracle.md`

## Checklist d'audit d'entrée (travail du relais R3)

| # | Point à vérifier | Comment |
|---|---|---|
| A1 | 8 US au format exact, avec leurs sources | Lecture |
| A2 | Le Sprint 01 contient exactement US-01 à US-03, et le chargement est dans l'US-01 | Section Sprint 01 |
| A3 | Les CA du Sprint 01 sont chiffrés et conformes à l'oracle | Comparer chaque valeur avec `docs/oracle.md` §2 et §4 |
| A4 | Les CA sont vérifiables par un tiers, sans solution technique | Se demander pour chacun : « Puis-je dire oui ou non en regardant l'écran ? » |
| A5 | Les CA du fuseau Haïti (Q-09), du fichier mélangé, du mode hors ligne et du hash existent | Recherche |

## Tâche 1 : trancher D-10, puis rédiger le prompt RMTCEV

**D-10** décide si le prompt mentionne les pièges P-01 à P-10. Recommandation : donner **les règles et les valeurs attendues**, pas les solutions d'implémentation. Inscrire la décision dans `travail/decisions.md`.

Structure (D-02) : **R**ôle, **M**ission, **T**âches, **C**ontexte/Contraintes, **E**xemples, **V**alidation.

```
## R : Rôle
Tu es un développeur front-end expérimenté qui livre des prototypes HTML autonomes, hors ligne, en français.

## M : Mission
Réaliser le Sprint 01 du projet PowerWatch : une page HTML unique qui charge le CSV de l'intendant
et affiche, pour la période choisie, les totaux, le coût estimé et le jour de fonctionnement maximal.
Seules les user stories US-01, US-02 et US-03 sont à réaliser.

## T : Tâches
1. … (une tâche par CA ou groupe de CA du Sprint 01, dans l'ordre)
N. Livrer le fichier complet en un seul bloc de code HTML.

## C : Contexte et contraintes
### Cahier des charges (intégral)
<coller ici cahier_des_charges.md EN ENTIER>
### Sprint 01 (intégral, avec les CA)
<coller ici la section Sprint 01 et les US-01 à US-03 avec TOUS leurs CA>
### Contraintes impératives
- Un seul fichier .html : CSS et JS inclus ; aucune ressource externe (CDN, police, image distante, réseau).
- S'ouvre par double-clic, sans serveur, sans Internet, sans compte.
- Le CSV est chargé par l'utilisateur via un bouton au libellé exact « Choisir un fichier ».
  Aucune donnée ne doit être écrite dans la page.
- Lecture seule : aucune modification, saisie ni enregistrement des données.
- N'implémente RIEN d'autre que US-01 à US-03 : pas de graphique, d'export, de tableau jour par jour,
  ni de stockage local.
- Interface en français ; formats : <H-01, H-02, Q-01>.

## E : Exemples
- Format du CSV : l'en-tête date,heures_solaire,heures_generatrice,litres_carburant et 4 lignes représentatives :
  2026-08-03,4,3,9 ; 2026-08-04,6,0,0 ; 2026-09-08,6,5,12.5 ; 2026-09-15,5,1,2.5.
  Point décimal dans le fichier, virgule à l'affichage (Q-01) ; fins de ligne CRLF.
  Ces lignes illustrent le format : n'écris aucune donnée dans la page, les données viennent uniquement
  du fichier choisi par l'utilisateur (C-12).
- Résultats attendus (oracle §2.2) : août 24 h, 71,0 L, 21 300 gourdes, 06/08/2026 ; … ; toute la période …
- Règle d'égalité illustrée : en août, 06/08 et 12/08 ont 5 h, donc on affiche 06/08/2026.

## V : Validation
Avant de répondre, vérifie toi-même chaque critère d'acceptation du Sprint 01 et confirme
que tes calculs redonnent exactement les résultats attendus ci-dessus.
Format de réponse : uniquement le fichier HTML complet, dans un seul bloc de code, sans explication.
```

> Le CDC et le Sprint 01 sont collés **en entier** : C-08 exige qu'ils soient fournis comme contexte. Les données du CSV restent fictives (C-13).

**Relecture, puis enregistrement du prompt avant la délégation (C-08) :**

- Relecteur du prompt RMTCEV : le membre de R3, joignable par message entre la 20e et la 30e minute de R4. Sans réponse en 5 min, R4 délègue quand même et écrit « relu par un seul membre » dans `prompts.md` §1 et dans `ETAT_PROJET.md`.
- Écrire le prompt final dans `Groupe_01_Cas_01/prompts.md` §1 et le commiter **avant** la délégation (dans Git Bash) ; c'est ce texte, et lui seul, qui est collé :

  ```bash
  git add Groupe_01_Cas_01/prompts.md && git commit -m "docs(r4): prompt RMTCEV final, avant délégation"
  ```

## Tâche 2 : exécuter la délégation (une seule fois)

1. **Ouvrir une session vierge** (D-09) : de préférence une IA web dans une conversation temporaire (ou nouvelle), mémoire et instructions personnalisées du compte désactivées, hors de tout Projet, Gem ou GPT personnalisé, sans autre pièce jointe que le prompt.
   - En ligne de commande, uniquement `claude --safe-mode` lancé dans un **dossier temporaire vide**, hors du dépôt (il désactive CLAUDE.md, règles, skills, plugins et hooks). Codex, Gemini CLI ou Antigravity CLI seulement si aucun fichier d'instructions global n'existe (`~/.codex/AGENTS.md`, `~/.gemini/GEMINI.md`).
   - Raison : une CLI ouverte dans un dossier vide charge quand même les instructions globales de l'utilisateur (`~/.claude/CLAUDE.md`, `~/.claude/rules/`, `~/.codex/AGENTS.md`).
2. Noter dans `prompts.md` §1, sous le prompt et sans en modifier le texte, **l'outil, le modèle, la date, l'heure et le mode exact de la session**.
3. Coller le prompt RMTCEV **exactement** tel qu'il figure dans `prompts.md` §1, commité à la tâche 1 : c'est ce texte, et lui seul, qui est collé, sans retouche.
   - Si l'IA pose une question au lieu de livrer, répondre uniquement « Applique les hypothèses du cahier des charges et livre le fichier complet. » et consigner l'échange dans `prompts.md` §1.
4. **Conserver la réponse brute complète** dans `travail/brut/delegation_reponse_brute.md`, par copier-coller intégral.
5. Extraire le bloc HTML **tel quel** dans `Groupe_01_Cas_01/prototype/version_IA.html` (Bloc-notes ou éditeur sans formatage au collage ni à l'enregistrement). Ne rien reformater, ne rien corriger, ne rien ajouter.
   - **Réponse tronquée** : demander « continue » dans la même session, concaténer les morceaux sans rien modifier, et le noter dans `prompts.md`.
   - **Plusieurs fichiers** (HTML, CSS et JS séparés) : enregistrer le HTML comme `version_IA.html`, garder le reste dans `travail/brut/` et consigner l'écart (E-xx) contre C-10.
   - **CLI qui écrit elle-même le fichier** : le copier tel quel vers `version_IA.html` et garder la transcription dans `travail/brut/`.
   - **Contrôle d'extraction, avant le commit** : copier le bloc HTML de la réponse brute (ou le fichier écrit par la CLI) dans un fichier temporaire hors du dépôt, puis lancer dans Git Bash `git diff --no-index --ignore-cr-at-eol <fichier temporaire> Groupe_01_Cas_01/prototype/version_IA.html`. La sortie doit être vide ; sinon, refaire l'extraction avant de commiter.
6. **Commiter immédiatement**, avant même d'ouvrir le fichier dans un navigateur (dans Git Bash) :

   ```bash
   git add Groupe_01_Cas_01/prototype/version_IA.html Groupe_01_Cas_01/prompts.md travail/brut/ && git commit -m "feat(proto): version_IA brute produite par <outil/modèle>" && git tag -a version-ia -m "version_IA brute (C-09)" && git push origin main --follow-tags
   git show version-ia --stat
   git ls-remote --tags origin
   ```

   `version_IA.html` doit figurer dans la liste de `git show`, et `version-ia` dans la sortie de `git ls-remote`. Le tag est **annoté** (`git tag -a`) : un tag léger n'est pas envoyé par `--follow-tags`.

7. **Ne plus jamais toucher `version_IA.html`** (RG-08). Les défauts constatés vont dans `travail/journal_ecarts.md`.

## Tâche 3 : `prompts.md`, première version

Dans `Groupe_01_Cas_01/prompts.md`, compléter la section 1 et créer les sections 2 à 4 :

- la section 1, **Prompt de délégation (RMTCEV)**, déjà commitée avant la délégation avec le texte exact envoyé : vérifier qu'y figurent l'outil, le modèle, la date, l'heure, le mode exact de la session vierge et la relecture ;
- une section 2, **Autres prompts importants**, à compléter par R6 depuis `travail/journal_prompts.md` ;
- une section 3, **Propositions de l'IA corrigées ou rejetées**, à compléter par R5 et R6 ;
- une section 4, **Écarts par rapport à la demande du client**, par exemple des données intégrées. Écrire « aucun » si c'est le cas.

## Tâche 4 : plan de test et fixtures (si le temps le permet, sinon à transmettre à R5)

- `tests/plan_de_test.md` : une ligne par CA du Sprint 01, avec la procédure pas à pas, les données (fichier), le **résultat attendu (oracle)** et le nom de la capture.
- `tests/fixtures/` : les fichiers **fictifs** f01 à f05 décrits dans `docs/oracle.md` §8. Compléter dans l'oracle le résultat attendu de chacun, **calculé à la main ou par script, jamais par l'IA testée**.
- Pour f05 : un même mois contient des litres `0.1` et `0.2` écrits avec un point décimal, comme dans le CSV original (jamais de décimale à virgule dans le contenu d'un CSV ; la virgule n'apparaît qu'à l'affichage, Q-01). Vérifier par script que la somme brute présente un artefact de flottant (par exemple 0.30000000000000004) ; attendu à l'écran : valeur arrondie à 1 décimale.

## Procédure (1 h)

| Temps | Étape |
|---|---|
| 0 à 10 min | Démarrage, audit A1 à A5, décision D-10 |
| 10 à 30 min | Rédaction du prompt RMTCEV avec l'IA assistante ; **relecture par le membre de R3** (entre la 20e et la 30e minute, par message) ; prompt final écrit et commité dans `prompts.md` §1 |
| 30 à 40 min | Délégation en session vierge, sauvegarde brute, contrôle d'extraction, commit, tag annoté `version-ia` et push |
| 40 à 50 min | `prompts.md` v1 (sections 1 à 4) ; plan de test et fixtures (ou transmission à R5) |
| 50 à 60 min | Passation : dire « fin de notre relais » (`AGENTS.md` §9) |

## Checklist de sortie (DoD)

- [ ] Le prompt RMTCEV comporte les 6 parties, le CDC intégral et le Sprint 01 intégral avec ses CA ; il a été relu par le membre de R3 (sinon « relu par un seul membre » est noté) et commité dans `prompts.md` §1 **avant** la délégation.
- [ ] Exécution unique, en session vierge ; outil, modèle, date, heure et mode exact de la session notés dans `prompts.md` §1.
- [ ] `version_IA.html` identique au bloc HTML de la réponse brute (contrôle `git diff --no-index` vide), commité **avant** tout test, avec le tag annoté `version-ia` visible dans `git ls-remote --tags origin` ; réponse brute dans `travail/brut/`.
- [ ] `prompts.md` v1 complété ; le prompt RMTCEV ne figure que dans `prompts.md` §1 (pas en JP-xx) ; les prompts d'aide à la rédaction adressés à l'IA assistante sont consignés en JP-xx.
- [ ] Plan de test et fixtures créés, ou mentionnés comme reste à faire pour R5.

## Interdits

- Relancer la délégation pour obtenir un meilleur résultat et garder la meilleure version. C-09 exige **la première**. Si une relance est vraiment inévitable (réponse vide ou refus), la documenter dans `prompts.md`.
- Corriger `version_IA.html`, même une faute de frappe.
- Utiliser des données réelles dans le prompt.

## À écrire dans `ETAT_PROJET.md` à la passation

- Outil, modèle et mode exact de la session de délégation.
- Relecture du prompt : nom du relecteur, ou « relu par un seul membre ».
- Hash du commit `version-ia`.
- Premiers défauts visibles (sans les corriger).
- État du plan de test et des fixtures.
- La mission de R5.

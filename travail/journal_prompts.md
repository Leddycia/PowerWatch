# Journal des prompts (JP-xx)

> **But** : garder les prompts **significatifs** au fil des relais (RG-11). R6 en choisira 2 ou 3 pour `prompts.md` §2 (C-08).
> On consigne le texte **exact** envoyé, sans le corriger. Les données doivent être fictives (C-13).
> Le prompt de délégation RMTCEV n'est pas ici : il va directement dans `Groupe_01_Cas_01/prompts.md` §1 (R4).

## Modèle d'entrée

```markdown
### JP-xx : <titre court>
- Relais / membre : RX / <prénom>
- Outil et modèle : <ex. Claude Code, Claude Opus 5.5 | ChatGPT, GPT-x | Antigravity CLI ou Gemini CLI, Gemini x>
- Date et heure : AAAA-MM-JJ HH:MM
- Prompt (texte exact) :
  > …
- Ce qu'il a produit : <fichiers, sections>
- Ce que l'humain a vérifié ou corrigé : …
- Candidat pour prompts.md ? oui / non (pourquoi)
```

---

### JP-01 : Analyse et cadrage initial

- **Relais / membre** : R1 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, heure non notée
- **Prompt (texte exact)** :
  > Lis les docs car on va faire le projet powerwatch. Analyse minutieusement tout ca. Nous allons construire des md d'agents egalement au cas ou les autres membres travaillent avec gemini ou codex. Planifie tout ca mais ne code encore rien. Tout doit d'abord etre parfaitement cadrer
- **Ce qu'il a produit** :
  - `PLAN_CADRAGE.md` v0 : synthèse C-xx et B-xx, oracle calculé sur le CSV, pièges P-01 à P-10, questions Q et H, ébauche du backlog, plan des fichiers d'agents ;
  - quatre questions de cadrage posées à l'équipe : taille du groupe, RMTCEV, organisation des fichiers d'agents, organisation du dépôt.
- **Ce que l'humain a vérifié ou corrigé** : l'équipe a répondu aux 4 questions. L'organisation en relais (JP-02) a modifié le plan.
- **Candidat pour `prompts.md`** : oui. C'est le prompt qui a produit l'essentiel du cadrage.

### JP-02 : Organisation en relais (réponse aux questions de cadrage)

- **Relais / membre** : R1 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, heure non notée
- **Prompt (texte exact, réponse à la question « taille du groupe »)** :
  > 6 personnes mais chaque personne aura 1h sur le projet.
  > N ap pull repository an, n ap bay IA n ap use la tout docs yo, n ap cadrer l epi n ap di l analyser repository an avant tout puis pou l continuer / améliorer sa ki gentan existant an sans li pa ale au delà de consignes yo.
  > N ap minutieux epi n ap assurer nou que kou n fini, nou di sa sous groupe la epi lòt moun nan ap pran la main
  > N ap travay en fonction de sa moun avan an gentan fè yo.
  > Konsa nou chak ap tou fon audit de sak gentan fèt yo
- **Autres réponses** : RMTCEV = « Hypothèse OK » ; fichiers d'agents = « Source unique » ; dépôt = « Espace + sous-dossier ».
- **Ce qu'il a produit** : `PLAN_CADRAGE.md` v1 avec le Sprint 01 à 3 US, l'organisation en relais 6 × 1 h, les protocoles de démarrage et de passation, et les règles anti-dérive.
- **Ce que l'humain a vérifié ou corrigé** : l'équipe a validé le Sprint 01 à 3 US et l'organisation en relais (D-01, D-05).
- **Candidat pour `prompts.md`** : oui. Il montre comment l'équipe a cadré le travail de l'IA (audit avant action, pas de dépassement des consignes). S'il est retenu, citer le texte créole exact, suivi de sa traduction française (H-03).

### JP-03 : Production du socle R1

- **Relais / membre** : R1 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, heure non notée
- **Prompt (texte exact)** :
  > Oui, rédige le socle de R1 : decisions.md, transcriptions B-xx/C-xx, oracle.md, AGENTS.md, CLAUDE.md, GEMINI.md, les 6 fiches agents/ et ETAT_PROJET.md. Groupe numéro : à préciser.
- **Ce qu'il a produit** : `travail/decisions.md`, `docs/brief_client.md`, `docs/consignes.md`, `docs/oracle.md`, `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `agents/01` à `06`, `ETAT_PROJET.md` et les journaux.
- **Ce que l'humain a vérifié ou corrigé** : relecture adversariale automatisée du socle (JP-04), puis corrections validées par Leddycia (JP-05) ; audit de R2 à venir (fidélité des transcriptions, recalcul manuel de l'oracle).
- **Candidat pour `prompts.md`** : possible.

### JP-04 : Relecture adversariale du socle

- **Relais / membre** : R1 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, heure non notée
- **Prompt (texte exact)** :
  > Je relis d'abord les fichiers du socle avant le commit.
- **Ce qu'il a produit** : relecture adversariale automatisée de 18 agents : 142 constats (131 des 8 relecteurs et 11 de la critique de complétude), dont 103 confirmés après tentative de réfutation et 39 réfutés.
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a décidé de l'application des constats confirmés (JP-05).
- **Candidat pour `prompts.md`** : oui. Il a déclenché la vérification du travail de l'IA (C-18) ; les erreurs trouvées alimentent `prompts.md` §3 (E-01 à E-12).

### JP-05 : Validation et application des corrections

- **Relais / membre** : R1 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, heure non notée
- **Prompt (texte exact)** :
  > Oui, applique toutes les corrections confirmées avec tes recommandations : je valide D-06 à D-09 et H-01 à H-06, retire CA-01.02/Q-08, corrige la mention de l'oracle, et consigne les erreurs de l'IA R1 dans journal_ecarts.md. Je passe moi-même le dépôt en privé.
- **Ce qu'il a produit** : application des corrections aux fichiers du socle ; écarts E-01 à E-12 dans `travail/journal_ecarts.md` ; décision D-12 (dépôt privé, ensuite remplacée par JP-07 : dépôt laissé public).
- **Ce que l'humain a vérifié ou corrigé** : validation de D-06 à D-09 et H-01 à H-06 ; retrait du CA « 36 jours chargés » (Q-08 passe à « Non en V1 ») ; mention honnête de l'oracle ; passage du dépôt en privé pris en charge par Leddycia (D-12, O-8), finalement abandonné (JP-07). Les corrections appliquées restent à relire avant le commit, puis à l'audit de R2.
- **Candidat pour `prompts.md`** : possible. Il montre l'arbitrage humain sur les propositions de l'IA (C-18).

### JP-06 : Numéro du groupe

- **Relais / membre** : R1 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, heure non notée
- **Prompt (texte exact)** :
  > C'est le Groupe_01
- **Ce qu'il a produit** : D-11 validée ; numéro 01 appliqué au socle (livrable `Groupe_01_Cas_01/`, dossier Drive `Groupe_01/`).
- **Ce que l'humain a vérifié ou corrigé** : numéro confirmé par l'équipe (D-11).
- **Candidat pour `prompts.md`** : non. Simple information d'organisation, sans production significative.

### JP-07 : Visibilité du dépôt

- **Relais / membre** : R1 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, heure non notée
- **Prompt (texte exact)** :
  > Je garde le dépôt public en connaissance de cause : marque O-8 comme « dépôt laissé public, décision de Leddycia », mets D-12 à jour, puis commite, tague relais-1 et pousse avec contrôle ls-remote.
- **Ce qu'il a produit** : D-12 mise à jour (dépôt laissé public), O-8 résolu, commit du socle R1, tag annoté `relais-1`, push et contrôle `git ls-remote`.
- **Ce que l'humain a vérifié ou corrigé** : l'IA a d'abord vérifié la visibilité (accès anonyme : dépôt toujours public) et a refusé de pousser tant que la décision n'était pas prise ; Leddycia a tranché.
- **Candidat pour `prompts.md`** : non. Décision d'organisation.

### JP-08 : Remise par Leddycia, invitations et protocole « fin de notre relais »

- **Relais / membre** : R1 (complément) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, vers 10:40
- **Prompt (texte exact)** :
  > On continue.
  >
  > Je me chargerai moi-meme de televerser les elements sur le drive.
  >
  > J'ai envoye les invitations.
  >
  > Fait en sorte que etat_projet.md se mets a jour quand la personne en question travaille. On aura qu'a dire fin de notre relais pour que tout se met a jour
- **Ce qu'il a produit** : `agents/00_protocole_relais.md` (phrases de commande, journal de bord, passation complète, variante IA web) ; branchement dans `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `ETAT_PROJET.md` (§8) et les fiches ; décisions D-13 et D-14 ; O-3 et O-7 mis à jour.
- **Ce que l'humain a vérifié ou corrigé** : le plan a été déduit de ce prompt et exécuté sans validation explicite préalable ; Leddycia a ensuite demandé la clôture (JP-09), ce qui vaut acceptation du travail réalisé. Relecture détaillée du protocole par un membre : non consignée, à faire par R2 lors de son audit.
- **Candidat pour `prompts.md`** : possible. Il montre comment l'équipe a organisé le travail assisté par l'IA en relais.

### JP-09 : Clôture du complément de R1

- **Relais / membre** : R1 (complément) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, 11:37
- **Prompt (texte exact)** :
  > fin de notre relais
- **Ce qu'il a produit** : première exécution réelle de la passation automatique (`agents/00_protocole_relais.md` §4) : journaux, `travail/audits/R1_audit.md`, ETAT §1 à §8, commit et push sans tag (complément : `relais-1` existait déjà), message de passation.
- **Ce que l'humain a vérifié ou corrigé** : à faire (relecture du compte rendu et du message avant envoi).
- **Candidat pour `prompts.md`** : possible. Il illustre la passation automatisée du travail en relais.

### JP-10 : Démarrage du relais R2

- **Relais / membre** : R2 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, 10:49
- **Prompt (texte exact)** :
  > Pendant que l'autre session travaille, passe au relais 2
- **Ce qu'il a produit** : protocole de démarrage (`AGENTS.md` §0) : lecture d'ETAT, du protocole et de la fiche 01 ; audit A1 à A5 en lecture seule (diffs `.docx` et PDF contre les transcriptions, empreinte du CSV, cohérence des décisions, état Git) ; rapport d'audit et plan présentés sans rien écrire. Constat bloquant : le complément de R1 n'était pas clôturé (session R1 encore active dans le même dossier).
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a validé le plan (JP-11).
- **Candidat pour `prompts.md`** : non. Démarrage de relais.

### JP-11 : Validation du plan et rédaction du cahier des charges

- **Relais / membre** : R2 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5 ; rédaction confiée à un workflow Claude Code de 9 agents (même modèle)
- **Date et heure** : 2026-10-18, 10:56
- **Prompt (texte exact)** :
  > Plan validé. Commence le brouillon du CDC hors dépôt ; je fais le contrôle mot à mot et le recalcul d'août et septembre.
- **Instructions transmises aux agents de rédaction** (rédigées par l'IA assistante de R2 à partir de la fiche 01 et des arbitrages validés ; texte exact, sans le bloc de contexte commun ni les angles de rédaction et de vérification) :
  > Arbitrages validés par l'humain du relais (audit R2, constat 9), qui corrigent la liste indicative de la fiche 01 :
  > 1. EF-01 (charger le fichier) cite B-06 (B-05b pour l'acteur) ; le libellé exact « Choisir un fichier » et le fait de ne pas intégrer les données viennent des consignes : contrainte du projet CT (C-12, lecture retenue D-06), pas EF.
  > 2. B-14 et B-15 sont des règles du client (rubrique « Les règles à respecter ») : seulement en RM (RM-03, RM-04), pas en ENF. Les ENF couvrent les contraintes du client B-16 et B-17 (rubrique « Nos contraintes »), B-27 pouvant appuyer ENF-02.
  > 3. Le comportement en cas de fichier invalide (Q-04) n'est pas une exigence : il reste uniquement au §11, sous la forme « À confirmer … (hypothèse provisoire : …) ».
  > 4. Aucune valeur de l'oracle dans le CDC : les valeurs attendues chiffrées iront dans les critères d'acceptation du backlog (R3).
  >
  > Rédige le contenu complet du futur fichier Groupe_01_Cas_01/cahier_des_charges.md (markdown), selon la structure exacte de agents/01_analyste_cdc.md : titre « # Cahier des charges : PowerWatch (Collège Les Palmistes) », sections 1 à 12 et 10 bis, avec les intitulés de la fiche (sans les étoiles ni les commentaires entre parenthèses de la fiche).
  > Exigences de fond :
  > - En tête, un court encadré : objet du document, sources (brief = B-xx, consignes = C-xx, decisions.md = D/Q/H), version et date 2026-10-18, relais R2.
  > - Chaque EF, ENF et RM est une phrase testable avec « doit », une seule capacité, et cite au moins un B-xx exact qui la justifie ; chaque CT cite son C-xx et porte la mention « contrainte du projet ».
  > - Tables EF et ENF : ID | exigence | source | priorité du client (rang 1 à 4 uniquement s'il découle d'un B-20.x, en citant ce B-20.x ; sinon une mention exacte comme « non classée par le client » ou « contrainte du client »).
  > - RM-01 = B-12, RM-02 = B-13, RM-03 = B-14, RM-04 = B-15, fidèles au texte du client (ne pas durcir « les litres peuvent avoir une décimale » en règle : le format exact est l'hypothèse Q-01).
  > - Aucune solution technique (décrire quoi, pas comment) ; seuls les CT du §7 peuvent reprendre les termes des consignes qu'ils citent.
  > - §8 Données d'entrée : uniquement ce que disent B-18 et B-19 (table des colonnes reprise).
  > - §9 Périmètre de la V1 : B-06 à B-11 et B-20.1 à B-20.4 (ordre de priorité du client), renvoi aux EF ; pas de sprint, pas de user story.
  > - §10 Hors périmètre : B-25 à B-27 recopiés mot pour mot, entre guillemets, avec leur identifiant ; préciser que ce sont des décisions du client (C-03).
  > - §10 bis Souhaits ultérieurs : B-21 à B-24 mot pour mot, « non tranchés par le client (C-04) », classement, justification et compatibilité renvoyés au product backlog (D-08) ; signaler les points dépendants (Q-11 à Q-14) ; pour B-24, on peut rappeler la décision d'équipe D-08 en la présentant comme une décision de l'équipe, pas du client.
  > - §11 Points à confirmer ou à décider : toutes les Q-01 à Q-14, chacune sous la forme « À confirmer : <question> (hypothèse provisoire : <hypothèse de decisions.md>) » ou, pour les Q au statut ouvert, « (aucune hypothèse : <conséquence de decisions.md>) », avec le statut et l'élément concerné ; puis une sous-section distincte « Choix de présentation de l'équipe » pour H-01 à H-06, présentés comme des choix de l'équipe à soumettre au client, non comme des demandes du client ; puis D-10 si utile, en une ligne. Si tu repères un point que le client n'a pas fixé et qu'aucune Q ne couvre, ne l'ajoute pas au CDC : liste-le dans nouvelles_questions.
  > - §12 Matrice de traçabilité : une ligne par élément du brief, de B-01 à B-27 (B-05a, B-05b, B-05c et B-20.1 à B-20.4 compris), vers les sections et identifiants qui le couvrent ; chaque B-06 à B-17 renvoie à au moins une EF, ENF ou RM ; une seconde table C-xx vers CT ; termine par la liste des B-xx qui ne sont couverts par aucune exigence, avec la raison (contexte, hors périmètre, souhait ultérieur).
  > - Pas de user stories, pas de MoSCoW, pas de critères d'acceptation (rôle de R3).
  > Rends : markdown (le fichier complet), nouvelles_questions, ecarts_fiche (chaque point où tu t'écartes de la liste indicative ou de la structure de la fiche, avec la raison).
- **Ce qu'il a produit** : deux brouillons indépendants (angle « fidélité au texte du client » et angle « lecteur IA déléguée »), une synthèse, cinq vérifications adverses (traçabilité, invention et périmètre, fidélité textuelle, DoD et structure, lecteur IA déléguée : 35 constats), une correction (29 constats appliqués, 6 rejetés avec leur raison). Résultat : `Groupe_01_Cas_01/cahier_des_charges.md` v1, contrôlé ensuite par script (citations, chiffres, termes techniques, tableaux, couverture).
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a retenu Q-15 à Q-17 parmi les points relevés (JP-13) ; sa relecture mot à mot du brouillon reste à confirmer. L'IA assistante a retiré une mention qu'elle avait elle-même introduite dans ses instructions (E-19).
- **Candidat pour `prompts.md`** : **oui**. Prompt qui a produit le cahier des charges, avec la vérification adverse de l'IA par l'IA (C-08, C-18).

### JP-12 : Contre-vérification A3 remplacée par un recalcul automatique

- **Relais / membre** : R2 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, entre 11:00 et 11:04
- **Prompt (texte exact)**, en trois messages :
  > Je n'ai pas de chiffres a ajouter. Le CSV recu n'est que les elements donnees
  >
  > Je ne fais pas de recalcul. Assure-toi que le calcul est le bon
  >
  > Oui : consigne D-15 dans decisions.md et mets les deux scripts en annexe de R2_audit.md, au moment d'écrire dans le dépôt.
- **Ce qu'il a produit** : explication de l'étape A3 (lignes brutes d'août et de septembre affichées, sans aucun total) ; trois recalculs indépendants (Python, awk, PowerShell) et comparaison automatique avec l'oracle §1 à §6 : aucun écart ; décision D-15 ; scripts en annexe de `travail/audits/R2_audit.md`.
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a refusé le recalcul à la main ; la limite (contrôle non humain, même outil que R1) est écrite dans D-15.
- **Candidat pour `prompts.md`** : non. Décision de méthode.

### JP-13 : Nouvelles questions au client Q-15 à Q-17

- **Relais / membre** : R2 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, 11:39
- **Prompt (texte exact)** :
  > Ajoute Q-15, Q-16 et Q-17 avec les hypothèses provisoires proposées ; renvoie les 12 autres points à R3 et R4 dans l'audit.
- **Ce qu'il a produit** : Q-15 (périmètre du tableau jour par jour), Q-16 (format des heures) et Q-17 (affichage du jour maximal) dans `travail/decisions.md` et dans le CDC (§4, §6, §11.1, §12.1) ; 12 points renvoyés à R3 et R4 dans `travail/audits/R2_audit.md`.
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a choisi les 3 questions parmi 15 relevées par les vérificateurs, avec les hypothèses proposées par l'IA.
- **Candidat pour `prompts.md`** : non.

### JP-14 : Clôture du relais R2

- **Relais / membre** : R2 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, 11:46
- **Prompt (texte exact)** :
  > fin de notre relais
- **Ce qu'il a produit** : passation complète (`agents/00_protocole_relais.md` §4) : journaux, `travail/audits/R2_audit.md`, ETAT §1 à §8, commit, tag annoté `relais-2`, push, message de passation. Prénom du membre de R3 demandé au membre (réponse : Leddycia).
- **Ce que l'humain a vérifié ou corrigé** : à faire (relecture du compte rendu et du message avant envoi).
- **Candidat pour `prompts.md`** : non.

### JP-15 : Démarrage du relais R3

- **Relais / membre** : R3 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5 ; prompt transmis par une autre session Claude Code de Leddycia, qui a ouvert la session R3
- **Date et heure** : 2026-10-18, 11:51
- **Prompt (texte exact)** :
  > Tu es l'IA assistante du relais R3 du projet PowerWatch (cas 01).
  > 0. D'abord : git fetch --tags origin, git status -sb (doit afficher ## main...origin/main sans rien d'autre ; sinon git pull --no-rebase --no-edit si l'arbre est propre), git tag -l (relais-1 et relais-2 doivent apparaître). Cite ensuite mot pour mot la règle RG-08 d'AGENTS.md.
  > 1. Lis AGENTS.md en entier, puis ETAT_PROJET.md, agents/00_protocole_relais.md, la fiche agents/02_product_owner.md et ses fichiers d'entrée. Tiens ETAT_PROJET.md à jour selon le protocole ; à « fin de notre relais », fais la passation complète.
  > 2. Analyse l'état actuel du dépôt (fichiers, contenu, derniers commits).
  > 3. Audite le travail du relais précédent avec la checklist d'audit de ma fiche.
  > 4. Présente-moi : (a) ton rapport d'audit (constat, preuve, gravité, action proposée), (b) ton plan pour mon heure de travail.
  > Ne modifie aucun fichier avant ma validation. Ne va jamais au-delà des consignes (docs/consignes.md) ni du brief (docs/brief_client.md) ; tout point non fixé par le client devient une question Q-xx.
- **Ce qu'il a produit** : synchronisation (`## main...origin/main`, tags `relais-1` et `relais-2`), citation de RG-08, audit A1 à A6 du cahier des charges en lecture seule (script hors du dépôt : citations, sources, termes techniques, Q-xx, matrice), rapport de 19 constats et plan, sans écriture dans le dépôt. Propositions : Q-18 à Q-20, ajout ciblé au CDC, CA-02.04 et CA-03.04.
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a validé l'audit, le plan et les trois hypothèses (JP-16).
- **Candidat pour `prompts.md`** : non. Prompt d'amorçage standard (`AGENTS.md` §14).

### JP-16 : Validation du plan de R3 et des questions Q-18 à Q-20

- **Relais / membre** : R3 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, 11:55
- **Prompt (texte exact)** :
  > Je valide l'audit, le plan, Q-18, Q-19 et Q-20, ainsi que l'ajout ciblé au CDC §11.1. Mon outil : Claude Code (application de bureau, Claude Opus 5.5). Je fais la relecture mot à mot pendant que tu rédiges.
- **Ce qu'il a produit** : R3 EN COURS (ETAT §1, §2, §8) ; `travail/audits/R3_audit.md` ; Q-18 à Q-20 dans `travail/decisions.md` et dans le cahier des charges ; rédaction de `Groupe_01_Cas_01/product_backlog.md`.
- **Ce que l'humain a vérifié ou corrigé** : relecture humaine mot à mot du cahier des charges par Leddycia, pendant la rédaction (résultat : conforme, JP-17).
- **Candidat pour `prompts.md`** : non.

### JP-17 : Clôture du relais R3

- **Relais / membre** : R3 / Leddycia
- **Outil et modèle** : Claude Code (application de bureau), Claude Opus 5.5
- **Date et heure** : 2026-10-18, 12:03
- **Prompt (texte exact)**, puis réponse à la question de l'IA sur le membre de R4 :
  > Relecture du backlog faite, rien à changer. Relecture mot à mot du CDC : conforme. fin de notre relais
  >
  > Bradley. Il va utiliser Antigravity (gemini).
- **Ce qu'il a produit** : passation complète (`agents/00_protocole_relais.md` §4) : journaux, `travail/audits/R3_audit.md`, ETAT §1 à §8, commit, tag annoté `relais-3`, push, message de passation ; membre de R4 inscrit au §2.
- **Ce que l'humain a vérifié ou corrigé** : relecture du product backlog (aucune correction) et relecture mot à mot du cahier des charges contre le brief (conforme) ; compte rendu et message de passation à relire avant envoi.
- **Candidat pour `prompts.md`** : non.

### JP-18 : Démarrage et validation du plan du relais R4

- **Relais / membre** : R4 / Bradley
- **Outil et modèle** : Antigravity (Gemini 3.8 Flash High)
- **Date et heure** : 2026-10-18, 12:49
- **Prompt (texte exact)** :
  > vas y
- **Ce qu'il a produit** : Validation du rapport d'audit A1 à A5 et du plan de travail pour le relais R4 ; passage de R4 à EN COURS dans `ETAT_PROJET.md` (§1, §2, §8) ; création de `travail/audits/R4_audit.md` ; validation de D-10, confirmation de Q-01 (point O-9 résolu) et précision de Q-10 (point O-10 #10) dans `travail/decisions.md`.
- **Ce que l'humain a vérifié ou corrigé** : Validation explicite du plan et des arbitrages par Bradley.
- **Candidat pour `prompts.md`** : non.

### JP-19 : Relecture croisée et validation du prompt RMTCEV

- **Relais / membre** : R4 / Bradley (avec Leddycia, membre de R3)
- **Outil et modèle** : Antigravity (Gemini 3.8 Flash High)
- **Date et heure** : 2026-10-18, 13:03
- **Prompt (texte exact)** :
  > c'est valide
- **Ce qu'il a produit** : Validation de la relecture croisée du prompt RMTCEV final contenu dans `Groupe_01_Cas_01/prompts.md` §1 (C-08) ; mise à jour de la mention de relecture préalable dans `prompts.md` §1.1 et dans `ETAT_PROJET.md` §8.
- **Ce que l'humain a vérifié ou corrigé** : Relecture humaine du texte complet du prompt (CDC intégral, Sprint 01 et CA, format RMTCEV).
- **Candidat pour `prompts.md`** : non.



### JP-20 : Démarrage du relais R5 (message de passation de R4)

- **Relais / membre** : R5 / Louis
- **Outil et modèle** : Claude Code (Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 14:00
- **Prompt (texte exact)** : message de passation de R4 collé tel quel (« Relais R4 terminé (porte G4 : atteinte). […] git pull puis lis ETAT_PROJET.md (§6 : ta mission). »)
- **Ce qu'il a produit** : protocole de démarrage (`AGENTS.md` §0) ; audit d'entrée A1 à A4 et pré-test de `version_IA.html` sous Chromium headless (fuseau America/Port-au-Prince), sans écriture dans le dépôt ; plan en 7 étapes.
- **Ce que l'humain a vérifié ou corrigé** : lecture du rapport d'audit et du plan.
- **Candidat pour `prompts.md`** : non.

### JP-21 : Validation du plan de R5

- **Relais / membre** : R5 / Louis
- **Outil et modèle** : Claude Code (Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 14:04
- **Prompt (texte exact)** :
  > Oui je suis Louis. Oui
- **Ce qu'il a produit** : confirmation du membre et de l'outil ; validation du plan, y compris les captures manuelles par Louis (liste déroulante, hors ligne, fuseau, empreinte) ; R5 marqué EN COURS.
- **Ce que l'humain a vérifié ou corrigé** : plan accepté sans modification.
- **Candidat pour `prompts.md`** : non.

### JP-22 : Captures manuelles de R5 dans Firefox

- **Relais / membre** : R5 / Louis
- **Outil et modèle** : Claude Code (Claude Opus 5.5)
- **Date et heure** : 2026-10-18, de 14:13 à 14:31
- **Prompt (texte exact)** : « je ne vois rien pour les captures » (avec une capture de l'état initial), puis « le reseau es coupe » (avec une capture), puis trois photos de l'écran envoyées sans texte.
- **Ce qu'il a produit** : CA-01.01, CA-01.03, CA-01.08 et CA-01.10 vus à l'écran par Louis dans Firefox, réseau réellement coupé (sauf CA-01.08, réseau rétabli) ; captures enregistrées sous les noms du plan de test (photo de CA-01.08 redressée par `ffmpeg`), plus `US01_CA02_firefox_toute_periode.png` (second navigateur) ; statuts passés de « à confirmer » à « respecté ».
- **Ce que l'humain a vérifié ou corrigé** : valeurs lues à l'écran (4 choix ; 3 choix et 54 h, 155,0 L avec f06 ; 97 h, 280,0 L, 84 000 gourdes, 06/08/2026 (5 h) ; empreinte `320155c7…a84b`).
- **Candidat pour `prompts.md`** : non.

### JP-23 : Clôture du relais R5

- **Relais / membre** : R5 / Louis
- **Outil et modèle** : Claude Code (Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 14:35
- **Prompt (texte exact)** :
  > fin de notre relais. le nom est Petiote
- **Ce qu'il a produit** : passation complète (`agents/00_protocole_relais.md` §4) : ETAT §1 à §8, `travail/audits/R5_audit.md`, commit, tag annoté `relais-5`, push ; Petiote inscrite comme membre de R6.
- **Ce que l'humain a vérifié ou corrigé** : prénom du membre de R6 fourni.
- **Candidat pour `prompts.md`** : non.

### JP-24 : Complément de R5, corrections avant le démarrage de R6

- **Relais / membre** : R5 (complément, après le tag `relais-5`) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 15:03
- **Prompt (texte exact)** :
  > Corrige tous les points en prenant le soin de faire un triple check a chaque etape si aucun pull pour le relais suivant n'a encore ete effectue
- **Contexte** : ce prompt suit, dans la même session, une relecture du dépôt après le push de R5 demandée par Leddycia (texte exact : « R5 a ete push. Verifie »), qui a relevé les points corrigés ici (`travail/audits/R5_audit.md`, section « Complément »).
- **Ce qu'il a produit** : complément de R5 : Q-01 remise à « provisoire » (E-23) ; f01 refait avec des égalités dans un ordre non chronologique et oracle §8 mis à jour (E-24) ; 4 captures de CA-03.02 refaites ; données personnelles masquées dans 4 captures manuelles (E-25) ; affichage des blocs de `prompts.md` réparé sans toucher au texte du prompt (E-26) ; chaque étape contrôlée trois fois (journal de bord du complément : `travail/audits/R5_audit.md`, section « Complément »).
- **Ce que l'humain a vérifié ou corrigé** : avant toute écriture, Leddycia a confirmé (15:07) que R6 n'avait pas encore fait de `git pull` et que le complément est fait à son nom.
- **Candidat pour `prompts.md`** : non.

### JP-25 : Clôture du complément de R5

- **Relais / membre** : R5 (complément) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 15:16
- **Prompt (texte exact)** :
  > fin de notre relais
- **Ce qu'il a produit** : clôture du complément (`agents/00_protocole_relais.md` §4, règle « Complément ») : `R5_audit.md` complété, ETAT §1 à §7 (R5 « complément FAIT », nouvelle entrée au §7, mission de R6 précisée), §8 vidé ; relecture indépendante avant le commit (vérificateurs en lecture seule, chacun avec un angle différent) ; commit et push sans tag (`relais-5` est déjà posé).
- **Ce que l'humain a vérifié ou corrigé** : compte rendu et message de passation à relire avant envoi.
- **Candidat pour `prompts.md`** : non.

### JP-26 : Complément de R4, quatre points mineurs avant le démarrage de R6

- **Relais / membre** : R4 (complément, après le tag `relais-4`) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 15:57
- **Prompt (texte exact)** :
  > Oui, corrige les quatre points mineurs restants de R4, si R6 n'a pas encore fait de git pull.
- **Contexte** : réponse à la question « Je corrige les quatre points mineurs maintenant ? », posée après la question de Leddycia « Les corrections de R4 ont ete faits? » (15:55) et le bilan des points relevés sur R4 qui restaient à corriger. Ces points venaient de la relecture du dépôt demandée après le push de R4 (texte exact : « R4 done », 13:50).
- **Ce qu'il a produit** : complément de R4 : résumés de Q-10 corrigés après un essai réel du BOM et du `;` (E-28) ; ETAT §3, état réel de `prompts.md` (E-28) ; `tests/plan_de_test.md` §2, `index.html` seulement en cas d'écart (E-28) ; bonnes pratiques de pièges reprises dans le prompt consignées (E-27) ; journal de bord du complément (copié dans `travail/audits/R4_audit.md`, section « Complément », à la clôture).
- **Ce que l'humain a vérifié ou corrigé** : avant toute écriture, Leddycia a confirmé (15:58) que R6 n'avait pas encore fait de `git pull`.
- **Candidat pour `prompts.md`** : non.

### JP-27 : Clôture du complément de R4

- **Relais / membre** : R4 (complément) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 16:19
- **Prompt (texte exact)** :
  > fin de notre relais
- **Ce qu'il a produit** : clôture du complément (`agents/00_protocole_relais.md` §4, règle « Complément ») : `R4_audit.md` complété avec la copie du journal de bord, ETAT §1 à §7 (R4 « complément FAIT », nouvelle entrée au §7), §8 vidé ; relecture indépendante finale avant le commit ; commit et push sans tag (`relais-4` est déjà posé).
- **Ce que l'humain a vérifié ou corrigé** : compte rendu et message de passation à relire avant envoi.
- **Candidat pour `prompts.md`** : non.

### JP-28 : Habillage du prototype, logo et question sur `index.html`

- **Relais / membre** : R6 (en parallèle, pendant le relais de Petiote) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5), avec les compétences « ui-ux-pro-max » et « design »
- **Date et heure** : 2026-10-18, 16:36
- **Prompt (texte exact)** :
  > Pendant que Petiote travaille, prepare-moi un plan pour faire un design plus propre et original du systeme. Si je m'en souviens bien, c'etait preciser qu'on pouvait faire notre propre index.html non?
  >
  > use /ui-ux-pro-max /design
  > Cree un logo pour powerwatch et assure-toi que tout est en parfait francais, sans em-dash et user-friendly.
- **Ce qu'il a produit** : réponse à la question (C-09 permet `index.html`, mais la fiche 04 et le plan de test §2 le limitent : d'où D-16) ; logo PowerWatch en SVG (soleil levant lu comme un cadran, aiguille en forme d'éclair pour la génératrice) ; plan d'habillage avec maquette, tableau des textes avant et après, éléments à ne pas toucher, horaire et limite de 19 h 30 ; page de proposition privée sur claude.ai. Proposition de l'outil de design rejetée : E-32 ; icône d'onglet retirée : E-33.
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a validé le plan et prévenu Petiote avant la construction (JP-29).
- **Candidat pour `prompts.md`** : oui, pour §3 (proposition d'IA rejetée, E-32).

### JP-29 : Construction d'`index.html`

- **Relais / membre** : R6 (en parallèle) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 17:13
- **Prompt (texte exact)** :
  > Oui, construis index.html selon le plan. J'ai prévenu Petiote.
- **Ce qu'il a produit** : `Groupe_01_Cas_01/prototype/index.html`, dont le bloc `<script>` est copié à l'identique depuis `version_IA.html` ; vérification automatique complète (Chrome 155 sans interface, fuseau `America/Port-au-Prince` et réseau coupé par émulation, chargement par le vrai `<input type="file">`) : 37 contrôles, 0 non respecté ; 17 captures suffixées `_index` ; textes de traçabilité pour Petiote (D-16, E-29 à E-33, JP-28 à JP-30, README, plan de test §4). Corrections faites par l'IA en cours de route : mise en page sur téléphone (bouton et liste trop étroits à 390 px) ; capture de CA-01.06 ajoutée, car l'écran d'octobre avait été pris après Septembre et non après « Toute la période ».
- **Ce que l'humain a vérifié ou corrigé** : Leddycia a validé le commit et le push (17:35, texte exact : « Oui, commite et pousse index.html et les 17 captures _index sur main. ») ; commit `6f59584`, poussé sur `main`.
- **Candidat pour `prompts.md`** : non (prompt court ; le contenu utile est dans E-29 à E-33).

### JP-30 : Transmission des textes de traçabilité à R6

- **Relais / membre** : R6 (en parallèle) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 17:37
- **Prompt (texte exact)** :
  > Push les textes pour Petiote et indique a son agent de les prendre en compte
- **Ce qu'il a produit** : `travail/transmission_R6_index.md` (blocs à intégrer par R6 : D-16, E-29 à E-33, JP-28 à JP-30, plan de test §4, README), commité et poussé sur `main` sans toucher aux fichiers de R6 ; message envoyé à la session Claude Code ouverte dans le dépôt pour l'audit de R6.
- **Ce que l'humain a vérifié ou corrigé** : blocs non intégrés par Petiote avant son push ; intégrés à la reprise de R6 par Leddycia (JP-31), numéros inchangés (encore libres).
- **Candidat pour `prompts.md`** : non.

### JP-31 : Reprise de R6 par Leddycia

- **Relais / membre** : R6 (reprise, après le push de Petiote) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 18:36 (première heure lue après l'envoi), puis 18:40
- **Prompt (texte exact)** :
  > Petiote a push. On va continuer son relais
  >
  > Oui, je valide le plan. C'est bien moi, Leddycia, avec Claude Code (Claude Opus 5.5). Lance les étapes 1 à 4 ; je réponds aux autres questions en parallèle.
- **Contexte** : le second message répond au rapport de reprise (contrôles K1 à K12 de `travail/audits/R6_audit.md`, section « Reprise ») et au plan complété (ETAT §8), présentés sans aucune écriture. Les étapes 1 à 4 du prompt sont celles de ce plan complété, notées depuis a à d (ETAT §8), et non celles du plan validé au début du relais.
- **Ce qu'il a produit** : reprise inscrite (ETAT §2 et §8, audit R6) ; blocs 1 à 6 de `travail/transmission_R6_index.md` intégrés (D-16, E-29 à E-33, JP-28 à JP-30, plan de test) ; README, `prompts.md` et plan de test §3 corrigés (étapes c et d du plan complété).
- **Ce que l'humain a vérifié ou corrigé** : validation du plan complété ; identité et outil confirmés par Leddycia.
- **Candidat pour `prompts.md`** : non.

### JP-32 : Réponses de Leddycia pendant la reprise (O-13, éditeur, test depuis le Drive, membres)

- **Relais / membre** : R6 (reprise) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 18:44 (première heure lue après l'envoi)
- **Prompt (texte exact)** :
  > Note que Gervais et Delly vont faire des verifications completes du projet.
  > Gervais fais le test depuis le drive
  > L'editeur est antigravity
  > C'etait une nouvelle session d'apres Bradley et le bloc html, fais ce qui doit etre conforme
  >
  > Les membres du groupe
  >
  > Delly J. Jifferson
  > Gervais Carvens J. W.
  > Joseph Djamy Bradley
  > Louis Dülze Hkloë Sassie Shaikelta
  > Petiote Samuel
  > Saint-Vil Angie-Reyna Leddycia
- **Contexte** : réponses aux questions 2 à 5 du rapport de reprise (fiche de contribution, O-13, test depuis le Drive, éditeur).
- **Ce qu'il a produit** : O-13 clos dans `prompts.md` §1.1, sans modifier l'archive brute (E-34) ; éditeur « Antigravity » dans le README ; Gervais inscrit comme testeur depuis le Drive ; noms complets des 6 membres repris tels quels dans `fiche_contribution.pdf`.
- **Ce que l'humain a vérifié ou corrigé** : confirmation du membre de R4 transmise par Leddycia ; liste des membres fournie par Leddycia.
- **Candidat pour `prompts.md`** : non.

### JP-33 : Prompt d'audit complet de Gervais signalé par Leddycia

- **Relais / membre** : R6 (reprise) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 18:47 (première heure lue après l'envoi)
- **Prompt (texte exact)** :
  > Note aussi que Gervais a un master prompt pour faire la verif (voir la session prompt d'audit projet complet)
- **Contexte** : le prompt d'audit est dans une autre session Claude Code de Leddycia (« Prompt d'audit projet complet ») : une vérification en lecture seule de tout le projet, que Gervais lancera après la sauvegarde du relais, de préférence avant le téléversement sur le Drive.
- **Ce qu'il a produit** : relecture de ce prompt pour aligner les livrables sur ses contrôles (script identique dans `version_IA.html` et `index.html`, Firefox sur `index.html`, suppression de `travail/transmission_R6_index.md` à la passation, test depuis le Drive) ; README et points ouverts d'ETAT §8 complétés en conséquence.
- **Ce que l'humain a vérifié ou corrigé** : à venir : résultat de l'audit de Gervais ; les corrections qui en découlent seront consignées dans un JP suivant et dans l'audit R6.
- **Candidat pour `prompts.md`** : non (le prompt d'audit de Gervais pourra l'être, avec son résultat).

### JP-34 : Suppression voulue de trois captures du livrable

- **Relais / membre** : R6 (reprise) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 19:20, puis 19:38 (premières heures lues après chaque envoi)
- **Prompt (texte exact)** :
  > La suppression est voulue. Je t'explique pourquoi ; mets à jour le README, le plan de test et les journaux en conséquence.
  >
  > Ce sont des photos de l'écran prises de biais, pas de vraies captures : peu lisibles et peu professionnelles pour le livrable.
- **Contexte** : réponse à la question sur les trois captures de `version_IA.html` trouvées supprimées à 19:13, hors de la session de l'IA assistante (K15 de l'audit R6) ; le premier message est un bouton de réponse proposé par l'IA ; le second donne le motif, en réponse à la question de l'IA (bouton proposé, texte repris tel quel).
- **Ce qu'il a produit** : README (colonne `version_IA.html` de CA-01.03, CA-01.08 et CA-01.10, paragraphe « Trois preuves de `version_IA.html` retirées »), plan de test §3 (rectificatif et colonne « Capture »), E-35, K15 de l'audit R6, ETAT §8.
- **Ce que l'humain a vérifié ou corrigé** : décision de suppression et motif, donnés par Leddycia ; motif reporté dans E-35 et, en bref, dans le README.
- **Candidat pour `prompts.md`** : non.

### JP-35 : Prompt de mise au courant pour Gervais

- **Relais / membre** : R6 (reprise) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 19:42 (première heure lue après l'envoi)
- **Prompt (texte exact)** :
  > Cree un prompt pour que Gervais puisse etre au courant de tout ca
- **Contexte** : après la sauvegarde du relais de 19:39 ; Gervais doit lancer son prompt de contre-audit (JP-33), puis faire le test depuis le Drive.
- **Ce qu'il a produit** : page privée claude.ai « Feuille de route de Gervais » : état du projet au commit de la sauvegarde, étapes dans l'ordre, complément à coller après le prompt de contre-audit (faits déjà connus, points en attente de la passation, test depuis le Drive), modèle de compte rendu du test ; contre-vérifiée en lecture seule avant publication.
- **Ce que l'humain a vérifié ou corrigé** : à venir : transmission de la page à Gervais par Leddycia.
- **Candidat pour `prompts.md`** : non.

### JP-36 : Texte autour du bloc HTML reçu par le membre de R4 (O-13)

- **Relais / membre** : R6 (reprise) / Leddycia
- **Outil et modèle** : Claude Code (application de bureau, Claude Opus 5.5)
- **Date et heure** : 2026-10-18, 19:42 puis 19:45 (premières heures lues après chaque envoi)
- **Prompt (texte exact)** :
  > n texte entouraient le bloc HTML que Bradley a reçu
  >
  > Un texte entouraient le bloc HTML que Bradley a reçu.
- **Contexte** : réponse à la question de R6 sur O-13 (marques ```html ou texte autour du bloc reçu). Le premier message, tronqué, n'a pas été pris comme réponse ; le second le complète.
- **Ce qu'il a produit** : E-36 ; `prompts.md` §1.1 (note O-13) et §3 (E-36) ; E-34 précisé ; O-13 clos ; point 5 du complément pour Gervais mis à jour.
- **Ce que l'humain a vérifié ou corrigé** : information du membre de R4, transmise par Leddycia.
- **Candidat pour `prompts.md`** : non.

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

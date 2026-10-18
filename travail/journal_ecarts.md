# Journal des écarts : propositions de l'IA corrigées ou rejetées (E-xx)

> **But** : prouver la « capacité à vérifier et corriger le travail de l'IA » (C-18) et alimenter `prompts.md` §3, qui exige **au moins une** proposition corrigée ou rejetée (C-08).
> Ce journal contient deux sortes d'écarts :
> - les défauts de `version_IA.html`, constatés par R5 et **jamais corrigés dans ce fichier** (RG-08), mais dans `index.html` ;
> - les propositions de l'**IA assistante** corrigées ou refusées pendant n'importe quel relais : fonction hors sprint, règle inventée, réécriture, etc.

## Modèle d'entrée

```markdown
### E-xx : <titre court>
- Date / relais / membre : AAAA-MM-JJ / RX / <prénom>
- Source : version_IA.html | IA assistante (<outil, modèle>)
- Observé : <ce que l'IA a produit ou proposé ; valeur affichée exacte>
- Attendu : <valeur de docs/oracle.md, règle B-xx, consigne C-xx>
- Référence : <CA-xx.yy | RM-xx (CDC) ou B-xx | C-xx | D-xx | RG-xx | P-xx>
- Gravité : bloquant | majeur | mineur
- Décision : corrigé | rejeté | accepté tel quel (justifier)
- Raison : …
- Correction : <commit> (dans index.html, ou dans le livrable concerné)
- Vérifié après correction : oui / non (par qui)
```

## Écarts

> E-01 à E-12 : erreurs de l'IA assistante de R1 (Claude Code, Claude Opus 5.5), détectées par une relecture adversariale automatisée (workflow Claude Code, 18 agents) ; corrections validées par l'humain de R1 (Leddycia). Ces écarts sont de bons candidats pour `prompts.md` §3 (C-08). Les relais suivants continuent la numérotation à E-13.

### E-01 : Nombre de lignes à litres décimaux

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : `docs/oracle.md` §1 et `PLAN_CADRAGE.md` §1.3 annonçaient 7 lignes de litres décimaux.
- **Attendu** : 4 lignes dans le CSV (08/09, 15/09, 02/10 et 14/10).
- **Référence** : oracle, B-14
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : chiffre faux dans la référence de vérification.
- **Correction** : socle R1 (`relais-1`), dans `docs/oracle.md` et `PLAN_CADRAGE.md`
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-02 : Signature du bug de fuseau

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : `PLAN_CADRAGE.md` §1.4 (P-01) donnait « septembre 28 h » comme signature du bug.
- **Attendu** : septembre à 32 h (simulation du bug, `docs/oracle.md` §5).
- **Référence** : P-01
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : une signature fausse aurait empêché R5 de reconnaître le bug de fuseau.
- **Correction** : socle R1 (`relais-1`), dans `PLAN_CADRAGE.md`
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-03 : Tags légers jamais envoyés

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : `git tag relais-X` et `git tag version-ia` créaient des tags légers, que `git push --follow-tags` n'envoie jamais (reproduit dans un dépôt de test).
- **Attendu** : tags annotés (`git tag -a`), visibles dans `git ls-remote --tags origin` après le push.
- **Référence** : C-09, AGENTS §9
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : la preuve de C-09 (tag `version-ia`) aurait été inaccessible à R5 et R6.
- **Correction** : socle R1 (`relais-1`), dans `AGENTS.md` §9, `agents/03_prompt_engineer.md` et partout où un tag est posé
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-04 : Oracle présenté comme « calculé sans IA »

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : l'oracle était présenté comme « calculé sans IA » ou « indépendamment de toute IA ».
- **Attendu** : valeurs calculées par un script Python déterministe, écrit et exécuté par l'IA assistante du relais R1, indépendamment de l'IA déléguée et du prototype ; script non conservé dans le dépôt ; contre-vérification humaine obligatoire par R2.
- **Référence** : C-18
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : affirmation fausse, que le jury pouvait contester. Les valeurs elles-mêmes ont été recalculées sans erreur par la relecture.
- **Correction** : socle R1 (`relais-1`), dans `AGENTS.md`, `docs/oracle.md`, `PLAN_CADRAGE.md`, `agents/01_analyste_cdc.md` (A3) et `ETAT_PROJET.md` (§3, §6 et §7)
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-05 : Session vierge non garantie

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : la « session vierge » de l'IA déléguée était obtenue avec une CLI lancée dans un dossier vide.
- **Attendu** : une session qui ne reçoit que le prompt RMTCEV (D-09). Or une CLI charge quand même les instructions globales de l'utilisateur (`~/.claude/CLAUDE.md`, `~/.claude/rules/`, `~/.codex/AGENTS.md`), présentes sur le poste de R1.
- **Référence** : C-08, D-09
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : `prompts.md` n'aurait pas reflété ce qui a réellement produit `version_IA.html`.
- **Correction** : socle R1 (`relais-1`) : D-09 réécrite dans `travail/decisions.md` (IA web en conversation temporaire, ou `claude --safe-mode`), et reprise dans les fichiers qui décrivent la délégation (`CLAUDE.md`, `GEMINI.md`, `agents/03_prompt_engineer.md`, `PLAN_CADRAGE.md`)
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-06 : CA et hypothèse non demandés (Q-08)

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : CA-01.02 « la page confirme 36 jours chargés » et hypothèse Q-08 « Oui » (rappeler la couverture de la période).
- **Attendu** : aucun élément du brief ne demande cet affichage ; une exigence que le brief ne justifie pas ne s'écrit pas (C-02, RG-01).
- **Référence** : C-02, RG-01
- **Gravité** : majeur
- **Décision** : rejeté
- **Raison** : exigence inventée. Q-08 devient « Non en V1 (non demandé par le client) ; à proposer au client dans les points à confirmer du CDC ».
- **Correction** : socle R1 (`relais-1`) : CA retiré (`agents/02_product_owner.md`, `PLAN_CADRAGE.md` §4) et Q-08 modifiée (`travail/decisions.md`)
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-07 : Souhaits B-21 à B-24 rangés hors périmètre

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : le gabarit du CDC rangeait B-21 à B-24 en « Hors périmètre ».
- **Attendu** : hors périmètre = B-25 à B-27 uniquement (décisions du client, C-03) ; B-21 à B-24 ne sont pas tranchés (C-04) et leur classement figure dans le backlog (D-08).
- **Référence** : C-03, C-04
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : le CDC aurait contredit le backlog et confondu les décisions du client avec des souhaits non tranchés.
- **Correction** : socle R1 (`relais-1`), dans `agents/01_analyste_cdc.md` (rubriques 10 et 10 bis)
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-08 : Fixture f05 mal décrite

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : la fixture f05 était décrite avec des décimales à virgule, impossibles dans un CSV à séparateur virgule, et ne déclenchait pas le piège P-04.
- **Attendu** : litres 0.1 et 0.2 écrits avec un point décimal dans un même mois ; somme brute avec un artefact de flottant ; affichage arrondi à 1 décimale.
- **Référence** : B-18, P-04
- **Gravité** : mineur
- **Décision** : corrigé
- **Raison** : la fixture n'aurait pas testé le piège visé.
- **Correction** : socle R1 (`relais-1`), dans `docs/oracle.md` §8 et `PLAN_CADRAGE.md`
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-09 : Identifiants B-xx inexistants

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : B-05 et B-20 étaient cités dans le plan et les fiches.
- **Attendu** : B-05a, B-05b, B-05c et B-20.1 à B-20.4 (`docs/brief_client.md`).
- **Référence** : C-02
- **Gravité** : mineur
- **Décision** : corrigé
- **Raison** : un identifiant introuvable casse la traçabilité vers le brief.
- **Correction** : socle R1 (`relais-1`), dans `PLAN_CADRAGE.md` et les fiches `agents/`
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-10 : Prompt RMTCEV non figé avant l'envoi

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : la fiche 03 faisait créer `prompts.md` après la délégation : le texte envoyé n'était pas figé.
- **Attendu** : prompt final écrit dans `Groupe_01_Cas_01/prompts.md` §1 et commité avant la délégation ; c'est ce texte, et lui seul, qui est collé.
- **Référence** : C-08
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : `prompts.md` doit contenir le prompt exact réellement envoyé.
- **Correction** : socle R1 (`relais-1`), dans `agents/03_prompt_engineer.md`
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-11 : Gemini CLI supposé disponible

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : `GEMINI.md` supposait Gemini CLI.
- **Attendu** : depuis le 18/06/2026, Gemini CLI n'est plus servi aux comptes personnels ; il est remplacé par Antigravity CLI, qui lit directement `AGENTS.md` et `GEMINI.md`.
- **Référence** : D-03
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : un membre qui utilise Gemini avec un compte personnel n'aurait pas pu charger les instructions comme prévu.
- **Correction** : socle R1 (`relais-1`), dans `GEMINI.md`
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-12 : Statut « validé » attribué par l'IA

- **Date / relais / membre** : 2026-10-18 / R1 / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : le statut « validé » (décidé par « Équipe (R1) ») était attribué par l'IA à D-06 à D-09 et H-01 à H-06, avant toute validation de l'équipe.
- **Attendu** : un statut « validé » reflète une validation humaine réelle, avec son auteur.
- **Référence** : C-18
- **Gravité** : mineur
- **Décision** : corrigé
- **Raison** : un arbitrage proposé par l'IA ne doit pas passer pour une décision de l'équipe.
- **Correction** : socle R1 (`relais-1`) : validation humaine du 2026-10-18 consignée dans `travail/decisions.md` (§1, §3 et §4) et dans `ETAT_PROJET.md` §7
- **Vérifié après correction** : à faire (relecture humaine avant le commit de R1, puis audit de R2)

### E-13 : Protocole de relais v1 incomplet (journal effacé, Git en un seul bloc, R7 inexistant)

- **Date / relais / membre** : 2026-10-18 / R1 (complément) / Leddycia
- **Source** : IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : la première version de `agents/00_protocole_relais.md` vidait ETAT §8 avant de le recopier dans le rapport d'audit ; mettait contrôle, commit, tag et push dans un seul bloc (un fichier interdit pouvait partir avant toute lecture) ; demandait d'écrire dans ETAT §7 le hash d'un commit pas encore créé ; ne gérait ni le tag déjà existant, ni un dépôt distant qui a avancé (cas réel : commit a468c31 fait sur le web), ni PowerShell, ni la sandbox de Codex ; visait un « R7 » à la fin de R6 ; faisait régénérer ETAT en entier par une IA web ; déclenchait un commit et un push sur le seul mot « sauvegarde ».
- **Attendu** : une passation qui ne perd aucune information, ne publie jamais un original de `docs/` ni `version_IA.html`, et fonctionne avec chaque outil (D-14, RG-08, C-09).
- **Référence** : D-14, RG-08, RG-11, C-09
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : détecté par deux passes de simulation automatisées (Claude Code, Codex, Antigravity, IA web, cohérence) : 87 puis 28 constats confirmés après tentative de réfutation.
- **Correction** : complément de R1 (commit postérieur au tag `relais-1`), dans `agents/00_protocole_relais.md`, `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `ETAT_PROJET.md`, `agents/06_finalisation_soutenance.md`, `PLAN_CADRAGE.md`
- **Vérifié après correction** : oui pour les commandes Git (testées dans un dépôt de test) ; relecture humaine à faire à la clôture

### E-14 : Texte de B-08 paraphrasé (« période choisie »)

- **Date / relais / membre** : 2026-10-18 / R2 / Leddycia
- **Source** : agents de rédaction du workflow de R2 (Claude Code, Claude Opus 5.5)
- **Observé** : le brouillon du CDC écrivait « B-07, B-08 et B-10 demandent les mêmes affichages pour la période choisie » et « EF-06 (litres de la période choisie, B-08) ».
- **Attendu** : B-08 dit seulement « pour la période » ; l'assimilation à la période choisie est une lecture de l'équipe et doit être présentée comme telle.
- **Référence** : B-08, C-02, RG-01
- **Gravité** : mineur
- **Décision** : corrigé
- **Raison** : une paraphrase présentée comme le texte du client aurait été rejetée au contrôle mot à mot.
- **Correction** : CDC v1, avant son premier commit (§4, notes « Priorités » ; source d'EF-06 ; RM-01)
- **Vérifié après correction** : oui (vérificateurs du workflow, puis contrôle des citations par script)

### E-15 : « Jour ouvrable » transformé en critère de calcul

- **Date / relais / membre** : 2026-10-18 / R2 / Leddycia
- **Source** : agents de rédaction du workflow de R2 (Claude Code, Claude Opus 5.5)
- **Observé** : « Jour : un jour ouvrable présent dans le fichier chargé ».
- **Attendu** : B-02 et B-18 décrivent le registre et l'échantillon ; aucun élément de B-06 à B-15 ne limite les calculs aux jours ouvrables. Définition retenue : « une ligne de données du fichier chargé, désignée par sa date (B-19) ».
- **Référence** : B-02, B-18, RG-01, RG-02
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : lue par l'IA déléguée, la définition pouvait faire filtrer ou rejeter les dates de week-end, une règle que le client n'a pas fixée.
- **Correction** : CDC v1, avant son premier commit (§4, « Termes employés ») ; le cas d'une date non ouvrable est renvoyé à R4 (`R2_audit.md`, point 9)
- **Vérifié après correction** : oui (vérificateurs du workflow)

### E-16 : « Toute la période » bornée aux dates de l'échantillon

- **Date / relais / membre** : 2026-10-18 / R2 / Leddycia
- **Source** : agents de rédaction du workflow de R2 (Claude Code, Claude Opus 5.5)
- **Observé** : « pour toute la période, sur le fichier fourni, tous ses jours, du 3 août au 16 octobre 2026 (B-18) ».
- **Attendu** : « pour toute la période, tous les jours du fichier chargé (sur le fichier fourni : du 3 août au 16 octobre 2026, B-18) », conforme au glossaire d'`AGENTS.md` et à Q-02.
- **Référence** : B-03, B-09, Q-02
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : la définition n'était pas testable sur un autre fichier et poussait à figer ces dates dans le code, contre la recopie hebdomadaire (B-03).
- **Correction** : CDC v1, avant son premier commit (§4, « Termes employés »)
- **Vérifié après correction** : oui (vérificateurs du workflow)

### E-17 : CT-04 lisible comme une permission d'intégrer les données

- **Date / relais / membre** : 2026-10-18 / R2 / Leddycia
- **Source** : agents de rédaction du workflow de R2 (Claude Code, Claude Opus 5.5)
- **Observé** : « Les données ne doivent pas être intégrées directement dans la page ; les y intégrer constituerait un écart par rapport à la demande du client, à signaler et à justifier dans prompts.md. »
- **Attendu** : une seule obligation, sans échappatoire : « Les données ne doivent pas être intégrées directement dans la page du prototype » (C-12, D-06).
- **Référence** : C-12, D-06, P-06
- **Gravité** : majeur
- **Décision** : corrigé
- **Raison** : deux obligations dans un même élément ; l'IA déléguée, qui ne connaît pas `prompts.md`, pouvait lire la seconde comme une permission sous condition.
- **Correction** : CDC v1, avant son premier commit (§7, CT-04 ; la conséquence prévue par C-12 reste au §12.2)
- **Vérifié après correction** : oui (vérificateurs du workflow)

### E-18 : Règle B-14 affaiblie, puis proposition de la durcir

- **Date / relais / membre** : 2026-10-18 / R2 / Leddycia
- **Source** : agents de rédaction et vérificateur « DoD et structure » du workflow de R2 (Claude Code, Claude Opus 5.5)
- **Observé** : la note sur RM-03 disait « seul le format des montants est imposé » ; un vérificateur a ensuite proposé « les litres doivent être affichés avec au plus une décimale ».
- **Attendu** : RM-03 garde le texte du client (« les litres peuvent avoir une décimale ») ; le format exact des litres reste le point à confirmer Q-01.
- **Référence** : B-14, Q-01, RG-02
- **Gravité** : mineur
- **Décision** : corrigé (note) et rejeté (durcissement)
- **Raison** : la première formulation affaiblit B-14, la seconde le durcit en règle : les deux tranchent un point que le client n'a pas fixé. L'écart entre B-14 et `AGENTS.md` R-04 est remonté à l'équipe (`R2_audit.md`, constat 10).
- **Correction** : CDC v1, avant son premier commit (§6, notes)
- **Vérifié après correction** : oui (correcteur du workflow)

### E-19 : Choix de l'équipe (H-xx) présentés comme soumis au client

- **Date / relais / membre** : 2026-10-18 / R2 / Leddycia
- **Source** : agents de rédaction du workflow de R2, à partir des instructions de l'IA assistante de R2 (Claude Code, Claude Opus 5.5)
- **Observé** : « soumis au client, qui peut les modifier » au §11.2 ; raison de H-05 : « le libellé par défaut varie selon le navigateur » ; puis, après correction, « H-01 à H-05 … sont à soumettre au client », mention qui venait des instructions de l'IA assistante elle-même.
- **Attendu** : `decisions.md` §3 présente les H-xx comme des choix de présentation de l'équipe, sans soumission au client ; le libellé « Choisir un fichier » est imposé par C-12 (CT-03) ; la raison technique de H-05 donnait l'indice du piège P-07, alors que D-10 reste à trancher par R4.
- **Référence** : `travail/decisions.md` §3, C-12, D-10, P-07
- **Gravité** : mineur
- **Décision** : corrigé
- **Raison** : affirmation sans source, et indice de solution technique donné à l'IA déléguée avant la décision D-10.
- **Correction** : CDC v1, avant son premier commit (§11.2) : les deux premières par le correcteur du workflow, la troisième par l'IA assistante lors de son contrôle
- **Vérifié après correction** : oui (contrôle par l'IA assistante) ; relecture humaine du CDC à confirmer par Leddycia

### E-20 : Citation de B-12 déformée dans la justification de Q-20

- **Date / relais / membre** : 2026-10-18 / R3 / Leddycia
- **Source** : IA assistante de R3 (Claude Code, Claude Opus 5.5)
- **Observé** : la justification de Q-20 dans `travail/decisions.md` citait entre guillemets B-12 sous la forme « n'est pas un prix officiel ».
- **Attendu** : texte exact du client : « il ne s'agit pas d'un prix officiel » (B-12).
- **Référence** : B-12, RG-01
- **Gravité** : mineur
- **Décision** : corrigé
- **Raison** : une citation entre guillemets doit reproduire le texte du client mot pour mot.
- **Correction** : `travail/decisions.md` (Q-20), avant le commit de R3, par l'IA assistante en se relisant
- **Vérifié après correction** : oui (IA assistante)

### E-21 : Esquisse du backlog de la fiche 02 : bénéfice non sourcé et fuseau testé sur les seuls totaux

- **Date / relais / membre** : 2026-10-18 / R3 / Leddycia
- **Source** : esquisse de la fiche `agents/02_product_owner.md`, rédigée par l'IA assistante de R1 (Claude Code, Claude Opus 5.5)
- **Observé** : (1) bénéfice de l'US-03 : « afin d'identifier les journées les plus dépendantes de la génératrice » ; (2) seul CA-01.05 teste le fuseau horaire, sur les totaux d'heures et de litres.
- **Attendu** : (1) un bénéfice tiré du brief : B-04 (« discuter avec le conseil d'administration de l'installation de panneaux supplémentaires ») ; (2) l'oracle §5 montre que le bug de fuseau fausse aussi le coût (23 100 au lieu de 21 300 gourdes en août) et le jour maximal (05/08/2026 au lieu de 06/08/2026).
- **Référence** : RG-01, B-04, P-01, Q-09, `docs/oracle.md` §5
- **Gravité** : mineur
- **Décision** : corrigé
- **Raison** : (1) valeur métier qui ne vient pas du client ; (2) CA incomplets pour une règle délicate : un prototype pourrait passer CA-01.05 et afficher un jour maximal faux.
- **Correction** : `Groupe_01_Cas_01/product_backlog.md` v1 (US-03 ; CA-02.04 et CA-03.04 ajoutés sans renuméroter) ; la fiche n'est pas modifiée (RG-10)
- **Vérifié après correction** : oui (contrôle DoD par script de l'IA assistante ; relecture humaine du backlog par Leddycia, sans correction, JP-17)

### E-22 : Environnement de test différent de la procédure (Linux au lieu de Windows)

- **Date / relais / membre** : 2026-10-18 / R5 / Louis
- **Source** : procédure de test (`agents/05_verificateur.md`, `tests/plan_de_test.md` §2), appliquée par l'IA assistante (Claude Code, Claude Opus 5.5)
- **Observé** : le poste de R5 est sous Kali Linux. Le fuseau est fixé par le système (`America/Port-au-Prince`, décalage de 240 min au 01/09/2026) et non par le réglage Windows « (UTC-05:00) Haïti ». L'empreinte est contrôlée par `sha256sum` et non par `Get-FileHash`. La passe principale est faite sous Chromium 150 headless piloté par le protocole DevTools (vrai `<input type="file">`, événement `change`), et le hors ligne y est émulé. Les captures automatiques n'ont pas de barre d'adresse `file:///`, et les captures « fuseau » sont des montages des trois mois, avec le fuseau lu dans le navigateur.
- **Attendu** : tests sous Windows, fuseau « (UTC-05:00) Haïti », Edge ou Chrome et Firefox, ouverture par double-clic, hors ligne réel, captures Win+Maj+S (fiche 05 ; Q-09).
- **Référence** : Q-09, P-01, fiche 05 (préparation et contrôles transverses)
- **Gravité** : mineur
- **Décision** : accepté tel quel
- **Raison** : le piège P-01 dépend d'un décalage négatif et non du système d'exploitation ; le décalage de −4 h (heure d'été d'Haïti en octobre 2026, comme le réglage Windows) le déclenche. Le pilotage par script rend la passe reproductible. Restent manuels, faits par Louis à l'écran : la coupure réseau réelle, le second navigateur (Firefox), la liste déroulante ouverte (CA-01.03, CA-01.10) et l'empreinte du CSV (CA-01.08). Le test sous Windows sur un autre PC reste prévu par R6 (test depuis le Drive).
- **Correction** : aucune (procédure documentée dans `tests/plan_de_test.md` §3)
- **Vérifié après correction** : sans objet

### E-23 : Hypothèse Q-01 présentée comme « confirmée »

- **Date / relais / membre** : 2026-10-18 / R5 (complément) / Leddycia
- **Source** : arbitrage de l'IA assistante de R4 (Antigravity, Gemini 3.8 Flash High), validé par Bradley d'un « vas y » (JP-18)
- **Observé** : Q-01 au statut « provisoire (confirmé) » dans le registre (`travail/decisions.md`, tableau Q et journal des changements) ; « Q-01 confirmé » dans ETAT_PROJET (O-9, entrée R4 du §7) et dans `travail/audits/R4_audit.md`.
- **Attendu** : le statut « provisoire » (en attente du client), seul prévu par la légende du registre ; l'équipe peut garder l'hypothèse pour le Sprint 01, sans la présenter comme une réponse du client.
- **Référence** : RG-02, `AGENTS.md` §4 (« Ne présente jamais une hypothèse Q-xx comme une règle du client »), légende de `travail/decisions.md`
- **Gravité** : mineur (l'hypothèse elle-même ne change pas, ni le prototype)
- **Décision** : corrigé
- **Raison** : au jury ou au client, « confirmé » laisserait croire que le client a fixé le format des litres.
- **Correction** : `travail/decisions.md` (Q-01 « provisoire » ; justification reformulée : « tranche le point O-9 » retiré, remplacé par « l'équipe garde cette hypothèse pour le Sprint 01 ; le client n'a pas répondu » ; ligne ajoutée au journal des changements) ; ETAT §5 (O-9) reformulé. Les traces historiques (entrée R4 d'ETAT §7, `R4_audit.md`, JP-18) ne sont pas réécrites (RG-10).
- **Vérifié après correction** : oui, par l'IA assistante du complément (statuts du tableau Q relus par script ; recherche de « confirmé » associé à Q-01 dans tout le dépôt : seules les traces historiques restent), puis par des vérificateurs indépendants en lecture seule (sous-agents Claude Code) avant le commit

### E-24 : Fichier de test f01 « mélangé » qui ne départage pas les égalités

- **Date / relais / membre** : 2026-10-18 / R5 (complément) / Leddycia
- **Source** : fixture créée par l'IA assistante de R4 (Antigravity, Gemini 3.8 Flash High) ; jugée conforme par l'audit d'entrée de l'IA assistante de R5 (Claude Code, Claude Opus 5.5, A4)
- **Observé** : seules 5 lignes d'août changeaient de place ; les 11 jours à 5 h restaient dans l'ordre chronologique. Par simulation : un prototype qui suit l'ordre du fichier avec `>` affichait les bons jours (06/08, 08/09, 02/10, 06/08) ; f01 ne détectait que l'erreur `>=`, déjà détectée par le CSV d'origine.
- **Attendu** : un fichier qui prouve CA-03.02 (« quel que soit l'ordre des lignes dans le fichier », RM-02 du cahier des charges, d'après B-13 : « le premier de ces jours dans l'ordre chronologique ») : le jour attendu ne doit pas être le premier des jours à égalité dans le fichier.
- **Référence** : CA-03.02, B-13, RM-02, P-03, `docs/oracle.md` §8
- **Gravité** : majeur pour la preuve de CA-03.02 (sans effet sur le prototype, qui donne les bons jours sur les deux versions de f01)
- **Décision** : corrigé
- **Raison** : un critère d'acceptation n'est vérifié que si le test peut échouer pour un prototype fautif (C-18, « capacité à vérifier »).
- **Correction** : `tests/fixtures/f01_lignes_melangees.csv` refait (mélange par script à graine fixe, jours à 5 h : 16/10, 02/10, 12/08, 13/10, 11/09, 05/10, 08/10, 06/08, 08/09, 15/10, 09/09) ; `docs/oracle.md` §8 ; 4 captures `US03_CA02_lignes_melangees_*.png` refaites ; ligne CA-03.02 de `tests/plan_de_test.md` §3
- **Vérifié après correction** : oui, par l'IA assistante du complément (mêmes 36 lignes et même en-tête que le CSV, 727 octets, CRLF ; simulation : le nouveau f01 détecte les trois erreurs, ordre du fichier avec `>`, ordre du fichier avec `>=` (sauf en août, où le bon jour sort par coïncidence) et tri par date puis `>=` (comme le CSV d'origine) ; `version_IA.html` sous Windows 11 dans Chrome 155 sans interface, fuseau d'Haïti et coupure réseau émulés : valeurs de l'oracle ; images relues), puis par des vérificateurs indépendants en lecture seule (sous-agents Claude Code) avant le commit

### E-25 : Données personnelles visibles dans des captures du livrable

- **Date / relais / membre** : 2026-10-18 / R5 (complément) / Leddycia
- **Source** : captures manuelles de R5 (Louis), ajoutées au livrable par l'IA assistante de R5 (Claude Code, Claude Opus 5.5) sans contrôle de ce qu'elles montraient en dehors de la page
- **Observé** : `US01_CA01_etat_initial.png`, `US01_CA02_firefox_toute_periode.png`, `US01_CA03_liste_periodes.png` et `US01_CA08_lecture_seule.png` montraient le chemin personnel du poste (nom d'utilisateur), l'invite du terminal (nom d'utilisateur et nom du poste) et des favoris du navigateur sans rapport avec le projet.
- **Attendu** : des captures qui ne montrent que la preuve ; les noms des personnes ne figurent que dans ETAT_PROJET, PLAN_CADRAGE, `travail/`, le README et la fiche de contribution ; aucune autre donnée personnelle réelle.
- **Référence** : RG-09, C-01, C-13
- **Gravité** : majeur (livrable à remettre et à noter, déjà versé sur un dépôt public)
- **Décision** : corrigé
- **Raison** : ces informations n'apportent aucune preuve et exposent une personne.
- **Correction** : CA-01.01 : barre des favoris remplie de sa couleur de fond, nom d'utilisateur masqué dans l'adresse ; CA-01.02 (Firefox) et CA-01.03 : bandeau du haut recadré ; CA-01.08 : 10 masques gris (adresse, titre et invites du terminal, fragment de la barre des favoris, chemin du résultat de `sha256sum`). L'onglet « about:sessionrestore » (page interne du navigateur, sans donnée personnelle) est conservé sur CA-01.01 et CA-01.08. Les valeurs de preuve restent lisibles (adresse `file:///…/version_IA.html`, empreinte `320155c7…a84b`, valeurs affichées). L'historique Git n'est pas réécrit : les versions précédentes restent dans les commits de R5 (`AGENTS.md` §11).
- **Vérifié après correction** : oui, par l'IA assistante du complément (images relues en entier et agrandies ; script : recadrages exacts et aucun pixel modifié hors des masques prévus ; aucune métadonnée dans les 34 captures), puis par des vérificateurs indépendants en lecture seule (sous-agents Claude Code), qui ont relu les 34 captures avant le commit

### E-26 : Blocs de code mal fermés dans `prompts.md`

- **Date / relais / membre** : 2026-10-18 / R5 (complément) / Leddycia
- **Source** : `Groupe_01_Cas_01/prompts.md` assemblé par l'IA assistante de R4 (Antigravity, Gemini 3.8 Flash High) et commité avant l'envoi (`b170333`)
- **Observé** : le bloc du prompt s'ouvrait l. 20 avec trois accents graves ; les blocs internes (cahier des charges, Sprint 01) utilisaient aussi trois accents graves, si bien que la l. 384 fermait le bloc du prompt trop tôt et que la l. 510 ouvrait un bloc jamais fermé. À l'affichage (GitHub ou tout lecteur Markdown), la fin du prompt sortait du bloc et les sections 2 à 4 de `prompts.md` apparaissaient comme du code.
- **Attendu** : le prompt affiché en un seul bloc, et les sections 2 à 4 lisibles.
- **Référence** : C-08 (prompt de délégation RMTCEV consigné dans `prompts.md`), DoD de `prompts.md` (`AGENTS.md` §12 : prompt « tel qu'envoyé »)
- **Gravité** : mineur (le texte envoyé n'est pas en cause)
- **Décision** : corrigé
- **Raison** : le livrable est lu par l'enseignant sous sa forme affichée.
- **Correction** : l. 20 et 510 en quatre accents graves ; le texte du prompt (l. 21 à 509) n'est pas modifié.
- **Vérifié après correction** : oui, par l'IA assistante du complément (texte des l. 21 à 509 identique octet pour octet à `b170333` ; analyse des blocs selon les règles CommonMark : un seul bloc, l. 20 à 510, sections 2 à 4 hors bloc), puis par des vérificateurs indépendants en lecture seule (sous-agents Claude Code) avant le commit

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

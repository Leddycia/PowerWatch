# Audit d'entrée : relais R6 (Petiote, Claude [modèle non précisé], 2026-10-18 16:59)

## Livrables audités : `Groupe_01_Cas_01/` et résultats du relais R5

| # | Constat | Preuve (fichier, CA ou règle) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|
| A1 | Passe réduite sur `version_IA.html` : chargement du CSV local, valeurs de toute la période correctes (97 h, 280,0 L, 84 000 gourdes, 06/08/2026 (5 h)) ; puis septembre correct (30 h, 84,0 L, 25 200 gourdes, 08/09/2026 (5 h)). Après chargement, le contexte navigateur a été placé hors ligne ; le changement de période a continué à fonctionner. Fuseau observé : `America/Port-au-Prince`, décalage de 240 minutes le 01/09/2026. | CA-01.01, CA-01.02, CA-01.04, CA-02.01, CA-03.01 ; navigateur local | conforme | laissé |
| A2 | Le tag `version-ia` est présent et `git diff version-ia -- Groupe_01_Cas_01/prototype/version_IA.html` ne produit aucune différence. | RG-08, C-09 | conforme | laissé |
| A3 | 34 fichiers de capture sont présents. L'inventaire comprend une preuve nommée pour chaque CA du Sprint 01 ; CA-03.02 possède une capture par période. La lisibilité de chaque image n'a pas été inspectée individuellement. | C-15, `tests/plan_de_test.md` §3, `Groupe_01_Cas_01/captures/` | conforme | laissé |
| A4 | Les identifiants US/CA du backlog concordent avec le plan de test et le prompt RMTCEV : Sprint 01 = US-01 à US-03 et 20 CA. Les sections 2 à 4 de `prompts.md` restent à compléter. | `product_backlog.md`, `tests/plan_de_test.md` §1 et §3, `prompts.md` | à corriger | compléter dans le cadre de R6 |
| A5 | L'inventaire du dossier livrable ne montre aucun fichier parasite. `README.md` est absent et doit être produit par R6. `index.html` est absent ; R5 documente qu'aucun écart aux CA n'a justifié sa création (C-09). | C-01, C-09, RG-12 ; `ETAT_PROJET.md` §3 | à corriger | créer le README ; expliquer l'absence d'`index.html` |
| O-13a | Le brut commence directement par `<!DOCTYPE html>` et ne contient pas de bloc Markdown ```html ni de texte d'enrobage. Il est impossible d'établir si ces marqueurs ont été retirés lors de la sauvegarde ou absents de la réponse reçue. | `travail/brut/delegation_reponse_brute.md`, prompt de délégation dans `prompts.md` §1.2, DoD `AGENTS.md` §12 | à corriger | laissé ouvert ; Bradley n'a pas répondu |
| O-13b | Le brut décrit une « nouvelle conversation web temporaire » ; `prompts.md` §1.1 décrit une « Nouvelle conversation web ». Le membre R6 indique ne pas avoir reçu de réponse de Bradley sur le mode exact. | `travail/brut/delegation_reponse_brute.md`, `prompts.md` §1.1, D-09 | à corriger | ne pas harmoniser par supposition ; mentionner l'information vérifiable et la confirmation manquante |
| O-14 | R5 signale qu'une ligne vide au milieu du CSV est ignorée sans message et que les heures décimales seraient arrondies à l'entier. Aucun de ces comportements ne viole les CA testés ; aucun correctif ne doit être ajouté hors Sprint 01. | `travail/audits/R5_audit.md`, `travail/journal_ecarts.md`, RG-04, Q-04, Q-16 | conforme (hors CA) | laisser ; signaler comme comportement connu dans le README |

## Ce qui a été seulement survolé ; résultats donnés par le membre

- Les 34 captures ont été vérifiées par leur nom et leur présence, mais pas ouvertes une par une pour juger leur lisibilité.
- Le membre a répondu qu'il n'a pas reçu de réponse de Bradley sur O-13.
- Le membre indique « Leddycia » pour le téléversement Drive ; l'heure du téléversement, le testeur, l'ordinateur et le navigateur restent à obtenir.
- Le membre a indiqué « CLAUDE » sans préciser le modèle. Le modèle exact reste non documenté.
- La passe réduite est celle du navigateur intégré : `version_IA.html` local, puis coupure réseau simulée. Ce n'est pas le test depuis le Drive sur un autre ordinateur exigé par C-14.

## Corrections apportées (une ligne par correction)

- Aucune correction au prototype des relais précédents ; `version_IA.html` reste intact (RG-08).
- Le README absent et les sections finales vides de `prompts.md` sont des livrables R6 à compléter, pas des corrections au prototype.

## Points remontés à l'équipe (decisions.md, ETAT_PROJET.md)

- O-13 demeure non résolu jusqu'à confirmation de Bradley ; aucune décision n'est ajoutée au registre sur la base d'une supposition.
- Leddycia doit confirmer le téléversement Drive, puis les faits du test depuis le Drive et le remplacement du README ; ils conditionnent le statut REMIS.
- Les heures décimales arrondies et les lignes vides ignorées sont mentionnées comme comportements hors CA (O-14), sans changement de périmètre.

## Ce que j'ai produit pendant mon relais

- À compléter au fil des étapes R6.

## Journal de bord du relais (copie intégrale d'ETAT §8, ajoutée à la passation)

À compléter à la passation avec la copie intégrale d'ETAT §8.

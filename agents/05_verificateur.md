# Fiche de rôle 05 : Vérificateur QA, tests et preuves (relais R5, partie 1 ; réutilisée par R6)

> À lire après `AGENTS.md` et `ETAT_PROJET.md`. Porte visée : **G5**.
> Le relais R5 enchaîne, sur 60 min : **démarrage** (0 à 5 min) ; **vérification de `version_IA.html`**, qui tient lieu d'audit d'entrée (cette fiche, 5 à 20 min) ; **corrections** (fiche 04, 20 à 40 min) ; **nouvelle vérification et captures d'`index.html`** (cette fiche, 40 à 50 min) ; **passation** (50 à 60 min). À la 50e minute, les captures manquantes sont notées dans `ETAT_PROJET.md` pour R6 (fiche 06, A3).

## Rôle et objectif

Vérifier, **preuve à l'appui**, que le prototype respecte chaque critère d'acceptation du Sprint 01, ainsi que les règles du client et les consignes. C'est le cœur du critère C-18 : « capacité à vérifier et à corriger le travail de l'IA ».

**Le vérificateur ne croit pas l'IA sur parole : il compare l'écran à l'oracle.**

## Entrées à lire

- `Groupe_01_Cas_01/product_backlog.md` (CA du Sprint 01), `tests/plan_de_test.md`, `tests/fixtures/`
- `docs/oracle.md` (valeurs justes, signature des bugs), `AGENTS.md` §7 (pièges)

## Checklist d'audit d'entrée (travail du relais R4)

| # | Point à vérifier | Comment |
|---|---|---|
| A1 | `version_IA.html` est brut et tagué | `git pull`, `git fetch --tags`, puis `git tag -l` (`version-ia` doit apparaître) ; `git show version-ia --stat` ; `git diff version-ia -- Groupe_01_Cas_01/prototype/version_IA.html` est vide |
| A2 | La réponse brute est conservée et l'extraction est fidèle (C-09) | `travail/brut/` existe et n'est pas vide. Copier le bloc HTML de la réponse brute dans un fichier temporaire hors du dépôt, puis, dans Git Bash : `git diff --no-index --ignore-cr-at-eol <fichier temporaire> Groupe_01_Cas_01/prototype/version_IA.html` doit être vide. Sinon : entrée E-xx dans `journal_ecarts.md`, sans jamais corriger `version_IA.html` |
| A3 | `prompts.md` contient le prompt RMTCEV complet | Les 6 parties ; CDC et Sprint 01 intégrés ; outil, modèle et date |
| A4 | Le plan de test et les fixtures existent | Sinon, les créer en premier (voir fiche 03, tâche 4) |

## Préparation de l'environnement de test (une fois)

1. **Fuseau horaire** : Paramètres, Heure et langue, Date et heure, désactiver « Définir le fuseau horaire automatiquement », puis choisir **« (UTC-05:00) Haïti »**. Penser à le **remettre** à la fin.
2. **Empreinte du CSV avant les tests** : dans PowerShell, à la racine du dépôt, `(Get-FileHash .\docs\energie_college.csv -Algorithm SHA256).Hash -eq '320155c76969aeb0e05779861b2520a150675f853318d2dfd6592eaf0107a84b'` doit afficher `True` (Get-FileHash affiche en majuscules ; la comparaison `-eq` ignore la casse). Si `False` : `git restore docs/energie_college.csv`, puis recontrôler ; vérifier que `.gitattributes` est présent.
3. **Mode hors ligne** : **pas maintenant**. Les IA de test ont besoin d'Internet : le contrôle hors ligne se fait **en fin de passe** (voir « Contrôles transverses »).
4. **Navigateurs** : Edge ou Chrome, **et** Firefox. Le second navigateur sert seulement au libellé du bouton (P-07) et à une période.
5. Ouvrir le fichier HTML **par double-clic dans l'Explorateur Windows**. L'adresse doit commencer par `file:///`.

## Exécution

Pour **chaque CA** du Sprint 01 (dans l'ordre du plan de test) :

1. Exécuter la procédure et noter le **résultat observé exact**.
2. Comparer avec l'oracle. Statut :
   - **respecté** : identique ;
   - **partiel** : le comportement est là, mais un détail diffère (format, libellé) ;
   - **non respecté** : la valeur est fausse ou la fonction absente.
3. Un écart crée une entrée **E-xx** dans `travail/journal_ecarts.md` (modèle dans le fichier).
4. Utiliser la **signature des bugs** pour diagnostiquer :
   - août à 26 h ou septembre à 32 h : bug de fuseau (P-01) ;
   - 12/08, 11/09 ou 16/10 en jour max (16/10 aussi pour toute la période) : mauvaise gestion de l'égalité (P-03, voir `docs/oracle.md` §4).

**Contrôles transverses** (sur chaque version testée) :

| Contrôle | Méthode | Attendu |
|---|---|---|
| Hors ligne (**en fin de passe**) | Débrancher le câble Ethernet **et** activer le mode avion ; vérifier dans le panneau rapide (Win+A) que le Wi-Fi est coupé ; `https://example.com` doit afficher une erreur dans chaque navigateur de test. Rouvrir la page par double-clic, charger le CSV, vérifier une période, capturer, puis rétablir le réseau | Tout fonctionne ; la période vérifiée donne les valeurs de l'oracle |
| Aucune ressource externe | Commande PowerShell ci-dessous (elle couvre les URL, `@import`, `fetch(`, `XMLHttpRequest` et `WebSocket`) ; dans l'éditeur (VS Code : Ctrl+F), rechercher aussi `//`, `url(` et `src=` ; examiner chaque ligne trouvée | Aucune ressource externe ; tout espace de noms `http://www.w3.org/…` (svg, xlink, xhtml) est toléré |
| Aucune donnée intégrée | Ouvrir sans charger de fichier ; rechercher `2026-08-03` dans le source | Aucune valeur calculée ni donnée du fichier affichée (les libellés fixes, comme le prix de référence de 300 gourdes/L, sont permis) ; aucune donnée dans le source |
| Bouton | Libellé visible | Exactement « Choisir un fichier », sur chaque navigateur |
| Lecture seule | Empreinte du CSV après les tests (même commande qu'à l'étape 2 de la préparation) ; pas de champ éditable ni d'export | `True` : empreinte identique |
| Hors sprint | Inventaire des fonctions visibles | Rien au-delà des US-01 à US-03 (sinon E-xx) |
| Rechargement (P-09) | Charger d'abord une fixture aux totaux différents (f04 ou f05), puis le fichier original | Exactement les valeurs de l'oracle (toute la période : 97 h, 280,0 L, 84 000 gourdes), sans cumul ni reste de la fixture |

Recherche des ressources externes (PowerShell, à la racine du dépôt) :

```powershell
Select-String -Path <fichier> -Pattern '(https?:)?//(?!www\.w3\.org/)[a-z0-9.-]+\.[a-z]{2,}|@import|fetch\(|XMLHttpRequest|WebSocket'
```

## Captures (sur la version finale uniquement)

- **Au moins une capture par CA** dans `Groupe_01_Cas_01/captures/`, nommée `USxx_CAyy_<detail>.png` (par exemple `US01_CA04_aout.png`). Une capture peut prouver plusieurs CA si les valeurs y sont lisibles.
- La capture montre **la valeur attendue lisible**, la période sélectionnée et, si possible, la barre d'adresse `file:///`.
- Pour les CA de type « fuseau » ou « hors ligne », capturer aussi le réglage Windows correspondant (fuseau Haïti ; pour le hors ligne, le panneau Win+A et l'erreur affichée par `https://example.com`).
- Outil Windows : Win+Maj+S.

## Tableau de résultats (à remplir dans `tests/plan_de_test.md` ; R6 le reprend dans le README)

| CA | Résultat attendu (oracle) | Observé sur `version_IA` | Statut `version_IA` | Observé sur `index` | Statut final | Capture |
|---|---|---|---|---|---|---|

## Checklist de sortie (DoD)

- [ ] Chaque CA du Sprint 01 a un statut, pour `version_IA` **et** pour la version finale.
- [ ] Chaque écart a son E-xx ; aucun écart n'est « oublié ».
- [ ] Tests faits avec le fuseau Haïti, sur 2 navigateurs (le second pour le libellé du bouton et une période), hors ligne en fin de passe ; empreinte du CSV contrôlée avant et après.
- [ ] Captures nommées selon la convention et présentes dans `captures/`.
- [ ] Fuseau horaire du PC remis comme avant.

## Interdits

- Marquer « respecté » sans l'avoir vu à l'écran.
- Corriger une valeur attendue de l'oracle pour la faire coller au prototype. Si l'oracle semble faux, le recalculer à la main et l'inscrire dans `decisions.md`.
- Tester sur `version_IA.html` modifié.

## Prompt d'amorçage spécifique

```
Mission R5 (vérification) : à partir de tests/plan_de_test.md et docs/oracle.md, guide-moi CA par CA
pour tester <version_IA.html | index.html>. Pour chaque CA, dis-moi exactement quoi faire et quoi regarder,
puis je te donne l'observé ; tu proposes un statut et, si écart, une entrée E-xx pour travail/journal_ecarts.md.
Ne propose aucune correction de code dans cette phase.
```

## À écrire dans `ETAT_PROJET.md` à la passation (fin de R5)

- Le tableau des statuts finaux.
- Les écarts restants et leur justification.
- La liste des captures, et celles qui manquent (R6 les reprend, fiche 06, A3).
- `index.html` créé ou non.
- La mission de R6.

# Fiche de rôle 04 : Développeur, corrections de `index.html` (relais R5, partie 2)

> À lire après `AGENTS.md`, `ETAT_PROJET.md` et **`agents/05_verificateur.md`** : le relais R5 commence par la vérification complète de `version_IA.html` (fiche 05), puis corrige (cette fiche).
> Porte visée : **G5**. Durée de la partie correction : environ 20 min dans l'heure de R5 (de la 20e à la 40e minute).

## Rôle et objectif

Partir de `version_IA.html` et produire **`index.html`**. On corrige **uniquement** les écarts constatés contre les CA du Sprint 01, les règles du client et les consignes, avec des modifications **minimales et traçables**. On n'ajoute aucune fonctionnalité.

> Si la vérification montre que `version_IA.html` respecte **déjà tous** les CA, on ne crée pas `index.html`. On l'écrit dans `ETAT_PROJET.md`, et R6 le mentionne dans le README (C-09).

## Entrées à lire

- `travail/journal_ecarts.md`, rempli par la vérification (fiche 05)
- `Groupe_01_Cas_01/product_backlog.md` (CA du Sprint 01), `docs/oracle.md`, `AGENTS.md` §4 et §7
- `Groupe_01_Cas_01/prototype/version_IA.html` (**lecture seule**)

## Procédure de correction

1. **Initialiser** : copier `version_IA.html` vers `index.html`, sans rien changer, puis commiter.

   ```bash
   cp Groupe_01_Cas_01/prototype/version_IA.html Groupe_01_Cas_01/prototype/index.html
   git add Groupe_01_Cas_01/prototype/index.html
   git commit -m "chore(proto): index.html initialisé depuis version_IA"
   ```

2. **Traiter les écarts par gravité** : d'abord les CA non respectés, ensuite les consignes (C-10 à C-12), enfin les CA partiels (format, libellé) ; aucune retouche qui ne corrige pas un écart consigné (RG-04).
3. **Pour chaque écart** :
   - demander à l'IA assistante une correction **ciblée** : citer l'E-xx, le CA et la valeur attendue de l'oracle ;
   - **relire le diff** : la correction ne doit toucher que ce qui est nécessaire ;
   - retester le CA concerné ;
   - commiter, dans Git Bash : `git add Groupe_01_Cas_01/prototype/index.html && git commit -m "fix(proto): E-<n> premier jour chronologique en cas d'égalité (CA-03.01)"` ; jamais de `git commit -a`, qui pourrait inclure une modification accidentelle de `version_IA.html` ;
   - mettre à jour l'E-xx dans `journal_ecarts.md` (décision, raison, commit).
4. **Si l'IA assistante propose autre chose** (ajout de fonction, refonte, bibliothèque) : **refuser**. Consigner la proposition rejetée et sa raison (par exemple « hors Sprint 01, RG-04 »). C'est exactement ce que demande C-08.

## Règles techniques pour `index.html` (rappel de `AGENTS.md` §7)

- HTML, CSS et JavaScript **natifs**, dans un seul fichier. Aucune balise `<script src>`, `<link href>` ou `@import` vers l'extérieur.
- Chargement par `<input type="file" accept=".csv">` masqué, avec un bouton ou label visible « Choisir un fichier » ; lecture par `FileReader`.
- Analyse : `split(/\r?\n/)` ; `trim()` des cellules et des en-têtes ; ignorer la dernière ligne si elle est vide (le fichier se termine par CRLF : le découpage donne un 38e élément vide, qui n'est pas une ligne invalide au sens de Q-04) ; vérifier les 4 colonnes attendues (Q-04).
- **Dates : jamais `new Date("AAAA-MM-JJ")`**. Le mois se lit par `date.slice(0, 7)` et l'affichage se fait par `split('-')`, pour donner JJ/MM/AAAA (P-01, H-01).
- Jour max : trier **une copie** par la chaîne de date (l'ordre ISO est chronologique), puis comparer en `>` strict (P-03).
- Formats : litres `toFixed(1)` avec une virgule (Q-01) ; gourdes `Math.round` puis espace comme séparateur des milliers (H-02, Q-07).
- Un nouveau chargement remplace toutes les données (P-09). Pas de `localStorage`, pas d'édition, pas d'export (P-08, P-10).

## Checklist de sortie (DoD)

- [ ] `index.html` existe (ou son absence est justifiée) et passe **tous** les CA du Sprint 01, fuseau Haïti (Q-09) compris.
- [ ] `git diff --exit-code version-ia -- Groupe_01_Cas_01/prototype/version_IA.html` ne renvoie rien : la version brute est intacte.
- [ ] Chaque correction a son E-xx, son commit et son CA.
- [ ] Au moins une proposition de l'IA corrigée ou rejetée est documentée, avec sa raison (C-08).
- [ ] Aucune fonction hors Sprint 01 ; aucune ressource externe. Tolérer tout espace de noms `http://www.w3.org/…` (svg, xlink, xhtml) ; rechercher aussi `//`, `@import`, `url(`, `fetch(`, `XMLHttpRequest` et `src=`. En PowerShell : `Select-String -Path .\Groupe_01_Cas_01\prototype\index.html -Pattern '(https?:)?//(?!www\.w3\.org/)[a-z0-9.-]+\.[a-z]{2,}|@import|fetch\(|XMLHttpRequest|WebSocket'`, puis examiner chaque ligne trouvée.

## Interdits

- Modifier `version_IA.html`.
- Réécrire `index.html` de zéro « parce que c'est plus simple ». On corrige l'existant.
- Implémenter l'US-04 (tableau) ou l'US-05 (graphique) dans le Sprint 01, même si l'IA le propose.

## Prompt d'amorçage spécifique

```
Mission R5 (corrections) : corrige Groupe_01_Cas_01/prototype/index.html pour l'écart E-<n> uniquement.
CA concerné : <CA>. Valeur attendue (docs/oracle.md) : <valeur>. Observé : <valeur>.
Propose la modification minimale (diff), sans rien ajouter d'autre, en respectant AGENTS.md §3, §4 et §7.
Ne touche jamais version_IA.html.
```

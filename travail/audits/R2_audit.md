# Audit d'entrée : relais R2 (Leddycia, Claude Code / Claude Opus 5.5, 2026-10-18 10:49)

## Livrable audité : socle de R1 (`docs/brief_client.md`, `docs/consignes.md`, `docs/oracle.md`, `docs/energie_college.csv`, `travail/decisions.md`) et complément de R1 (`agents/00_protocole_relais.md` v2)

| # | Constat | Preuve (fichier:ligne, B/C/CA) | Gravité (conforme / à corriger / bloquant) | Action (corrigé / laissé / remonté) |
|---|---|---|---|---|
| 1 | Au démarrage, le complément de R1 n'était pas clôturé : ETAT §8 rempli, 12 fichiers modifiés non commités, `agents/00_protocole_relais.md` non suivi, session R1 encore active dans le même dossier. Un `git add -A` de sa passation aurait embarqué les fichiers de R2. | `git status` à 10:49 ; ETAT §8 (version d'avant 11:37) ; protocole §2.1 | bloquant (pour toute écriture) | laissé : audit en lecture seule, brouillons hors du dépôt ; levé à 11:37 (complément de R1 poussé) |
| 2 | `main` local en retard d'un commit : a468c31 (modification d'ETAT §2 sur le web, R2 attribué à Leddycia), sur la ligne voisine de celle modifiée par R1 : conflit probable. | `git rev-list --left-right --count main...origin/main` → `0 1` | à corriger | remonté à R1, qui l'a intégré en gardant les deux apports (`R1_audit.md`) |
| 3 | R2 est tenu par le membre de R1, qui a validé l'oracle ; `AGENTS.md` §6 affiche les valeurs : le recalcul A3 ne peut plus être indépendant. | a468c31 ; ETAT §2 ; `AGENTS.md` §6 | à corriger | remonté (voir aussi #6) |
| 4 | A1 : diff mot à mot du texte extrait du `.docx` (corps et pied de page) contre `docs/brief_client.md` : aucun mot ajouté ni retiré. Seuls écarts : puces Markdown, numéros 1. à 4. (numérotation automatique de Word), libellé « Pied de page de l'original » (ajout déclaré). | diff produit hors du dépôt (27 écarts, tous de mise en forme) | conforme | laissé |
| 5 | A2 : diff mot à mot du texte extrait du PDF (`pdftotext`) contre `docs/consignes.md` : aucun mot ajouté ni retiré. Seuls écarts : puces, ordre de lecture du tableau d'en-tête, espaces induits par le gras, libellé du pied de page. Règle de taille du Sprint 01 (C-07) et arborescence des livrables (C-01) identiques. | diff produit hors du dépôt (38 écarts, tous de mise en forme) | conforme | laissé |
| 6 | A3 : la contre-vérification humaine n'a pas été faite, par décision de Leddycia (JP-12). Elle est remplacée par trois recalculs automatiques indépendants (Python en décimal exact, awk sur les lignes re-triées, PowerShell `Import-Csv`) et une comparaison automatique avec les tableaux de l'oracle : **aucun écart** (§1, §2.1, §2.2, §3, §4, §5 et les 36 lignes du §6). | annexes A et B ; D-15 | à corriger (écart à la fiche 01, A3) | remonté : D-15 dans `decisions.md` ; limite : même outil et même modèle que R1 |
| 7 | A4 : empreinte SHA-256 du CSV conforme ; `.gitattributes` présent (`docs/energie_college.csv -text`). 727 octets, 37 CRLF, ASCII sans BOM. | `Get-FileHash` → `True` | conforme | laissé |
| 8 | A5 : `decisions.md` cohérent avec `AGENTS.md` : Sprint 01 = US-01 à US-03 (D-01) ; Q-01 à Q-14 « provisoire » ou « ouvert », jamais présentées comme règles du client. | `travail/decisions.md` §1 (D-01) et §2 | conforme | laissé |
| 9 | Liste indicative de la fiche 01 : EF-01 cite C-12 (le libellé « Choisir un fichier » vient des consignes) ; ENF-03 et ENF-04 doublent RM-03 et RM-04 (B-14, B-15) ; le message de fichier invalide (Q-04) pouvait devenir une exigence. | `agents/01_analyste_cdc.md`, liste indicative et note Q-04 | à corriger | corrigé dans le CDC (arbitrages validés par Leddycia) : EF-01 = B-06 ; libellé en CT-03 ; B-14 et B-15 seulement en RM ; Q-04 seulement au §11 ; la fiche n'est pas modifiée |
| 10 | B-14 dit « les litres peuvent avoir une décimale » ; `AGENTS.md` R-04 et la fiche 01 (ENF-04) écrivent « au plus une décimale », l'index non normatif du brief « une décimale au plus ». | `docs/brief_client.md` B-14 ; `AGENTS.md` §4 ; fiche 01 | à corriger | remonté : le CDC garde le texte du client et renvoie le format exact à Q-01 ; à trancher par l'équipe dans `decisions.md` |
| 11 | La DoD de la fiche 01 admet une CT citant un B-xx (« contrainte du client »), alors que sa structure (§7) réserve les CT aux contraintes du projet. | `agents/01_analyste_cdc.md`, structure §7 et checklist de sortie | à corriger (mineur) | remonté ; le CDC suit la structure (CT = C-xx seulement ; B-16 et B-17 = ENF) |
| 12 | Relecture du protocole v2 (demandée par R1, JP-08) : lisible et cohérent avec la fiche 01 ; trois manques mineurs (voir section dédiée). | `agents/00_protocole_relais.md` | à corriger (mineur) | remonté |

## Ce qui a été seulement survolé ; résultats donnés par le membre

- **A1 et A2** : l'IA a produit les diffs mot à mot (aucun écart de texte). Le contrôle humain des passages normatifs (B-09 à B-20.4, B-25 à B-27 ; C-01, C-07 à C-12, C-15, C-19, C-20) a été annoncé par Leddycia ; son résultat n'a pas été communiqué à l'IA.
- **A3** : aucun total donné par le membre (« Je ne fais pas de recalcul. Assure-toi que le calcul est le bon », JP-12). Recalcul automatique : août 12 jours, 24 h, 71 L, 21 300 gourdes, jour max 2026-08-06 (5 h, égalité avec le 12/08) ; septembre 12 jours, 30 h, 84 L, 25 200 gourdes, jour max 2026-09-08 (5 h, égalité avec le 09/09 et le 11/09) ; octobre 12 jours, 43 h, 125 L, 37 500 gourdes, jour max 2026-10-02 ; toute la période 36 jours, 97 h, 280 L, 84 000 gourdes, jour max 2026-08-06. Bug de fuseau simulé (« Haiti Standard Time ») : août 26 h / 77 L, septembre 32 h / 90 L, octobre 39 h / 113 L, identiques à l'oracle §5.

## Relecture du protocole de relais v2

- **Conforme** : contrôle d'ETAT §8 avant l'audit (§2.1), synchronisation (§2.2), fichiers temporaires hors du dépôt (§3.5), Git en deux blocs (§4.7) ; la procédure de la fiche 01 (passation par « fin de notre relais ») est cohérente.
- **Manque 1** : aucun cas pour un relais précédent **encore actif dans une autre session du même dossier** (cas réel de ce relais) : §2.1 suppose que le membre clôture ou archive. Proposition : audit en lecture seule et aucune écriture avant le push de l'autre session.
- **Manque 2** : §2.3, étape 3, prévoit les « totaux du recalcul A3 » donnés par le membre, sans dire quoi faire s'il refuse le recalcul (cas réel : D-15).
- **Manque 3** : le protocole ne dit pas où consigner un point non fixé par le client qui n'est pas retenu comme Q-xx (cas réel : les 12 points ci-dessous). Ce rapport sert de lieu de renvoi.

## Corrections apportées (une ligne par correction)

- Aucune correction des fichiers de R1 (RG-10). Les écarts à la liste indicative de la fiche 01 sont appliqués dans le seul cahier des charges (#9).

## Points remontés à l'équipe (decisions.md, ETAT_PROJET.md)

- **D-15** (validé, Leddycia, JP-12) : contre-vérification humaine A3 remplacée par un recalcul automatique indépendant.
- **Q-15 à Q-17** (provisoires, Leddycia, JP-13) : périmètre du tableau jour par jour, format des heures, affichage du jour maximal.
- **B-14 et R-04** (#10) et **DoD de la fiche 01** (#11) : à trancher par l'équipe.
- **Relecture humaine mot à mot du CDC** : annoncée par Leddycia, non confirmée à la clôture ; à faire par R3 dans son audit d'entrée (fiche 02, A2 à A6).
- **O-2** : membre de R3 = Leddycia (réponse du membre à la passation) ; R4 à R6 à compléter.
- **Points non fixés par le client, non retenus comme Q-xx, renvoyés à R3 et R4** (JP-13) :

| # | Point | À traiter par |
|---|---|---|
| 1 | Colonnes du tableau jour par jour : toutes celles de B-19, y compris `heures_solaire` ? | R3 (CA de l'US-04) |
| 2 | Ordre des lignes du tableau jour par jour : chronologique ou ordre du fichier ? | R3 (CA de l'US-04) |
| 3 | Litres (valeur ou total) à plus d'une décimale : valeur valide ? arrondi d'affichage ? (Q-01, Q-07) | R4 (fixture f05) |
| 4 | « Toute la période » pour un autre fichier = toutes les lignes chargées (lecture du CDC §4, glossaire d'`AGENTS.md`) | R3 (CA de l'US-01) |
| 5 | Nouveau fichier chargé : remplacement complet des données précédentes, sans cumul (piège P-09) | R3 (CA de l'US-01), R4 |
| 6 | Fichier d'un autre nom ou d'une autre taille que l'échantillon fourni (recopie hebdomadaire, B-03) | R3 et R4 (fixtures) |
| 7 | Ligne d'en-tête obligatoire, ordre des colonnes, point comme séparateur décimal (Q-04) | R4 (fixture f02) |
| 8 | Fichier sans ligne de données (en-tête seul ou vide) : invalide au sens de Q-04 ? | R4 (fixture) |
| 9 | Date d'un jour non ouvrable (samedi, dimanche, jour férié) : ligne valide ? (Q-04) | R4 (fixture) |
| 10 | Fichier séparé par des virgules mais précédé d'un BOM : accepté ou rejeté ? (précision de Q-10, à faire dans `decisions.md` avant le prompt) | R4 |
| 11 | Rappel du prix de référence et de « pas un prix officiel » (B-12) à côté du coût | R3 (CA de l'US-02) |
| 12 | Poste de consultation de la directrice : le même ordinateur que l'intendance ? (Q-09) | R4 et R5 (tests) |

## Ce que j'ai produit pendant mon relais

- `Groupe_01_Cas_01/cahier_des_charges.md` v1 (rédigé par un workflow de 9 agents hors du dépôt, puis contrôlé par script).
- `travail/decisions.md` : D-15, Q-15 à Q-17 et leurs lignes au journal des changements.
- `travail/journal_prompts.md` : JP-10 à JP-14 ; `travail/journal_ecarts.md` : E-14 à E-19.
- `ETAT_PROJET.md` tenu à jour pendant le relais (§1, §2, §8), puis passation (§1 à §8).
- Ce rapport, avec la relecture du protocole v2 et les scripts du recalcul A3 en annexe.

## Journal de bord du relais (copie intégrale d'ETAT §8, ajoutée à la passation)

> Rempli automatiquement selon `agents/00_protocole_relais.md`. Vidé à « fin de notre relais ».

| Relais | Membre | Outil et modèle | Fiche | Porte visée | Début |
|---|---|---|---|---|---|
| R2 | Leddycia | Claude Code (application de bureau, Claude Opus 5.5) | `agents/01_analyste_cdc.md` | G2 | 10:49 |

**Plan validé** (JP-11) : 1. audit d'entrée A1 à A5 en lecture seule (fait avant la validation) ; 2. contrôle mot à mot de A1 et A2 et recalcul A3 par Leddycia ; 3. en parallèle, brouillon du cahier des charges hors du dépôt, relu par Leddycia ; 4. dès que le complément de R1 est poussé : `git pull`, R2 EN COURS, CDC placé dans `Groupe_01_Cas_01/`, JP-xx et E-xx ; 5. contrôle de la DoD de la fiche 01 ; 6. « fin de notre relais ».

**Audit d'entrée (synthèse)** (détail : `travail/audits/R2_audit.md`) :
- Complément de R1 non clôturé au démarrage (ETAT §8 rempli, 12 fichiers modifiés non commités) | `git status`, ETAT §8 | bloquant pour l'écriture ; levé à 11:37 (complément de R1 poussé).
- `main` local en retard d'un commit (a468c31, modifié sur le web) | `git rev-list` | à corriger ; intégré par R1.
- R2 tenu par le membre de R1, qui a validé l'oracle : recalcul A3 non indépendant | a468c31, `AGENTS.md` §6 | remonté.
- A1 et A2 : diff mot à mot `.docx` et PDF contre les transcriptions : aucun mot ajouté ni retiré (mise en forme seulement) | diff hors du dépôt | conforme.
- A3 : recalcul humain non fait (décision de Leddycia, D-15) ; remplacé par trois recalculs automatiques indépendants et une comparaison automatique avec l'oracle §1 à §6 : aucun écart | JP-12 | à corriger, remonté.
- A4 : empreinte du CSV conforme, `.gitattributes` présent | `Get-FileHash` → `True` | conforme.
- A5 : `decisions.md` cohérent avec `AGENTS.md` (Sprint 01 = US-01 à US-03 ; Q-xx jamais présentées en règles) | `decisions.md` §1 et §2 | conforme.
- Liste indicative de la fiche 01 : EF-01 cite C-12 ; ENF-03 et ENF-04 doublent RM-03 et RM-04 ; Q-04 présentable en exigence | `agents/01_analyste_cdc.md` | à corriger dans le CDC (arbitrages validés).
- Survolé : le contrôle mot à mot humain de A1 et A2 a été annoncé par Leddycia ; son résultat n'a pas été communiqué à l'IA. Résultats du membre : aucun total (A3 non fait, D-15).

**Journal de bord**

| Heure | Étape | Ce qui a été fait | Fichiers | État |
|---|---|---|---|---|
| 10:49 | 1 | (JP-10) Audit d'entrée A1 à A5 en lecture seule : diffs `.docx` et PDF, empreinte du CSV, cohérence des décisions, état Git ; rapport et plan présentés | aucun fichier du dépôt | fait |
| 10:56 | 3 | (JP-11) Brouillon du CDC lancé hors du dépôt : workflow Claude Code de 9 agents (2 brouillons, synthèse, 5 vérificateurs, correction) | dossier temporaire | fait |
| 11:03 | 2 | (JP-12, D-15) A3 : Leddycia ne fait pas le recalcul ; trois recalculs automatiques indépendants (Python, awk, PowerShell) et comparaison automatique avec l'oracle §1 à §6 : aucun écart | scripts hors du dépôt (annexe de `R2_audit.md`) | fait |
| 11:32 | 3 | Brouillon reçu : 35 constats des vérificateurs, 29 appliqués, 6 rejetés ; contrôles par script (citations, chiffres, termes techniques, tableaux, couverture) ; mention « à soumettre au client » retirée du §11.2 (E-19) | dossier temporaire | fait |
| 11:39 | 3 | (JP-13) Q-15 à Q-17 intégrées au brouillon (§4, §6, §11.1, §12.1) | dossier temporaire | fait |
| 11:41 | 4 | Complément de R1 poussé (11:37) ; dépôt à jour ; R2 EN COURS ; rapport d'audit créé | `ETAT_PROJET.md`, `travail/audits/R2_audit.md` | fait |
| 11:43 | 4 | Cahier des charges v1 placé ; D-15 et Q-15 à Q-17 consignées ; JP-10 à JP-13 ; E-14 à E-19 ; scripts du recalcul A3 en annexe de l'audit | `Groupe_01_Cas_01/cahier_des_charges.md`, `travail/decisions.md`, `travail/journal_prompts.md`, `travail/journal_ecarts.md`, `travail/audits/R2_audit.md` | fait |
| 11:45 | 5 | Contrôle de la DoD de la fiche 01 et d'`AGENTS.md` §12 par script : 5 rubriques de C-20, source B-xx de chaque EF, ENF et RM, C-xx de chaque CT, matrice B-01 à B-27, B-21 à B-27 mot pour mot, Q-01 à Q-17 avec statuts identiques à `decisions.md`, aucune valeur de l'oracle, termes techniques limités aux CT : conforme. Relecture humaine mot à mot du CDC : à confirmer par Leddycia | `Groupe_01_Cas_01/cahier_des_charges.md` | fait |
| 11:46 | 6 | (JP-14) « fin de notre relais » : passation complète (protocole §4) ; membre de R3 indiqué par Leddycia : Leddycia | `ETAT_PROJET.md`, `travail/audits/R2_audit.md`, `travail/journal_prompts.md` | fait |

**Points ouverts du relais** :
- 12 points non fixés par le client, renvoyés à R3 et R4 (liste : `travail/audits/R2_audit.md`).
- B-14 : le CDC garde le texte du client (« les litres peuvent avoir une décimale ») ; `AGENTS.md` R-04 et la fiche 01 écrivent « au plus une décimale ». À trancher par l'équipe (`decisions.md`), sans correction silencieuse.
- Fiche 01 : sa DoD admet une CT citant un B-xx, alors que sa structure (§7) réserve les CT aux consignes. Le CDC suit la structure.
- O-2 : membres de R3 à R6 à compléter au §2 (nécessaire pour le message de passation).

## Annexes : scripts du recalcul A3 (D-15)

Exécutés le 2026-10-18 hors du dépôt, en lecture seule, avec Python 3.14 (`python -I -X utf8 <script> docs/energie_college.csv [docs/oracle.md]`, depuis la racine du dépôt). Méthodes 2 et 3, lancées en ligne de commande :

- **awk** (Git Bash) : `tail -n +2 docs/energie_college.csv | tr -d '\r' | sort -t, -k1,1 | awk -F, '{m=substr($1,1,7); h[m]+=$3; l[m]+=$4; n[m]++; if(!(m in mx) || $3>mx[m]){mx[m]=$3; jd[m]=$1}; H+=$3; L+=$4; N++; if(N==1 || $3>MX){MX=$3; JD=$1}} END{for(m in h) printf "%s jours=%d heures=%g litres=%g cout=%g max=%g jour=%s\n", m, n[m], h[m], l[m], l[m]*300, mx[m], jd[m]; printf "TOUT jours=%d heures=%g litres=%g cout=%g max=%g jour=%s\n", N, H, L, L*300, MX, JD}'`
- **PowerShell** : `Import-Csv`, valeurs converties en `[decimal]` (culture invariante), lignes triées par date, nouveau maximum retenu seulement s'il est strictement plus grand ; bug de fuseau simulé par `[TimeZoneInfo]::ConvertTimeFromUtc` avec le fuseau « Haiti Standard Time ».

### Annexe A : `recalcul_oracle.py` (méthode 1, Python en décimal exact)

```python
"""Audit A3 (R2) : recalcul indépendant de l'oracle, méthode 1 (Python, Decimal). Lecture seule."""
import csv
import hashlib
import sys
from datetime import date, datetime, timedelta, timezone
from decimal import Decimal

path = sys.argv[1]
raw = open(path, "rb").read()
crlf = raw.count(b"\r\n")
print("sha256", hashlib.sha256(raw).hexdigest())
print("octets", len(raw), "| CRLF", crlf, "| LF seuls", raw.count(b"\n") - crlf, "| BOM", raw[:3] == b"\xef\xbb\xbf",
      "| ASCII", all(b < 128 for b in raw), "| finit par CRLF", raw.endswith(b"\r\n"))

with open(path, newline="", encoding="ascii") as f:
    rows = list(csv.DictReader(f))
print("lignes de données", len(rows), "| en-tête", list(rows[0].keys()))

recs = []
for r in rows:
    y, m, d = map(int, r["date"].split("-"))
    recs.append({"ds": r["date"], "date": date(y, m, d), "hs": Decimal(r["heures_solaire"]),
                 "hg": Decimal(r["heures_generatrice"]), "l": Decimal(r["litres_carburant"])})

ds = [r["ds"] for r in recs]
print("trié", ds == sorted(ds), "| doublons", len(ds) - len(set(ds)),
      "| week-ends", [r["ds"] for r in recs if r["date"].weekday() >= 5])
print("litres décimaux", [(r["ds"], str(r["l"])) for r in recs if r["l"] != r["l"].to_integral_value()])
print("incohérences heures/litres", [r["ds"] for r in recs if (r["hg"] == 0) != (r["l"] == 0)])
ratios = [r["l"] / r["hg"] for r in recs if r["hg"]]
print("ratio litres/heure min", min(ratios), "max", max(ratios))

PERIODES = {"Août 2026": "2026-08", "Septembre 2026": "2026-09", "Octobre 2026": "2026-10", "Toute la période": ""}
for nom, prefixe in PERIODES.items():
    sel = sorted((r for r in recs if r["ds"].startswith(prefixe)), key=lambda r: r["ds"])
    hg = sum(r["hg"] for r in sel)
    litres = sum(r["l"] for r in sel)
    hmax = max(r["hg"] for r in sel)
    egalites = [r["ds"] for r in sel if r["hg"] == hmax]
    zeros = [r["ds"][5:] for r in sel if r["hg"] == 0]
    print(f"{nom}: jours={len(sel)} du {sel[0]['ds']} au {sel[-1]['ds']} | heures={hg} | litres={litres} "
          f"| coût={litres * 300} | max={hmax} h, premier={egalites[0]} | égalités={egalites} | jours à 0 h={len(zeros)} {zeros}")

# Piège P-01 : date lue comme minuit UTC, puis rangée dans le mois local à UTC-5.
tz = timezone(timedelta(hours=-5))
bug = {}
for r in recs:
    local = datetime(r["date"].year, r["date"].month, r["date"].day, tzinfo=timezone.utc).astimezone(tz)
    cle = f"{local.year}-{local.month:02d}"
    acc = bug.setdefault(cle, [Decimal(0), Decimal(0), 0])
    acc[0] += r["hg"]
    acc[1] += r["l"]
    acc[2] += 1
print("signature du bug de fuseau (mois: heures, litres, jours):",
      {k: (str(v[0]), str(v[1]), v[2]) for k, v in sorted(bug.items())})

print("détail jour par jour (date, solaire, génératrice, litres) :")
for r in recs:
    print(f"  {r['ds']} {r['hs']} {r['hg']} {r['l']}")
```

### Annexe B : `comparer_oracle.py` (comparaison automatique avec `docs/oracle.md`)

```python
"""Audit A3 (R2) : comparaison automatique de docs/oracle.md (§2.1, §2.2, §3, §6) avec le CSV. Lecture seule."""
import csv
import re
import sys
from decimal import Decimal

csv_path, oracle_path = sys.argv[1], sys.argv[2]
with open(csv_path, newline="", encoding="ascii") as f:
    rows = {r["date"]: r for r in csv.DictReader(f)}
oracle = open(oracle_path, encoding="utf-8").read()
ecarts = []


def fr(d):  # 2026-08-03 -> 03/08/2026
    y, m, j = d.split("-")
    return f"{j}/{m}/{y}"


def litres_affiches(v):
    return f"{Decimal(v).quantize(Decimal('0.1'))}".replace(".", ",")


def milliers(n):
    return f"{int(n):,}".replace(",", " ")


# §6 : détail jour par jour
lignes6 = re.findall(r"^\| (\d+) \| (2026-\d\d-\d\d) \| (\S+) \| (\S+) \| (\S+) \| (\S+) \| (\S+) \|$", oracle, re.M)
print("§6 : lignes lues dans l'oracle :", len(lignes6))
for num, d, aff, hs, hg, l, laff in lignes6:
    r = rows.get(d)
    if r is None:
        ecarts.append(f"§6 {d} absent du CSV")
        continue
    attendu = (fr(d), r["heures_solaire"], r["heures_generatrice"], r["litres_carburant"], litres_affiches(r["litres_carburant"]))
    if (aff, hs, hg, l, laff) != attendu:
        ecarts.append(f"§6 {d} : oracle {(aff, hs, hg, l, laff)} ≠ CSV {attendu}")
manquantes = set(rows) - {d for _, d, *_ in lignes6}
if manquantes:
    ecarts.append(f"§6 : dates du CSV absentes de l'oracle : {sorted(manquantes)}")
nums = [int(n) for n, *_ in lignes6]
if nums != list(range(1, 37)):
    ecarts.append(f"§6 : numérotation non continue : {nums}")

# Totaux recalculés
PER = {"Août 2026": "2026-08", "Septembre 2026": "2026-09", "Octobre 2026": "2026-10", "Toute la période": ""}
calc = {}
for nom, p in PER.items():
    sel = sorted((r for d, r in rows.items() if d.startswith(p)), key=lambda r: r["date"])
    hs = sum(Decimal(r["heures_solaire"]) for r in sel)
    hg = sum(Decimal(r["heures_generatrice"]) for r in sel)
    l = sum(Decimal(r["litres_carburant"]) for r in sel)
    mx = max(Decimal(r["heures_generatrice"]) for r in sel)
    jour = next(r["date"] for r in sel if Decimal(r["heures_generatrice"]) == mx)
    calc[nom] = dict(jours=len(sel), hs=hs, hg=hg, l=l, cout=l * 300, jour=jour, mx=mx, premier=sel[0]["date"], dernier=sel[-1]["date"])

# §6 : lignes de totaux par mois et total général
for nom, tot in zip(["Août 2026", "Septembre 2026", "Octobre 2026"],
                    re.findall(r"\| \| \*\*Total\*\* \| \| \*\*(\S+)\*\* \| \*\*(\S+)\*\* \| \*\*(\S+)\*\* \| \*\*(\S+)\*\* \|", oracle)):
    c = calc[nom]
    if tot != (str(c["hs"]), str(c["hg"]), str(int(c["l"])), litres_affiches(c["l"])):
        ecarts.append(f"§6 total {nom} : oracle {tot} ≠ calcul {(c['hs'], c['hg'], c['l'])}")
m = re.search(r"\*\*Toute la période\*\* : (\d+) heures solaires, (\d+) heures de génératrice, (\d+) litres", oracle)
c = calc["Toute la période"]
if not m or m.groups() != (str(c["hs"]), str(c["hg"]), str(int(c["l"]))):
    ecarts.append(f"§6 toute la période : oracle {m and m.groups()} ≠ calcul {(c['hs'], c['hg'], c['l'])}")

# §2.1 valeurs brutes
for nom in PER:
    c = calc[nom]
    motif = re.escape(nom).replace(r"\ ", " ")
    m = re.search(rf"^\| (?:\*\*)?{motif}(?:\*\*)? \| (?:\*\*)?(\d+)(?:\*\*)? \| (?:\*\*)?(\d+)(?:\*\*)? \| (?:\*\*)?(\d+)(?:\*\*)? \| (?:\*\*)?([\d ]+)(?:\*\*)? \| (?:\*\*)?(2026-\d\d-\d\d)(?:\*\*)? \| (?:\*\*)?(\d+)(?:\*\*)? \|$", oracle, re.M)
    attendu = (str(c["jours"]), str(c["hg"]), str(int(c["l"])), milliers(c["cout"]), c["jour"], str(c["mx"]))
    if not m or m.groups() != attendu:
        ecarts.append(f"§2.1 {nom} : oracle {m and m.groups()} ≠ calcul {attendu}")

# §2.2 affichage attendu
for nom in PER:
    c = calc[nom]
    m = re.search(rf"^\| {re.escape(nom)} \| (\d+) h \| ([\d,]+) L \| ([\d ]+) gourdes \| (\S+) \((\d+) h\) \|$", oracle, re.M)
    attendu = (str(c["hg"]), litres_affiches(c["l"]), milliers(c["cout"]), fr(c["jour"]), str(c["mx"]))
    if not m or m.groups() != attendu:
        ecarts.append(f"§2.2 {nom} : oracle {m and m.groups()} ≠ calcul {attendu}")

# §3 couverture (recherche limitée à la section 3 : les noms de période apparaissent aussi au §2.1)
section3 = oracle[oracle.index("## 3. "):oracle.index("## 4. ")]
for nom in PER:
    c = calc[nom]
    m = re.search(rf"^\| {re.escape(nom)} \| (\S+) \| (\S+) \| (\d+) \|", section3, re.M)
    attendu = (fr(c["premier"]), fr(c["dernier"]), str(c["jours"]))
    if not m or m.groups() != attendu:
        ecarts.append(f"§3 {nom} : oracle {m and m.groups()} ≠ calcul {attendu}")

print("Contrôles §2.1, §2.2, §3, §6 :", "AUCUN ÉCART" if not ecarts else "\n".join(ecarts))
```

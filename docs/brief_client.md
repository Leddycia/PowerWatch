# Brief client, cas 01 : PowerWatch (transcription)

> **Transcription fidèle** de `docs/01_Demande_client.docx`. En cas de doute, **l'original fait foi**.
> Seuls ajouts : le titre et cet encadré d'en-tête de la transcription, les identifiants **`[B-xx]`** en gras, qui permettent de citer chaque élément du brief (traçabilité exigée par la consigne C-02), le libellé « Pied de page de l'original » devant le texte du pied de page, et l'index rapide en fin de fichier, qui n'est qu'un résumé non normatif (seul le texte du client fait foi). Le texte du client n'a pas été reformulé. Seules les apostrophes typographiques ont été remplacées par des apostrophes droites.
> Fichier en lecture seule : on ne le modifie que pour corriger une erreur de transcription, et on le signale dans le rapport d'audit.

---

**CAS 01 : POWERWATCH**
**Demande du client**
*Collège Les Palmistes*

## Notre organisation et notre besoin

**[B-01]** Le Collège Les Palmistes accueille environ 600 élèves. Comme le courant du réseau public est irrégulier, l'établissement utilise des panneaux solaires et, lorsque cela ne suffit pas, une génératrice diesel. **[B-02]** Chaque jour ouvrable, le gardien note dans un registre papier le nombre d'heures de fonctionnement des panneaux solaires, le nombre d'heures de fonctionnement de la génératrice et la quantité de carburant consommée.

**[B-03]** Chaque semaine, l'intendant recopie ce registre dans un fichier CSV. **[B-04]** La directrice souhaite disposer d'un petit tableau de bord pour suivre la consommation de la génératrice et son coût, afin de préparer le budget et de discuter avec le conseil d'administration de l'installation de panneaux supplémentaires.

## Les personnes concernées

- **[B-05a]** **La directrice :** consulte le tableau de bord pour suivre la consommation et le coût.
- **[B-05b]** **L'intendant :** charge le fichier CSV dans l'outil et vérifie les chiffres.
- **[B-05c]** **Le gardien :** tient le registre papier ; il n'utilise pas l'outil.

## Ce que nous attendons de l'outil

L'outil doit permettre de :

- **[B-06]** charger le fichier CSV fourni par l'intendant ;
- **[B-07]** afficher, pour la période choisie, le total des heures de génératrice et le total des litres de carburant consommés ;
- **[B-08]** afficher le coût estimé du carburant pour la période ;
- **[B-09]** choisir un mois (août, septembre ou octobre 2026) ou afficher toute la période ;
- **[B-10]** afficher le jour où la génératrice a fonctionné le plus longtemps sur la période choisie ;
- **[B-11]** afficher les données sous forme de tableau, jour par jour.

## Les règles à respecter

- **[B-12]** Le coût estimé du carburant se calcule ainsi : litres consommés × 300 gourdes. Ce prix de référence est fixé par l'intendance pour ce suivi ; il ne s'agit pas d'un prix officiel.
- **[B-13]** Si plusieurs jours ont le même nombre maximal d'heures de génératrice, l'outil affiche le premier de ces jours dans l'ordre chronologique.
- **[B-14]** Les montants sont affichés en gourdes, sans décimale ; les litres peuvent avoir une décimale.
- **[B-15]** Les données du fichier ne doivent pas être modifiées par l'outil.

## Nos contraintes

- **[B-16]** L'outil sera utilisé sur l'ordinateur du bureau de l'intendance, où la connexion Internet n'est pas toujours disponible : il doit fonctionner sans Internet.
- **[B-17]** Aucun compte utilisateur n'est nécessaire pour cette première version.

## Les données fournies

**[B-18]** Le fichier energie_college.csv contient un échantillon de 36 jours ouvrables (12 par mois), du 3 août au 16 octobre 2026 ; les données d'octobre s'arrêtent donc au 16 octobre. Les colonnes sont séparées par des virgules ; les valeurs sont écrites sans accents pour éviter les problèmes d'encodage.

**[B-19]**

| Colonne | Signification |
|---|---|
| date | date du jour au format AAAA-MM-JJ |
| heures_solaire | nombre d'heures de fonctionnement des panneaux solaires |
| heures_generatrice | nombre d'heures de fonctionnement de la génératrice |
| litres_carburant | litres de carburant consommés par la génératrice |

## Nos priorités pour la première version

Par ordre d'importance :

1. **[B-20.1]** Voir le total des heures de génératrice et des litres consommés pour un mois donné.
2. **[B-20.2]** Connaître le coût estimé du carburant pour ce mois.
3. **[B-20.3]** Repérer le jour où la génératrice a le plus fonctionné.
4. **[B-20.4]** Consulter le détail jour par jour.

Nous aimerions aussi, plus tard :

- **[B-21]** afficher un graphique en barres des heures de génératrice par mois ;
- **[B-22]** comparer deux mois côte à côte ;
- **[B-23]** afficher la part des heures solaires par rapport aux heures de génératrice ;
- **[B-24]** recevoir une alerte par SMS lorsque la consommation du mois dépasse un seuil.

## Ce qui ne fait pas partie de la première version

- **[B-25]** la connexion directe à la génératrice ou à un compteur électrique ;
- **[B-26]** la saisie des données dans l'outil (le CSV reste la seule source) ;
- **[B-27]** la gestion de comptes et de mots de passe.

---

*Pied de page de l'original : « IA générative appliquée aux projets technologiques | Projet final | Cas 01 : PowerWatch ».*

## Index rapide des identifiants

| ID | Thème | ID | Thème |
|---|---|---|---|
| B-01 | Contexte : collège, solaire et génératrice | B-14 | Règle : formats (montants en gourdes sans décimale ; litres : une décimale au plus) |
| B-02 | Relevé quotidien du gardien | B-15 | Règle : données non modifiées |
| B-03 | Recopie hebdomadaire du registre dans un CSV par l'intendant | B-16 | Contrainte : sans Internet |
| B-04 | Objectif : suivi, budget, conseil d'administration | B-17 | Contrainte : sans compte |
| B-05a/b/c | Acteurs : directrice, intendant, gardien | B-18 | Données : échantillon de 36 jours, virgules, sans accents |
| B-06 | Charger le CSV | B-19 | Données : colonnes |
| B-07 | Totaux heures et litres pour la période | B-20.1 à B-20.4 | Priorités V1, dans l'ordre |
| B-08 | Coût estimé pour la période | B-21 | Plus tard : graphique en barres |
| B-09 | Choix mois / toute la période | B-22 | Plus tard : comparaison de deux mois |
| B-10 | Jour de fonctionnement maximal | B-23 | Plus tard : part solaire / génératrice |
| B-11 | Tableau jour par jour | B-24 | Plus tard : alerte SMS |
| B-12 | Règle : coût = litres × 300 gourdes | B-25 à B-27 | Hors V1 : connexion matérielle, saisie, comptes |
| B-13 | Règle : égalité, premier jour chronologique | | |

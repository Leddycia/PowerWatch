# Product Backlog : PowerWatch

> **Objet** : découper en user stories la première version (V1) décrite dans le cahier des charges, les ordonner, et fixer pour chacune des critères d'acceptation (CA) observables et vérifiables. Les CA du Sprint 01 servent de contrat à l'IA chargée du prototype (C-08) et de grille de vérification (C-15).
>
> **Sources**, citées à chaque élément :
> - **B-xx** : brief du client (`docs/brief_client.md`) ; **C-xx** : consignes du cours (`docs/consignes.md`) ;
> - **EF, ENF, RM, CT** : exigences, règles et contraintes du `cahier_des_charges.md` ;
> - **D-xx, Q-xx, H-xx** : décisions, questions au client et choix de présentation de l'équipe (cahier des charges §11 ; registre de l'équipe).
>
> **Version** : v1 du 2026-10-18, rédigée au relais R3 (Groupe 01, cas 01).
>
> **Règles de lecture** :
> - chaque CA suit le format « Étant donné… quand… alors… » et décrit ce que l'on voit à l'écran, jamais la façon de le programmer ;
> - **fichier de référence** : `energie_college.csv`, fourni par le client (B-18) ; les **valeurs attendues** ont été calculées par l'équipe sur ce fichier, indépendamment de l'IA chargée du prototype (oracle de l'équipe, hors livrable) ; un CA ne dit jamais « le bon total » mais la valeur exacte ;
> - quand un CA dépend d'un point que le client n'a pas fixé, il cite la Q-xx : c'est une **hypothèse provisoire**, appliquée en attendant la réponse du client, **jamais une règle du client** ;
> - formats appliqués par les CA : heures suivies de « h » (Q-16) ; litres toujours avec une décimale et la virgule, suivis de « L » (Q-01) ; montants sans décimale, espace des milliers, suivis de « gourdes » (B-14, H-02) ; dates JJ/MM/AAAA (H-01) ; libellés des périodes de H-04 ;
> - les **fichiers de test** cités (lignes mélangées, colonne manquante, etc.) sont des fichiers fictifs préparés par l'équipe à partir du format de B-18 et B-19 (C-13) ;
> - le MoSCoW porte sur la **V1** ; le Sprint 01 n'en réalise qu'une partie (C-07).

---

## 1. Vue d'ensemble

| Ordre | ID | Titre | Acteur | MoSCoW | Sources | Sprint |
|---|---|---|---|---|---|---|
| 1 | US-01 | Charger le fichier et voir les totaux d'heures et de litres d'une période | Directrice (chargement par l'intendant) | Must | B-04 à B-07, B-09, B-14 à B-19, B-20.1 ; H-06 | **Sprint 01** |
| 2 | US-02 | Connaître le coût estimé du carburant de la période | Directrice | Must | B-04, B-08, B-12, B-14, B-20.2 | **Sprint 01** |
| 3 | US-03 | Repérer le jour où la génératrice a le plus fonctionné | Directrice | Must | B-04, B-10, B-13, B-20.3 | **Sprint 01** |
| 4 | US-04 | Consulter le détail jour par jour dans un tableau | Intendant | Must | B-03, B-05b, B-11, B-14, B-15, B-20.4 | plus tard |
| 5 | US-05 | Graphique en barres des heures de génératrice par mois | Directrice | Should | B-04, B-21 | plus tard |
| 6 | US-06 | Comparer deux mois côte à côte | Directrice | Could | B-04, B-22 (Q-13) | plus tard |
| 7 | US-07 | Part des heures solaires par rapport aux heures de génératrice | Directrice | Could, **bloquée** (Q-11) | B-04, B-23 | plus tard |
| 8 | US-08 | Alerte par SMS au-delà d'un seuil de consommation | Directrice | **Won't (V1)** | B-04, B-24 ; en conflit avec B-16 et C-11 (Q-12) | non retenue en V1 |

## 2. User stories

### US-01 : Charger le fichier et voir les totaux d'heures et de litres d'une période

- **Énoncé** : En tant que directrice, je veux voir, une fois le fichier CSV de l'intendant chargé, le total des heures de génératrice et le total des litres de carburant consommés pour un mois choisi ou pour toute la période, afin de suivre la consommation de la génératrice.
- **Sources** : B-04, B-05a, B-05b, B-06, B-07, B-09, B-14 à B-19, B-20.1 ; EF-01 à EF-05, ENF-01, ENF-02, RM-03, RM-04 ; CT-01 à CT-05. Acteur : H-06 (le besoin de priorité 1 est celui de la directrice ; le chargement par l'intendant, B-05b, figure dans les CA). Le chargement fait partie de cette user story (C-07).
- **MoSCoW** : **Must**. Priorité 1 du client (B-20.1) ; sans chargement ni totaux, l'outil ne montre aucun résultat (C-07).
- **Critères d'acceptation** :

| CA | Critère | Sources et hypothèses |
|---|---|---|
| CA-01.01 | Étant donné l'ordinateur sans connexion Internet, quand on ouvre le fichier de l'outil par double-clic, alors la page s'affiche avec un bouton « Choisir un fichier », et aucune valeur calculée ni donnée du fichier n'est affichée avant le chargement (les libellés fixes, comme le prix de référence de 300 gourdes par litre, sont permis). | B-06, B-16, B-17 ; ENF-01, ENF-02 ; CT-02, CT-03, CT-04 ; H-05 |
| CA-01.02 | Étant donné la page ouverte, quand l'intendant charge `energie_college.csv` avec le bouton « Choisir un fichier », alors aucun message d'erreur n'apparaît et la période sélectionnée est « Toute la période », avec 97 h et 280,0 L. | B-05b, B-06 ; EF-01 ; hypothèse provisoire Q-03 (période par défaut) |
| CA-01.03 | Étant donné `energie_college.csv` chargé, quand la directrice ouvre le choix de la période, alors exactement quatre choix sont proposés : « Août 2026 », « Septembre 2026 », « Octobre 2026 » et « Toute la période ». | B-09 ; EF-02, EF-03 ; H-04 ; hypothèse provisoire Q-02 (liste déduite du fichier) |
| CA-01.04 | Étant donné `energie_college.csv` chargé, quand la directrice choisit chaque période, alors le total des heures de génératrice et le total des litres affichés sont : Août 2026 : 24 h et 71,0 L ; Septembre 2026 : 30 h et 84,0 L ; Octobre 2026 : 43 h et 125,0 L ; Toute la période : 97 h et 280,0 L. | B-07, B-09, B-14 ; EF-04, EF-05, RM-03 ; hypothèses provisoires Q-01 (format des litres) et Q-16 (format des heures) |
| CA-01.05 | Étant donné l'ordinateur réglé sur le fuseau horaire « (UTC-05:00) Haïti » et `energie_college.csv` chargé, quand la directrice choisit « Août 2026 », puis « Septembre 2026 », puis « Octobre 2026 », alors les totaux affichés sont ceux de CA-01.04 (le 01/09/2026 est compté en septembre et le 01/10/2026 en octobre) ; « 26 h » (août), « 32 h » (septembre) et « 39 h » (octobre) n'apparaissent pas. | B-07, B-09 ; EF-02, EF-04 ; hypothèse provisoire Q-09 (fuseau d'Haïti) |
| CA-01.06 | Étant donné `energie_college.csv` chargé et « Toute la période » affichée, quand la directrice choisit « Octobre 2026 », alors les totaux passent à 43 h et 125,0 L sans qu'il faille charger de nouveau le fichier. | B-07, B-09 ; EF-02, EF-04, EF-05 |
| CA-01.07 | Étant donné la page ouverte, quand l'intendant charge un fichier dont la ligne d'en-tête ne contient pas la colonne `litres_carburant`, alors un message d'erreur clair s'affiche, qui désigne la ligne d'en-tête comme ligne fautive, et aucun total n'est affiché. | B-06, B-19 ; EF-01 ; hypothèse provisoire Q-04 (fichier invalide rejeté) |
| CA-01.08 | Étant donné l'empreinte SHA-256 de `energie_college.csv` relevée avant l'essai (`320155c76969aeb0e05779861b2520a150675f853318d2dfd6592eaf0107a84b`), quand l'intendant charge le fichier puis que la directrice consulte les quatre périodes, alors l'empreinte du fichier est identique après l'essai et la page ne propose aucun moyen de saisir, de modifier ou d'enregistrer une valeur. | B-15, B-26 ; RM-04 |
| CA-01.09 | Étant donné un premier fichier valide chargé (celui de CA-01.10), quand l'intendant charge ensuite `energie_college.csv`, alors « Toute la période » affiche 97 h et 280,0 L, et non le cumul des deux fichiers. | B-06, B-26 (« le CSV reste la seule source ») ; EF-01, EF-03 (cahier des charges §4 : « tous les jours du fichier chargé ») |
| CA-01.10 | Étant donné un fichier valide qui ne contient que l'en-tête et les 24 lignes d'août et de septembre de `energie_college.csv`, quand l'intendant le charge, alors le choix de la période propose seulement « Août 2026 », « Septembre 2026 » et « Toute la période », et « Toute la période » affiche 54 h et 155,0 L. | B-09 ; EF-02, EF-03 (cahier des charges §4) ; hypothèse provisoire Q-02 (liste déduite du fichier) |
| CA-01.11 | Étant donné la page ouverte, quand l'intendant charge un fichier dont une ligne de données contient `abc` dans la colonne `heures_generatrice`, alors un message d'erreur clair indique le numéro de cette ligne, et aucun total n'est affiché. | B-06, B-19 ; EF-01 ; hypothèse provisoire Q-04 (fichier invalide rejeté) |

### US-02 : Connaître le coût estimé du carburant de la période

- **Énoncé** : En tant que directrice, je veux connaître le coût estimé du carburant pour la période choisie, afin de préparer le budget.
- **Sources** : B-04, B-08, B-12, B-14, B-20.2 ; EF-06, RM-01, RM-03.
- **MoSCoW** : **Must**. Priorité 2 du client (B-20.2) ; la préparation du budget est l'un des deux buts du tableau de bord (B-04).
- **Critères d'acceptation** :

| CA | Critère | Sources et hypothèses |
|---|---|---|
| CA-02.01 | Étant donné `energie_college.csv` chargé, quand la directrice choisit chaque période, alors le coût estimé affiché, sans décimale, est : Août 2026 : 21 300 gourdes ; Septembre 2026 : 25 200 gourdes ; Octobre 2026 : 37 500 gourdes ; Toute la période : 84 000 gourdes. | B-08, B-12, B-14 ; EF-06, RM-01, RM-03 ; H-02 ; hypothèse provisoire Q-06 (prix constant) |
| CA-02.02 | Étant donné `energie_college.csv` chargé, quand le coût est affiché, alors son libellé contient les mots « coût estimé » et indique le prix de référence de 300 gourdes par litre. | B-08, B-12 ; EF-06, RM-01 |
| CA-02.03 | Étant donné « Août 2026 » affiché avec 21 300 gourdes, quand la directrice choisit « Septembre 2026 », alors le coût passe à 25 200 gourdes sans qu'il faille charger de nouveau le fichier. | B-08, B-09 ; EF-06 |
| CA-02.04 | Étant donné l'ordinateur réglé sur le fuseau horaire « (UTC-05:00) Haïti » et `energie_college.csv` chargé, quand la directrice choisit « Août 2026 », puis « Septembre 2026 », puis « Octobre 2026 », alors les coûts affichés sont ceux de CA-02.01 ; « 23 100 gourdes », « 27 000 gourdes » et « 33 900 gourdes » n'apparaissent pas. | B-08, B-09 ; EF-06 ; hypothèse provisoire Q-09 (fuseau d'Haïti) |
| CA-02.05 | Étant donné `energie_college.csv` chargé, quand le coût est affiché, alors la mention « prix de référence de l'intendance, pas un prix officiel » est visible à côté du coût. | B-12 ; RM-01 ; hypothèse provisoire Q-20 (rappel du prix de référence) |

### US-03 : Repérer le jour où la génératrice a le plus fonctionné

- **Énoncé** : En tant que directrice, je veux repérer le jour où la génératrice a fonctionné le plus longtemps sur la période choisie, afin d'appuyer la discussion avec le conseil d'administration sur l'installation de panneaux supplémentaires.
- **Sources** : B-04, B-10, B-13, B-20.3 ; EF-07, RM-02.
- **MoSCoW** : **Must**. Priorité 3 du client (B-20.3).
- **Critères d'acceptation** :

| CA | Critère | Sources et hypothèses |
|---|---|---|
| CA-03.01 | Étant donné `energie_college.csv` chargé, quand la directrice choisit chaque période, alors le jour de fonctionnement maximal affiché est : Août 2026 : 06/08/2026 (5 h) ; Septembre 2026 : 08/09/2026 (5 h) ; Octobre 2026 : 02/10/2026 (5 h) ; Toute la période : 06/08/2026 (5 h). Dans chaque période, plusieurs jours atteignent 5 h : le jour affiché est le premier dans l'ordre chronologique (et non 12/08/2026, 11/09/2026 ou 16/10/2026). | B-10, B-13 ; EF-07, RM-02 ; H-01 ; hypothèses provisoires Q-16 (format des heures) et Q-17 (date et heures du jour) |
| CA-03.02 | Étant donné un fichier qui contient les mêmes 36 lignes que `energie_college.csv`, dans un ordre mélangé, quand l'intendant le charge et que la directrice choisit chaque période, alors les jours affichés sont identiques à ceux de CA-03.01. | B-13 (« le premier de ces jours dans l'ordre chronologique ») ; RM-02 |
| CA-03.03 | Étant donné un fichier valide dont un mois ne compte que des jours à 0 h de génératrice, quand la directrice choisit ce mois, alors le message « Aucun fonctionnement de la génératrice sur la période » s'affiche à la place d'un jour. | B-10 ; EF-07 ; hypothèse provisoire Q-05 (période sans fonctionnement) |
| CA-03.04 | Étant donné l'ordinateur réglé sur le fuseau horaire « (UTC-05:00) Haïti » et `energie_college.csv` chargé, quand la directrice choisit chaque période, alors les jours affichés sont ceux de CA-03.01 ; « 05/08/2026 », « 07/09/2026 » et « 01/10/2026 » n'apparaissent pas. | B-10 ; EF-07 ; H-01 ; hypothèse provisoire Q-09 (fuseau d'Haïti) |

### US-04 : Consulter le détail jour par jour dans un tableau

- **Énoncé** : En tant qu'intendant, je veux consulter les données jour par jour sous forme de tableau, afin de vérifier les chiffres recopiés du registre.
- **Sources** : B-03, B-05b, B-11, B-14, B-15, B-20.4 ; EF-08, RM-03, RM-04.
- **MoSCoW** : **Must**. Priorité 4 du client (B-20.4) ; hors Sprint 01 (D-07, §5).
- **Critères d'acceptation** :

| CA | Critère | Sources et hypothèses |
|---|---|---|
| CA-04.01 | Étant donné `energie_college.csv` chargé, quand la directrice ou l'intendant choisit « Août 2026 », alors le tableau compte 12 lignes, du 03/08/2026 au 18/08/2026. | B-11 ; EF-08 ; H-01 ; hypothèse provisoire Q-15 (jours de la période choisie) |
| CA-04.02 | Étant donné `energie_college.csv` chargé, quand on consulte le tableau, alors ses colonnes sont la date, les heures solaires, les heures de génératrice et les litres de carburant. | B-11, B-19 ; EF-08 ; hypothèse provisoire Q-18 (colonnes du tableau) |
| CA-04.03 | Étant donné « Septembre 2026 » choisi, quand on lit la ligne du 08/09/2026, alors elle affiche 6 h (solaire), 5 h (génératrice) et 12,5 L. | B-11, B-14 ; EF-08, RM-03 ; H-01 ; hypothèses provisoires Q-01 et Q-16 |
| CA-04.04 | Étant donné le fichier aux 36 lignes mélangées (CA-03.02) chargé et « Toute la période » choisie, quand on consulte le tableau, alors ses 36 lignes vont du 03/08/2026 au 16/10/2026 dans l'ordre chronologique. | B-11 ; EF-08 ; hypothèse provisoire Q-19 (ordre chronologique) |
| CA-04.05 | Étant donné le tableau affiché, quand on essaie de modifier une valeur, alors aucune cellule n'est modifiable et aucun enregistrement n'est proposé. | B-15, B-26 ; RM-04 |

### US-05 : Graphique en barres des heures de génératrice par mois

- **Énoncé** : En tant que directrice, je veux afficher un graphique en barres des heures de génératrice par mois, afin d'appuyer la discussion avec le conseil d'administration sur l'installation de panneaux supplémentaires.
- **Sources** : B-04, B-21 ; souhait ultérieur non tranché par le client (C-04) ; Q-14.
- **MoSCoW** : **Should** (D-08) : voir §3 et §4.
- **Critères d'acceptation** :

| CA | Critère | Sources et hypothèses |
|---|---|---|
| CA-05.01 | Étant donné `energie_college.csv` chargé, quand la directrice affiche le graphique, alors il montre une barre par mois : août 24 h, septembre 30 h, octobre 43 h. | B-21 ; hypothèse provisoire Q-16 |
| CA-05.02 | Étant donné le graphique affiché, quand on lit la barre d'octobre, alors elle porte la mention « données au 16/10 ». | B-18, B-21 ; hypothèse provisoire Q-14 (octobre partiel) |
| CA-05.03 | Étant donné l'ordinateur sans connexion Internet, quand la directrice affiche le graphique, alors il s'affiche entièrement. | B-16 ; ENF-01 |

### US-06 : Comparer deux mois côte à côte

- **Énoncé** : En tant que directrice, je veux comparer deux mois côte à côte, afin de suivre l'évolution de la consommation de la génératrice.
- **Sources** : B-04, B-22 ; souhait ultérieur non tranché par le client (C-04) ; Q-13 (ouvert).
- **MoSCoW** : **Could** (D-08) : voir §3 et §4.
- **Critères d'acceptation** (indicateurs : valeurs à compléter après réponse du client, Q-13) :

| CA | Critère | Sources et hypothèses |
|---|---|---|
| CA-06.01 | Étant donné `energie_college.csv` chargé, quand la directrice choisit deux mois, alors les indicateurs retenus par le client sont affichés côte à côte pour ces deux mois (liste des indicateurs : à compléter après réponse du client). | B-22 ; Q-13 (ouvert) |
| CA-06.02 | Étant donné deux mois comparés, quand on lit un indicateur, alors sa valeur est identique à celle affichée pour ce mois choisi seul (par exemple août : 24 h et 71,0 L, CA-01.04). | B-22 ; Q-13 (ouvert) |

### US-07 : Part des heures solaires par rapport aux heures de génératrice

- **Énoncé** : En tant que directrice, je veux voir la part des heures solaires par rapport aux heures de génératrice, afin d'argumenter l'installation de panneaux supplémentaires devant le conseil d'administration.
- **Sources** : B-04, B-23 ; souhait ultérieur non tranché par le client (C-04) ; Q-11 (ouvert).
- **MoSCoW** : **Could, bloquée** (D-08) : la formule n'est pas fixée par le client ; on ne l'invente pas (C-05).
- **Critères d'acceptation** (formule, unité et présentation : valeurs à compléter après réponse du client, Q-11) :

| CA | Critère | Sources et hypothèses |
|---|---|---|
| CA-07.01 | Étant donné `energie_college.csv` chargé et une période choisie, quand la directrice consulte la part solaire, alors la valeur affichée suit la formule fixée par le client (valeurs à compléter après réponse du client). | B-23 ; Q-11 (ouvert) |
| CA-07.02 | Étant donné la part solaire affichée, quand on vérifie le fichier, alors elle n'utilise que les colonnes `heures_solaire` et `heures_generatrice` du fichier chargé, sans les modifier. | B-15, B-19, B-23 ; RM-04 |

### US-08 : Alerte par SMS au-delà d'un seuil de consommation

- **Énoncé** : En tant que directrice, je veux recevoir une alerte par SMS lorsque la consommation du mois dépasse un seuil, afin de suivre la consommation de la génératrice et son coût.
- **Sources** : B-04, B-24 ; en conflit avec B-16 et C-11 ; Q-12 (ouvert ; le destinataire réel reste à confirmer).
- **MoSCoW** : **Won't (V1)** (D-08, décision de l'équipe et non du client) : voir §3 et §4.
- **Critères d'acceptation** (seuil, unité, destinataire et canal : valeurs à compléter après réponse du client, Q-12) :

| CA | Critère | Sources et hypothèses |
|---|---|---|
| CA-08.01 | Étant donné le seuil fixé par le client, quand la consommation du mois dépasse ce seuil, alors une alerte est envoyée au destinataire fixé par le client (seuil, unité, destinataire et canal : valeurs à compléter après réponse du client). | B-24 ; Q-12 (ouvert) |
| CA-08.02 | Étant donné l'ordinateur sans connexion Internet, quand on utilise l'outil, alors toutes les autres fonctions restent utilisables, même si l'alerte ne peut pas partir. | B-16 ; ENF-01 |

## 3. Justification de l'ordre et du MoSCoW

**Ordre.** Les quatre premières user stories suivent exactement l'ordre d'importance fixé par le client (B-20.1 à B-20.4) : totaux, coût, jour maximal, détail jour par jour. Viennent ensuite les souhaits « plus tard » (B-21 à B-24), classés par l'équipe (D-08) : d'abord le Should, puis les Could (US-06 avant US-07, car US-07 est bloquée tant que le client n'a pas fixé sa formule), enfin le Won't.

**MoSCoW (release V1).**

| US | MoSCoW | Justification |
|---|---|---|
| US-01 à US-04 | Must | Ce sont les quatre priorités du client pour la première version (B-20.1 à B-20.4). Le Sprint 01 n'en réalise que trois à cause de la taille du sprint (C-07) : US-04 reste Must pour la V1. |
| US-05 | Should | Souhait du client (B-21) directement utile à la discussion avec le conseil d'administration (B-04). Compatible avec ses règles (§4) ; un seul point à confirmer, qui a une hypothèse (Q-14). |
| US-06 | Could | Compatible avec les règles du client, mais les indicateurs à comparer ne sont pas précisés (Q-13, ouvert) : l'US ne peut pas être détaillée avant la réponse du client. |
| US-07 | Could, bloquée | La formule de la part solaire n'est pas fixée par le client (Q-11, ouvert) ; on ne l'invente pas (C-05). |
| US-08 | Won't (V1) | Incompatible avec la contrainte « fonctionner sans Internet » (B-16) et avec la règle du prototype (C-11) ; seuil, destinataire et canal non fixés (Q-12, ouvert). Décision de l'équipe (D-08), à revoir avec le client. |

## 4. Souhaits « plus tard »

Les souhaits B-21 à B-24 ne sont pas tranchés par le client (C-04). L'équipe les classe (D-08) et vérifie leur compatibilité avec les règles du client (B-12 à B-17) et avec ce qui est hors périmètre (B-25 à B-27).

| Souhait du client | US | Classement | Compatibilité avec les règles du client | Point à décider |
|---|---|---|---|---|
| B-21 : « afficher un graphique en barres des heures de génératrice par mois » | US-05 | Should | **Compatible** : le graphique se calcule à partir du seul fichier CSV (B-26), sans Internet (B-16) et sans modifier les données (B-15). Octobre est partiel (B-18) : il faut l'indiquer. | Q-14 (provisoire : mention « données au 16/10 ») |
| B-22 : « comparer deux mois côte à côte » | US-06 | Could | **Compatible** : mêmes données et mêmes règles que US-01 à US-03 (B-12 à B-15), sans Internet. Mais les indicateurs à comparer ne sont pas fixés. | Q-13 (ouvert) |
| B-23 : « afficher la part des heures solaires par rapport aux heures de génératrice » | US-07 | Could, bloquée | **Compatible** avec les règles (colonne `heures_solaire` présente, B-19 ; calcul sans Internet ni modification des données), mais **la règle de calcul n'est pas fixée** : l'US reste bloquée (C-05). | Q-11 (ouvert) |
| B-24 : « recevoir une alerte par SMS lorsque la consommation du mois dépasse un seuil » | US-08 | Won't (V1) | **Incompatible** avec B-16 (l'outil doit fonctionner sans Internet) et avec C-11 : envoyer un SMS suppose un service ou un réseau extérieur. Le seuil n'est pas fixé (C-05). | Q-12 (ouvert) |

## 5. Sprint 01

**Objectif** : l'intendant charge le CSV et la directrice voit immédiatement, pour un mois ou pour toute la période, combien d'heures la génératrice a tourné, combien de litres elle a consommés, ce que cela coûte et quel jour elle a le plus fonctionné.

**User stories retenues** (groupe de 6 personnes, donc 3 user stories, C-07 ; décision D-01) :

| US | Titre | CA |
|---|---|---|
| US-01 | Charger le fichier et voir les totaux d'heures et de litres d'une période (**le chargement fait partie de cette US**, C-07) | CA-01.01 à CA-01.11 |
| US-02 | Connaître le coût estimé du carburant de la période | CA-02.01 à CA-02.05 |
| US-03 | Repérer le jour où la génératrice a le plus fonctionné | CA-03.01 à CA-03.04 |

**Hors Sprint 01** : US-04 (tableau jour par jour) reste au backlog, car le client la classe en 4e priorité (B-20.4, D-07) ; US-05 à US-08 sont des souhaits « plus tard ». Aucun Sprint 02 n'est prévu à ce stade (C-17).

**Hypothèses provisoires appliquées par le Sprint 01** (jamais des règles du client) : Q-01, Q-02, Q-03, Q-04, Q-05, Q-06, Q-09, Q-16, Q-17, Q-20 ; choix de présentation de l'équipe : H-01, H-02, H-04, H-05.

**Fichiers de test nécessaires** (fictifs, préparés par l'équipe à partir du format de B-18 et B-19) : les 36 lignes de `energie_college.csv` dans un ordre mélangé (CA-03.02) ; un en-tête sans `litres_carburant` (CA-01.07) ; une valeur `abc` dans `heures_generatrice` (CA-01.11) ; un mois sans aucune heure de génératrice (CA-03.03) ; l'en-tête et les 24 lignes d'août et de septembre de `energie_college.csv` (CA-01.09, CA-01.10).

**Definition of Done du Sprint 01** :

- tous les CA de US-01, US-02 et US-03 sont respectés, vérifiés sur la page, et prouvés par une capture d'écran (C-15) ;
- le prototype est un seul fichier HTML autonome, qui s'ouvre par double-clic, sans connexion Internet, sans serveur et sans compte (CT-01, CT-02) ;
- le fichier CSV est chargé par le bouton « Choisir un fichier » ; aucune donnée n'est intégrée dans la page (CT-03, CT-04) ; seules des données fictives sont utilisées (CT-05) ;
- les données du fichier ne sont jamais modifiées (RM-04) ;
- aucune fonction hors du Sprint 01 n'est présente : ni tableau jour par jour, ni graphique, ni comparaison, ni part solaire, ni alerte, ni saisie de données, ni compte (C-08, C-23, B-25 à B-27).

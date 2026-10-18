# Cahier des charges : PowerWatch (Collège Les Palmistes)

> **Objet** : décrire ce que le Collège Les Palmistes attend de la première version (V1) de PowerWatch, un petit tableau de bord de suivi de la génératrice. Le document dit **quoi**, jamais **comment**. Il sert aussi de contexte à l'IA chargée de réaliser le prototype (C-08).
>
> **Sources**, citées entre parenthèses à chaque élément :
> - **B-xx** : brief du client, cas 01 (« Demande du client »), selon les identifiants de sa transcription `docs/brief_client.md` ; le texte du client fait foi ;
> - **C-xx** : consignes du projet final du cours (transcription `docs/consignes.md`) ;
> - **D-xx** (décisions d'équipe), **Q-xx** (questions au client) et **H-xx** (choix de présentation de l'équipe) : registre des décisions de l'équipe, `travail/decisions.md` ; les Q-xx et les H-xx sont reproduits au §11.
>
> **Version** : v1 du 2026-10-18, rédigée au relais R2 (Groupe 01, cas 01) ; points à confirmer Q-18 à Q-20 ajoutés au relais R3.
>
> **Règles de lecture** :
> - « doit » marque une exigence, une règle ou une contrainte ;
> - « l'outil » désigne le tableau de bord demandé par le client ; « le prototype » désigne sa réalisation dans le cadre du projet (§7) ;
> - ce document décrit toute la V1 attendue par le client, dont le découpage relève du product backlog ; le prototype du projet réalise les user stories du Sprint 01 de ce backlog (C-23), et une fonctionnalité ajoutée hors du Sprint compte parmi les propositions de l'IA à corriger ou à rejeter (C-08) ;
> - une Q-xx est une question au client : son hypothèse provisoire s'applique en attendant sa réponse, mais ce n'est **jamais** une règle du client ; Q-11 à Q-14 portent sur des souhaits ultérieurs (§10 bis), dont ce document ne tire aucune exigence : une éventuelle hypothèse ne vaudrait que si le souhait était réalisé plus tard ;
> - ce document ne contient aucune valeur attendue chiffrée : elles figureront dans les critères d'acceptation du product backlog.

---

## 1. Contexte

- Le Collège Les Palmistes accueille environ 600 élèves. Comme le courant du réseau public est irrégulier, l'établissement utilise des panneaux solaires et, lorsque cela ne suffit pas, une génératrice diesel (B-01).
- Chaque jour ouvrable, le gardien note dans un registre papier le nombre d'heures de fonctionnement des panneaux solaires, le nombre d'heures de fonctionnement de la génératrice et la quantité de carburant consommée (B-02).
- Chaque semaine, l'intendant recopie ce registre dans un fichier CSV (B-03).
- La directrice souhaite disposer d'un petit tableau de bord pour suivre la consommation de la génératrice et son coût (B-04) : c'est l'outil décrit dans ce document.

Le brief ne nomme pas le pays du collège ; les montants y sont exprimés en gourdes (B-12, B-14). Voir Q-09 (§11.1).

## 2. Objectifs

La directrice souhaite disposer d'un petit tableau de bord (B-04) :

- pour suivre la consommation de la génératrice et son coût ;

afin de :

- préparer le budget ;
- discuter avec le conseil d'administration de l'installation de panneaux supplémentaires.

Pour la première version, le client classe ses besoins par ordre d'importance (B-20.1 à B-20.4) : voir §9.

## 3. Acteurs

| Acteur | Rôle selon le client | Utilise l'outil | Source |
|---|---|---|---|
| La directrice | « consulte le tableau de bord pour suivre la consommation et le coût » | oui | B-05a, B-04 |
| L'intendant | « charge le fichier CSV dans l'outil et vérifie les chiffres » ; chaque semaine, il recopie le registre dans un fichier CSV | oui | B-05b, B-03 |
| Le gardien | « tient le registre papier ; il n'utilise pas l'outil » | non | B-05c, B-02 |

- Le conseil d'administration est cité comme interlocuteur de la directrice (B-04) ; il ne figure pas parmi « Les personnes concernées » du brief et n'est pas présenté comme utilisateur de l'outil.
- Aucun compte utilisateur n'est nécessaire pour cette première version (B-17) : voir ENF-02.

## 4. Exigences fonctionnelles

### Termes employés

- **Jour** : une ligne de données du fichier chargé, désignée par sa date (colonne `date`) (B-19). D'après le client, le gardien tient le registre chaque jour ouvrable (B-02), et le fichier fourni contient des jours ouvrables (B-18).
- **Période choisie** : le mois choisi (EF-02) ou toute la période (EF-03) (B-09).
- **Jours de la période choisie** : pour un mois, les jours du fichier chargé dont la date tombe dans ce mois ; pour toute la période, tous les jours du fichier chargé (sur le fichier fourni : du 3 août au 16 octobre 2026, B-18).

### Exigences

| ID | Exigence | Source | Priorité du client |
|---|---|---|---|
| EF-01 | L'outil doit permettre de charger le fichier CSV fourni par l'intendant. | B-06 (acteur : B-05b) | non classée par le client |
| EF-02 | L'outil doit permettre de choisir un mois (août, septembre ou octobre 2026). | B-09 | rang 1 (B-20.1 : « pour un mois donné ») |
| EF-03 | L'outil doit permettre d'afficher toute la période, au lieu d'un seul mois. | B-09 | non classée par le client |
| EF-04 | L'outil doit permettre d'afficher, pour la période choisie, le total des heures de génératrice, c'est-à-dire la somme des valeurs de la colonne `heures_generatrice` des jours de cette période. | B-07 (colonne : B-19) | rang 1 (B-20.1) |
| EF-05 | L'outil doit permettre d'afficher, pour la période choisie, le total des litres de carburant consommés, c'est-à-dire la somme des valeurs de la colonne `litres_carburant` des jours de cette période. | B-07 (colonne : B-19) | rang 1 (B-20.1) |
| EF-06 | L'outil doit permettre d'afficher le coût estimé du carburant pour la période choisie, calculé selon RM-01. | B-08 (période : B-07, B-09 ; calcul : B-12) | rang 2 (B-20.2) |
| EF-07 | L'outil doit permettre d'afficher le jour où la génératrice a fonctionné le plus longtemps sur la période choisie, c'est-à-dire le jour de cette période dont la valeur de `heures_generatrice` est la plus élevée ; en cas d'égalité, RM-02 s'applique. | B-10 (égalité : B-13 ; colonne : B-19) | rang 3 (B-20.3) |
| EF-08 | L'outil doit permettre d'afficher les données sous forme de tableau, jour par jour. | B-11 | rang 4 (B-20.4) |

### Notes

- **Priorités** : les rangs 1 à 4 sont ceux du client (B-20.1 à B-20.4). Le client formule ses deux premières priorités pour un mois donné (B-20.1, B-20.2). B-07 et B-10 demandent ces affichages pour la période choisie ; B-08 demande le coût « pour la période », que l'équipe lit comme la même période choisie (B-07, B-09). Ces affichages valent donc aussi pour toute la période (EF-03). EF-01 (chargement) et EF-03 (toute la période) ne sont pas classées par le client.
- **Liste des mois** : EF-02 reprend les mois cités par le client (B-09). La liste des mois proposés suit l'hypothèse provisoire Q-02 ; les libellés de H-04 sont ceux des mois de B-09.
- **Règles applicables** (§6) : EF-06 suit RM-01 (calcul) et RM-03 (montants) ; EF-05 et EF-08 suivent RM-03 (litres) ; EF-07 suit RM-02 (égalité) ; toutes les EF respectent RM-04 (données non modifiées).
- **Contraintes du projet liées** (§7) : CT-03 et CT-04 portent sur la façon dont le prototype réalise EF-01.
- **Points à confirmer liés** (§11.1) : EF-01 → Q-04, Q-10 ; EF-02 → Q-02 ; EF-02 et EF-03 → Q-03 ; EF-04 à EF-06 → Q-08 ; EF-05 et EF-08 → Q-01 ; EF-06 → Q-06, Q-07, Q-20 ; EF-07 → Q-05, Q-17 ; EF-04, EF-07 et EF-08 → Q-16 ; EF-08 → Q-15, Q-18, Q-19. Le comportement face à un fichier invalide n'est pas fixé par le client : il relève uniquement de Q-04.
- **Choix de présentation de l'équipe applicables** (§11.2) : EF-01 → H-05 ; EF-02 et EF-03 → H-04 ; EF-06 → H-02 ; EF-07 et EF-08 → H-01.

## 5. Exigences non fonctionnelles

| ID | Exigence | Source | Priorité du client |
|---|---|---|---|
| ENF-01 | L'outil doit fonctionner sans Internet : il sera utilisé sur l'ordinateur du bureau de l'intendance, où la connexion Internet n'est pas toujours disponible. | B-16 | contrainte du client (rubrique « Nos contraintes ») |
| ENF-02 | L'outil doit pouvoir être utilisé sans compte utilisateur ni mot de passe dans cette première version. | B-17 (appui : B-27) | contrainte du client (rubrique « Nos contraintes ») |

### Notes

- B-14 et B-15 sont des règles du client (rubrique « Les règles à respecter ») : elles figurent au §6 (RM-03, RM-04), et non ici.
- L'environnement de l'ordinateur du bureau de l'intendance (système, navigateur, fuseau horaire) n'est pas précisé par le client : voir Q-09.
- Contrainte du projet voisine : CT-02 (§7), qui vient des consignes et non du client.

## 6. Règles métier

| ID | Règle | Source | S'applique à |
|---|---|---|---|
| RM-01 | Le coût estimé du carburant doit se calculer ainsi : litres consommés × 300 gourdes. Précision du client : « Ce prix de référence est fixé par l'intendance pour ce suivi ; il ne s'agit pas d'un prix officiel. » | B-12 | EF-06 (litres de la période, B-08) ; Q-06, Q-07, Q-20 |
| RM-02 | Si plusieurs jours de la période choisie ont le même nombre maximal d'heures de génératrice, l'outil doit afficher le premier de ces jours dans l'ordre chronologique, c'est-à-dire l'ordre de leurs dates, quel que soit l'ordre des lignes dans le fichier. | B-13 (période choisie : B-10) | EF-07 |
| RM-03 | Les montants doivent être affichés en gourdes, sans décimale ; les litres peuvent avoir une décimale. | B-14 | EF-06 (montants) ; EF-05, EF-08 (litres) ; Q-01, Q-07 ; H-02 |
| RM-04 | Les données du fichier ne doivent pas être modifiées par l'outil. | B-15 | toutes les EF, en particulier EF-01 et EF-08 ; Q-04 ; H-01 |

### Notes

- RM-03 : le client fixe l'affichage des montants (en gourdes, sans décimale) et autorise une décimale pour les litres. Le format exact d'affichage des litres n'est pas fixé : c'est le point à confirmer Q-01. Le client ne fixe pas non plus le format d'affichage des heures : c'est le point à confirmer Q-16.
- RM-04 : afficher une valeur dans un autre format (par exemple une date au format JJ/MM/AAAA, H-01) n'est pas une modification des données du fichier.

## 7. Contraintes

Cette section ne contient que des **contraintes du projet**, issues des consignes du cours (et, pour CT-01 et CT-04, de leur lecture retenue par l'équipe, D-06), et non du client. Les contraintes exprimées par le client (B-16, B-17) sont les exigences ENF-01 et ENF-02 (§5).

| ID | Contrainte | Source | Nature | Lien |
|---|---|---|---|---|
| CT-01 | Le prototype final doit être un fichier HTML autonome : le CSS et le JavaScript sont inclus dans le fichier. | C-10 ; lecture retenue par l'équipe (D-06) : C-10 cite aussi les données, mais notre cas fournit un CSV, donc les données ne sont pas incluses (CT-04) | contrainte du projet | CT-04 |
| CT-02 | Le prototype doit s'ouvrir par double-clic dans un navigateur, sans connexion Internet, sans serveur et sans compte utilisateur. | C-11 | contrainte du projet | ENF-01, ENF-02 |
| CT-03 | La page du prototype doit charger le fichier CSV à l'aide d'un bouton « Choisir un fichier ». | C-12 | contrainte du projet | EF-01 ; H-05 |
| CT-04 | Les données ne doivent pas être intégrées directement dans la page du prototype. | C-12 ; décision d'équipe D-06 (pour un cas fourni avec un CSV, C-12 prime sur C-10 : aucune donnée CSV intégrée) | contrainte du projet | EF-01 ; CT-01 |
| CT-05 | Seules des données fictives doivent être utilisées, dans les prompts comme dans le prototype. | C-13 | contrainte du projet | — |

## 8. Données d'entrée

Texte du client (B-18) :

> Le fichier energie_college.csv contient un échantillon de 36 jours ouvrables (12 par mois), du 3 août au 16 octobre 2026 ; les données d'octobre s'arrêtent donc au 16 octobre. Les colonnes sont séparées par des virgules ; les valeurs sont écrites sans accents pour éviter les problèmes d'encodage.

Ce texte décrit le fichier fourni par le client, qu'il présente comme « un échantillon » (B-18).

Colonnes du fichier (B-19) :

| Colonne | Signification |
|---|---|
| date | date du jour au format AAAA-MM-JJ |
| heures_solaire | nombre d'heures de fonctionnement des panneaux solaires |
| heures_generatrice | nombre d'heures de fonctionnement de la génératrice |
| litres_carburant | litres de carburant consommés par la génératrice |

Ce que B-18 et B-19 ne précisent pas relève des points à confirmer (§11.1) : fichier non conforme (Q-04), fichier produit avec un autre séparateur ou avec un BOM (Q-10), fichier couvrant d'autres mois (Q-02).

## 9. Périmètre de la V1

La V1 couvre ce que le client attend de l'outil (rubrique « Ce que nous attendons de l'outil », « L'outil doit permettre de : ») :

| Source | Texte du client | Exigences |
|---|---|---|
| B-06 | « charger le fichier CSV fourni par l'intendant » | EF-01 |
| B-07 | « afficher, pour la période choisie, le total des heures de génératrice et le total des litres de carburant consommés » | EF-04, EF-05 |
| B-08 | « afficher le coût estimé du carburant pour la période » | EF-06 |
| B-09 | « choisir un mois (août, septembre ou octobre 2026) ou afficher toute la période » | EF-02, EF-03 |
| B-10 | « afficher le jour où la génératrice a fonctionné le plus longtemps sur la période choisie » | EF-07 |
| B-11 | « afficher les données sous forme de tableau, jour par jour » | EF-08 |

Ordre fixé par le client (rubrique « Nos priorités pour la première version », « Par ordre d'importance : ») :

| Rang | Source | Texte du client | Exigences |
|---|---|---|---|
| 1 | B-20.1 | « Voir le total des heures de génératrice et des litres consommés pour un mois donné. » | EF-02, EF-04, EF-05 |
| 2 | B-20.2 | « Connaître le coût estimé du carburant pour ce mois. » | EF-06 |
| 3 | B-20.3 | « Repérer le jour où la génératrice a le plus fonctionné. » | EF-07 |
| 4 | B-20.4 | « Consulter le détail jour par jour. » | EF-08 |

EF-01 (chargement) et EF-03 (toute la période) ne sont pas classées par le client. S'appliquent aussi à toute la V1 : ENF-01 et ENF-02 (§5), RM-01 à RM-04 (§6). Le prototype du projet respecte en outre les contraintes du projet CT-01 à CT-05 (§7), qui viennent des consignes et non du client. Le découpage et la planification de la V1 relèvent du product backlog.

## 10. Hors périmètre

Texte du client (rubrique « Ce qui ne fait pas partie de la première version »). Ce sont des **décisions déjà prises par le client** : elles sont respectées (C-03), et aucune exigence du présent document ne les contredit.

- **B-25** : « la connexion directe à la génératrice ou à un compteur électrique »
- **B-26** : « la saisie des données dans l'outil (le CSV reste la seule source) »
- **B-27** : « la gestion de comptes et de mots de passe »

Liens : B-26 rejoint EF-01 (le fichier CSV est la seule source de données) et RM-04 ; B-27 appuie ENF-02.

## 10 bis. Souhaits ultérieurs

Texte du client (« Nous aimerions aussi, plus tard : »). Ces souhaits sont **non tranchés par le client (C-04)** : le présent document n'en tire aucune exigence. Leur classement (D-08), la justification de ce classement et la vérification de leur compatibilité avec les règles du client figurent dans le product backlog.

| Source | Souhait du client | Point dépendant (§11.1) |
|---|---|---|
| B-21 | « afficher un graphique en barres des heures de génératrice par mois » | Q-14 (provisoire) : octobre partiel (B-18) |
| B-22 | « comparer deux mois côte à côte » | Q-13 (ouvert) : indicateurs à comparer non précisés |
| B-23 | « afficher la part des heures solaires par rapport aux heures de génératrice » | Q-11 (ouvert) : formule non fixée par le client ; on ne l'invente pas (C-05) |
| B-24 | « recevoir une alerte par SMS lorsque la consommation du mois dépasse un seuil » | Q-12 (ouvert) : seuil, destinataire et canal non fixés (C-05) |

Pour B-24, **l'équipe** (et non le client) a décidé de ne pas le retenir pour la V1 (décision d'équipe D-08) : une alerte par SMS est incompatible avec le fonctionnement sans Internet (B-16) et avec C-11.

## 11. Points à confirmer ou à décider

### 11.1 Questions au client (Q-01 à Q-20)

Ces points ne sont pas fixés par le client ; ils figurent ici comme points encore à confirmer ou à décider (C-20). En attendant la réponse du client, l'hypothèse provisoire est appliquée ; elle n'est **pas** une règle du client. Un point au statut « ouvert » n'a pas d'hypothèse applicable. Q-11 à Q-14 portent sur des souhaits ultérieurs (§10 bis), dont le présent document ne tire aucune exigence : une éventuelle hypothèse ne vaudrait que si le souhait était réalisé plus tard. Pour les souhaits qui dépendent d'une règle non fixée par le client (Q-11 à Q-13), aucune hypothèse n'est retenue (C-05).

| ID | Point à confirmer | Statut | Élément concerné |
|---|---|---|---|
| Q-01 | À confirmer : quel format d'affichage pour les litres ? (hypothèse provisoire : toujours une décimale, avec la virgule comme séparateur décimal, suivie de l'unité « L ») | provisoire | RM-03 (B-14) ; EF-05, EF-08 |
| Q-02 | À confirmer : la liste des mois proposés est-elle figée (août à octobre 2026) ou déduite du fichier ? (hypothèse provisoire : déduite du fichier ; sur le fichier fourni, elle donne exactement les mois de B-09) | provisoire | EF-02 (B-09) ; B-03 ; §8 (B-18) |
| Q-03 | À confirmer : quelle période est sélectionnée par défaut après le chargement ? (hypothèse provisoire : « Toute la période ») | provisoire | EF-02, EF-03 |
| Q-04 | À confirmer : que faire d'un fichier invalide (colonne manquante, valeur non numérique ou négative, date invalide, date en double) ? (hypothèse provisoire : rejet complet avec un message clair qui indique la ligne fautive ; aucun total affiché) | provisoire | EF-01 (B-06) ; RM-04 (B-15) ; §8 |
| Q-05 | À confirmer : sur une période sans aucune heure de génératrice, quel « jour max » afficher ? (hypothèse provisoire : le message « Aucun fonctionnement de la génératrice sur la période ») | provisoire | EF-07 (B-10) |
| Q-06 | À confirmer : le prix de 300 gourdes est-il modifiable par l'intendance ? (hypothèse provisoire : constante de 300 gourdes par litre en V1) | provisoire | RM-01 (B-12) ; EF-06 |
| Q-07 | À confirmer : comment arrondir le coût si des litres avaient plus d'une décimale ? (hypothèse provisoire : arrondi à la gourde la plus proche) | provisoire | RM-01, RM-03 ; EF-06 |
| Q-08 | À confirmer : faut-il rappeler la couverture réelle de la période (nombre de jours, premier et dernier jour) ? (hypothèse provisoire : non en V1, car le client ne le demande pas ; la question lui est posée parce que ce rappel éviterait de lire un échantillon comme un mois complet pour préparer le budget, B-04, B-18) | provisoire | EF-04 à EF-06 ; §8 |
| Q-09 | À confirmer : dans quel pays est le collège ? Quels navigateur, système et fuseau horaire sur l'ordinateur du bureau de l'intendance ? (hypothèse provisoire : collège supposé en Haïti, ce qui est déduit des gourdes ; tests sur Edge ou Chrome et sur Firefox, sous Windows, dans le fuseau horaire d'Haïti) | provisoire | §1 ; ENF-01 (B-16) |
| Q-10 | À confirmer : avec quel outil le fichier CSV est-il produit ? Un Excel réglé en français pourrait l'exporter avec le point-virgule comme séparateur et un BOM (marque d'ordre des octets). (hypothèse provisoire : seul le format décrit en B-18, avec la virgule comme séparateur, est accepté ; tout autre format est rejeté avec un message, comme en Q-04) | provisoire | EF-01 (B-06) ; §8 (B-18) |
| Q-11 | À confirmer : quelle formule pour la « part solaire » : heures solaires / (heures solaires + heures de génératrice), ou heures solaires / heures de génératrice ? Par jour ou en cumul ? En pourcentage ou en graphique ? (aucune hypothèse : le souhait B-23 reste bloqué tant que le client n'a pas fixé la règle ; on n'invente pas une règle non fixée, C-05) | ouvert | souhait B-23 (§10 bis) |
| Q-12 | À confirmer : pour l'alerte, quel seuil (valeur, unité en litres, en heures ou en gourdes), quel destinataire, quel canal possible sans Internet ? (aucune hypothèse : le souhait B-24 n'est pas retenu pour la V1, décision d'équipe D-08 ; il est incompatible avec B-16 et C-11, et son seuil n'est pas fixé, C-05) | ouvert | souhait B-24 (§10 bis) |
| Q-13 | À confirmer : pour comparer deux mois, quels indicateurs ? (aucune hypothèse : le client ne les a pas précisés ; le souhait B-22 ne peut pas être détaillé avant sa réponse) | ouvert | souhait B-22 (§10 bis) |
| Q-14 | À confirmer : sur le graphique, faut-il afficher octobre, partiel, tel quel ? (hypothèse provisoire : oui, avec la mention « données au 16/10 ») | provisoire | souhait B-21 (§10 bis) ; B-18 |
| Q-15 | À confirmer : le tableau jour par jour montre-t-il les jours de la période choisie, ou toutes les données chargées ? Contrairement à B-07 et B-10, B-11 ne cite pas la période. (hypothèse provisoire : les jours de la période choisie) | provisoire | EF-08 (B-11) |
| Q-16 | À confirmer : quel format d'affichage pour les heures de génératrice (totaux, jour maximal, tableau) ? Le client ne fixe que celui des montants et des litres (B-14). (hypothèse provisoire : la valeur du fichier, suivie de l'unité « h ») | provisoire | EF-04, EF-07, EF-08 ; RM-03 (B-14) |
| Q-17 | À confirmer : pour le jour où la génératrice a fonctionné le plus longtemps, faut-il afficher la date seule, ou aussi le nombre d'heures de génératrice de ce jour ? (hypothèse provisoire : la date et le nombre d'heures de génératrice de ce jour) | provisoire | EF-07 (B-10) |
| Q-18 | À confirmer : quelles colonnes le tableau jour par jour affiche-t-il ? B-11 demande « les données » sans préciser les colonnes. (hypothèse provisoire : les 4 colonnes du fichier décrites en B-19 : date, heures solaires, heures de génératrice, litres de carburant) | provisoire | EF-08 (B-11) ; §8 (B-19) |
| Q-19 | À confirmer : dans quel ordre les lignes du tableau jour par jour sont-elles affichées ? (hypothèse provisoire : l'ordre chronologique des dates, quel que soit l'ordre des lignes dans le fichier) | provisoire | EF-08 (B-11) |
| Q-20 | À confirmer : faut-il rappeler, à côté du coût estimé, que les 300 gourdes par litre sont un prix de référence de l'intendance et non un prix officiel ? Le client le précise (B-12) sans demander cet affichage. (hypothèse provisoire : oui, avec la mention « prix de référence de l'intendance, pas un prix officiel ») | provisoire | EF-06 (B-08) ; RM-01 (B-12) |

### 11.2 Choix de présentation de l'équipe (H-01 à H-06)

Ces choix sont **des choix de l'équipe** (statut « validé » dans le registre de l'équipe, 2026-10-18). Ce ne sont **ni des demandes du client ni des règles métier**. H-01 à H-05 portent sur la présentation de l'outil ; H-06 est un choix de rédaction du product backlog.

| ID | Choix de l'équipe | Élément concerné | Raison donnée par l'équipe |
|---|---|---|---|
| H-01 | Dates affichées au format JJ/MM/AAAA ; le fichier reste en AAAA-MM-JJ. | EF-07, EF-08 | Usage francophone ; il s'agit d'un affichage, pas d'une modification des données (B-15, RM-04). |
| H-02 | Montants écrits avec une espace comme séparateur des milliers, sans décimale, suivis du mot « gourdes ». | EF-06 ; RM-03 | B-14 ; lisibilité. |
| H-03 | Interface et livrables entièrement en français. | tout l'outil | Brief et client francophones. |
| H-04 | Libellés des périodes : « Août 2026 », « Septembre 2026 », « Octobre 2026 », « Toute la période ». | EF-02, EF-03 | B-09. |
| H-05 | Bouton de chargement au libellé exact « Choisir un fichier », quel que soit le navigateur. Le libellé lui-même est imposé par les consignes (C-12, CT-03) et n'est pas un choix de l'équipe ; le choix de l'équipe porte sur un libellé identique d'un navigateur à l'autre. | EF-01 ; CT-03 | C-12 (CT-03). |
| H-06 | Choix de rédaction du product backlog : le besoin de priorité 1 (B-20.1) y est porté par la directrice (B-05a), et le chargement par l'intendant (B-05b) figure dans les critères d'acceptation de ce besoin. Sans effet sur les exigences du présent document. | product backlog | B-20.1 est un besoin de suivi de la directrice ; selon C-07, le chargement fait partie de la première user story. |

### 11.3 Décision d'équipe encore à trancher

- D-10 (décision de méthode de l'équipe, à trancher par le relais R4) : contenu du prompt de délégation ; elle ne modifie aucune exigence du présent document.

## 12. Matrice de traçabilité

### 12.1 Brief du client vers le cahier des charges

Colonne « Sections » : sections des §1 à §10 bis où l'élément est cité. Les renvois du §11 (Q-xx, H-xx, D-xx) et les contraintes du projet liées (CT-xx) figurent dans la colonne « Autres renvois ».

| B-xx | Élément du brief | Sections | Exigences (EF, ENF, RM) | Autres renvois |
|---|---|---|---|---|
| B-01 | Collège d'environ 600 élèves ; réseau public irrégulier ; panneaux solaires et génératrice diesel | §1 | aucune (contexte) | Q-09 |
| B-02 | Relevé de chaque jour ouvrable par le gardien, dans un registre papier | §1, §3, §4 | aucune (contexte) | — |
| B-03 | Recopie hebdomadaire du registre dans un fichier CSV par l'intendant | §1, §3 | aucune (contexte) | Q-02 |
| B-04 | Petit tableau de bord de la directrice : suivi de la consommation et du coût ; budget ; conseil d'administration | §1, §2, §3 | aucune (objectif) | Q-08 |
| B-05a | La directrice consulte le tableau de bord | §3 | aucune (acteur) | H-06 |
| B-05b | L'intendant charge le fichier CSV et vérifie les chiffres | §3, §4 | EF-01 (acteur du chargement) | H-06 |
| B-05c | Le gardien tient le registre papier ; il n'utilise pas l'outil | §3 | aucune (acteur hors outil) | — |
| B-06 | Charger le fichier CSV fourni par l'intendant | §4, §9 | EF-01 | CT-03, CT-04 ; Q-04, Q-10 ; H-05 |
| B-07 | Total des heures de génératrice et total des litres pour la période choisie | §4, §9 | EF-04, EF-05 ; EF-06 (période) | Q-01, Q-08, Q-16 |
| B-08 | Coût estimé du carburant pour la période | §4, §6, §9 | EF-06 | Q-06, Q-07, Q-08, Q-20 ; H-02 |
| B-09 | Choisir un mois (août, septembre ou octobre 2026) ou afficher toute la période | §4, §9 | EF-02, EF-03 ; EF-06 (période) | Q-02, Q-03 ; H-04 |
| B-10 | Jour où la génératrice a fonctionné le plus longtemps sur la période choisie | §4, §6, §9 | EF-07 ; RM-02 (période choisie) | Q-05, Q-16, Q-17 ; H-01 |
| B-11 | Données sous forme de tableau, jour par jour | §4, §9 | EF-08 | Q-01, Q-15, Q-16, Q-18, Q-19 ; H-01 |
| B-12 | Coût estimé = litres consommés × 300 gourdes ; prix de référence de l'intendance, pas un prix officiel | §1, §4, §6 | RM-01 (appliquée par EF-06) | Q-06, Q-07, Q-09, Q-20 |
| B-13 | Égalité : le premier de ces jours dans l'ordre chronologique | §4, §6 | RM-02 (appliquée par EF-07) | — |
| B-14 | Montants en gourdes, sans décimale ; les litres peuvent avoir une décimale | §1, §5, §6 | RM-03 | Q-01, Q-07, Q-09, Q-16 ; H-02 |
| B-15 | Les données du fichier ne doivent pas être modifiées par l'outil | §5, §6 | RM-04 | Q-04 ; H-01 (un changement de format d'affichage n'est pas une modification) |
| B-16 | Ordinateur du bureau de l'intendance, Internet pas toujours disponible : fonctionner sans Internet | §5, §7, §10 bis | ENF-01 | CT-02 ; Q-09, Q-12 ; D-08 (B-24) |
| B-17 | Aucun compte utilisateur pour cette première version | §3, §5, §7 | ENF-02 | CT-02 |
| B-18 | Échantillon de 36 jours ouvrables (12 par mois), du 3 août au 16 octobre 2026 ; virgules ; valeurs sans accents | §4, §8, §10 bis | aucune (description des données) | Q-02, Q-04, Q-08, Q-10, Q-14 |
| B-19 | Colonnes du fichier et leur signification | §4, §8 | aucune exigence propre (colonnes citées par EF-04, EF-05 et EF-07) | Q-18 ; H-01 |
| B-20.1 | Priorité 1 : totaux des heures de génératrice et des litres pour un mois donné | §2, §4, §9 | rang 1 de EF-02, EF-04, EF-05 | H-06 |
| B-20.2 | Priorité 2 : coût estimé du carburant pour ce mois | §2, §4, §9 | rang 2 de EF-06 | — |
| B-20.3 | Priorité 3 : jour où la génératrice a le plus fonctionné | §2, §4, §9 | rang 3 de EF-07 | — |
| B-20.4 | Priorité 4 : détail jour par jour | §2, §4, §9 | rang 4 de EF-08 | — |
| B-21 | Plus tard : graphique en barres des heures de génératrice par mois | §10 bis | aucune (souhait ultérieur) | Q-14 ; D-08 |
| B-22 | Plus tard : comparer deux mois côte à côte | §10 bis | aucune (souhait ultérieur) | Q-13 ; D-08 |
| B-23 | Plus tard : part des heures solaires par rapport aux heures de génératrice | §10 bis | aucune (souhait ultérieur) | Q-11 ; D-08 |
| B-24 | Plus tard : alerte par SMS lorsque la consommation du mois dépasse un seuil | §10 bis | aucune (souhait ultérieur) | Q-12 ; D-08 |
| B-25 | Hors V1 : connexion directe à la génératrice ou à un compteur électrique | §10 | aucune (hors périmètre) | — |
| B-26 | Hors V1 : saisie des données dans l'outil (le CSV reste la seule source) | §10 | aucune (hors périmètre) ; rejoint EF-01 et RM-04 | — |
| B-27 | Hors V1 : gestion de comptes et de mots de passe | §5, §10 | appui de ENF-02 (hors périmètre) | — |

Contrôle : chacun des éléments B-06 à B-17 renvoie à au moins une EF, une ENF ou une RM.

### 12.2 Consignes du cours vers le cahier des charges

| C-xx | Consigne (résumé) | Contrainte du projet | Autre couverture |
|---|---|---|---|
| C-02 | Chaque exigence doit pouvoir être reliée au brief ; aucune exigence qu'aucun élément du brief ne justifie | — | colonne « Source » des §4 à §6 ; §12.1 |
| C-03 | « Ce qui ne fait pas partie de la première version » : décisions déjà prises par le client, à respecter | — | §10 |
| C-04 | Souhaits « plus tard » non tranchés, à classer dans le backlog avec une justification, en vérifiant leur compatibilité avec les règles du client | — | §10 bis |
| C-05 | Souhait qui dépend d'une règle non fixée par le client : ne pas l'inventer, le signaler comme point à décider | — | §10 bis ; §11.1 (Q-11 à Q-13) |
| C-10 | Prototype final en fichier HTML autonome (CSS, JavaScript et données inclus) | CT-01 | lecture retenue D-06 : données non incluses (CT-04) |
| C-11 | Ouverture par double-clic dans un navigateur, sans connexion Internet, sans serveur et sans compte utilisateur | CT-02 | recoupe ENF-01 et ENF-02 (exprimées aussi par le client, B-16, B-17) |
| C-12 | Chargement du CSV par un bouton « Choisir un fichier » ; données intégrées = écart à signaler et justifier dans prompts.md | CT-03, CT-04 | D-06 ; H-05 |
| C-13 | Données fictives uniquement, dans les prompts comme dans le prototype | CT-05 | — |
| C-20 | Contenu obligatoire du cahier des charges | — | contexte, objectifs et acteurs : §1 à §3 ; exigences fonctionnelles et non fonctionnelles : §4 et §5 ; règles métier et contraintes : §6 et §7 ; périmètre de la première version et hors périmètre : §9 et §10 (avec §10 bis) ; points encore à confirmer ou à décider : §11 |

Les autres consignes ne créent pas de contrainte dans ce document : C-01 (nom et emplacement de ce fichier) est respectée par sa forme ; C-08 (ce document sert de contexte au prompt de délégation ; une fonctionnalité ajoutée hors du Sprint est une proposition de l'IA à corriger ou à rejeter) et C-23 (le prototype réalise les user stories du Sprint 01) sont rappelées dans les règles de lecture ; C-06, C-07, C-09, C-14 à C-19, C-21 et C-22 portent sur le backlog, les prompts, le prototype, sa vérification, l'organisation ou la remise.

### 12.3 Éléments du brief sans exigence propre

Ces éléments ne fondent aucune exigence (EF, ENF ou RM) ; certains sont seulement cités en appui d'une exigence (acteur, colonne, hors périmètre).

| B-xx | Raison |
|---|---|
| B-01, B-02, B-03 | contexte (§1) : ils décrivent la situation du client, pas une capacité de l'outil |
| B-04 | objectifs (§2) |
| B-05a, B-05c | acteurs (§3) |
| B-05b | acteur (§3) ; cité comme acteur d'EF-01 (§4), sans exigence propre |
| B-18, B-19 | description des données fournies (§8) ; B-19 donne les colonnes citées par EF-04, EF-05 et EF-07, sans créer d'exigence propre |
| B-20.1 à B-20.4 | ordre d'importance du client : il classe les EF (colonne « Priorité du client » du §4 ; §9) sans créer d'exigence propre |
| B-21 à B-24 | souhaits ultérieurs, non tranchés par le client (§10 bis, C-04) |
| B-25, B-26 | hors périmètre, décisions du client (§10, C-03) |
| B-27 | hors périmètre, décision du client (§10, C-03) ; il sert seulement d'appui à ENF-02 |

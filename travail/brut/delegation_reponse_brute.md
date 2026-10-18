# Réponse brute de la délégation Sprint 01

- **Date et heure de réception** : 2026-10-18 13:17
- **Outil** : ChatGPT (OpenAI)
- **Modèle** : GPT-4o
- **Mode de session** : Nouvelle conversation web temporaire, mémoire et instructions personnalisées désactivées, sans document joint, hors GPT personnalisé (D-09)
- **Texte brut reçu** :

<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PowerWatch — Suivi énergétique</title>
    <style>
        :root {
            --navy: #142b45;
            --blue: #2463eb;
            --blue-light: #edf4ff;
            --green: #16835d;
            --green-light: #e9f7f0;
            --orange: #d97706;
            --orange-light: #fff5e7;
            --background: #f4f6fa;
            --surface: #ffffff;
            --text: #243247;
            --muted: #718096;
            --border: #e3e8ef;
            --danger: #b42318;
            --danger-light: #fff0ee;
        }

        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            background: var(--background);
            color: var(--text);
            font-family: Arial, Helvetica, sans-serif;
            font-size: 15px;
            line-height: 1.5;
        }

        button,
        select,
        input {
            font: inherit;
        }

        .topbar {
            background: var(--navy);
            color: #fff;
            padding: 22px 24px;
        }

        .topbar-inner {
            max-width: 1100px;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 18px;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 13px;
        }

        .brand-mark {
            width: 43px;
            height: 43px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 12px;
            background: var(--blue);
            font-size: 23px;
            font-weight: 700;
        }

        .brand-name {
            margin: 0;
            font-size: 23px;
            font-weight: 700;
            letter-spacing: -0.6px;
        }

        .brand-subtitle {
            margin: 2px 0 0;
            color: #c4d1e2;
            font-size: 12px;
        }

        .topbar-tag {
            padding: 7px 12px;
            border: 1px solid #465b73;
            border-radius: 20px;
            color: #e2eaf4;
            font-size: 12px;
            white-space: nowrap;
        }

        main {
            width: min(1100px, calc(100% - 36px));
            margin: 32px auto 48px;
        }

        .page-heading {
            margin-bottom: 24px;
        }

        .page-heading h2 {
            margin: 0 0 6px;
            color: var(--navy);
            font-size: 27px;
            letter-spacing: -0.7px;
        }

        .page-heading p {
            margin: 0;
            color: var(--muted);
            font-size: 14px;
        }

        .panel {
            margin-bottom: 24px;
            padding: 23px;
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: 14px;
        }

        .section-heading {
            display: flex;
            align-items: center;
            gap: 10px;
            margin: 0 0 18px;
            color: var(--navy);
            font-size: 16px;
            font-weight: 700;
        }

        .section-icon {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 32px;
            height: 32px;
            border-radius: 9px;
            background: var(--blue-light);
            color: var(--blue);
            font-size: 16px;
        }

        .upload-area {
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 18px;
            padding: 18px;
            border: 1px dashed #b9c8db;
            border-radius: 11px;
            background: #fbfcfe;
        }

        .upload-description {
            display: flex;
            align-items: center;
            gap: 13px;
            min-width: 0;
        }

        .upload-icon {
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            width: 43px;
            height: 43px;
            border-radius: 10px;
            background: var(--blue-light);
            color: var(--blue);
            font-size: 21px;
        }

        .upload-description strong {
            display: block;
            color: var(--navy);
            font-size: 14px;
            overflow-wrap: anywhere;
        }

        .upload-description p {
            margin: 4px 0 0;
            color: var(--muted);
            font-size: 12px;
        }

        .file-button {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            min-height: 43px;
            padding: 11px 18px;
            border: 0;
            border-radius: 9px;
            background: var(--blue);
            color: #fff;
            font-weight: 700;
            cursor: pointer;
            transition: background 0.2s;
        }

        .file-button:hover {
            background: #174dc3;
        }

        .file-button:focus-visible,
        select:focus-visible {
            outline: 3px solid #93b4ff;
            outline-offset: 3px;
        }

        .price-note {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-top: 16px;
            color: var(--muted);
            font-size: 12px;
        }

        .price-note strong {
            color: var(--navy);
        }

        .error-message {
            display: none;
            margin-top: 16px;
            padding: 13px 15px;
            border: 1px solid #f2c5c0;
            border-radius: 9px;
            background: var(--danger-light);
            color: var(--danger);
            font-size: 13px;
            overflow-wrap: anywhere;
        }

        .error-message.visible {
            display: block;
        }

        .success-message {
            display: none;
            margin-top: 16px;
            padding: 12px 14px;
            border: 1px solid #b8e2ce;
            border-radius: 9px;
            background: var(--green-light);
            color: #126b4a;
            font-size: 13px;
            overflow-wrap: anywhere;
        }

        .success-message.visible {
            display: block;
        }

        .dashboard {
            display: none;
        }

        .dashboard.visible {
            display: block;
        }

        .period-panel {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 18px;
            flex-wrap: wrap;
        }

        .period-panel .section-heading {
            margin: 0;
        }

        .period-control {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .period-control label {
            color: var(--muted);
            font-size: 13px;
        }

        .period-control select {
            min-width: 190px;
            padding: 11px 36px 11px 12px;
            border: 1px solid #ccd5e1;
            border-radius: 8px;
            background: #fff;
            color: var(--navy);
            cursor: pointer;
        }

        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(2, minmax(0, 1fr));
            gap: 18px;
            margin-bottom: 20px;
        }

        .metric-card {
            min-width: 0;
            padding: 22px;
            border: 1px solid var(--border);
            border-radius: 13px;
            background: var(--surface);
        }

        .metric-top {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 10px;
            margin-bottom: 20px;
        }

        .metric-label {
            color: var(--muted);
            font-size: 13px;
            font-weight: 600;
        }

        .metric-icon {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 38px;
            height: 38px;
            flex-shrink: 0;
            border-radius: 10px;
            font-size: 19px;
        }

        .hours-card .metric-icon {
            background: var(--blue-light);
            color: var(--blue);
        }

        .litres-card .metric-icon {
            background: var(--green-light);
            color: var(--green);
        }

        .cost-card .metric-icon {
            background: var(--orange-light);
            color: var(--orange);
        }

        .maximum-card .metric-icon {
            background: #f1edff;
            color: #6d4acb;
        }

        .metric-value {
            margin: 0;
            color: var(--navy);
            font-size: clamp(25px, 3vw, 35px);
            font-weight: 700;
            letter-spacing: -1px;
            overflow-wrap: anywhere;
        }

        .metric-description {
            margin: 8px 0 0;
            color: var(--muted);
            font-size: 12px;
        }

        .cost-card {
            border-color: #f0dfc5;
        }

        .cost-card .metric-value {
            color: #a85b08;
            font-size: clamp(22px, 2.7vw, 31px);
            letter-spacing: -0.6px;
        }

        .reference-notice {
            margin-top: 15px;
            padding-top: 13px;
            border-top: 1px solid #f0dfc5;
            color: #8a5a22;
            font-size: 11px;
            line-height: 1.6;
        }

        .maximum-card .metric-value {
            font-size: clamp(21px, 2.7vw, 30px);
            letter-spacing: -0.5px;
        }

        .maximum-card .metric-value.no-operation {
            font-size: 17px;
            line-height: 1.6;
            letter-spacing: 0;
        }

        .footer {
            padding-top: 18px;
            border-top: 1px solid var(--border);
            color: var(--muted);
            font-size: 12px;
            text-align: center;
        }

        @media (max-width: 650px) {
            .topbar {
                padding: 18px;
            }

            .topbar-inner {
                align-items: flex-start;
            }

            .brand-name {
                font-size: 21px;
            }

            .topbar-tag {
                display: none;
            }

            main {
                width: calc(100% - 28px);
                margin-top: 25px;
            }

            .page-heading h2 {
                font-size: 23px;
            }

            .panel {
                padding: 17px;
            }

            .upload-area {
                align-items: stretch;
                flex-direction: column;
            }

            .file-button {
                width: 100%;
            }

            .period-panel {
                align-items: stretch;
                flex-direction: column;
            }

            .period-control {
                align-items: stretch;
                flex-direction: column;
                gap: 7px;
            }

            .period-control select {
                width: 100%;
            }

            .metrics-grid {
                grid-template-columns: 1fr;
                gap: 13px;
            }

            .metric-card {
                padding: 19px;
            }

            .metric-top {
                margin-bottom: 15px;
            }
        }
    </style>
</head>
<body>
    <header class="topbar">
        <div class="topbar-inner">
            <div class="brand">
                <div class="brand-mark" aria-hidden="true">P</div>
                <div>
                    <h1 class="brand-name">PowerWatch</h1>
                    <p class="brand-subtitle">Suivi énergétique · Collège Les Palmistes</p>
                </div>
            </div>
            <div class="topbar-tag">Tableau de bord énergétique</div>
        </div>
    </header>

    <main>
        <section class="page-heading">
            <h2>Suivi de la génératrice</h2>
            <p>Consultez les heures de fonctionnement, la consommation et le coût estimé du carburant.</p>
        </section>

        <section class="panel" aria-labelledby="upload-title">
            <h2 class="section-heading" id="upload-title">
                <span class="section-icon" aria-hidden="true">↥</span>
                Chargement des données
            </h2>

            <div class="upload-area">
                <div class="upload-description">
                    <div class="upload-icon" aria-hidden="true">▤</div>
                    <div>
                        <strong id="file-name">Aucun fichier chargé</strong>
                        <p>Sélectionnez le fichier CSV fourni par l'intendant.</p>
                    </div>
                </div>

                <div>
                    <input
                        type="file"
                        id="csv-file"
                        accept=".csv,text/csv"
                        hidden
                    >
                    <button
                        type="button"
                        class="file-button"
                        id="choose-file"
                    >Choisir un fichier</button>
                </div>
            </div>

            <div class="price-note">
                <span aria-hidden="true">ⓘ</span>
                <span>Prix de référence : <strong>300 gourdes par litre</strong></span>
            </div>

            <div
                id="error-message"
                class="error-message"
                role="alert"
                aria-live="assertive"
            ></div>

            <div
                id="success-message"
                class="success-message"
                role="status"
                aria-live="polite"
            ></div>
        </section>

        <section class="dashboard" id="dashboard" aria-label="Indicateurs énergétiques">
            <section class="panel period-panel">
                <h2 class="section-heading">
                    <span class="section-icon" aria-hidden="true">◷</span>
                    Période d'analyse
                </h2>

                <div class="period-control">
                    <label for="period-select">Période sélectionnée</label>
                    <select id="period-select" disabled>
                        <option value="all">Toute la période</option>
                    </select>
                </div>
            </section>

            <section class="metrics-grid" aria-label="Totaux et indicateurs">
                <article class="metric-card hours-card">
                    <div class="metric-top">
                        <span class="metric-label">Heures de génératrice</span>
                        <span class="metric-icon" aria-hidden="true">◷</span>
                    </div>
                    <p class="metric-value" id="total-hours">—</p>
                    <p class="metric-description">Total des heures de fonctionnement</p>
                </article>

                <article class="metric-card litres-card">
                    <div class="metric-top">
                        <span class="metric-label">Carburant consommé</span>
                        <span class="metric-icon" aria-hidden="true">♨</span>
                    </div>
                    <p class="metric-value" id="total-litres">—</p>
                    <p class="metric-description">Total des litres consommés</p>
                </article>

                <article class="metric-card cost-card">
                    <div class="metric-top">
                        <span class="metric-label">Coût estimé</span>
                        <span class="metric-icon" aria-hidden="true">G</span>
                    </div>
                    <p class="metric-value" id="total-cost">—</p>
                    <p class="metric-description">Estimation du coût du carburant</p>
                    <div class="reference-notice">
                        prix de référence de l'intendance, pas un prix officiel
                    </div>
                </article>

                <article class="metric-card maximum-card">
                    <div class="metric-top">
                        <span class="metric-label">Jour de fonctionnement maximal</span>
                        <span class="metric-icon" aria-hidden="true">↗</span>
                    </div>
                    <p class="metric-value" id="maximum-day">—</p>
                    <p class="metric-description">Jour avec le plus d'heures de génératrice</p>
                </article>
            </section>
        </section>

        <footer class="footer">
            PowerWatch · Suivi énergétique du Collège Les Palmistes
        </footer>
    </main>

    <script>
        "use strict";

        const PRIX_PAR_LITRE = 300;

        const inputFichier = document.getElementById("csv-file");
        const boutonChoisir = document.getElementById("choose-file");
        const nomFichier = document.getElementById("file-name");
        const selectPeriode = document.getElementById("period-select");
        const tableauDeBord = document.getElementById("dashboard");
        const messageErreur = document.getElementById("error-message");
        const messageSucces = document.getElementById("success-message");

        const affichageHeures = document.getElementById("total-hours");
        const affichageLitres = document.getElementById("total-litres");
        const affichageCout = document.getElementById("total-cost");
        const affichageMaximum = document.getElementById("maximum-day");

        const COLONNES_REQUISES = [
            "date",
            "heures_solaire",
            "heures_generatrice",
            "litres_carburant"
        ];

        const MOIS_FRANCAIS = [
            "Janvier", "Février", "Mars", "Avril",
            "Mai", "Juin", "Juillet", "Août",
            "Septembre", "Octobre", "Novembre", "Décembre"
        ];

        let donneesChargees = [];
        let nomFichierCharge = "";

        boutonChoisir.addEventListener("click", function () {
            inputFichier.click();
        });

        selectPeriode.addEventListener("change", function () {
            actualiserIndicateurs();
        });

        inputFichier.addEventListener("change", function (evenement) {
            const fichier = evenement.target.files[0];

            if (!fichier) {
                return;
            }

            reinitialiserApplication();
            nomFichier.textContent = fichier.name;

            const lecteur = new FileReader();

            lecteur.onload = function (resultat) {
                try {
                    const contenu = resultat.target.result;

                    if (typeof contenu !== "string" || contenu.length === 0) {
                        throw new Error("Le fichier CSV est vide.");
                    }

                    const nouvellesDonnees = analyserCSV(contenu);

                    donneesChargees = nouvellesDonnees;
                    nomFichierCharge = fichier.name;

                    construireListePeriodes();

                    selectPeriode.value = "all";
                    selectPeriode.disabled = false;

                    tableauDeBord.classList.add("visible");

                    messageSucces.textContent =
                        "Fichier chargé et vérifié avec succès : " +
                        fichier.name + ".";

                    messageSucces.classList.add("visible");

                    actualiserIndicateurs();
                } catch (erreur) {
                    reinitialiserApplication();
                    nomFichier.textContent = fichier.name;

                    afficherErreur(erreur.message);
                }
            };

            lecteur.onerror = function () {
                reinitialiserApplication();
                nomFichier.textContent = fichier.name;
                afficherErreur("Impossible de lire le fichier sélectionné.");
            };

            lecteur.readAsText(fichier, "UTF-8");
        });

        function reinitialiserApplication() {
            donneesChargees = [];
            nomFichierCharge = "";

            tableauDeBord.classList.remove("visible");

            selectPeriode.replaceChildren();
            selectPeriode.add(
                new Option("Toute la période", "all")
            );
            selectPeriode.value = "all";
            selectPeriode.disabled = true;

            affichageHeures.textContent = "—";
            affichageLitres.textContent = "—";
            affichageCout.textContent = "—";
            affichageMaximum.textContent = "—";
            affichageMaximum.classList.remove("no-operation");

            messageErreur.textContent = "";
            messageErreur.classList.remove("visible");

            messageSucces.textContent = "";
            messageSucces.classList.remove("visible");
        }

        function afficherErreur(message) {
            messageErreur.textContent = message;
            messageErreur.classList.add("visible");
        }

        function analyserCSV(contenu) {
            const lignes = decouperCSV(contenu);

            if (lignes.length === 0) {
                throw new Error(
                    "Erreur à la ligne 1 : l'en-tête du fichier CSV est absent."
                );
            }

            const entete = lignes[0].valeurs;

            for (const colonne of COLONNES_REQUISES) {
                if (!entete.includes(colonne)) {
                    throw new Error(
                        "Erreur à la ligne 1 (en-tête) : " +
                        "la colonne obligatoire « " + colonne +
                        " » est absente."
                    );
                }
            }

            const indices = {
                date: entete.indexOf("date"),
                solaire: entete.indexOf("heures_solaire"),
                generatrice: entete.indexOf("heures_generatrice"),
                litres: entete.indexOf("litres_carburant")
            };

            const resultats = [];
            const datesRencontrees = new Set();

            for (let index = 1; index < lignes.length; index++) {
                const ligne = lignes[index];
                const valeurs = ligne.valeurs;
                const numeroLigne = ligne.numero;

                if (
                    valeurs.length === 1 &&
                    valeurs[0].trim() === ""
                ) {
                    continue;
                }

                if (valeurs.length !== entete.length) {
                    throw new Error(
                        "Erreur à la ligne " + numeroLigne +
                        " : le nombre de valeurs ne correspond pas " +
                        "au nombre de colonnes de l'en-tête."
                    );
                }

                const dateBrute = valeurs[indices.date].trim();

                if (!dateEstValide(dateBrute)) {
                    throw new Error(
                        "Erreur à la ligne " + numeroLigne +
                        " : date invalide. Le format attendu est AAAA-MM-JJ."
                    );
                }

                if (datesRencontrees.has(dateBrute)) {
                    throw new Error(
                        "Erreur à la ligne " + numeroLigne +
                        " : la date " + dateBrute +
                        " est présente plusieurs fois dans le fichier."
                    );
                }

                datesRencontrees.add(dateBrute);

                const heuresSolaires = lireNombre(
                    valeurs[indices.solaire],
                    "heures_solaire",
                    numeroLigne
                );

                const heuresGeneratrice = lireNombre(
                    valeurs[indices.generatrice],
                    "heures_generatrice",
                    numeroLigne
                );

                const litresCarburant = lireNombre(
                    valeurs[indices.litres],
                    "litres_carburant",
                    numeroLigne
                );

                resultats.push({
                    date: dateBrute,
                    mois: dateBrute.slice(0, 7),
                    heuresSolaires: heuresSolaires,
                    heuresGeneratrice: heuresGeneratrice,
                    litresCarburant: litresCarburant
                });
            }

            if (resultats.length === 0) {
                throw new Error(
                    "Le fichier ne contient aucune ligne de données exploitable."
                );
            }

            return resultats;
        }

        function decouperCSV(contenu) {
            const lignes = [];
            let valeurs = [];
            let champ = "";
            let dansGuillemets = false;
            let numeroLigne = 1;
            let numeroLigneDebut = 1;

            for (let index = 0; index < contenu.length; index++) {
                const caractere = contenu[index];

                if (dansGuillemets) {
                    if (caractere === '"') {
                        if (contenu[index + 1] === '"') {
                            champ += '"';
                            index++;
                        } else {
                            dansGuillemets = false;
                        }
                    } else {
                        if (caractere === "\n") {
                            numeroLigne++;
                        } else if (
                            caractere === "\r" &&
                            contenu[index + 1] !== "\n"
                        ) {
                            numeroLigne++;
                        }

                        champ += caractere;
                    }

                    continue;
                }

                if (caractere === '"' && champ.length === 0) {
                    dansGuillemets = true;
                    continue;
                }

                if (caractere === ",") {
                    valeurs.push(champ);
                    champ = "";
                    continue;
                }

                if (caractere === "\n" || caractere === "\r") {
                    valeurs.push(champ);

                    lignes.push({
                        valeurs: valeurs,
                        numero: numeroLigneDebut
                    });

                    valeurs = [];
                    champ = "";

                    if (
                        caractere === "\r" &&
                        contenu[index + 1] === "\n"
                    ) {
                        index++;
                    }

                    numeroLigne++;
                    numeroLigneDebut = numeroLigne;
                    continue;
                }

                champ += caractere;
            }

            if (dansGuillemets) {
                throw new Error(
                    "Erreur à la ligne " + numeroLigne +
                    " : un champ CSV contient des guillemets non fermés."
                );
            }

            if (champ.length > 0 || valeurs.length > 0) {
                valeurs.push(champ);

                lignes.push({
                    valeurs: valeurs,
                    numero: numeroLigneDebut
                });
            }

            return lignes;
        }

        function dateEstValide(date) {
            const correspondance = /^(\d{4})-(\d{2})-(\d{2})$/.exec(date);

            if (!correspondance) {
                return false;
            }

            const annee = Number(correspondance[1]);
            const mois = Number(correspondance[2]);
            const jour = Number(correspondance[3]);

            if (annee < 1 || mois < 1 || mois > 12 || jour < 1) {
                return false;
            }

            const joursDansMois = new Date(
                Date.UTC(annee, mois, 0)
            ).getUTCDate();

            return jour <= joursDansMois;
        }

        function lireNombre(valeur, colonne, numeroLigne) {
            const texte = valeur.trim();

            if (
                texte === "" ||
                !/^(?:\d+(?:\.\d+)?|\.\d+)$/.test(texte)
            ) {
                throw new Error(
                    "Erreur à la ligne " + numeroLigne +
                    " : la valeur de « " + colonne +
                    " » doit être un nombre valide positif ou nul."
                );
            }

            const nombre = Number(texte);

            if (!Number.isFinite(nombre) || nombre < 0) {
                throw new Error(
                    "Erreur à la ligne " + numeroLigne +
                    " : valeur numérique invalide dans « " + colonne + " »."
                );
            }

            return nombre;
        }

        function construireListePeriodes() {
            const moisPresents = [...new Set(
                donneesChargees.map(function (ligne) {
                    return ligne.mois;
                })
            )].sort();

            selectPeriode.replaceChildren();

            moisPresents.forEach(function (mois) {
                const parties = mois.split("-");
                const annee = Number(parties[0]);
                const numeroMois = Number(parties[1]);

                const libelle =
                    MOIS_FRANCAIS[numeroMois - 1] + " " + annee;

                selectPeriode.add(
                    new Option(libelle, mois)
                );
            });

            selectPeriode.add(
                new Option("Toute la période", "all")
            );
        }

        function actualiserIndicateurs() {
            if (donneesChargees.length === 0) {
                return;
            }

            const periode = selectPeriode.value;

            const donneesPeriode = donneesChargees.filter(
                function (ligne) {
                    return periode === "all" || ligne.mois === periode;
                }
            );

            let totalHeures = 0;
            let totalLitres = 0;
            let maximumHeures = 0;
            let jourMaximum = null;

            for (const ligne of donneesPeriode) {
                totalHeures += ligne.heuresGeneratrice;
                totalLitres += ligne.litresCarburant;

                if (
                    ligne.heuresGeneratrice > maximumHeures ||
                    (
                        ligne.heuresGeneratrice === maximumHeures &&
                        ligne.heuresGeneratrice > 0 &&
                        jourMaximum !== null &&
                        ligne.date < jourMaximum.date
                    )
                ) {
                    maximumHeures = ligne.heuresGeneratrice;
                    jourMaximum = ligne;
                }
            }

            affichageHeures.textContent =
                formaterNombre(totalHeures, 0) + " h";

            affichageLitres.textContent =
                formaterNombre(totalLitres, 1) + " L";

            affichageCout.textContent =
                formaterMontant(totalLitres * PRIX_PAR_LITRE) +
                " gourdes";

            if (maximumHeures === 0 || jourMaximum === null) {
                affichageMaximum.textContent =
                    "Aucun fonctionnement de la génératrice sur la période";

                affichageMaximum.classList.add("no-operation");
            } else {
                affichageMaximum.textContent =
                    formaterDate(jourMaximum.date) +
                    " (" + formaterNombre(maximumHeures, 0) + " h)";

                affichageMaximum.classList.remove("no-operation");
            }
        }

        function formaterNombre(nombre, decimales) {
            return nombre.toLocaleString("fr-FR", {
                minimumFractionDigits: decimales,
                maximumFractionDigits: decimales,
                useGrouping: true
            });
        }

        function formaterMontant(montant) {
            const arrondi = Math.round(montant);

            return arrondi.toLocaleString("fr-FR", {
                minimumFractionDigits: 0,
                maximumFractionDigits: 0,
                useGrouping: true
            }).replace(/[\u202f\u00a0]/g, " ");
        }

        function formaterDate(date) {
            const parties = date.split("-");

            return parties[2] + "/" + parties[1] + "/" + parties[0];
        }
    </script>
</body>
</html>

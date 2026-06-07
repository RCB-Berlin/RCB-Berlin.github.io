# RCB-Berlin.github.io
A simple app for learning noun genders for Momente A1.2
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Der Die Das - Momente A1.2</title>
    <style>
        :root {
            --primary: #2563eb;
            --success: #16a34a;
            --danger: #dc2626;
            --background: #f8fafc;
            --card-bg: #ffffff;
            --text: #1e293b;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background-color: var(--background);
            color: var(--text);
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
        }

        .container {
            width: 100%;
            max-width: 550px;
            background: var(--card-bg);
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        h1 {
            font-size: 1.8rem;
            font-weight: 800;
            margin-top: 0;
            margin-bottom: 4px;
            text-align: center;
            color: #0f172a;
        }

        .subtitle {
            font-size: 1.05rem;
            font-weight: 500;
            color: #64748b;
            text-align: center;
            margin-bottom: 25px;
        }

        .stats-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
            background: #f1f5f9;
            padding: 12px 15px;
            border-radius: 8px;
            font-size: 0.9rem;
            margin-bottom: 25px;
            font-weight: 600;
        }

        .level-badge {
            background-color: #dbeafe;
            color: #1e40af;
            padding: 2px 8px;
            border-radius: 4px;
        }

        .card {
            text-align: center;
            padding: 25px 20px;
            border: 2px solid #e2e8f0;
            border-radius: 12px;
            margin-bottom: 20px;
            min-height: 150px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        .german-word {
            font-size: 1.9rem;
            font-weight: 700;
            margin-bottom: 8px;
            color: #0f172a;
        }

        .plural-hint {
            font-size: 0.95rem;
            color: #64748b;
            font-style: italic;
            margin-bottom: 12px;
        }

        .streak-indicator {
            font-size: 0.8rem;
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            padding: 2px 8px;
            border-radius: 20px;
            margin-bottom: 10px;
            color: #475569;
        }

        .retire-zone {
            margin-top: 15px;
            background: #fff7ed;
            border: 1px dashed #f97316;
            padding: 8px 14px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            font-size: 0.9rem;
            font-weight: 600;
            color: #c2410c;
        }

        .retire-zone input {
            width: 16px;
            height: 16px;
            cursor: pointer;
        }

        .btn-peek {
            background: none;
            border: 1px dashed #cbd5e1;
            color: #64748b;
            padding: 6px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 500;
            transition: all 0.2s;
            margin-top: 5px;
        }

        .btn-peek:hover {
            border-color: var(--primary);
            color: var(--primary);
            background-color: #eff6ff;
        }

        .peek-translation-display {
            margin-top: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            color: #334155;
            background: #f8fafc;
            padding: 4px 12px;
            border-radius: 6px;
            border: 1px solid #e2e8f0;
        }

        .options-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-bottom: 20px;
        }

        button.btn-gender {
            padding: 15px;
            font-size: 1.1rem;
            font-weight: 600;
            border: 2px solid #cbd5e1;
            background: var(--card-bg);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
        }

        /* Color mapping based on the textbook */
        button.btn-gender.btn-der {
            color: #2563eb;
            border-color: #bfdbfe;
        }
        button.btn-gender.btn-der:hover {
            border-color: #2563eb;
            background-color: #eff6ff;
        }

        button.btn-gender.btn-die {
            color: #dc2626;
            border-color: #fecaca;
        }
        button.btn-gender.btn-die:hover {
            border-color: #dc2626;
            background-color: #fef2f2;
        }

        button.btn-gender.btn-das {
            color: #16a34a;
            border-color: #bbf7d0;
        }
        button.btn-gender.btn-das:hover {
            border-color: #16a34a;
            background-color: #f0fdf4;
        }

        .feedback-box {
            padding: 15px;
            border-radius: 10px;
            font-weight: 600;
            text-align: center;
            margin-bottom: 20px;
            display: none;
        }

        .feedback-success {
            background-color: #dcfce7;
            color: #15803d;
            border: 1px solid #bbf7d0;
        }

        .feedback-danger {
            background-color: #fee2e2;
            color: #b91c1c;
            border: 1px solid #fecaca;
        }

        .reveal-header {
            font-size: 1.3rem;
            display: block;
            margin-bottom: 4px;
        }

        .english-translation {
            display: block;
            font-size: 0.9rem;
            color: #475569;
            margin: 8px 0;
            font-weight: bold;
            border-top: 1px dashed rgba(0,0,0,0.1);
            padding-top: 8px;
        }

        .rule-hint {
            font-size: 0.85rem;
            font-weight: 400;
            opacity: 0.9;
            display: block;
            margin-top: 4px;
        }

        button.btn-next {
            width: 100%;
            padding: 14px;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            display: none;
        }

        button.btn-next:hover {
            background-color: #1d4ed8;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Der Die Das</h1>
    <div class="subtitle">Momente A1.2</div>
    
    <div class="stats-bar">
        <span>Level: <span id="current-level" class="level-badge">1</span></span>
        <span>Trefferquote: <span id="accuracy-rating">0%</span></span>
        <span id="dynamic-stat-label">Level-Fortschritt: <span id="progress-next-level">0%</span></span>
    </div>

    <div class="card">
        <div class="streak-indicator" id="word-streak">Serie: 0/3</div>
        <div class="german-word" id="word-target">Loading...</div>
        <div class="plural-hint" id="word-plural"></div>
        
        <button class="btn-peek" id="btn-peek" onclick="peekTranslation()">👁️ Hint: Show Translation</button>
        <div id="peek-display" class="peek-translation-display" style="display: none;"></div>

        <div class="retire-zone" id="retire-container" style="display: none;">
            <input type="checkbox" id="chk-retire">
            <label for="chk-retire">📦 Wort gelernt (wenn richtig)</label>
        </div>
    </div>

    <div class="options-grid" id="choices-container">
        <button class="btn-gender btn-der" onclick="submitAnswer('der')">der</button>
        <button class="btn-gender btn-die" onclick="submitAnswer('die')">die</button>
        <button class="btn-gender btn-das" onclick="submitAnswer('das')">das</button>
    </div>

    <div class="feedback-box" id="feedback"></div>

    <button class="btn-next" id="btn-next" onclick="nextWord()">Nächstes Wort &rarr;</button>
</div>

<script>
    const vocabularyLevels = {
        1: [
            { article: "die", noun: "Wohngemeinschaft / WG", plural: "-en / -s", english: "shared flat", hint: "Compounds with '-gemeinschaft' take 'die'." },
            { article: "die", noun: "Wohnung", plural: "-en", english: "flat / apartment", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "das", noun: "Apartment", plural: "-s", english: "flat / apartment", hint: "Modern loan words ending flatly are often neuter." },
            { article: "die", noun: "Küche", plural: "-n", english: "kitchen", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "das", noun: "Bad", plural: "-er", english: "bathroom", hint: "Monosyllabic root neuter spatial room." },
            { article: "die", noun: "Toilette", plural: "-n", english: "toilet", hint: "Borrowed words ending in standard '-e' map as feminine." },
            { article: "der", noun: "Flur", plural: "-e", english: "entrance hall", hint: "Strong structural tracking corridor item." },
            { article: "das", noun: "Wohnzimmer", plural: "-", english: "living room", hint: "Compound word. Ends with 'das Zimmer'." },
            { article: "das", noun: "Schlafzimmer", plural: "-", english: "bedroom", hint: "Compound word. Ends with 'das Zimmer'." },
            { article: "das", noun: "Kinderzimmer", plural: "-", english: "children's room", hint: "Compound word. Ends with 'das Zimmer'." },
            { article: "das", noun: "Arbeitszimmer", plural: "-e", english: "study", hint: "Compound word. Ends with 'das Zimmer'." },
            { article: "das", noun: "Billardzimmer", plural: "-", english: "pool room, billards/pool hall", hint: "Compound word. Ends with 'das Zimmer'." },
            { article: "das", noun: "Erdgeschoss", plural: "-e", english: "ground floor", hint: "Compound word ending with structural unit 'das Geschoss'." },
            { article: "das", noun: "Dachgeschoss", plural: "-e", english: "attic storey", hint: "Compound word ending with structural unit 'das Geschoss'." },
            { article: "der", noun: "Stock", plural: "Stockwerke", english: "floor / storey", hint: "Strong core masculine structure baseline item." },
            { article: "der", noun: "Keller", plural: "-", english: "basement / cellar", hint: "Nouns ending in generic utility form '-er' are mostly masculine." },
            { article: "die", noun: "Balkon", plural: "-e", english: "balcony", hint: "Borrowed structural architectural elements skew masculine/mixed." },
            { article: "der", noun: "Garten", plural: "-ä-", english: "garden", hint: "Core environmental outdoor spaces terminating in -en are masculine." },
            { article: "die", noun: "Terrasse", plural: "-n", english: "terrace", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Spielplatz", plural: "-ä-e", english: "playground", hint: "Compound word ending with 'der Platz'." }
        ],
        2: [
            { article: "die", noun: "Miete", plural: "-n", english: "rent", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Mietpreis", plural: "-e", english: "rental price", hint: "Compound word ending with 'der Preis'." },
            { article: "der", noun: "Mieter", plural: "-", english: "tenant (male)", hint: "Masculine agent suffix denoting human occupations '-er'." },
            { article: "die", noun: "Mieterin", plural: "-nen", english: "tenant (female)", hint: "Feminine professional status suffix transformation '-in'." },
            { article: "die", noun: "Nebenkosten", plural: "Plural only", english: "running costs", hint: "Plural-only accounting aggregate term." },
            { article: "der", noun: "Quadratmeter", plural: "-", english: "square metre", hint: "Compound ending with standard dimensional unit 'der Meter'." },
            { article: "die", noun: "Anzeige", plural: "-n", english: "ad", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "das", noun: "Mehrfamilienhaus", plural: "-ä-er", english: "multiple-family dwelling", hint: "Compound word ending with 'das Haus'." },
            { article: "die", noun: "Hausordnung", plural: "-en", english: "house rules", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "der", noun: "Bewohner", plural: "-", english: "resident (male)", hint: "Masculine human agent noun formatting suffix '-er'." },
            { article: "die", noun: "Bewohnerin", plural: "-nen", english: "resident (female)", hint: "Feminine human occupation suffix configuration '-in'." },
            { article: "der", noun: "Mitbewohner", plural: "-", english: "flat mate (male)", hint: "Masculine occupant unit formatting structural suffix '-er'." },
            { article: "die", noun: "Mitbewohnerin", plural: "-nen", english: "flat mate (female)", hint: "Feminine occupant unit mapping configuration suffix '-in'." },
            { article: "die", noun: "Nachbarin", plural: "-nen", english: "neighbour (female)", hint: "Feminine relational target suffix alignment '-in'." },
            { article: "der", noun: "Nachbar", plural: "-n", english: "neighbour (male)", hint: "Weak masculine foundational personal entity." },
            { article: "die", noun: "Tür", plural: "-en", english: "door", hint: "Strong feminine monosyllabic structural entry." },
            { article: "das", noun: "Fenster", plural: "-", english: "window", hint: "Neuter architectural opening element terminating in '-er'." },
            { article: "die", noun: "Treppe", plural: "-n", english: "staircase / stairs", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Ecke", plural: "-n", english: "corner", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Platz", plural: "Sg.", english: "space", hint: "Monosyllabic conceptual allocation is masculine." }
        ],
        3: [
            { article: "der", noun: "Kühlschrank", plural: "-ä-e", english: "fridge", hint: "Compound word ending with structural containment 'der Schrank'." },
            { article: "der", noun: "Herd", plural: "-e", english: "cooker", hint: "Strong masculine mechanical utility kitchen baseline appliance." },
            { article: "die", noun: "Spülmaschine", plural: "-n", english: "dishwasher", hint: "Compound word ending with standard engine term 'die Maschine'." },
            { article: "die", noun: "Waschmaschine", plural: "-n", english: "washing machine", hint: "Compound word ending with standard engine term 'die Maschine'." },
            { article: "die", noun: "Heizung", plural: "-en", english: "radiator / heating", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "die", noun: "Dusche", plural: "-n", english: "shower", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Steckdose", plural: "-n", english: "socket", hint: "Compound word ending in generic containment '-e' (die Dose)." },
            { article: "die", noun: "Klingel", plural: "-n", english: "doorbell", hint: "Feminine tracking device structure ending in typical structural form." },
            { article: "das", noun: "Licht", plural: "Sg.", english: "light", hint: "Natural physics elements and light categories skew neuter." },
            { article: "der", noun: "Fernseher", plural: "-", english: "television", hint: "Masculine device agent form formatting ending in '-er'." },
            { article: "das", noun: "Smartphone", plural: "-s", english: "smartphone", hint: "Modern technical global loans are structurally neuter." },
            { article: "das", noun: "Foto", plural: "-s", english: "photo", hint: "International terms ending in structural vocalic 'o' are neuter." },
            { article: "das", noun: "Geschirr", plural: "Sg.", english: "dishes", hint: "Collective groupings configured with prefix 'Ge-' skew neuter." },
            { article: "der", noun: "Topf", plural: "-ö-e", english: "pot", hint: "Strong physical cooking utility containment unit is masculine." },
            { article: "der", noun: "Boden", plural: "-ö-", english: "floor", hint: "Foundational flat surfaces ending in structural '-en' are masculine." },
            { article: "der", noun: "Abfall", plural: "-ä-e", english: "rubbish / trash", hint: "Derived from verbal root system (abfallen) - masculine form." },
            { article: "der", noun: "Müll", plural: "Sg.", english: "rubbish / trash", hint: "Strong core concept aggregate content structural baseline." },
            { article: "die", noun: "Unordnung", plural: "Sg.", english: "mess", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "der", noun: "Haushalt", plural: "-e", english: "housekeeping", hint: "Compound word terminating with nominalized verb tracking 'das Leben'." },
            { article: "die", noun: "Sachen", plural: "Plural only", english: "things", hint: "Plural aggregate designation tracking form." }
        ],
        4: [
            { article: "das", noun: "Großraumbüro", plural: "-s", english: "open-plan office", hint: "Compound word ending with workspace classification 'das Büro'." },
            { article: "das", noun: "Zweierbüro", plural: "-s", english: "office for two", hint: "Compound word ending with workspace classification 'das Büro'." },
            { article: "das", noun: "Einzelbüro", plural: "-s", english: "individual office", hint: "Compound word ending with workspace classification 'das Büro'." },
            { article: "der", noun: "Empfang", plural: "Sg.", english: "reception", hint: "Derived from core verbal prefix system (empfangen) - masculine." },
            { article: "der", noun: "Kopierraum", plural: "-ä-e", english: "copy room", hint: "Compound word ending with structural cell 'der Raum'." },
            { article: "die", noun: "Teeküche", plural: "-n", english: "kitchenette", hint: "Compound word ending with structural item 'die Küche'." },
            { article: "die", noun: "Kantine", plural: "-n", english: "canteen", hint: "Loan words mapping dining locations often end in feminine configurations." },
            { article: "der", noun: "Beamer", plural: "-", english: "video projector", hint: "Modern technical agent loan unit ending in standard '-er'." },
            { article: "der", noun: "Lautsprecher", plural: "-", english: "speaker", hint: "Compound ending with tool agent configuration 'der Sprecher'." },
            { article: "das", noun: "Headset", plural: "-s", english: "headset", hint: "Anglophone technical configuration standard is neuter." },
            { article: "der", noun: "Ordner", plural: "-", english: "file / binder", hint: "Masculine configuration agent formatting ending in '-er'." },
            { article: "die", noun: "Datei", plural: "-en", english: "digital file", hint: "Nouns ending in abstract system configuration suffix '-ei' are feminine." },
            { article: "die", noun: "Software", plural: "Sg.", english: "software", hint: "Abstract modern technological system imports map as feminine." },
            { article: "der", noun: "Tacker", plural: "-", english: "stapler", hint: "Utility device transformation notation ending in '-er'." },
            { article: "der", noun: "Locher", plural: "-", english: "hole punch", hint: "Utility tool operational format ending in '-er'." },
            { article: "die", noun: "Schere", plural: "-n", english: "scissors", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Textmarker", plural: "-", english: "highlighter", hint: "Compound tool descriptor ending in agent notation '-er'." },
            { article: "der", noun: "Briefumschlag", plural: "-ä-e", english: "envelope", hint: "Compound word ending with dynamic root 'der Umschlag'." },
            { article: "das", noun: "Notizzettel", plural: "-", english: "notepad paper", hint: "Compound formatting targeting paper elements ('das Zettel/Blatt')." },
            { article: "der", noun: "Papierkorb", plural: "-ö-e", english: "paper basket", hint: "Compound word ending with container designation 'der Korb'." }
        ],
        5: [
            { article: "das", noun: "Berufsleben", plural: "Sg.", english: "working life", hint: "Compound word terminating with nominalized verb tracking 'das Leben'." },
            { article: "die", noun: "Stelle", plural: "-n", english: "job", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Halbtagsstelle", plural: "-n", english: "half-day job", hint: "Compound placement ending with job unit 'die Stelle'." },
            { article: "die", noun: "Teilzeit", plural: "Sg.", english: "part-time", hint: "Compound temporal tracker ending with standard 'die Zeit'." },
            { article: "das", noun: "Homeoffice", plural: "Sg.", english: "work from home", hint: "Modern global corporate technical import maps as neuter." },
            { article: "das", noun: "Vorstellungsgespräch", plural: "-e", english: "job interview", hint: "Compound word terminating with dialogue concept 'das Gespräch'." },
            { article: "das", noun: "Start-up", plural: "-s", english: "start-up company", hint: "Modern dynamic enterprise import standard maps as neuter." },
            { article: "das", noun: "Marketing", plural: "Sg.", english: "marketing", hint: "Anglophone abstract corporate structural activities evaluate as neuter." },
            { article: "das", noun: "Logistik", plural: "Sg.", english: "logistics", hint: "Abstract science and organizational classifications ending in '-ik' take 'die'." },
            { article: "die", noun: "Abteilung", plural: "-en", english: "department", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "der", noun: "Chef", plural: "-s", english: "boss (male)", hint: "Natural masculine assignment based on direct status notation." },
            { article: "die", noun: "Chefin", plural: "-nen", english: "boss (female)", hint: "Feminine professional status suffix transformation '-in'." },
            { article: "der", noun: "Kunde", plural: "-n", english: "client / customer (male)", hint: "Weak masculine personal profile element ending in '-e'." },
            { article: "die", noun: "Kundin", plural: "-nen", english: "client / customer (female)", hint: "Feminine personal professional customer alignment suffix '-in'." },
            { article: "das", noun: "Geld", plural: "Sg.", english: "money", hint: "Neuter baseline unit for currency asset frameworks." },
            { article: "der", noun: "Fachmann", plural: "Fachleute", english: "specialist (male)", hint: "Natural masculine personal entity ending in 'der Mann'." },
            { article: "die", noun: "Fachfrau", plural: "-en", english: "specialist (female)", hint: "Natural feminine personal entity ending in 'die Frau'." },
            { article: "die", noun: "Fachleute", plural: "Plural only", english: "specialists", hint: "Plural collective human group classification form." },
            { article: "die", noun: "Selbstständigkeit", plural: "Sg.", english: "independence", hint: "Nouns ending in the suffix '-keit' are always 100% feminine." },
            { article: "der", noun: "Profi", plural: "-s", english: "professional", hint: "Shortened colloquial personal identification label maps as masculine." }
        ],
        6: [
            { article: "die", noun: "Besprechung", plural: "-en", english: "meeting", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "die", noun: "Projektleitung", plural: "-en", english: "project management", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "das", noun: "Projekt", plural: "-e", english: "project", hint: "Latinate structural abstract target units evaluate as neuter." },
            { article: "der", noun: "Plan", plural: "-ä-e", english: "plan / map", hint: "Strong core masculine abstract tracking structural grid item." },
            { article: "der", noun: "Workflow", plural: "-s", english: "workflow", hint: "Modern structural corporate tracking paths evaluate as masculine." },
            { article: "die", noun: "Organisation", plural: "Sg.", english: "organisation", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "die", noun: "Teamarbeit", plural: "Sg.", english: "teamwork", hint: "Compound word terminating with task classification 'die Arbeit'." },
            { article: "das", noun: "Team", plural: "-s", english: "team", hint: "Collective organizational corporate units from English are neuter." },
            { article: "der", noun: "Workshop", plural: "-s", english: "workshop", hint: "Corporate dynamic tracking blocks map as masculine structures." },
            { article: "die", noun: "Präsentation", plural: "-en", english: "presentation", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "das", noun: "Modell", plural: "-e", english: "model", hint: "Technical representations ending in typical structure formats are neuter." },
            { article: "das", noun: "Programm", plural: "-e", english: "program", hint: "Greek-derived international structures ending in double consonants take 'das'." },
            { article: "die", noun: "Agentur", plural: "-en", english: "agency", hint: "Abstract institutions matching corporate loan frames take 'die'." },
            { article: "die", noun: "Werbung", plural: "-en", english: "advertising", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "die", noun: "Kommunikation", plural: "Sg.", english: "communication", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "die", noun: "Medien", plural: "Plural only", english: "media", hint: "Plural collection layout for communication frameworks." },
            { article: "die", noun: "Website", plural: "-s", english: "website", hint: "Modern digital container layouts take feminine formatting." },
            { article: "die", noun: "Webseite", plural: "-n", english: "webpage", hint: "Compound word tracking written sheet formatting 'die Seite'." },
            { article: "die", noun: "App", plural: "-s", english: "app", hint: "Abbreviated technical systems from English map as feminine." },
            { article: "das", noun: "Video", plural: "-s", english: "video", hint: "International terms ending in vocalic formatting elements take 'das'." }
        ],
        7: [
            { article: "der", noun: "Anwalt", plural: "-ä-e", english: "lawyer (male)", hint: "Natural masculine personal occupational standard alignment." },
            { article: "die", noun: "Anwältin", plural: "-nen", english: "lawyer (female)", hint: "Feminine professional suffix mapping conversion layout '-in'." },
            { article: "der", noun: "Polizist", plural: "-en", english: "police officer (male)", hint: "Masculine human tracking classifications ending in '-ist'." },
            { article: "die", noun: "Polizistin", plural: "-en", english: "police officer (female)", hint: "Feminine occupational tracking layout suffix '-in'." },
            { article: "der", noun: "Fotograf", plural: "-en", english: "photographer (male)", hint: "Masculine operational human tracking designations ending in '-graf'." },
            { article: "die", noun: "Fotografin", plural: "-nen", english: "photographer (female)", hint: "Feminine structural configuration layout suffix format '-in'." },
            { article: "der", noun: "Blogger", plural: "-", english: "blogger (male)", hint: "Masculine informational media agent profile tracking suffix '-er'." },
            { article: "die", noun: "Bloggerin", plural: "-nen", english: "blogger (female)", hint: "Feminine informational tracking structural option layout '-in'." },
            { article: "der", noun: "Influencer", plural: "-", english: "influencer (male)", hint: "Masculine visibility personal agent platform profile suffix '-er'." },
            { article: "die", noun: "Influencerin", plural: "-nen", english: "influencer (female)", hint: "Feminine platform system structural execution profile suffix '-in'." },
            { article: "der", noun: "Berater", plural: "-", english: "consultant (male)", hint: "Masculine advisory human agent design signature suffix '-er'." },
            { article: "die", noun: "Beraterin", plural: "-nen", english: "consultant (female)", hint: "Feminine corporate advisory profile specification layout '-in'." },
            { article: "der", noun: "Manager", plural: "-", english: "manager (male)", hint: "Masculine enterprise system agent formatting layout suffix '-er'." },
            { article: "die", noun: "Managerin", plural: "-nen", english: "manager (female)", hint: "Feminine enterprise task manager profile format layout '-in'." },
            { article: "der", noun: "Psychologe", plural: "-n", english: "psychologist (male)", hint: "Masculine weak noun layout detailing scientific human tracking." },
            { article: "die", noun: "Psychologin", plural: "-nen", english: "psychologist (female)", hint: "Feminine clinical tracking operational layout notation '-in'." },
            { article: "der", noun: "Experte", plural: "-n", english: "expert (male)", hint: "Weak masculine identification marker structure configuration." },
            { article: "die", noun: "Expertin", plural: "-nen", english: "expert (female)", hint: "Feminine tracking capacity knowledge designation structure '-in'." },
            { article: "der", noun: "Spezialist", plural: "-en", english: "specialist (male)", hint: "Masculine human focus field designation target layout '-ist'." },
            { article: "die", noun: "Spezialistin", plural: "-nen", english: "specialist (female)", hint: "Feminine tracking target competency design notation '-in'." }
        ],
        8: [
            { article: "der", noun: "Handwerker", plural: "-", english: "craftsman", hint: "Masculine trade structural agent design execution suffix '-er'." },
            { article: "die", noun: "Handwerkerin", plural: "-nen", english: "craftswoman", hint: "Feminine trade technical profile specification tracking suffix '-in'." },
            { article: "der", noun: "Krankenpfleger", plural: "-", english: "nurse (male)", hint: "Masculine medical care service agent framework formatting '-er'." },
            { article: "die", noun: "Krankenpflegerin", plural: "-nen", english: "nurse (female)", hint: "Feminine care provider professional layout definition format '-in'." },
            { article: "der", noun: "Koch", plural: "-ö-e", english: "chef / cook (male)", hint: "Strong core masculine kitchen authority marker designation." },
            { article: "die", noun: "Köchin", plural: "-nen", english: "chef / cook (female)", hint: "Feminine kitchen execution status designation format suffix '-in'." },
            { article: "der", noun: "Politiker", plural: "-", english: "politician (male)", hint: "Masculine state administrative agent layout specification suffix '-er'." },
            { article: "die", noun: "Politikerin", plural: "-nen", english: "politician (female)", hint: "Feminine governance administrative role alignment design suffix '-in'." },
            { article: "der", noun: "Astronaut", plural: "-en", english: "astronaut (male)", hint: "Masculine scientific aerospace tracking identification framework." },
            { article: "die", noun: "Astronautin", plural: "-nen", english: "astronaut (female)", hint: "Feminine aerospace professional task design specification '-in'." },
            { article: "der", noun: "Trainer", plural: "-", english: "trainer (male)", hint: "Masculine functional development system supervisor format '-er'." },
            { article: "die", noun: "Trainerin", plural: "-nen", english: "trainer (female)", hint: "Feminine target skill system capability guide format '-in'." },
            { article: "der", noun: "Coach", plural: "-es", english: "coach", hint: "Imported human training role standard evaluates as masculine structure." },
            { article: "der", noun: "Bachelor", plural: "-", english: "bachelor's degree", hint: "Academic credential loan elements map as masculine entities." },
            { article: "das", noun: "Semester", plural: "-", english: "semester", hint: "Academic timeline measurement intervals take neuter layout configurations." },
            { article: "die", noun: "Note", plural: "-n", english: "mark / grade", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Prüfung", plural: "-en", english: "exam", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "die", noun: "Schule", plural: "-en", english: "school", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Grundschule", plural: "-n", english: "primary school", hint: "Compound word ending with educational institution 'die Schule'." },
            { article: "der", noun: "Kindergarten", plural: "-ä-", english: "kindergarten", hint: "Compound word terminating with terrain landscape 'der Garten'." }
        ],
        9: [
            { article: "der", noun: "Körper", plural: "-", english: "body", hint: "Anatomical structural master framework terminating in '-er' is masculine." },
            { article: "das", noun: "Körperteil", plural: "-e", english: "body part", hint: "Compound word ending with component category division 'das Teil'." },
            { article: "der", noun: "Kopf", plural: "-ö-e", english: "head", hint: "Strong singular masculine command anatomy block structure." },
            { article: "das", noun: "Auge", plural: "-n", english: "eye", hint: "Exceptions to the typical vocalic final rule; eye is neuter." },
            { article: "die", noun: "Nase", plural: "-n", english: "nose", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "das", noun: "Ohr", plural: "-en", english: "ear", hint: "Core sensory processing singular sound target block is neuter." },
            { article: "der", noun: "Mund", plural: "-ü-er", english: "mouth", hint: "Strong expressive articulation singular structural orifice is masculine." },
            { article: "der", noun: "Hals", plural: "-ä-e", english: "neck / throat", hint: "Strong structural connector trunk unit is masculine." },
            { article: "die", noun: "Brust", plural: "Sg.", english: "chest", hint: "Monosyllabic anatomical core segment taking feminine alignment." },
            { article: "der", noun: "Bauch", plural: "-ä-e", english: "belly", hint: "Strong dynamic metabolic physical container region is masculine." },
            { article: "der", noun: "Arm", plural: "-e", english: "arm", hint: "Strong locomotive tool projection core is masculine." },
            { article: "die", noun: "Hand", plural: "-ä-e", english: "hand", hint: "Core operational manual extremity executing as feminine." },
            { article: "der", noun: "Finger", plural: "-", english: "finger", hint: "Anatomical sub-digit tracking configuration ending in '-er' is masculine." },
            { article: "das", noun: "Bein", plural: "-e", english: "leg", hint: "Core locomotive support structural body framework is neuter." },
            { article: "das", noun: "Knie", plural: "-", english: "knee", hint: "Structural structural join tracking zone is neuter." },
            { article: "der", noun: "Schmerz", plural: "-en", english: "ache / pain", hint: "Physical sensation feedback root item maps as masculine." },
            { article: "die", noun: "Krankheit", plural: "-en", english: "disease / illness", hint: "Nouns ending in the suffix '-heit' are always 100% feminine." },
            { article: "das", noun: "Übergewicht", plural: "Sg.", english: "overweight", hint: "Compound word terminating with mass unit calculation 'das Gewicht'." },
            { article: "das", noun: "Herz", plural: "-en", english: "heart", hint: "Unique irregular anatomical core engine noun evaluates as neuter." },
            { article: "das", noun: "Fieber", plural: "Sg.", english: "fever", hint: "Symptomatic thermal processing state evaluates as neuter format." }
        ],
        10: [
            { article: "der", noun: "Schnupfen", plural: "Sg.", english: "cold / catarrh", hint: "Substantivized medical response behaviors ending in '-en' are masculine." },
            { article: "die", noun: "Erkältung", plural: "-en", english: "cold", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "der", noun: "Husten", plural: "Sg.", english: "cough", hint: "Substantivized medical reflexive action ending in '-en' is masculine." },
            { article: "der", noun: "Hustensaft", plural: "-ä-e", english: "cough syrup", hint: "Compound fluid solution ending with base type 'der Saft'." },
            { article: "das", noun: "Medikament", plural: "-e", english: "medicine", hint: "Nouns ending in the suffix '-ment' are always 100% neuter." },
            { article: "die", noun: "Tablette", plural: "-n", english: "pill", hint: "Borrowed medical product forms matching vocalic rules take 'die'." },
            { article: "die", noun: "Salbe", plural: "-n", english: "ointment / salve", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Honig", plural: "Sg.", english: "honey", hint: "Nouns terminating in structural format marker '-ig' are masculine." },
            { article: "die", noun: "Apotheke", plural: "-n", english: "pharmacy", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "das", noun: "Krankenhaus", plural: "-ä-er", english: "hospital", hint: "Compound word ending with spatial unit destination 'das Haus'." },
            { article: "die", noun: "Reparatur", plural: "-en", english: "repair", hint: "Loan structures terminating in suffix format '-ur' take 'die'." },
            { article: "die", noun: "Bewegung", plural: "-en", english: "exercise / movement", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "der", noun: "Ratschlag", plural: "-ä-e", english: "advice", hint: "Compound abstract delivery terminal ending in 'der Schlag'." },
            { article: "die", noun: "Ruhe", plural: "Sg.", english: "rest", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Gesundheit", plural: "Sg.", english: "health", hint: "Nouns ending in the suffix '-heit' are always 100% feminine." },
            { article: "die", noun: "Situation", plural: "-en", english: "situation", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "der", noun: "Grund", plural: "-ü-e", english: "reason", hint: "Strong conceptual causal base element evaluated as masculine." },
            { article: "der", noun: "Fehler", plural: "-", english: "mistake", hint: "Abstract default deviation unit ending in standard form '-er'." },
            { article: "die", noun: "Umfrage", plural: "-n", english: "survey", hint: "Compound question query structure matching standard vocalic rule." },
            { article: "die", noun: "Bitte", plural: "-n", english: "request", hint: "Nouns ending in '-e' are ~90% feminine." }
        ],
        11: [
            { article: "die", noun: "Kleidung", plural: "Sg.", english: "clothes", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "die", noun: "Klamotten", plural: "Plural only", english: "clothes (colloquial)", hint: "Plural-only colloquial fashion grouping identifier." },
            { article: "die", noun: "Billigkleidung", plural: "Sg.", english: "fast fashion", hint: "Compound asset layout ending with standard collection 'die Kleidung'." },
            { article: "die", noun: "Secondhandkleidung", plural: "Sg.", english: "second-hand clothes", hint: "Compound asset block ending with generic target 'die Kleidung'." },
            { article: "das", noun: "Kleidungsstück", plural: "-e", english: "article of clothing", hint: "Compound word terminating with distinct unit component 'das Stück'." },
            { article: "die", noun: "Tauschbörse", plural: "-n", english: "clothing swap exchange", hint: "Compound system ending with standard market concept 'die Börse'." },
            { article: "der", noun: "Billigladen", plural: "-ä-", english: "cut-price shop", hint: "Compound word ending with operational storefront unit 'der Laden'." },
            { article: "die", noun: "Qualität", plural: "-en", english: "quality", hint: "Nouns terminating in the abstract suffix unit '-ität' are 100% feminine." },
            { article: "die", noun: "Kombination", plural: "-en", english: "combination", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "der", noun: "Pullover", plural: "-", english: "pullover", hint: "Garment imports configured into standard terminal structures take 'der'." },
            { article: "das", noun: "Hemd", plural: "-en", english: "shirt", hint: "Foundational structural upper torso garment core is neuter." },
            { article: "die", noun: "Bluse", plural: "-n", english: "blouse", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Hose", plural: "-n", english: "trousers", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Jeans", plural: "-", english: "jeans", hint: "Anglophone product item tracking collective layout maps as feminine." },
            { article: "das", noun: "Kleid", plural: "-er", english: "dress", hint: "Foundational singular fashion body element core evaluated as neuter." },
            { article: "der", noun: "Rock", plural: "-ö-e", english: "skirt", hint: "Strong historical lower-body base configuration is masculine." },
            { article: "der", noun: "Anzug", plural: "-ü-e", english: "suit", hint: "Derived from vertical action framework patterns - masculine form." },
            { article: "der", noun: "Mantel", plural: "-ä-", english: "coat", hint: "Garment protective configurations ending in '-el' skew masculine." },
            { article: "der", noun: "Hut", plural: "-ü-e", english: "hat", hint: "Strong distinct cranial structural cover element is masculine." },
            { article: "die", noun: "Mütze", plural: "-n", english: "cap", hint: "Nouns ending in '-e' are ~90% feminine." }
        ],
        12: [
            { article: "der", noun: "Schuh", plural: "-e", english: "shoe", hint: "Strong manual mobile base traction hardware unit is masculine." },
            { article: "der", noun: "Stiefel", plural: "-", english: "boot", hint: "Protective tall structural tracking devices ending in '-el' are masculine." },
            { article: "die", noun: "Socke", plural: "-n", english: "sock", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Strumpf", plural: "-ü-e", english: "stocking", hint: "Strong compact tight textile insulation layer is masculine." },
            { article: "der", noun: "Bart", plural: "-ä-e", english: "beard", hint: "Cranial androgenic organic follicle layer is masculine." },
            { article: "die", noun: "Locke", plural: "-n", english: "curl", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Haare", plural: "Plural only", english: "hair", hint: "Plural presentation standard when targeting head coverage asset sets." },
            { article: "die", noun: "Natur", plural: "Sg.", english: "nature", hint: "System ecosystems matching tracking framework formatting take 'die'." },
            { article: "der", noun: "Baum", plural: "-ä-e", english: "tree", hint: "Vertical solid forest botanical life forms are masculine." },
            { article: "die", noun: "Wiese", plural: "-n", english: "meadow", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Fluss", plural: "-ü-e", english: "river", hint: "Linear fluid hydrological active pathways are masculine." },
            { article: "der", noun: "See", plural: "-n", english: "lake", hint: "Be careful: 'der See' is lake, while 'die See' identifies open ocean." },
            { article: "das", noun: "Meer", plural: "-e", english: "sea", hint: "Neuter baseline unit for tracking expansive maritime sheets." },
            { article: "der", noun: "Strand", plural: "-ä-e", english: "beach", hint: "Granular coastal layout tracking structure evaluates as masculine." },
            { article: "die", noun: "Insel", plural: "-n", english: "island", hint: "Geographical structural isolations ending in '-el' take 'die'." },
            { article: "der", noun: "Dschungel", plural: "-", english: "jungle", hint: "Climatic ecosystem blocks ending in structural formatting map as masculine." },
            { article: "die", noun: "Wüste", plural: "-n", english: "desert", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Berg", plural: "-e", english: "mountain", hint: "Vertical geological massive structural entities are masculine." },
            { article: "der", noun: "Park", plural: "-s", english: "park", hint: "Managed urban environment enclaves take masculine orientation." },
            { article: "der", noun: "Tierpark", plural: "-s", english: "zoo", hint: "Compound word terminating with environmental space 'der Park'." }
        ],
        13: [
            { article: "der", noun: "Regen", plural: "Sg.", english: "rain", hint: "Precipitation types and weather formats evaluate as masculine." },
            { article: "der", noun: "Schnee", plural: "Sg.", english: "snow", hint: "Frozen crystal weather precipitation standards are masculine." },
            { article: "der", noun: "Schneemann", plural: "-ä-er", english: "snowman", hint: "Compound structural persona unit ending with 'der Mann'." },
            { article: "das", noun: "Gewitter", plural: "-", english: "thunderstorm", hint: "Meteorological phenomenon groupings prefixed with 'Ge-' evaluate as neuter." },
            { article: "der", noun: "Hagel", plural: "Sg.", english: "hail", hint: "Solid frozen atmospheric drops ending in '-el' are masculine." },
            { article: "die", noun: "Wolke", plural: "-n", english: "cloud", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Wind", plural: "-e", english: "wind", hint: "Kinetic dynamic gas currents in meteorology are masculine." },
            { article: "der", noun: "Nebel", plural: "-", english: "fog", hint: "Suspended moisture atmospheric layer ending in standard '-el' is masculine." },
            { article: "das", noun: "Grad", plural: "-e", english: "degree", hint: "Neuter classification baseline format tracking scaling steps." },
            { article: "der", noun: "Himmel", plural: "Sg.", english: "sky", hint: "Celestial canopy container environment maps as masculine." },
            { article: "der", noun: "Mond", plural: "Sg.", english: "moon", hint: "Foundational distinct planetary tracking satellite is masculine." },
            { article: "die", noun: "Welt", plural: "Sg.", english: "world", hint: "Strong foundational macro sphere context category identifier." },
            { article: "die", noun: "Region", plural: "-en", english: "region", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "die", noun: "Umwelt", plural: "Sg.", english: "environment", hint: "Compound global biosphere matrix ending with macro context 'die Welt'." },
            { article: "das", noun: "Ausland", plural: "Sg.", english: "foreign countries", hint: "Compound location matrix ending with physical terrain 'das Land'." },
            { article: "das", noun: "Afrika", plural: "Sg.", english: "Africa", hint: "Geographical continents without descriptor modifiers evaluate as neuter." },
            { article: "das", noun: "Europa", plural: "Sg.", english: "Europe", hint: "Geographical continents without descriptor modifiers evaluate as neuter." },
            { article: "das", noun: "Indien", plural: "Sg.", english: "India", hint: "Geographical nations without descriptor modifiers evaluate as neuter." },
            { article: "das", noun: "Italien", plural: "Sg.", english: "Italy", hint: "Geographical nations without descriptor modifiers evaluate as neuter." },
            { article: "das", noun: "Norwegen", plural: "Sg.", english: "Norway", hint: "Geographical nations without descriptor modifiers evaluate as neuter." },
            { article: "der", noun: "Pelikan", plural: "-e", english: "pelican", hint: "Exotic animal definitions ending in specific consonants skew masculine." }
        ],
        14: [
            { article: "die", noun: "Stadt", plural: "-ä-e", english: "city / town", hint: "Strong foundational feminine single cell urban cluster core." },
            { article: "die", noun: "Stadtmitte", plural: "-en", english: "city centre", hint: "Compound word terminating with focal anchor element 'die Mitte'." },
            { article: "das", noun: "Zentrum", plural: "Zentren", english: "centre", hint: "Nouns ending in classical configuration suffix '-um' are 100% neuter." },
            { article: "die", noun: "Altstadt", plural: "-ä-e", english: "old town", hint: "Compound word tracking core localization system 'die Stadt'." },
            { article: "das", noun: "Viertel", plural: "-", english: "district / part of town", hint: "Fractional regional measurements ending in standard format layout are neuter." },
            { article: "der", noun: "Platz", plural: "-ä-e", english: "public square", hint: "Strong singular masculine designated urban node locator point." },
            { article: "der", noun: "Weg", plural: "-e", english: "way / path", hint: "Strong vector connection routing line standard is masculine." },
            { article: "die", noun: "Kreuzung", plural: "-en", english: "crossroads", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "die", noun: "Ampel", plural: "-n", english: "traffic lights", hint: "Feminine routing guide mechanism tracking standard final format." },
            { article: "die", noun: "Brücke", plural: "-n", english: "bridge", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Meter", plural: "-", english: "metre", hint: "Metric unit scalar tracking baselines are structured as masculine." },
            { article: "der", noun: "Aufzug", plural: "-ü-e", english: "lift / elevator", hint: "Verbal derivation describing mechanical vector lifting action - masculine." },
            { article: "die", noun: "Autobahn", plural: "-en", english: "motorway", hint: "Compound tracking grid terminating with pathway vector 'die Bahn'." },
            { article: "der", noun: "Fuß", plural: "-ü-e", english: "foot", hint: "Foundational locomotion anatomical baseline terminal is masculine." },
            { article: "der", noun: "Fahrer", plural: "-", english: "driver (male)", hint: "Masculine traffic agent designation profile suffix formatting '-er'." },
            { article: "die", noun: "Fahrerin", plural: "-nen", english: "driver (female)", hint: "Feminine traffic execution capacity alignment suffix marker '-in'." },
            { article: "der", noun: "Fußgänger", plural: "-", english: "pedestrian (male)", hint: "Masculine locomotive transit actor suffix configuration '-er'." },
            { article: "die", noun: "Fußgängerin", plural: "-nen", english: "pedestrian (female)", hint: "Feminine transit tracking profile structure design suffix '-in'." },
            { article: "der", noun: "Roller", plural: "-", english: "scooter", hint: "Mechanical mobile utility platform format notation ending in '-er'." },
            { article: "das", noun: "Motorrad", plural: "-ä-er", english: "motorbike", hint: "Compound word terminating with dynamic wheel element 'das Rad'." }
        ],
        15: [
            { article: "das", noun: "Kaufhaus", plural: "-ä-er", english: "department store", hint: "Compound word ending with destination base context 'das Haus'." },
            { article: "die", noun: "Bank", plural: "-en", english: "bank", hint: "Institutional fiscal entities map as structural feminine units." },
            { article: "die", noun: "Post", plural: "Sg.", english: "post office", hint: "Logistics infrastructure facility segment taking standard feminine article." },
            { article: "die", noun: "Polizei", plural: "Sg.", english: "police", hint: "Abstract enforcement institutions ending in structural form '-ei' are feminine." },
            { article: "die", noun: "Bibliothek", plural: "-en", english: "library", hint: "Greek structural loan configurations tracking repositories take 'die'." },
            { article: "der", noun: "Zoo", plural: "-s", english: "zoo", hint: "Short international animal park loan markers evaluate as masculine." },
            { article: "der", noun: "Brunnen", plural: "-", english: "fountain", hint: "Hydrological structural utilities ending in standard '-en' are masculine." },
            { article: "der", noun: "Markt", plural: "-ä-e", english: "market", hint: "Strong central transaction territorial configuration is masculine." },
            { article: "der", noun: "Rathaus", plural: "-ä-er", english: "town hall", hint: "Compound word evaluating down to primary target base 'das Haus'." },
            { article: "der", noun: "Schloss", plural: "-ö-er", english: "castle", hint: "Historical strategic macro compound site framework maps as neuter." },
            { article: "die", noun: "Kirche", plural: "-n", english: "church", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Einwohner", plural: "-", english: "inhabitant", hint: "Masculine regional demographic actor signature suffix form '-er'." },
            { article: "der", noun: "Mensch", plural: "-en", english: "human being", hint: "Foundational personal entity tracking classification - mixed weak masculine." },
            { article: "die", noun: "Leute", plural: "Plural only", english: "people", hint: "Plural-only collective personal human population tracker." },
            { article: "der", noun: "Mitmensch", plural: "-en", english: "fellow man", hint: "Compound target layer tracking baseline person 'der Mensch'." },
            { article: "die", noun: "Generation", plural: "-en", english: "generation", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "die", noun: "Politik", plural: "Sg.", english: "politics", hint: "Abstract administrative sciences terminating in suffix unit '-ik' take 'die'." },
            { article: "die", noun: "Religion", plural: "-en", english: "religion", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "das", noun: "Recht", plural: "Sg.", english: "law", hint: "Abstract systemic legal foundational concepts register as neuter." },
            { article: "die", noun: "Mauer", plural: "-n", english: "(Berlin) Wall", hint: "Protective continuous masonry barriers take feminine assignment patterns." }
        ],
        16: [
            { article: "das", noun: "Festival", plural: "-s", english: "festival", hint: "Cultural mass entertainment loan frameworks evaluate as neuter." },
            { article: "die", noun: "Kultur", plural: "Sg.", english: "culture", hint: "Abstract social system domains ending in structural format '-ur' take 'die'." },
            { article: "die", noun: "Kunst", plural: "Sg.", english: "art", hint: "Feminine abstract creative operational performance classification." },
            { article: "das", noun: "Märchen", plural: "-", english: "fairy tale", hint: "Nouns ending in the diminutive suffix element '-chen' are always 100% neuter." },
            { article: "der", noun: "Roman", plural: "-e", english: "novel", hint: "Literary narrative medium structures take masculine format tags." },
            { article: "der", noun: "Kinderfilm", plural: "-e", english: "children's film", hint: "Compound media projection format ending with 'der Film'." },
            { article: "das", noun: "Spiel", plural: "-e", english: "game", hint: "Core recreational activity framework unit evaluates as neuter." },
            { article: "das", noun: "Wortspiel", plural: "-e", english: "pun / wordplay", hint: "Compound ludic activity ending with baseline core 'das Spiel'." },
            { article: "das", noun: "Lied", plural: "-er", english: "song", hint: "Core acoustic creative musical singular format unit is neuter." },
            { article: "die", noun: "Aktivität", plural: "-en", english: "activity", hint: "Nouns terminating in the abstract suffix unit '-ität' are 100% feminine." },
            { article: "die", noun: "Veranstaltung", plural: "-en", english: "event", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "das", noun: "Ereignis", plural: "-se", english: "event", hint: "Abstract occurrences terminating in core system suffix '-nis' skew neuter." },
            { article: "das", noun: "Freien", plural: "Sg.", english: "outdoors", hint: "Substantivized space layout context used in phrase 'im Freien' - neuter." },
            { article: "das", noun: "Picknick", plural: "-s", english: "picnic", hint: "Outdoor culinary activity configuration checks out as neuter." },
            { article: "das", noun: "Grillfest", plural: "-e", english: "barbecue party", hint: "Compound tracking structural unit ending with target 'das Fest'." },
            { article: "der", noun: "Grill", plural: "-s", english: "grill", hint: "Mechanical thermal food apparatus hardware is masculine." },
            { article: "das", noun: "Zelt", plural: "-e", english: "tent", hint: "Foundational flexible canvas structure module evaluated as neuter." },
            { article: "das", noun: "Boot", plural: "-e", english: "boat", hint: "Core floatation transit displacement platform maps as neuter." },
            { article: "das", noun: "Reisebüro", plural: "-s", english: "travel agency", hint: "Compound word tracking terminal corporate structure 'das Büro'." },
            { article: "das", noun: "Päckchen", plural: "-", english: "small parcel", hint: "Nouns ending in the diminutive suffix element '-chen' are always 100% neuter." }
        ],
        17: [
            { article: "das", noun: "Grillfleisch", plural: "Sg.", english: "barbecued meat", hint: "Compound biological matter tracking food type 'das Fleisch'." },
            { article: "das", noun: "Gemüse", plural: "Sg.", english: "vegetables", hint: "Botanical culinary group matrices prefixed with tracking 'Ge-' are neuter." },
            { article: "der", noun: "Tofu", plural: "Sg.", english: "tofu", hint: "Global non-native nutrition products evaluate mostly as masculine." },
            { article: "der", noun: "Ball", plural: "-ä-e", english: "ball", hint: "Strong baseline kinetic spherical physical sports item is masculine." },
            { article: "der", noun: "Volleyball", plural: "Sg.", english: "volleyball sport", hint: "Sports named after their tracking baseline gear share its masculine article." },
            { article: "der", noun: "Volleyballplatz", plural: "-ä-e", english: "volleyball court", hint: "Compound word terminating with spatial tracking block 'der Platz'." },
            { article: "das", noun: "Frisbee", plural: "-s", english: "frisbee", hint: "Dynamic recreational kinetic aerodynamic plastic disk is neuter." },
            { article: "der", noun: "Triathlon", plural: "-s", english: "triathlon", hint: "Athletic multicourse structural events take masculine markers." },
            { article: "das", noun: "Training", plural: "Sg.", english: "training", hint: "Sports activity concepts adopting modern formatting map as neuter." },
            { article: "das", noun: "Instrument", plural: "-e", english: "musical instrument", hint: "Nouns ending in the suffix '-ment' are always 100% neuter." },
            { article: "das", noun: "Haustier", plural: "-e", english: "pet", hint: "Compound tracking biological organism base 'das Tier'." },
            { article: "der", noun: "Hund", plural: "-e", english: "dog", hint: "Strong core tracking biological fauna baseline is masculine." },
            { article: "die", noun: "Katze", plural: "-n", english: "cat", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "das", noun: "Kamel", plural: "-e", english: "camel", hint: "Exotic zoological transport ungulates take neuter designations." },
            { article: "der", noun: "Hai", plural: "-e", english: "shark", hint: "Marine predator apex classifications take masculine markers." },
            { article: "die", noun: "Informatik", plural: "Sg.", english: "computer science", hint: "Abstract logic sciences terminating in suffix unit '-ik' take 'die'." },
            { article: "das", noun: "Werkzeug", plural: "-e", english: "tool", hint: "Compound utility apparatus ending with active material 'das Zeug'." },
            { article: "der", noun: "Gegenstand", plural: "-ä-e", english: "object / thing", hint: "Compound structural design element ending with 'der Stand'." },
            { article: "der", noun: "Lifestyle", plural: "-s", english: "lifestyle", hint: "Anglophone existential framework concepts take masculine designations." },
            { article: "der", noun: "Schlaf", plural: "Sg.", english: "sleep", hint: "Abstract verbal root transformations mapping physical states are masculine." }
        ],
        18: [
            { article: "die", noun: "Liebe", plural: "Sg.", english: "love", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Sympathie", plural: "-n", english: "sympathy", hint: "Abstract personal affinity markers matching final formatting rules take 'die'." },
            { article: "das", noun: "Paar", plural: "-e", english: "couple", hint: "Dual-element relational unit matrix structures register as neuter." },
            { article: "die", noun: "Hochzeit", plural: "-en", english: "wedding", hint: "Compound celebratory standard ending with tracking segment 'die Zeit'." },
            { article: "der / die", noun: "Bekannte", plural: "-n", english: "acquaintance", hint: "Substantivized adjective shifting profiles matching biological subject." },
            { article: "das", noun: "Treffen", plural: "-", english: "get-together", hint: "Nominalized infinitive action frameworks are always 100% neuter." },
            { article: "die", noun: "Pause", plural: "-n", english: "break", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Karneval", plural: "Sg.", english: "carnival", hint: "Traditional festive tracking celebration epochs take masculine markers." },
            { article: "die", noun: "Feiertag", plural: "-e", english: "holiday", hint: "Compound chronological block segment ending with 'der Tag' (masculine)." },
            { article: "das", noun: "Ostern", plural: "Sg.", english: "Easter", hint: "Sacred seasonal timeline markers operate without tracking modifiers as neuter." },
            { article: "das", noun: "Neujahr", plural: "Sg.", english: "New Year", hint: "Compound calendrical target cell ending with chronological 'das Jahr'." },
            { article: "der", noun: "Glückwunsch", plural: "-ü-e", english: "congratulation", hint: "Compound expressive act ending with emotional core 'der Wunsch'." },
            { article: "die", noun: "Karte", plural: "-n", english: "card / ticket", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "die", noun: "Kreditkarte", plural: "-n", english: "credit card", hint: "Compound processing token ending with validation unit 'die Karte'." },
            { article: "der", noun: "Führerschein", plural: "-e", english: "driving licence", hint: "Compound credential document ending with verification unit 'der Schein'." },
            { article: "das", noun: "Verbot", plural: "-e", english: "ban / prohibition", hint: "Abstract restrictive declaration derived from root format group rules." },
            { article: "die", noun: "Aktion", plural: "-en", english: "campaign / action", hint: "International loan terms ending in the suffix '-ion' are 100% feminine." },
            { article: "das", noun: "Angebot", plural: "-e", english: "offer", hint: "Derived administrative proposal output block evaluates as neuter." },
            { article: "die", noun: "Lösung", plural: "-en", english: "solution", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "der", noun: "Tipp", plural: "-s", english: "tip / advice", hint: "Short actionable informational unit imports register as masculine." },
            { article: "der", noun: "Kommentar", plural: "-e", english: "comment", hint: "Textual evaluations ending in structured consonant layers skew masculine." }
        ],
        19: [
            { article: "das", noun: "Datum", plural: "Daten", english: "date", hint: "Nouns ending in classical configuration suffix '-um' are 100% neuter." },
            { article: "die", noun: "Zukunft", plural: "Sg.", english: "future", hint: "Abstract upcoming horizon timeline classification takes feminine article." },
            { article: "der", noun: "Unfall", plural: "-ä-e", english: "accident", hint: "Dynamic kinetic interruption event ending with baseline action 'der Fall'." },
            { article: "die", noun: "Angst", plural: "-ä-e", english: "anxiety / fear", hint: "Internal psychological stress response monosyllabic core takes 'die'." },
            { article: "das", noun: "Netz", plural: "Sg.", english: "network signal", hint: "Interconnected data capture infrastructure standard is neuter." },
            { article: "die", noun: "Nähe", plural: "Sg.", english: "proximity", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Blick", plural: "-e", english: "glance / sight", hint: "Visual sensory projection root element evaluates as masculine." },
            { article: "die", noun: "Szene", plural: "Sg.", english: "scene", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Schritt", plural: "-e", english: "step", hint: "Physical dynamic advancement unit increment registers as masculine." },
            { article: "der", noun: "Spruch", plural: "-ü-e", english: "slogan / saying", hint: "Oral abstract structural expression forms register as masculine." },
            { article: "das", noun: "Kompliment", plural: "-e", english: "compliment", hint: "Nouns ending in the suffix '-ment' are always 100% neuter." },
            { article: "die", noun: "Notiz", plural: "-en", english: "written note", hint: "Short informational capture sheets ending in hard consonants take 'die'." },
            { article: "die", noun: "Einleitung", plural: "-en", english: "introduction", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "die", noun: "Erfahrung", plural: "-en", english: "experience", hint: "Nouns ending in the suffix '-ung' are always 100% feminine." },
            { article: "der", noun: "Konflikt", plural: "-e", english: "conflict", hint: "Opposition interactive structural dynamics register as masculine." },
            { article: "der", noun: "Superstar", plural: "-s", english: "superstar", hint: "Media icon profiling entities from English assume masculine profiles." },
            { article: "der", noun: "Helm", plural: "-e", english: "helmet", hint: "Solid cranial preservation armor shell models are masculine." },
            { article: "die", noun: "Leine", plural: "-n", english: "leash / rope", hint: "Nouns ending in '-e' are ~90% feminine." },
            { article: "der", noun: "Wahnsinn", plural: "Sg.", english: "madness", hint: "Compound psychological metrics ending with concept tracking 'der Sinn'." },
            { article: "das", noun: "Magazin", plural: "-e", english: "magazine", hint: "Information collection print mediums take neuter structures." },
            { article: "die", noun: "Bürogemeinschaft", plural: "-en", english: "joint office setup", hint: "Compounds with '-gemeinschaft' take 'die'." }
        ]
    };

    let activeLevel = 1;
    let maxLevel = 1; 
    let deck = []; 
    let levelCompletedNouns = new Set(); 
    let levelCorrectCountLog = {}; 
    let levelStats = { correctCount: 0, totalAttempts: 0 };
    let currentItem = null;
    let hasAnswered = false;

    function initGame() {
        activeLevel = 1;
        maxLevel = Math.max(...Object.keys(vocabularyLevels).map(Number));
        deck = [];
        resetLevelMetrics();
        appendLevelWords(activeLevel);
        updateUi();
        nextWord();
    }

    function resetLevelMetrics() {
        levelCompletedNouns.clear();
        levelCorrectCountLog = {};
        levelStats = { correctCount: 0, totalAttempts: 0 };
    }

    function appendLevelWords(levelNum) {
        const newWords = vocabularyLevels[levelNum].map(item => ({...item, streak: 0}));
        deck = [...deck, ...newWords].sort(() => Math.random() - 0.5);
    }

    function isFinalLevel() {
        return activeLevel === maxLevel;
    }

    function calculateProgressPercentage() {
        let masteredProgress = levelCompletedNouns.size * 10;
        
        let incrementalProgress = 0;
        for (let noun in levelCorrectCountLog) {
            if (levelCompletedNouns.has(noun)) {
                continue; 
            }
            let correctCount = levelCorrectCountLog[noun];
            let points = Math.floor(correctCount / 2);
            incrementalProgress += Math.min(points, 2);
        }

        let baseProgress = masteredProgress + incrementalProgress;

        let accuracyVal = 0;
        if (levelStats.totalAttempts > 0) {
            accuracyVal = Math.round((levelStats.correctCount / levelStats.totalAttempts) * 100);
        }

        if (accuracyVal < 70) {
            let difference = 70 - accuracyVal;
            baseProgress -= difference;
        }

        if (baseProgress < 0) baseProgress = 0;
        if (baseProgress > 100) baseProgress = 100;
        
        return baseProgress;
    }

    function updateUi() {
        let accuracyPercentage = 0;
        if (levelStats.totalAttempts > 0) {
            accuracyPercentage = Math.round((levelStats.correctCount / levelStats.totalAttempts) * 100);
        }
        document.getElementById('accuracy-rating').innerText = `${accuracyPercentage}%`;
        document.getElementById('current-level').innerText = activeLevel;

        const containerLabel = document.getElementById('dynamic-stat-label');
        if (isFinalLevel()) {
            let totalRemainingCount = deck.length + (currentItem && !hasAnswered ? 1 : 0);
            containerLabel.innerHTML = `Remaining Words: <span id="progress-next-level">${totalRemainingCount}</span>`;
        } else {
            containerLabel.innerHTML = `Level-Fortschritt: <span id="progress-next-level">${calculateProgressPercentage()}%</span>`;
        }
    }

    function safeInsertIntoDeck(wordItem, targetIndex) {
        let index = targetIndex;
        if (index > deck.length) index = deck.length;

        while (index < deck.length && deck[index].noun === wordItem.noun) {
            index++;
        }
        if (index === 0 && deck.length > 0 && deck[0].noun === wordItem.noun) {
            index = 1;
        }

        deck.splice(index, 0, wordItem);
    }

    function triggerEndGameDisplay() {
        document.getElementById('word-target').innerText = "Ausgezeichnet! 👑";
        document.getElementById('word-plural').innerText = "You have mastered and cleared all vocabulary modules from Momente A1.2!";
        document.getElementById('word-streak').style.display = 'none';
        document.getElementById('btn-peek').style.display = 'none';
        document.getElementById('peek-display').style.display = 'none';
        document.getElementById('choices-container').style.display = 'none';
        document.getElementById('feedback').style.display = 'none';
        document.getElementById('btn-next').style.display = 'none';
    }

    function nextWord() {
        if (!isFinalLevel()) {
            let currentProgress = calculateProgressPercentage();
            if (currentProgress >= 100 && vocabularyLevels[activeLevel + 1]) {
                activeLevel++;
                alert(`Level Up! 🎉 Loading the Level ${activeLevel} vocabulary package into your running deck!`);
                resetLevelMetrics();
                appendLevelWords(activeLevel);
                updateUi();
            }
        }

        let uniqueNounsInRotation = new Set(deck.map(w => w.noun));
        if (currentItem) uniqueNounsInRotation.add(currentItem.noun);

        let unmasteredWords = [...uniqueNounsInRotation].filter(noun => !levelCompletedNouns.has(noun));

        if (uniqueNounsInRotation.size === 0 || (uniqueNounsInRotation.size <= 2 && unmasteredWords.length === 0)) {
            triggerEndGameDisplay();
            return;
        }

        hasAnswered = false;
        
        if (deck.length > 1 && currentItem && deck[0].noun === currentItem.noun) {
            let duplicate = deck.shift();
            safeInsertIntoDeck(duplicate, 1);
        }

        currentItem = deck.shift(); 
        
        document.getElementById('word-target').innerText = currentItem.noun;
        document.getElementById('word-plural').innerText = `Plural: ${currentItem.plural}`;
        document.getElementById('word-streak').innerText = `Trefferserie: ${currentItem.streak}/3`;
        
        const retireBoxContainer = document.getElementById('retire-container');
        const checkbox = document.getElementById('chk-retire');
        checkbox.checked = false;
        if (currentItem.streak >= 3) {
            retireBoxContainer.style.display = 'flex';
        } else {
            retireBoxContainer.style.display = 'none';
        }

        document.getElementById('btn-peek').style.display = 'inline-block';
        const peekDisplay = document.getElementById('peek-display');
        peekDisplay.style.display = 'none';
        peekDisplay.innerText = '';

        const feedbackBox = document.getElementById('feedback');
        feedbackBox.style.display = 'none';
        feedbackBox.className = 'feedback-box';
        document.getElementById('btn-next').style.display = 'none';
        
        const buttons = document.querySelectorAll('.btn-gender');
        buttons.forEach(btn => {
            btn.style.opacity = '1';
            btn.style.pointerEvents = 'auto';
        });

        updateUi();
    }

    function peekTranslation() {
        const peekDisplay = document.getElementById('peek-display');
        peekDisplay.innerText = `Meaning: "${currentItem.english}"`;
        peekDisplay.style.display = 'block';
        document.getElementById('btn-peek').style.display = 'none';
    }

    function submitAnswer(chosenGender) {
        if (hasAnswered) return;
        hasAnswered = true;

        levelStats.totalAttempts++;
        
        // Minor alteration applied: Safely matches flexible strings like "der / die" using include logic
        const isCorrect = currentItem.article.includes(chosenGender);
        const feedbackBox = document.getElementById('feedback');
        const chkRetire = document.getElementById('chk-retire');
        
        document.getElementById('retire-container').style.display = 'none';

        const buttons = document.querySelectorAll('.btn-gender');
        buttons.forEach(btn => btn.style.pointerEvents = 'none');

        if (isCorrect) {
            levelStats.correctCount++;
            currentItem.streak++; 

            if (!levelCorrectCountLog[currentItem.noun]) {
                levelCorrectCountLog[currentItem.noun] = 0;
            }
            levelCorrectCountLog[currentItem.noun]++;

            if (levelCorrectCountLog[currentItem.noun] >= 4) {
                levelCompletedNouns.add(currentItem.noun);
            }

            const shouldPurge = (currentItem.streak >= 3 && chkRetire && chkRetire.checked);

         // Create the capitalized version once here, so both messages can use it
            let capitalizedArticle = currentItem.article.charAt(0).toUpperCase() + currentItem.article.slice(1);

            if (shouldPurge) {
                document.getElementById('btn-peek').style.display = 'none';
                document.getElementById('peek-display').style.display = 'none';
                feedbackBox.innerHTML = `
                    <span class="reveal-header">Richtig! 📦✨</span>
                    <span>Wort gelernt! <b><i>${capitalizedArticle} ${currentItem.noun}</i></b> ist nicht mehr auf der Liste. 🤓</span>
                `;
            } else {
                feedbackBox.innerHTML = `
                    <span class="reveal-header">Richtig! 🎉</span>
                    <span><b style="font-size: 1.1rem;"><i>${capitalizedArticle} ${currentItem.noun}</i></b></span>
                    <span class="rule-hint">Aktuelle Serie: ${currentItem.streak}</span>
                `;
                const randomPos = Math.floor(Math.random() * deck.length) + 2;
                safeInsertIntoDeck(currentItem, randomPos);
            }
            feedbackBox.classList.add('feedback-success');
       } else {
            currentItem.streak = 0;

            // Capitalize the article for the wrong answer message too
            let capitalizedArticle = currentItem.article.charAt(0).toUpperCase() + currentItem.article.slice(1);

            document.getElementById('btn-peek').style.display = 'none';
            document.getElementById('peek-display').style.display = 'none';

            feedbackBox.innerHTML = `
                <span class="reveal-header">Falsch. ❌</span>
                <span style="font-size: 1.5rem;">☝️🤓 <b>${capitalizedArticle} ${currentItem.noun}</b></span>
                <span class="english-translation">English: "${currentItem.english}"</span>
                <span class="rule-hint"><b>Tip:</b> ${currentItem.hint}</span>
            `;
            feedbackBox.classList.add('feedback-danger');

            safeInsertIntoDeck(currentItem, 4);
        }

        feedbackBox.style.display = 'block';
        document.getElementById('btn-next').style.display = 'block';
        updateUi();
    }

    window.onload = initGame;
</script>

</body>
</html>

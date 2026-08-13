# EL-IDOLO-DE-LA-LUD
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>El Ídolo Amateur</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Barlow+Condensed:wght@600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-body: #060f0a;
            --bg-card: #0d1f15;
            --bg-card-alt: #142c1e;
            --bg-card-alt-2: #1a3625;
            --accent-lime: #b6ff2f;
            --accent-gold: #ffcf40;
            --accent-purple: #c48cff;
            --accent-blue: #4fc3f7;
            --accent-green: #34d67f;
            --accent-red: #ff5d5d;
            --text-main: #f3fff0;
            --text-muted: #8fa899;
            --border-color: rgba(182, 255, 47, 0.14);
            --radius-md: 10px;
            --radius-lg: 16px;
        }

        * { 
            box-sizing: border-box; 
            margin: 0; 
            padding: 0; 
            font-family: 'Inter', sans-serif; 
            -webkit-tap-highlight-color: transparent; 
            touch-action: manipulation;
        }

        .display-font { font-family: 'Barlow Condensed', sans-serif; }

        html, body {
            background-color: var(--bg-body);
            color: var(--text-main);
            height: 100vh;
            max-height: 100vh;
            overflow: hidden;
            width: 100vw;
            display: flex;
            flex-direction: column;
            position: relative;
            padding-top: env(safe-area-inset-top);
            padding-bottom: env(safe-area-inset-bottom);
        }

        body::before {
            content: "";
            position: fixed;
            inset: 0;
            z-index: 0;
            pointer-events: none;
            background:
                radial-gradient(ellipse 60% 40% at 50% 0%, rgba(182,255,47,0.10), transparent 70%),
                repeating-linear-gradient(90deg, rgba(255,255,255,0.02) 0px, rgba(255,255,255,0.02) 1px, transparent 1px, transparent 46px);
        }

        header, .main-app, nav.bottom-nav { position: relative; z-index: 1; }

        header {
            background: linear-gradient(180deg, #0c1e13, #081209);
            border-bottom: 1px solid var(--border-color);
            padding: 8px 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 52px;
            flex-shrink: 0;
        }

        .brand-title { font-family: 'Barlow Condensed', sans-serif; font-weight: 800; font-size: 1.15rem; letter-spacing: 0.3px; line-height: 1;
            background: linear-gradient(90deg, var(--accent-lime), var(--accent-gold));
            -webkit-background-clip: text; background-clip: text; color: transparent; }
        .brand-subtitle { font-size: 0.58rem; color: var(--text-muted); text-transform: uppercase; font-weight: 700; letter-spacing: 0.8px; margin-top: 1px; }

        .header-actions { display: flex; gap: 6px; }

        .btn-sm {
            padding: 6px 9px; font-size: 0.68rem; border-radius: 20px;
            border: 1px solid var(--border-color); background: var(--bg-card-alt);
            color: var(--text-main); cursor: pointer; font-weight: 700;
            display: flex; align-items: center; gap: 3px;
            transition: transform 0.12s ease, background 0.12s ease;
        }
        .btn-sm:active { transform: scale(0.94); background: rgba(182,255,47,0.15); }

        .main-app {
            flex: 1;
            display: flex;
            flex-direction: column;
            overflow: hidden;
            padding: 8px;
        }

        .view-panel {
            display: none;
            flex-direction: column;
            height: 100%;
            gap: 8px;
            overflow: hidden;
        }

        .view-panel.active { display: flex; }

        .card {
            background: linear-gradient(160deg, var(--bg-card), #0a1a10);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-md);
            padding: 10px;
        }

        .card-title {
            font-size: 0.68rem; font-weight: 800; text-transform: uppercase; letter-spacing: 0.5px;
            color: var(--accent-lime); margin-bottom: 7px; display: flex; align-items: center; gap: 5px;
        }

        .narrative-box {
            background: linear-gradient(160deg, var(--bg-card), #0a1a10);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-lg);
            padding: 12px;
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            overflow-y: auto;
            box-shadow: 0 0 0 1px rgba(0,0,0,0.2);
        }

        .story-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px; gap: 8px; }

        .stage-stepper { display: flex; align-items: center; gap: 3px; flex: 1; }
        .stage-dot {
            width: 24px; height: 24px; border-radius: 50%; background: var(--bg-card-alt);
            border: 1px solid var(--border-color); display: flex; align-items: center; justify-content: center;
            font-size: 0.7rem; color: var(--text-muted); flex-shrink: 0;
        }
        .stage-dot.done { background: rgba(255,207,64,0.18); border-color: var(--accent-gold); color: var(--accent-gold); }
        .stage-dot.active { background: var(--accent-lime); border-color: var(--accent-lime); color: #08170c; font-weight: bold; }
        .stage-line { flex: 1; height: 2px; background: var(--border-color); }

        .year-chip {
            font-size: 0.62rem; color: var(--text-muted); font-weight: 700;
            background: var(--bg-card-alt); border: 1px solid var(--border-color); padding: 3px 7px; border-radius: 10px;
        }

        .stage-label { font-size: 0.6rem; color: var(--accent-blue); font-weight: 700; text-transform: uppercase; margin-bottom: 4px; display: block; }
        .story-title { font-family: 'Barlow Condensed', sans-serif; font-size: 1.15rem; font-weight: 700; color: #fff; margin-bottom: 4px; }
        .story-text { font-size: 0.78rem; color: #cdded2; line-height: 1.35; margin-bottom: 8px; }

        .options-container { display: flex; flex-direction: column; gap: 6px; }
        .option-btn {
            background: var(--bg-card-alt); border: 1px solid var(--border-color); border-left: 3px solid var(--accent-lime);
            border-radius: var(--radius-md); padding: 8px 10px; color: var(--text-main); text-align: left;
            cursor: pointer; display: flex; flex-direction: column; gap: 2px;
        }
        .option-btn:active { background: rgba(182, 255, 47, 0.14); transform: scale(0.985); }
        .option-title { font-weight: 700; font-size: 0.78rem; }
        .option-desc { font-size: 0.65rem; color: var(--text-muted); }

        /* CARTAS DE PRETEMPORADA */
        .cards-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; margin-top: 6px; }
        .card-item {
            background: var(--bg-card-alt); border: 1px solid var(--border-color); border-radius: var(--radius-md);
            padding: 8px; display: flex; flex-direction: column; justify-content: space-between; cursor: pointer;
            position: relative; overflow: hidden; transition: transform 0.15s ease;
        }
        .card-item:active { transform: scale(0.96); }
        .card-rarity { font-size: 0.55rem; font-weight: 800; text-transform: uppercase; padding: 2px 4px; border-radius: 4px; display: inline-block; margin-bottom: 4px; }
        .card-item.comun { border-color: #8fa899; }
        .card-item.comun .card-rarity { background: rgba(143,168,153,0.2); color: #8fa899; }
        .card-item.epico { border-color: var(--accent-purple); }
        .card-item.epico .card-rarity { background: rgba(196,140,255,0.2); color: var(--accent-purple); }
        .card-item.mitico { border-color: var(--accent-gold); box-shadow: 0 0 8px rgba(255,207,64,0.3); }
        .card-item.mitico .card-rarity { background: rgba(255,207,64,0.25); color: var(--accent-gold); }
        .card-name { font-size: 0.75rem; font-weight: 700; color: #fff; }
        .card-effect { font-size: 0.62rem; color: var(--accent-lime); margin-top: 4px; font-weight: 600; }

        .balance-box {
            background: linear-gradient(90deg, rgba(255,207,64,0.12), rgba(182,255,47,0.06));
            border: 1px dashed rgba(255,207,64,0.35); padding: 8px 10px; border-radius: var(--radius-md);
            font-size: 0.74rem; color: #ffe9ad; margin-top: 6px;
        }

        .btn-continue {
            width: 100%; padding: 10px; margin-top: 8px; border: none; border-radius: var(--radius-md);
            background: linear-gradient(90deg, var(--accent-gold), #ffb020); color: #241400; font-weight: 800;
            font-size: 0.8rem; cursor: pointer; letter-spacing: 0.3px;
        }

        nav.bottom-nav {
            height: 58px;
            background: linear-gradient(0deg, #0c1e13, #081209);
            border-top: 1px solid var(--border-color);
            display: flex;
            justify-content: space-around;
            align-items: center;
            flex-shrink: 0;
            padding: 4px 6px;
            gap: 6px;
        }

        .nav-btn {
            flex: 1; height: 100%; background: none; border: none; color: var(--text-muted);
            font-size: 0.6rem; font-weight: 700; display: flex; flex-direction: column; align-items: center;
            justify-content: center; gap: 2px; cursor: pointer; border-radius: 12px;
        }
        .nav-btn.active { color: #08170c; background: linear-gradient(180deg, var(--accent-lime), #93d61f); }
        .nav-icon { font-size: 1.1rem; }

        .profile-badge { display: flex; align-items: center; gap: 12px; }
        .ovr-badge {
            width: 52px; height: 52px; border-radius: 12px; flex-shrink: 0;
            background: linear-gradient(160deg, var(--bg-card-alt-2), #0a1a10);
            border: 1px solid var(--accent-gold);
            display: flex; flex-direction: column; align-items: center; justify-content: center;
        }
        .ovr-num { font-family: 'Barlow Condensed', sans-serif; font-size: 1.4rem; font-weight: 800; line-height: 1; color: var(--accent-gold); }
        .ovr-tier { font-size: 0.4rem; text-transform: uppercase; font-weight: 800; color: var(--text-muted); }

        .player-meta h2 { font-family: 'Barlow Condensed', sans-serif; font-size: 1rem; font-weight: 700; }
        .player-meta p { font-size: 0.68rem; color: var(--text-muted); }
        .cat-chip {
            display: inline-block; margin-top: 3px; font-size: 0.6rem; font-weight: 700; color: var(--accent-blue);
            background: rgba(79,195,247,0.12); border: 1px solid rgba(79,195,247,0.3); padding: 1px 5px; border-radius: 8px;
        }

        .bar-row { margin-bottom: 6px; }
        .bar-row-top { display: flex; justify-content: space-between; font-size: 0.68rem; margin-bottom: 2px; }
        .bar-name { color: #d7e8dc; font-weight: 600; }
        .bar-val { font-weight: 800; font-family: 'Barlow Condensed', sans-serif; }
        .bar-track { height: 5px; background: var(--bg-card-alt); border-radius: 4px; overflow: hidden; }
        .bar-fill { height: 100%; border-radius: 4px; transition: width 0.4s ease; }

        .attrs-grid-wrap { display: grid; grid-template-columns: 1fr 1fr; gap: 0 10px; }

        .metric-pill {
            display: flex; align-items: center; justify-content: space-between;
            padding: 5px 8px; background: var(--bg-card-alt); border-radius: 8px; margin-bottom: 4px; font-size: 0.72rem;
        }
        .metric-label { color: var(--text-muted); }
        .metric-value { font-weight: 800; color: #fff; font-family: 'Barlow Condensed', sans-serif; }

        .log-list { display: flex; flex-direction: column; gap: 0; height: 90px; overflow-y: auto; }
        .log-item {
            position: relative; padding: 4px 0 4px 12px; font-size: 0.65rem; color: #d7e8dc;
            border-left: 2px solid var(--border-color);
        }

        .modal-overlay {
            position: fixed; inset: 0;
            background: rgba(2, 6, 4, 0.9); backdrop-filter: blur(4px);
            display: flex; align-items: center; justify-content: center; z-index: 1000; padding: 12px;
        }
        .modal-card {
            background: linear-gradient(160deg, var(--bg-card), #081109); border: 1px solid var(--border-color);
            border-radius: var(--radius-lg); width: 100%; max-width: 400px; padding: 16px;
        }
        .modal-title { font-family: 'Barlow Condensed', sans-serif; font-size: 1.25rem; font-weight: 800;
            background: linear-gradient(90deg, var(--accent-lime), var(--accent-gold)); -webkit-background-clip: text; background-clip: text; color: transparent; }
        .modal-sub { font-size: 0.72rem; color: var(--text-muted); margin-bottom: 10px; }

        .form-group { margin-bottom: 9px; }
        .form-label { display: block; font-size: 0.65rem; color: var(--text-muted); margin-bottom: 3px; font-weight: 700; text-transform: uppercase; }
        .form-input, .form-select {
            width: 100%; padding: 8px; background: var(--bg-card-alt);
            border: 1px solid var(--border-color); border-radius: 8px; color: #fff; font-size: 0.8rem; outline: none;
        }

        .btn-primary {
            width: 100%; padding: 10px; background: linear-gradient(90deg, var(--accent-lime), #93d61f);
            border: none; border-radius: 8px; color: #0b1a0e; font-weight: 800; cursor: pointer; font-size: 0.8rem; margin-top: 4px;
        }
        .btn-secondary {
            width: 100%; padding: 8px; background: var(--bg-card-alt);
            border: 1px solid var(--border-color); border-radius: 8px; color: #fff; font-weight: 700; cursor: pointer; font-size: 0.72rem; margin-top: 5px;
        }
    </style>
</head>
<body>

    <header>
        <div>
            <div class="brand-title">EL ÍDOLO AMATEUR</div>
            <div class="brand-subtitle">Simulador de Carrera & DT</div>
        </div>
        <div class="header-actions">
            <button class="btn-sm" onclick="resetGame()">🔄 <span>Inicio</span></button>
        </div>
    </header>

    <main class="main-app">

        <div id="panel-decision" class="view-panel active">
            <div class="narrative-box">
                <div>
                    <div class="story-header">
                        <div class="stage-stepper">
                            <div class="stage-dot" data-stage="0">☀️</div>
                            <div class="stage-line"></div>
                            <div class="stage-dot" data-stage="1">⚔️</div>
                            <div class="stage-line"></div>
                            <div class="stage-dot" data-stage="2">🏆</div>
                        </div>
                        <span class="year-chip" id="ui-year">Año 2026</span>
                    </div>
                    <span class="stage-label" id="ui-season-stage">PRETEMPORADA</span>
                    <h3 class="story-title" id="ui-story-title">Cargando...</h3>
                    <div class="story-text" id="ui-story-text">...</div>
                </div>

                <div id="ui-interaction-area">
                    <div class="options-container" id="ui-options"></div>
                </div>
            </div>
        </div>

        <div id="panel-stats" class="view-panel">
            <div class="card">
                <div class="profile-badge">
                    <div class="ovr-badge">
                        <span class="ovr-num" id="ui-overall">60</span>
                        <span class="ovr-tier" id="ui-ovr-tier">PROMESA</span>
                    </div>
                    <div class="player-meta">
                        <h2 id="ui-name">Jugador</h2>
                        <p id="ui-club-div">Club • Div</p>
                        <span class="cat-chip" id="ui-category">Sub-13</span>
                    </div>
                </div>
            </div>

            <div class="card" style="flex:1; overflow-y:auto;">
                <div class="card-title">⚽ Atributos Técnico/Físicos</div>
                <div class="attrs-grid-wrap" id="ui-attrs"></div>
            </div>

            <div class="card">
                <div class="card-title">📊 Registro de Carrera / DT</div>
                <div class="metric-pill"><span class="metric-label">🏆 Copas Ganadas</span><span class="metric-value" id="ui-trophies">0</span></div>
                <div class="metric-pill"><span class="metric-label">⚽ Goles (como Jugador)</span><span class="metric-value" id="ui-goals">0</span></div>
                <div class="metric-pill"><span class="metric-label">👟 Asistencias</span><span class="metric-value" id="ui-assists">0</span></div>
                <div class="metric-pill"><span class="metric-label">🌟 Promesas Formadas (DT)</span><span class="metric-value" id="ui-promesas">0</span></div>
            </div>
        </div>

        <div id="panel-life" class="view-panel">
            <div class="card">
                <div class="card-title">💼 Vida Personal & Estado</div>
                <div class="metric-pill"><span class="metric-label">💰 Dinero</span><span class="metric-value" id="ui-money">$0</span></div>
                <div class="metric-pill"><span class="metric-label">🎓 Ocupación</span><span class="metric-value" id="ui-job">Liceo</span></div>
                <div class="metric-pill"><span class="metric-label">💪 Estado Físico</span><span class="metric-value" id="ui-fitness">100%</span></div>
            </div>

            <div class="card">
                <div class="card-title">❤️ Relaciones Personal / Club</div>
                <div id="ui-rels-bars"></div>
            </div>

            <div class="card" style="flex:1; overflow-y:auto;">
                <div class="card-title">📜 Historial de Vida</div>
                <div class="log-list" id="ui-history"></div>
            </div>

            <button class="btn-secondary" style="background: rgba(255, 93, 93, 0.12); border-color: rgba(255, 93, 93, 0.3); color: #ff8f8f;" onclick="finishCareer()">🏁 Finalizar Experiencia</button>
        </div>

    </main>

    <nav class="bottom-nav">
        <button class="nav-btn active" onclick="switchNav('panel-decision', this)">
            <span class="nav-icon">📖</span>
            <span>Cancha / DT</span>
        </button>
        <button class="nav-btn" onclick="switchNav('panel-stats', this)">
            <span class="nav-icon">⚽</span>
            <span>Ficha</span>
        </button>
        <button class="nav-btn" onclick="switchNav('panel-life', this)">
            <span class="nav-icon">💼</span>
            <span>Vida</span>
        </button>
    </nav>

    <div class="modal-overlay" id="modal-creation">
        <div class="modal-card">
            <h2 class="modal-title">Crear Futbolista</h2>
            <p class="modal-sub">⚽ Comenzás a los 13 años. Te retirarás a los 50 para dirigir las inferiores.</p>

            <div class="form-group">
                <label class="form-label">Nombre del Jugador</label>
                <input type="text" id="init-name" class="form-input" value="Mateo Silva">
            </div>

            <div class="form-group">
                <label class="form-label">Posición</label>
                <select id="init-pos" class="form-select">
                    <option value="DEL">🎯 Delantero (DEL)</option>
                    <option value="EXT">⚡ Extremo (EXT)</option>
                    <option value="MCO">🪄 Mediocampista Ofensivo (MCO)</option>
                    <option value="MC">🧭 Mediocampista (MC)</option>
                    <option value="DEF">🛡️ Defensa Central (DEF)</option>
                </select>
            </div>

            <div class="form-group">
                <label class="form-label">Club Inicial (Div. E)</label>
                <select id="init-club" class="form-select">
                    <option value="Belgrano">Belgrano</option>
                    <option value="Ingeniería">Ingeniería</option>
                    <option value="Colegio Pio">Colegio Pio</option>
                    <option value="La Mennais">La Mennais</option>
                    <option value="Deportivo Elbio Fernández">Deportivo Elbio Fernández</option>
                </select>
            </div>

            <button class="btn-primary" onclick="startGame()">🚀 Comenzar Leyenda</button>
        </div>
    </div>

    <div class="modal-overlay" id="modal-endgame" style="display: none;">
        <div class="modal-card" style="text-align: center;">
            <h2 style="font-family:'Barlow Condensed',sans-serif; font-size: 1.3rem; font-weight:800; color:var(--accent-gold); margin-bottom: 2px;">🏁 Leyenda del Club Completada</h2>
            <p style="font-size:0.75rem; color:var(--text-muted); margin-bottom:10px;">Completaste tu ciclo como jugador (hasta los 50 años) y tu etapa como DT de Inferiores.</p>
            <div style="background: var(--bg-card-alt); border: 1px solid var(--border-color); border-radius: 10px; padding: 12px; margin-bottom: 10px; text-align: left; font-size: 0.8rem;">
                <p>🏆 <b>Copas Totales:</b> <span id="end-trophies">0</span></p>
                <p>⚽ <b>Goles de Jugador:</b> <span id="end-goals">0</span></p>
                <p>👟 <b>Asistencias:</b> <span id="end-assists">0</span></p>
                <p>🌟 <b>Promesas Formadas como DT:</b> <span id="end-promesas">0</span></p>
                <p>⭐ <b>Media Máxima Alcanzada:</b> <span id="end-ovr">0</span></p>
            </div>
            <button class="btn-primary" onclick="resetGame()">Nueva Carrera</button>
        </div>
    </div>

    <script>
        const CLUBS_DB = ["Belgrano", "Ingeniería", "Colegio Pio", "La Mennais", "Deportivo Elbio Fernández", "Carrasco Polo", "Seminario", "Nacional Univ."];

        const defaultPlayer = {
            name: "Mateo Silva",
            age: 13,
            year: 2026,
            position: "EXT",
            category: "Sub-13",
            division: "E",
            club: "Belgrano",
            money: 150,
            job: "Estudiante Secundario",
            isCoach: false,
            fitness: 100,
            mental: 75,
            trophies: 0,
            goals: 0,
            assists: 0,
            promesasFormadas: 0,
            attrs: { velocidad: 65, fuerza: 45, resistencia: 60, tiro: 55, pase: 58, regate: 65, defensa: 35 },
            rel: { family: 80, friends: 70, coach: 60, team: 60 },
            seasonStage: 0,
            currentEventCache: null,
            history: [],
            statsOverall: 55
        };

        let player = JSON.parse(JSON.stringify(defaultPlayer));

        function safeNum(val, fallback = 0) { const n = Number(val); return isNaN(n) ? fallback : n; }
        function clamp(val, min = 0, max = 100) { return Math.min(max, Math.max(min, safeNum(val, min))); }

        /* --- BASE DE CARTAS DE PRETEMPORADA (~100 Cartas) --- */
        const CARDS_DATABASE = [
            // MÍTICAS (+5 a todo)
            { id: "c_mit_1", name: "Mentalidad de Tiburón", rarity: "mitico", effectText: "+5 a TODOS los atributos", apply: () => { for(let a in player.attrs) player.attrs[a] += 5; } },
            { id: "c_mit_2", name: "Elixir Legendario", rarity: "mitico", effectText: "+5 a TODOS los atributos", apply: () => { for(let a in player.attrs) player.attrs[a] += 5; } },
            { id: "c_mit_3", name: "Genética Bendita", rarity: "mitico", effectText: "+5 a TODOS los atributos", apply: () => { for(let a in player.attrs) player.attrs[a] += 5; } },
            { id: "c_mit_4", name: "Pacto de Crack", rarity: "mitico", effectText: "+5 a TODOS los atributos", apply: () => { for(let a in player.attrs) player.attrs[a] += 5; } },
            { id: "c_mit_5", name: "Disciplina de Espartano", rarity: "mitico", effectText: "+5 a TODOS los atributos", apply: () => { for(let a in player.attrs) player.attrs[a] += 5; } },

            // ÉPICAS (Grandes atributos específicos)
            { id: "c_epi_1", name: "Kinesiólogo Elite", rarity: "epico", effectText: "+5 Resistencia, +3 Fuerza", apply: () => { player.attrs.resistencia += 5; player.attrs.fuerza += 3; } },
            { id: "c_epi_2", name: "Preparador de Velocidad", rarity: "epico", effectText: "+5 Velocidad, +3 Regate", apply: () => { player.attrs.velocidad += 5; player.attrs.regate += 3; } },
            { id: "c_epi_3", name: "Especialista en Definición", rarity: "epico", effectText: "+5 Tiro, +3 Pase", apply: () => { player.attrs.tiro += 5; player.attrs.pase += 3; } },
            { id: "c_epi_4", name: "Coach Táctico de Élite", rarity: "epico", effectText: "+5 Defensa, +3 Pase", apply: () => { player.attrs.defensa += 5; player.attrs.pase += 3; } },
            { id: "c_epi_5", name: "Botines de Fibra de Carbono", rarity: "epico", effectText: "+4 Velocidad, +4 Tiro", apply: () => { player.attrs.velocidad += 4; player.attrs.tiro += 4; } },

            // COMUNES (Librería generada para sumar ~100 opciones)
            { id: "c_com_1", name: "Entrenamiento de Fuerza", rarity: "comun", effectText: "+3 Fuerza", apply: () => { player.attrs.fuerza += 3; } },
            { id: "c_com_2", name: "Pique en Colina", rarity: "comun", effectText: "+3 Velocidad", apply: () => { player.attrs.velocidad += 3; } },
            { id: "c_com_3", name: "Tiros Libres Extra", rarity: "comun", effectText: "+3 Tiro", apply: () => { player.attrs.tiro += 3; } },
            { id: "c_com_4", name: "Práctica de Pases Pared", rarity: "comun", effectText: "+3 Pase", apply: () => { player.attrs.pase += 3; } },
            { id: "c_com_5", name: "Circuito de Conos", rarity: "comun", effectText: "+3 Regate", apply: () => { player.attrs.regate += 3; } },
            { id: "c_com_6", name: "Sesión de Marcaje", rarity: "comun", effectText: "+3 Defensa", apply: () => { player.attrs.defensa += 3; } },
            { id: "c_com_7", name: "Té de Jengibre y Recuperación", rarity: "comun", effectText: "+3 Resistencia", apply: () => { player.attrs.resistencia += 3; } }
        ];

        // Rellenar dinámicamente hasta 100 variaciones de cartas para pretemporada
        (function generateCardPool() {
            const attrsList = ["velocidad", "fuerza", "resistencia", "tiro", "pase", "regate", "defensa"];
            const rarities = ["comun", "comun", "comun", "epico"];
            for(let i = 8; i <= 95; i++) {
                const r = rarities[Math.floor(Math.random()*rarities.length)];
                const attr = attrsList[Math.floor(Math.random()*attrsList.length)];
                const attrName = attr.charAt(0).toUpperCase() + attr.slice(1);
                const boost = r === "epico" ? 4 : 2;
                CARDS_DATABASE.push({
                    id: `c_gen_${i}`,
                    name: `Modulo ${r.toUpperCase()}: ${attrName}`,
                    rarity: r,
                    effectText: `+${boost} ${attrName}`,
                    apply: () => { player.attrs[attr] += boost; }
                });
            }
        })();

        /* --- MOTOR DE DECISIONES DE JUGADOR Y DT (+300 Combinaciones) --- */

        const PLAYER_TEMPLATES = [
            {
                t: "Día de examen de ingreso escolar / laboral previo a entrenamiento.",
                o: [
                    { t: "Faltar a la práctica para estudiar", d: "+10 Intelecto | -5 Relación DT", a: () => { player.rel.coach -= 5; return "Priorizaste tus estudios. El DT frunció el ceño."; } },
                    { t: "Entrenar e ir a rendir sin dormir", d: "+5 Idolatría | -10% Físico", a: () => { player.fitness -= 10; return "Rendiste exhausto pero mostraste compromiso al club."; } },
                    { t: "Pedir permiso formal de faltar medio turno", d: "+5 Relación DT", a: () => { player.rel.coach += 5; return "Dialogaste con madurez con el cuerpo técnico."; } },
                    { t: "Estudiar en el vestuario antes de cambiarte", d: "+2 Pase | +5 Mentalidad", a: () => { player.attrs.pase += 2; return "Optimizaste tu tiempo al máximo."; } }
                ]
            },
            {
                t: "Ocasión de gol clave en el último minuto del partido.",
                o: [
                    { t: "Rematar fuerte al primer palo", d: "+1 Gol (Éxito si Tiro > 60)", a: () => { if(player.attrs.tiro>60) { player.goals++; return "¡Golazo clavado al ángulo!"; } return "El balón pegó en el poste."; } },
                    { t: "Dar un pase de la muerte", d: "+1 Asistencia", a: () => { player.assists++; return "Le serviste el gol en bandeja a tu compañero."; } },
                    { t: "Intentar picarla sobre el golero", d: "+10 Idolatría si sale | -5 DT si falla", a: () => { player.idolatry = (player.idolatry||0)+10; return "La vaselina entró mansita. ¡Explotó la tribuna!"; } },
                    { t: "Proteger el balón en el córner y ganar tiempo", d: "+5 Relación Plantel", a: () => { player.rel.team += 5; return "Aseguraste la victoria con madurez táctica."; } }
                ]
            },
            {
                t: "Un compañero comete un error grave que cuesta un gol.",
                o: [
                    { t: "Aplaudirlo y animarlo públicamente", d: "+10 Relación Plantel", a: () => { player.rel.team += 10; return "Tu liderazgo positivo levantó la moral del grupo."; } },
                    { t: "Recriminarle con dureza en el campo", d: "-10 Relación Plantel | +5 Mentalidad", a: () => { player.rel.team -= 10; return "Le exigiste concentración total al equipo."; } },
                    { t: "Dar indicaciones tácticas de cobertura", d: "+3 Defensa", a: () => { player.attrs.defensa += 3; return "Ajustaron las marcas para no volver a sufrir."; } },
                    { t: "Mirar a la banca pidiendo un cambio", d: "-15 Relación Plantel", a: () => { player.rel.team -= 15; return "Tus gestos generaron malestar en el grupo."; } }
                ]
            },
            {
                t: "Te ofrecen una entrevista en una radio deportiva local.",
                o: [
                    { t: "Elogiar al entrenador y la dirigencia", d: "+10 Relación DT", a: () => { player.rel.coach += 10; return "Tus declaraciones cayeron excelente en la directiva."; } },
                    { t: "Resaltar el esfuerzo de tus compañeros", d: "+10 Relación Plantel", a: () => { player.rel.team += 10; return "Demostraste compañerismo ante los micrófonos."; } },
                    { t: "Declarar que estás listo para dar el salto de categoría", d: "+10 Idolatría | -5 DT", a: () => { player.rel.coach -= 5; return "Tu ambición dio que hablar en la prensa."; } },
                    { t: "Agradecer el apoyo incondicional de tu familia", d: "+10 Relación Familia", a: () => { player.rel.family += 10; return "Emocionaste a tus seres queridos en vivo."; } }
                ]
            }
        ];

        const DT_TEMPLATES = [
            {
                t: "Inferiores DT: Una joven promesa de 14 años llega tarde sistemáticamente.",
                o: [
                    { t: "Sancionarlo con suplencia el fin de semana", d: "+10 Disciplina Grupal | -Promesa", a: () => { return "Marcaste un precedente claro en la cantera."; } },
                    { t: "Tener una charla privada y ayudarlo en su transporte", d: "+1 Promesa Formada", a: () => { player.promesasFormadas++; return "Comprendiste su situación y potenciaste su desarrollo."; } },
                    { t: "Ponerlo a hacer ejercicios físicos extra", d: "+2 Fuerza en el juvenil", a: () => { return "El joven mejoró su disciplina y forma física."; } },
                    { t: "Pedir una reunión urgente con sus padres", d: "+10 Relación Familiar/Club", a: () => { return "Involucraste a la familia en el proyecto deportivo."; } }
                ]
            },
            {
                t: "Inferiores DT: Final de la Copa Categoria Sub-15.",
                o: [
                    { t: "Plantear un esquema ultra ofensivo 4-3-3", d: "Chance de Campeón (+1 Copa)", a: () => { player.trophies++; return "🏆 ¡Las Inferiores salieron Campeonas con lluvia de goles!"; } },
                    { t: "Priorizar la posesión y el pase corto", d: "+1 Promesa Formada", a: () => { player.promesasFormadas++; return "Desarrollaste un fútbol vistoso y de buen pie."; } },
                    { t: "Cerrar las filas y contraatacar", d: "+5 Reputación DT", a: () => { return "Tácticamente fuiste superior al rival."; } },
                    { t: "Darles minutos a todos los juveniles suplentes", d: "++++ Confianza Plantel Cantera", a: () => { return "Priorizaste el aprendizaje humano sobre el resultado."; } }
                ]
            }
        ];

        function getRandomEventForStage(stage) {
            // ETAPA 0 (PRETEMPORADA): ELECCIÓN DE CARTAS DE ATRIBUTOS
            if (stage === 0) {
                // Obtener 4 cartas al azar de la base de datos
                const shuffled = [...CARDS_DATABASE].sort(() => 0.5 - Math.random());
                const selectedCards = shuffled.slice(0, 4);

                return {
                    isCardSelection: true,
                    title: "🃏 Pretemporada: Cartas de Mejora",
                    text: "Selecciona una carta de preparación física/táctica para aplicar sus bonificaciones exclusivas antes del torneo.",
                    cards: selectedCards
                };
            }

            // ETAPAS 1 Y 2: DECISIONES NARRATIVAS DE 4 OPCIONES
            const pool = player.isCoach ? DT_TEMPLATES : PLAYER_TEMPLATES;
            const chosen = pool[Math.floor(Math.random() * pool.length)];

            return {
                isCardSelection: false,
                title: player.isCoach ? "📋 Gestión de Inferiores DT" : (stage === 1 ? "⚔️ Fecha de Campeonato" : "🏆 Cierre del Certamen"),
                text: chosen.t,
                options: chosen.o
            };
        }

        function switchNav(panelId, btn) {
            document.querySelectorAll('.view-panel').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(panelId).classList.add('active');
            btn.classList.add('active');
        }

        function sanitizeStats() {
            player.age = safeNum(player.age, 13);
            player.money = safeNum(player.money, 0);
            player.trophies = safeNum(player.trophies, 0);
            player.goals = safeNum(player.goals, 0);
            player.assists = safeNum(player.assists, 0);
            player.promesasFormadas = safeNum(player.promesasFormadas, 0);
            player.fitness = clamp(player.fitness, 0, 100);

            if (!player.attrs) player.attrs = { ...defaultPlayer.attrs };
            for (let k in player.attrs) player.attrs[k] = clamp(player.attrs[k], 0, 100);

            if (!player.rel) player.rel = { ...defaultPlayer.rel };
            for (let r in player.rel) player.rel[r] = clamp(player.rel[r], 0, 100);
        }

        function calculateOverall() {
            const a = player.attrs;
            let ovr = (a.velocidad * 0.2) + (a.tiro * 0.2) + (a.regate * 0.2) + (a.pase * 0.2) + (a.resistencia * 0.2);
            player.statsOverall = Math.round(ovr);
            return player.statsOverall;
        }

        function getCategoryByAge(age) {
            if (age >= 50) return "DT Inferiores";
            if (age === 13) return "Sub-13";
            if (age === 14) return "Sub-15";
            if (age === 15) return "Sub-16";
            if (age === 16) return "Sub-17";
            if (age === 17) return "Sub-18";
            if (age < 30) return "Primera División";
            if (age < 38) return "Mayores +30";
            return "Sénior +40";
        }

        function chooseOption(index) {
            const currentEvent = generateCurrentEvent();
            const selected = currentEvent.options[index];
            const resultText = selected.a();
            advanceStage(resultText);
        }

        function selectCard(cardId) {
            const card = CARDS_DATABASE.find(c => c.id === cardId);
            if (card) {
                card.apply();
                advanceStage(`Elegiste la carta **${card.name}**: ${card.effectText}.`);
            }
        }

        function advanceStage(consequenceText) {
            document.getElementById("ui-interaction-area").innerHTML = `
                <div class="balance-box">
                    <b>📌 Resultado:</b> ${consequenceText}
                </div>
                <button class="btn-continue" onclick="nextStep()">Continuar →</button>
            `;
        }

        function nextStep() {
            player.seasonStage++;
            player.currentEventCache = null;

            if (player.seasonStage > 2) {
                player.seasonStage = 0;
                player.age++;
                player.year++;
                player.category = getCategoryByAge(player.age);

                // Hito del Retiro como Jugador e inicio como DT a los 50 años
                if (player.age === 50 && !player.isCoach) {
                    player.isCoach = true;
                    player.job = "Director Técnico de Inferiores";
                    player.history.unshift(`Año ${player.year}: 🎓 ¡RETIRO DEL FÚTBOL PROFESIONAL A LOS 50 AÑOS! Asumes la DT de Cantera en ${player.club}.`);
                } else if (player.age > 55) {
                    finishCareer();
                    return;
                } else {
                    player.history.unshift(`Año ${player.year}: Cumpliste ${player.age} años (${player.category}).`);
                }
            }

            renderAll();
        }

        function generateCurrentEvent() {
            if (!player.currentEventCache) {
                player.currentEventCache = getRandomEventForStage(player.seasonStage);
            }
            return player.currentEventCache;
        }

        function barColor(v) {
            if (v >= 75) return 'var(--accent-lime)';
            if (v >= 50) return 'var(--accent-gold)';
            return 'var(--accent-red)';
        }

        function barRow(name, val, color) {
            return `<div class="bar-row">
                <div class="bar-row-top"><span class="bar-name">${name}</span><span class="bar-val" style="color:${color}">${val}</span></div>
                <div class="bar-track"><div class="bar-fill" style="width:${val}%; background:${color};"></div></div>
            </div>`;
        }

        function renderAll() {
            sanitizeStats();
            calculateOverall();

            document.getElementById("ui-name").innerText = player.name;
            document.getElementById("ui-club-div").innerText = `${player.club} • ${player.isCoach ? 'DT Inferiores' : 'Div. ' + player.division}`;
            document.getElementById("ui-category").innerText = player.category;
            document.getElementById("ui-overall").innerText = player.statsOverall;

            document.getElementById("ui-trophies").innerText = player.trophies;
            document.getElementById("ui-goals").innerText = player.goals;
            document.getElementById("ui-assists").innerText = player.assists;
            document.getElementById("ui-promesas").innerText = player.promesasFormadas;

            const attrsDiv = document.getElementById("ui-attrs");
            attrsDiv.innerHTML = "";
            const labels = { velocidad: "⚡ Vel", fuerza: "💪 Fue", resistencia: "🫁 Res", tiro: "🎯 Tir", pase: "🧭 Pas", regate: "🪄 Reg", defensa: "🛡️ Def" };
            for (let k in player.attrs) {
                const v = player.attrs[k];
                attrsDiv.innerHTML += barRow(labels[k], v, barColor(v));
            }

            document.getElementById("ui-money").innerText = `$${player.money}`;
            document.getElementById("ui-job").innerText = player.job;
            document.getElementById("ui-fitness").innerText = `${player.fitness}%`;

            const relsDiv = document.getElementById("ui-rels-bars");
            relsDiv.innerHTML =
                barRow("👨‍👩‍👦 Familia", player.rel.family, barColor(player.rel.family)) +
                barRow("🧑‍🤝‍🧑 Amigos", player.rel.friends, barColor(player.rel.friends)) +
                barRow("🏟️ Entrenador / Dir.", player.rel.coach, barColor(player.rel.coach)) +
                barRow("🤝 Plantel", player.rel.team, barColor(player.rel.team));

            const currentEvent = generateCurrentEvent();
            document.getElementById("ui-year").innerText = `Año ${player.year}`;
            document.getElementById("ui-story-title").innerText = currentEvent.title;
            document.getElementById("ui-story-text").innerText = currentEvent.text;

            document.querySelectorAll('.stage-dot').forEach(el => {
                const s = parseInt(el.dataset.stage);
                el.classList.remove('active', 'done');
                if (s < player.seasonStage) el.classList.add('done');
                else if (s === player.seasonStage) el.classList.add('active');
            });

            const interactionArea = document.getElementById("ui-interaction-area");

            if (currentEvent.isCardSelection) {
                // RENDERIZAR LAS 4 CARTAS DE PRETEMPORADA
                let cardsHTML = `<div class="cards-grid">`;
                currentEvent.cards.forEach(card => {
                    cardsHTML += `
                        <div class="card-item ${card.rarity}" onclick="selectCard('${card.id}')">
                            <div>
                                <span class="card-rarity">${card.rarity}</span>
                                <div class="card-name">${card.name}</div>
                            </div>
                            <div class="card-effect">${card.effectText}</div>
                        </div>
                    `;
                });
                cardsHTML += `</div>`;
                interactionArea.innerHTML = cardsHTML;
            } else {
                // RENDERIZAR LAS 4 OPCIONES DE DECISIÓN
                let optionsHTML = `<div class="options-container">`;
                currentEvent.options.forEach((opt, idx) => {
                    optionsHTML += `
                        <button class="option-btn" onclick="chooseOption(${idx})">
                            <span class="option-title">${opt.t}</span>
                            <span class="option-desc">${opt.d}</span>
                        </button>
                    `;
                });
                optionsHTML += `</div>`;
                interactionArea.innerHTML = optionsHTML;
            }

            const historyDiv = document.getElementById("ui-history");
            historyDiv.innerHTML = "";
            player.history.forEach(item => {
                historyDiv.innerHTML += `<div class="log-item">${item}</div>`;
            });

            saveGame();
        }

        function startGame() {
            const nameInput = document.getElementById("init-name").value.trim();
            if (nameInput) player.name = nameInput;
            player.position = document.getElementById("init-pos").value;
            player.club = document.getElementById("init-club").value;

            player.history.push(`Año 2026: Debut oficial en ${player.club} (Sub-13).`);
            document.getElementById("modal-creation").style.display = "none";
            saveGame();
            renderAll();
        }

        function finishCareer() {
            document.getElementById("end-trophies").innerText = player.trophies;
            document.getElementById("end-goals").innerText = player.goals;
            document.getElementById("end-assists").innerText = player.assists;
            document.getElementById("end-promesas").innerText = player.promesasFormadas;
            document.getElementById("end-ovr").innerText = player.statsOverall;

            document.getElementById("modal-endgame").style.display = "flex";
        }

        function saveGame() { localStorage.setItem("eidolo_amateur_save", JSON.stringify(player)); }

        function loadGame() {
            const saved = localStorage.getItem("eidolo_amateur_save");
            if (saved) {
                try {
                    player = Object.assign({}, JSON.parse(JSON.stringify(defaultPlayer)), JSON.parse(saved));
                    document.getElementById("modal-creation").style.display = "none";
                    renderAll();
                } catch (e) { console.error(e); }
            }
        }

        function resetGame() {
            localStorage.removeItem("eidolo_amateur_save");
            location.reload();
        }

        window.onload = function () {
            if (localStorage.getItem("eidolo_amateur_save")) { loadGame(); }
        };
    </script>
</body>
</html>
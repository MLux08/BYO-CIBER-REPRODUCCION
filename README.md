# BYO-CIBER-REPRODUCCION
JUEGO REPASO TEMA LA ADOLESCENCIA Y REPRODUCCIÓN. 6º PRIMARIA CONOCIMIENTO DEL MEDIO
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BIO-CYBER 2050: Misión Vida y Reproducción - Tema 3</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800;900&family=Rajdhani:wght@500;600;700&display=swap" rel="stylesheet">
    <script src="[suspicious link removed]"></script>
    <style>
        :root {
            --bg-dark: #070913;
            --card-bg: rgba(15, 23, 42, 0.92);
            --cyber-cyan: #00f3ff;
            --cyber-purple: #bc13fe;
            --cyber-green: #00ff66;
            --cyber-pink: #ff007f;
            --cyber-yellow: #ffea00;
            --text-main: #f1f5f9;
            --text-muted: #94a3b8;
            --border-glow: 0 0 15px rgba(0, 243, 255, 0.4);
            --card-radius: 16px;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; user-select: none; }

        body {
            font-family: 'Rajdhani', sans-serif;
            background: radial-gradient(circle at center, #10172a 0%, #05070e 100%);
            color: var(--text-main);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            overflow-x: hidden;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(rgba(0, 243, 255, 0.03) 1px, transparent 1px),
                        linear-gradient(90deg, rgba(0, 243, 255, 0.03) 1px, transparent 1px);
            background-size: 40px 40px;
            z-index: -1;
            pointer-events: none;
        }

        .screen { display: none; width: 100%; max-width: 1000px; flex-direction: column; gap: 20px; }
        .screen.active { display: flex; }

        .welcome-card {
            background: var(--card-bg);
            border: 2px solid var(--cyber-cyan);
            box-shadow: var(--border-glow);
            border-radius: var(--card-radius);
            padding: 35px;
            text-align: center;
            display: flex;
            flex-direction: column;
            gap: 20px;
            backdrop-filter: blur(10px);
        }

        .welcome-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 2.2rem;
            font-weight: 900;
            background: linear-gradient(135deg, var(--cyber-cyan), var(--cyber-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .input-group { display: flex; flex-direction: column; gap: 8px; text-align: left; }
        .input-group label { font-family: 'Orbitron', sans-serif; font-size: 0.95rem; color: var(--cyber-cyan); }
        .cyber-input {
            background: rgba(0,0,0,0.6); border: 2px solid var(--cyber-purple); color: white;
            padding: 14px 18px; border-radius: 10px; font-size: 1.1rem; font-family: 'Rajdhani', sans-serif;
            outline: none; transition: all 0.3s ease;
        }
        .cyber-input:focus { border-color: var(--cyber-cyan); box-shadow: 0 0 15px rgba(0, 243, 255, 0.5); }

        .cyber-header {
            width: 100%; max-width: 1000px; background: var(--card-bg);
            border: 2px solid var(--cyber-cyan); box-shadow: var(--border-glow);
            border-radius: var(--card-radius); padding: 16px 24px; display: flex;
            justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 15px;
        }

        .stats-panel {
            display: flex; align-items: center; gap: 15px; background: rgba(0,0,0,0.4);
            padding: 8px 16px; border-radius: 30px; border: 1px solid rgba(0, 243, 255, 0.2);
        }

        .stat-box { font-weight: 700; font-size: 1rem; }
        .stat-value { color: var(--cyber-yellow); font-family: 'Orbitron', sans-serif; }

        .audio-btn {
            background: linear-gradient(135deg, var(--cyber-purple), #7e22ce);
            color: white; border: none; padding: 8px 16px; border-radius: 20px;
            font-family: 'Orbitron', sans-serif; font-size: 0.8rem; font-weight: 700; cursor: pointer;
        }

        .mission-nav { display: grid; grid-template-columns: repeat(auto-fit, minmax(210px, 1fr)); gap: 10px; }
        .mission-tab {
            background: rgba(15, 23, 42, 0.6); border: 1px solid rgba(255,255,255,0.1);
            padding: 12px; border-radius: 12px; text-align: center; cursor: not-allowed;
            opacity: 0.5; transition: all 0.3s ease; font-family: 'Orbitron', sans-serif;
            font-size: 0.8rem; font-weight: 700; color: var(--text-muted); display: flex; flex-direction: column; gap: 4px;
        }
        .mission-tab.unlocked { cursor: pointer; opacity: 1; border-color: rgba(0,243,255,0.4); }
        .mission-tab.active {
            background: linear-gradient(135deg, rgba(0, 243, 255, 0.2), rgba(188, 19, 254, 0.2));
            border-color: var(--cyber-cyan); color: var(--cyber-cyan); box-shadow: 0 0 15px rgba(0, 243, 255, 0.3);
        }

        .progress-bar-container { width: 100%; height: 12px; background: rgba(0,0,0,0.5); border-radius: 6px; overflow: hidden; border: 1px solid rgba(0, 243, 255, 0.3); }
        .progress-fill { height: 100%; width: 0%; background: linear-gradient(90deg, var(--cyber-cyan), var(--cyber-green)); transition: width 0.4s ease; box-shadow: 0 0 10px var(--cyber-green); }

        .quest-card {
            background: var(--card-bg); border: 1px solid rgba(0, 243, 255, 0.3);
            border-radius: var(--card-radius); padding: 26px; backdrop-filter: blur(12px);
            box-shadow: 0 10px 30px rgba(0,0,0,0.5); display: flex; flex-direction: column; gap: 18px;
        }

        .quest-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 10px; }
        .quest-number { font-family: 'Orbitron', sans-serif; color: var(--cyber-purple); font-weight: 800; }
        .difficulty-tag { font-family: 'Orbitron', sans-serif; font-size: 0.8rem; padding: 4px 10px; border-radius: 12px; font-weight: 700; }
        .diff-easy { background: rgba(0, 255, 102, 0.2); color: var(--cyber-green); border: 1px solid var(--cyber-green); }
        .diff-medium { background: rgba(255, 234, 0, 0.2); color: var(--cyber-yellow); border: 1px solid var(--cyber-yellow); }
        .diff-hard { background: rgba(255, 0, 127, 0.2); color: var(--cyber-pink); border: 1px solid var(--cyber-pink); }

        .quest-title { font-size: 1.3rem; font-weight: 700; color: var(--cyber-cyan); }
        .quest-body { font-size: 1.05rem; line-height: 1.5; }

        .img-diagram-box {
            position: relative; text-align: center; background: rgba(0,0,0,0.4);
            border: 1px solid rgba(0, 243, 255, 0.2); border-radius: 12px; padding: 12px;
            margin: 10px 0; display: flex; flex-direction: column; align-items: center; gap: 10px;
        }
        .img-diagram-box img { max-width: 100%; max-height: 320px; object-fit: contain; border-radius: 8px; }

        .scheme-box {
            background: rgba(15, 23, 42, 0.8); border: 1.5px dashed var(--cyber-cyan);
            border-radius: 12px; padding: 18px; display: flex; flex-direction: column; gap: 12px;
        }
        .scheme-node { display: flex; align-items: center; gap: 10px; flex-wrap: wrap; font-size: 1.05rem; background: rgba(0,0,0,0.3); padding: 8px 14px; border-radius: 8px; }

        .options-list { display: flex; flex-direction: column; gap: 10px; }
        .option-btn {
            background: rgba(30, 41, 59, 0.7); border: 1.5px solid rgba(255,255,255,0.15);
            color: var(--text-main); padding: 12px 18px; border-radius: 10px; font-size: 1rem;
            font-family: 'Rajdhani', sans-serif; font-weight: 600; text-align: left;
            cursor: pointer; transition: all 0.2s ease; display: flex; align-items: center; gap: 10px;
        }
        .option-btn:hover:not(:disabled) { background: rgba(0, 243, 255, 0.15); border-color: var(--cyber-cyan); transform: translateX(4px); }
        .option-btn.selected { border-color: var(--cyber-yellow); background: rgba(255, 234, 0, 0.15); }
        .option-btn.correct-opt { background: rgba(0, 255, 102, 0.2) !important; border-color: var(--cyber-green) !important; color: #86efac !important; }
        .option-btn.wrong-opt { background: rgba(255, 0, 127, 0.2) !important; border-color: var(--cyber-pink) !important; color: #fca5a5 !important; }

        .match-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
        @media (max-width: 650px) { .match-grid { grid-template-columns: 1fr; } }
        .select-custom {
            background: #0f172a; border: 2px solid var(--cyber-cyan); color: #f1f5f9;
            padding: 10px 12px; border-radius: 8px; font-size: 1rem; font-family: 'Rajdhani', sans-serif;
            font-weight: 600; width: 100%; outline: none; cursor: pointer;
        }

        .cyber-btn {
            background: linear-gradient(135deg, var(--cyber-cyan), #0284c7); color: #070913;
            border: none; padding: 12px 26px; border-radius: 10px; font-family: 'Orbitron', sans-serif;
            font-size: 0.9rem; font-weight: 800; cursor: pointer; transition: all 0.3s ease;
            text-transform: uppercase; box-shadow: 0 0 15px rgba(0, 243, 255, 0.4);
        }
        .cyber-btn:hover:not(:disabled) { transform: translateY(-2px); box-shadow: 0 0 25px rgba(0, 243, 255, 0.8); }
        .cyber-btn:disabled { opacity: 0.4; cursor: not-allowed; box-shadow: none; }

        .feedback-box {
            background: rgba(0,0,0,0.6); border-radius: 12px; padding: 16px 20px;
            border-left: 5px solid var(--cyber-cyan); display: none; flex-direction: column; gap: 8px;
        }
        .feedback-box.correct { border-left-color: var(--cyber-green); background: rgba(0, 255, 102, 0.08); }
        .feedback-box.wrong { border-left-color: var(--cyber-pink); background: rgba(255, 0, 127, 0.08); }

        .results-card {
            background: var(--card-bg); border: 2px solid var(--cyber-green);
            box-shadow: 0 0 30px rgba(0, 255, 102, 0.4); border-radius: var(--card-radius);
            padding: 35px; text-align: center; display: flex; flex-direction: column; gap: 20px;
        }
        .pdf-btn {
            background: linear-gradient(135deg, var(--cyber-yellow), #d97706); color: #070913;
            border: none; padding: 14px 30px; border-radius: 12px; font-family: 'Orbitron', sans-serif;
            font-size: 1.05rem; font-weight: 900; cursor: pointer; transition: all 0.3s ease;
            box-shadow: 0 0 20px rgba(255, 234, 0, 0.5); margin: 0 auto;
        }
        .pdf-btn:hover { transform: scale(1.05); box-shadow: 0 0 30px rgba(255, 234, 0, 0.9); }
    </style>
</head>
<body>

<!-- REGISTRATION SCREEN -->
<div class="screen active" id="screen-register">
    <div class="welcome-card">
        <div class="welcome-title">⚡ BIO-CYBER 2050</div>
        <p style="font-size:1.2rem; color:var(--text-muted);">Misión Vida y Reproducción — Conocimiento del Medio 6º Primaria</p>
        
        <div class="input-group">
            <label for="student-name">👤 Nombre y Apellidos del Alumno/a:</label>
            <input type="text" id="student-name" class="cyber-input" placeholder="Escribe tu nombre completo..." autocomplete="off">
        </div>

        <div class="input-group">
            <label for="student-class">🏫 Curso y Grupo:</label>
            <input type="text" id="student-class" class="cyber-input" value="6º de Primaria" autocomplete="off">
        </div>

        <button class="cyber-btn" style="margin-top:10px;" onclick="startGame()">🚀 INICIAR LA MISIÓN BIO-CYBER</button>
    </div>
</div>

<!-- GAMEPLAY SCREEN -->
<div class="screen" id="screen-game">
    <div class="cyber-header">
        <div style="font-family:'Orbitron',sans-serif; color:var(--cyber-cyan);">
            👤 <span id="hdr-player-name">---</span>
        </div>
        <div class="stats-panel">
            <div class="stat-box">⭐ XP: <span id="xp-val" class="stat-value">0</span></div>
            <div class="stat-box">🏆 Rango: <span id="rank-val" class="stat-value" style="color:var(--cyber-cyan);">Recluta</span></div>
        </div>
        <button class="audio-btn" id="audio-toggle" onclick="toggleAudio()">🎵 MÚSICA ON</button>
    </div>

    <div class="mission-nav">
        <div class="mission-tab active unlocked" id="tab-m1" onclick="switchMission(1)">
            <span>NIVEL 1: Pubertad</span>
            <span style="font-size:0.75rem; color:var(--cyber-yellow);" id="badge-m1">0/10 completados</span>
        </div>
        <div class="mission-tab" id="tab-m2" onclick="switchMission(2)">
            <span>NIVEL 2: Anatomía</span>
            <span style="font-size:0.75rem; color:var(--cyber-yellow);" id="badge-m2">0/10 completados</span>
        </div>
        <div class="mission-tab" id="tab-m3" onclick="switchMission(3)">
            <span>NIVEL 3: Fecundación y Parto</span>
            <span style="font-size:0.75rem; color:var(--cyber-yellow);" id="badge-m3">0/10 completados</span>
        </div>
        <div class="mission-tab" id="tab-m4" onclick="switchMission(4)">
            <span>NIVEL 4: Salud e Igualdad</span>
            <span style="font-size:0.75rem; color:var(--cyber-yellow);" id="badge-m4">0/10 completados</span>
        </div>
    </div>

    <div class="progress-bar-container">
        <div class="progress-fill" id="overall-progress"></div>
    </div>

    <div id="quest-container"></div>
</div>

<!-- RESULTS SCREEN -->
<div class="screen" id="screen-results">
    <div class="results-card">
        <div style="font-family:'Orbitron',sans-serif; color:var(--cyber-green); font-size:2.2rem; font-weight:900;">🎉 ¡MISIÓN BIO-CYBER COMPLETADA!</div>
        <p style="font-size:1.3rem;">¡Enhorabuena, <strong id="res-student-name" style="color:var(--cyber-cyan);"></strong>!</p>
        
        <div style="display:flex; justify-content:center; gap:25px; margin:15px 0; flex-wrap:wrap;">
            <div style="background:rgba(0,0,0,0.5); padding:15px 25px; border-radius:12px; border:1px solid var(--cyber-yellow);">
                <div style="font-size:0.9rem; color:var(--text-muted);">PUNTUACIÓN TOTAL</div>
                <div style="font-size:2rem; font-family:'Orbitron',sans-serif; color:var(--cyber-yellow);" id="res-total-xp">0 XP</div>
            </div>
            <div style="background:rgba(0,0,0,0.5); padding:15px 25px; border-radius:12px; border:1px solid var(--cyber-green);">
                <div style="font-size:0.9rem; color:var(--text-muted);">PRECISIÓN Y ACIERTOS</div>
                <div style="font-size:2rem; font-family:'Orbitron',sans-serif; color:var(--cyber-green);" id="res-accuracy">0 / 40</div>
            </div>
            <div style="background:rgba(0,0,0,0.5); padding:15px 25px; border-radius:12px; border:1px solid var(--cyber-cyan);">
                <div style="font-size:0.9rem; color:var(--text-muted);">RANGO ACADÉMICO</div>
                <div style="font-size:1.4rem; font-family:'Orbitron',sans-serif; color:var(--cyber-cyan);" id="res-final-rank">Máster Bio-Médico</div>
            </div>
        </div>

        <button class="pdf-btn" onclick="generatePDFReport()">📄 GENERAR E IMPRIMIR INFORME PDF</button>
        <button class="cyber-btn" style="margin: 10px auto 0;" onclick="location.reload()">🔄 VOLVER A JUGAR</button>
    </div>
</div>

<script>
const IMAGES = {
    fem: "APARATO_REP._FEM..png",
    masc: "APARATO_REP._MASC.png",
    part: "PART.png",
    fases_parto: "FASES_PARTO.png"
};

let studentData = { name: "", class: "6º de Primaria" };
let userXp = 0;
let completedQuests = new Set();
let userAnswers = {};
let currentMission = 1;
let audioCtx = null, isAudioPlaying = false, bgmTimer = null;

// BATERÍA COMPLETA DE 40 DESAFÍOS (10 POR NIVEL)
const QUEST_DATA = [
    // --- NIVEL 1: PUBERTAD Y CARACTERES SEXUALES ---
    {
        id: "m1_q1", mission: 1, idx: 1, type: "mc5", points: 50, diff: "FÁCIL",
        title: "Diferencia entre Pubertad y Adolescencia",
        text: "¿Cuál es la diferencia biológica entre la pubertad y la adolescencia?",
        options: [
            "La pubertad son los cambios emocionales y la adolescencia es la alimentación.",
            "La pubertad es la fase biológica de maduración de los órganos reproductores y la adolescencia abarca los cambios físicos, psicológicos y sociales.",
            "Ambos términos significan exactamente lo mismo sin ninguna diferencia.",
            "La pubertad ocurre a los 50 años y la adolescencia a los 5 años.",
            "La pubertad se refiere únicamente a la respiración celular."
        ],
        correct: 1,
        explain: "La pubertad es el periodo de cambios físicos y maduración sexual, mientras que la adolescencia es una etapa más amplia de desarrollo integral."
    },
    {
        id: "m1_q2", mission: 1, idx: 2, type: "match", points: 100, diff: "MEDIO",
        title: "Clasificación de Caracteres Sexuales",
        text: "Relaciona cada rasgo físico con su tipo de carácter sexual:",
        pairs: [
            { key: "Órganos reproductores al nacer (Ovarios / Testículos)", correct: "Carácter Primario" },
            { key: "Desarrollo de mamas y ensanchamiento de caderas", correct: "Carácter Secundario Femenino" },
            { key: "Voz más grave y vello facial / barba", correct: "Carácter Secundario Masculino" }
        ],
        optionsList: ["Carácter Primario", "Carácter Secundario Femenino", "Carácter Secundario Masculino"],
        explain: "Los caracteres primarios están presentes desde el nacimiento. Los secundarios se desarrollan en la pubertad impulsados por las hormonas."
    },
    {
        id: "m1_q3", mission: 1, idx: 3, type: "fill", points: 100, diff: "MEDIO",
        title: "Concepto de Animal Vivíparo",
        text: "Completa el texto seleccionando las palabras adecuadas:",
        template: "El ser humano tiene reproducción {1} y es un animal {2}, lo que significa que el embrión se desarrolla dentro del {3} materno.",
        blanks: [
            { id: 1, correct: "sexual", choices: ["sexual", "asexual", "vegetativa"] },
            { id: 2, correct: "vivíparo", choices: ["vivíparo", "ovíparo", "ovovivíparo"] },
            { id: 3, correct: "útero", choices: ["útero", "estómago", "pulmón"] }
        ],
        explain: "Las personas nos reproducimos mediante la unión de dos gametos (reproducción sexual) y los bebés nacen del útero materno (vivíparos)."
    },
    {
        id: "m1_q4", mission: 1, idx: 4, type: "mc5", points: 50, diff: "FÁCIL",
        title: "Edad de Inicio de la Pubertad",
        text: "¿Alrededor de qué edad suele comenzar habitualmente la pubertad en niños y niñas?",
        options: [
            "Entre los 2 y los 4 años.",
            "Entre los 10 y los 12 años aproximadamente.",
            "A los 30 años exactamente.",
            "A los 70 años durante la ancianidad.",
            "A los 18 meses de vida."
        ],
        correct: 1,
        explain: "La pubertad suele iniciarse entre los 10 y 12 años, aunque el ritmo varía de forma completamente normal entre cada persona."
    },
    {
        id: "m1_q5", mission: 1, idx: 5, type: "scheme", points: 150, diff: "DIFÍCIL",
        title: "Esquema General de la Reproducción Humana",
        text: "Completa los nodos del esquema del proceso reproductivo:",
        nodes: [
            { label: "Gametos Femeninos:", correct: "Óvulos", choices: ["Óvulos", "Espermatozoides", "Cigotos"] },
            { label: "Gametos Masculinos:", correct: "Espermatozoides", choices: ["Espermatozoides", "Óvulos", "Placenta"] },
            { label: "Unión de Gametos (Lugar):", correct: "Trompa de Falopio", choices: ["Trompa de Falopio", "Vejiga", "Estómago"] }
        ],
        explain: "Los óvulos y los espermatozoides se unen en las trompas de Falopio dando comienzo a la fecundación."
    },
    {
        id: "m1_q6", mission: 1, idx: 6, type: "mc5", points: 100, diff: "MEDIO",
        title: "Función de las Hormonas en la Pubertad",
        text: "¿Qué sustancias químicas desencadenan los cambios físicos y la maduración en la pubertad?",
        options: [
            "Los ácidos gástricos del estómago.",
            "Las hormonas producidas por el sistema endocrino y las gónadas.",
            "La saliva y los jugos pancreáticos.",
            "El sudor de las glándulas sudoríparas.",
            "El aire inspirado por los alveolos."
        ],
        correct: 1,
        explain: "Las hormonas viajan por la sangre ordenando el desarrollo de los caracteres sexuales secundarios."
    },
    {
        id: "m1_q7", mission: 1, idx: 7, type: "mc5", points: 50, diff: "FÁCIL",
        title: "El Estirón Puberal",
        text: "¿Cómo se llama el rápido crecimiento en altura que se experimenta en la pubertad?",
        options: [
            "Ciclo menstrual.",
            "El estirón puberal.",
            "Hematosis alveolar.",
            "Alumbramiento.",
            "Fecundación."
        ],
        correct: 1,
        explain: "El estirón puberal se debe al rápido crecimiento del sistema esquelético y muscular durante esta etapa."
    },
    {
        id: "m1_q8", mission: 1, idx: 8, type: "fill", points: 100, diff: "MEDIO",
        title: "Cambios Emocionales en la Adolescencia",
        text: "Completa el texto sobre los cambios psicológicos:",
        template: "Durante la adolescencia no solo cambia el cuerpo, sino también la búsqueda de la propia {1} y el deseo de mayor {2} en las decisiones cotidianas.",
        blanks: [
            { id: 1, correct: "identidad", choices: ["identidad", "dentadura", "estatura"] },
            { id: 2, correct: "autonomía", choices: ["autonomía", "infancia", "respiración"] }
        ],
        explain: "La adolescencia se caracteriza por la conformación de la identidad personal y el desarrollo de la autonomía."
    },
    {
        id: "m1_q9", mission: 1, idx: 9, type: "match", points: 100, diff: "MEDIO",
        title: "Diferenciación de Caracteres Sexuales Masculinos",
        text: "Relaciona cada rasgo masculino con su origen:",
        pairs: [
            { key: "Presencia de pene y testículos", correct: "Presente desde el nacimiento" },
            { key: "Crecimiento de barba y cambio de voz", correct: "Aparece en la pubertad" }
        ],
        optionsList: ["Presente desde el nacimiento", "Aparece en la pubertad"],
        explain: "Los órganos genitales son primarios (al nacer); la barba y voz grave son secundarios (en la pubertad)."
    },
    {
        id: "m1_q10", mission: 1, idx: 10, type: "mc5", points: 100, diff: "MEDIO",
        title: "Ritmo de Desarrollo Individual",
        text: "¿Por qué dos compañeros de la misma edad pueden tener alturas distintas en 6º de Primaria?",
        options: [
            "Porque uno de ellos tiene una enfermedad grave obligatoriamente.",
            "Porque cada cuerpo tiene su propio reloj biológico y ritmo de desarrollo normal.",
            "Porque solo los chicos crecen y las chicas no.",
            "Porque depende del color de pelo de cada uno.",
            "Porque respiran aire de distinto tipo."
        ],
        correct: 1,
        explain: "Cada cuerpo evoluciona a su propio ritmo. La diversidad en la velocidad de crecimiento es completamente natural."
    },

    // --- NIVEL 2: ANATOMÍA DE LOS APARATOS REPRODUCTORES Y GAMETOS ---
    {
        id: "m2_q1", mission: 2, idx: 1, type: "mc5", points: 50, diff: "FÁCIL",
        title: "Gónadas Femeninas",
        text: "¿Cómo se llaman las gónadas femeninas encargadas de producir los óvulos?",
        options: [
            "Los testículos.",
            "Los ovarios.",
            "Los nefrones.",
            "Los bronquios.",
            "Los capilares."
        ],
        correct: 1,
        explain: "Los ovarios son las gónadas femeninas situadas en la cavidad pélvica."
    },
    {
        id: "m2_q2", mission: 2, idx: 2, type: "mc5", points: 50, diff: "FÁCIL",
        title: "Gónadas Masculinas",
        text: "¿Dónde se producen continuamente los espermatozoides a partir de la pubertad?",
        options: [
            "En el estómago.",
            "En los testículos.",
            "En los pulmones.",
            "En las glándulas sudoríparas.",
            "En la tráquea."
        ],
        correct: 1,
        explain: "Los testículos fabrican espermatozoides continuamente y se alojan dentro de la bolsa del escroto."
    },
    {
        id: "m2_q3", mission: 2, idx: 3, type: "img_label", points: 150, diff: "DIFÍCIL",
        title: "Identificación Visual: Aparato Reproductor Femenino",
        imgKey: "fem",
        text: "Observa el esquema del Aparato Reproductor Femenino y asigna el nombre a cada etiqueta:",
        labels: [
            { id: 1, text: "Conducto superior arqueado:", correct: "Trompa de Falopio", choices: ["Trompa de Falopio", "Vagina", "Útero"] },
            { id: 2, text: "Órgano redondeado ovalado:", correct: "Ovario", choices: ["Ovario", "Vulva", "Próstata"] },
            { id: 3, text: "Órgano muscular central hueco:", correct: "Útero", choices: ["Útero", "Vagina", "Uréter"] },
            { id: 4, text: "Conducto de comunicación inferior:", correct: "Vagina", choices: ["Vagina", "Trompa de Falopio", "Ovario"] }
        ],
        explain: "El aparato femenino está formado por Ovarios, Trompas de Falopio, Útero, Vagina y Vulva."
    },
    {
        id: "m2_q4", mission: 2, idx: 4, type: "img_label", points: 150, diff: "DIFÍCIL",
        title: "Identificación Visual: Aparato Reproductor Masculino",
        imgKey: "masc",
        text: "Observa el diagrama del Aparato Reproductor Masculino e identifica sus partes principales:",
        labels: [
            { id: 1, text: "Conducto largo de transporte:", correct: "Conducto deferente", choices: ["Conducto deferente", "Uretra", "Pene"] },
            { id: 2, text: "Glándula redondeada debajo de la vejiga:", correct: "Próstata", choices: ["Próstata", "Testículo", "Escroto"] },
            { id: 3, text: "Órgano productor en la bolsa externa:", correct: "Testículo", choices: ["Testículo", "Útero", "Vena"] },
            { id: 4, text: "Conducto que recorre el pene:", correct: "Uretra", choices: ["Uretra", "Conducto deferente", "Trompa"] }
        ],
        explain: "El aparato masculino consta de Testículos (en el Escroto), Conductos deferentes, Próstata, Uretra y Pene."
    },
    {
        id: "m2_q5", mission: 2, idx: 5, type: "match", points: 100, diff: "MEDIO",
        title: "Comparación de Gametos",
        text: "Relaciona cada propiedad con el gameto femenino o masculino:",
        pairs: [
            { key: "Célula grande, esférica e inmóvil", correct: "Óvulo" },
            { key: "Célula pequeña con cola larga y móvil", correct: "Espermatozoide" },
            { key: "Gónada que la produce", correct: "Ovario / Testículo" }
        ],
        optionsList: ["Óvulo", "Espermatozoide", "Ovario / Testículo"],
        explain: "El óvulo reserva nutrientes y es inmóvil; el espermatozoide se desplaza activamente gracias a su flagelo."
    },
    {
        id: "m2_q6", mission: 2, idx: 6, type: "mc5", points: 100, diff: "MEDIO",
        title: "Función de la Próstata y Vesículas Seminales",
        text: "¿Qué líquido producen la próstata y las vesículas seminales para ayudar a los espermatozoides?",
        options: [
            "La bilis para digerir grasas.",
            "El líquido seminal que nutre y facilita el transporte de los espermatozoides.",
            "La orina para limpiar la vejiga.",
            "El sudor corporal.",
            "La sangre arterial."
        ],
        correct: 1,
        explain: "El líquido seminal proporciona energía y un medio acuoso protector a los espermatozoides formando el semen."
    },
    {
        id: "m2_q7", mission: 2, idx: 7, type: "fill", points: 100, diff: "MEDIO",
        title: "La Vulva y los Genitales Externos Femeninos",
        text: "Completa la frase sobre la anatomía externa femenina:",
        template: "La {1} es el conjunto de los órganos genitales externos femeninos que protegen la entrada de la {2} y de la uretra.",
        blanks: [
            { id: 1, correct: "vulva", choices: ["vulva", "próstata", "matriz"] },
            { id: 2, correct: "vagina", choices: ["vagina", "tráquea", "trompa"] }
        ],
        explain: "La vulva está formada por pliegues cutáneos (labios) que resguardan los orificios vaginal y uretral."
    },
    {
        id: "m2_q8", mission: 2, idx: 8, type: "mc5", points: 100, diff: "MEDIO",
        title: "El Escroto y la Temperatura",
        text: "¿Por qué los testículos se alojan fuera de la cavidad abdominal dentro del escroto?",
        options: [
            "Porque no caben dentro del vientre.",
            "Para mantenerse a una temperatura ligeramente inferior a la del cuerpo, necesaria para la producción de espermatozoides.",
            "Para estar más cerca de los pulmones.",
            "Porque se mueven con los músculos de los brazos.",
            "Para producir jugo gástrico."
        ],
        correct: 1,
        explain: "La espermatogénesis requiere unos 2-3 °C menos que la temperatura corporal interna."
    },
    {
        id: "m2_q9", mission: 2, idx: 9, type: "mc5", points: 50, diff: "FÁCIL",
        title: "Doble Función de la Uretra Masculina",
        text: "¿Qué dos líquidos circulan por la uretra masculina en momentos diferentes?",
        options: [
            "La saliva y el aire.",
            "La orina (excreción) y el semen (reproducción).",
            "La sangre y la bilis.",
            "El sudor y las lágrimas.",
            "El quimo y el quilo."
        ],
        correct: 1,
        explain: "La uretra masculina es un conducto compartido entre el aparato excretor y el reproductor."
    },
    {
        id: "m2_q10", mission: 2, idx: 10, type: "scheme", points: 150, diff: "DIFÍCIL",
        title: "Esquema Anatómico Comparativo",
        text: "Completa los componentes del esquema de gónadas y gametos:",
        nodes: [
            { label: "Gónada Femenina (Ovario) produce ➔", correct: "Óvulo", choices: ["Óvulo", "Semen", "Próstata"] },
            { label: "Gónada Masculina (Testículo) produce ➔", correct: "Espermatozoide", choices: ["Espermatozoide", "Endometrio", "Uréter"] }
        ],
        explain: "Las gónadas son los órganos productores de los gametos correspondientes."
    },

    // --- NIVEL 3: FECUNDACIÓN, GESTACIÓN Y PARTO ---
    {
        id: "m3_q1", mission: 3, idx: 1, type: "mc5", points: 100, diff: "MEDIO",
        title: "Lugar de la Fecundación",
        text: "¿En qué lugar exacto del aparato reproductor femenino tiene lugar la fecundación?",
        options: [
            "En la vejiga urinaria.",
            "En las Trompas de Falopio.",
            "En el estómago.",
            "En la uretra.",
            "En el intestino grueso."
        ],
        correct: 1,
        explain: "La unión del óvulo y el espermatozoide se produce en la trompa de Falopio."
    },
    {
        id: "m3_q2", mission: 3, idx: 2, type: "img_label", points: 150, diff: "DIFÍCIL",
        title: "Identificación Visual: Estructuras de la Gestación",
        imgKey: "part",
        text: "Observa el esquema del embarazo dentro del útero e identifica sus 4 elementos:",
        labels: [
            { id: 1, text: "Órgano de la pared uterina arriba a la izquierda:", correct: "Placenta", choices: ["Placenta", "Vagina", "Testículo"] },
            { id: 2, text: "Cordón que une la placenta con el bebé:", correct: "Cordón umbilical", choices: ["Cordón umbilical", "Tráquea", "Uréter"] },
            { id: 3, text: "Líquido protector en la bolsa amniótica:", correct: "Líquido amniótico", choices: ["Líquido amniótico", "Sangre", "Orina"] },
            { id: 4, text: "Pared muscular elástica envolvente:", correct: "Útero", choices: ["Útero", "Ovario", "Estómago"] }
        ],
        explain: "Durante la gestación, la Placenta, el Cordón umbilical y el Líquido amniótico nutren y protegen al feto en el Útero."
    },
    {
        id: "m3_q3", mission: 3, idx: 3, type: "fill", points: 100, diff: "MEDIO",
        title: "El Cigoto y la Anidación Uterina",
        text: "Completa la secuencia inicial tras la fecundación:",
        template: "Tras la fecundación se forma el {1}, la primera célula del nuevo ser. Esta célula se divide y viaja hacia el {2} donde se fija en sus paredes en el proceso de anidación.",
        blanks: [
            { id: 1, correct: "cigoto", choices: ["cigoto", "gameto", "feto"] },
            { id: 2, correct: "útero", choices: ["útero", "ovario", "riñón"] }
        ],
        explain: "El cigoto se convierte en embrión y se implanta en la pared mucosa del útero."
    },
    {
        id: "m3_q4", mission: 3, idx: 4, type: "mc5", points: 100, diff: "MEDIO",
        title: "Paso de Embrión a Feto",
        text: "¿A partir de qué mes de embarazo el embrión tiene formados todos sus órganos y pasa a llamarse feto?",
        options: [
            "En el primer día de fecundación.",
            "A partir del 3º mes de embarazo.",
            "En el momento del parto a los 9 meses.",
            "A los 5 años del nacimiento.",
            "En la pubertad."
        ],
        correct: 1,
        explain: "Hacia el final del 3º mes de gestación, el ser en desarrollo presenta todos los órganos y adquiere forma humana (feto)."
    },
    {
        id: "m3_q5", mission: 3, idx: 5, type: "match", points: 150, diff: "DIFÍCIL",
        title: "Secuencia Cronológica de las 3 Fases del Parto",
        text: "Asocia cada fase del parto con lo que sucede en ella:",
        pairs: [
            { key: "1ª Fase: Dilatación", correct: "El cuello uterino se abre y se rompe la bolsa amniótica" },
            { key: "2ª Fase: Expulsión", correct: "El bebé sale al exterior por la vagina" },
            { key: "3ª Fase: Alumbramiento", correct: "Expulsión de la placenta y del cordón umbilical" }
        ],
        optionsList: [
            "El cuello uterino se abre y se rompe la bolsa amniótica",
            "El bebé sale al exterior por la vagina",
            "Expulsión de la placenta y del cordón umbilical"
        ],
        explain: "Las tres etapas del parto son Dilatación, Expulsión (nacimiento del bebé) y Alumbramiento (salida de la placenta)."
    },
    {
        id: "m3_q6", mission: 3, idx: 6, type: "mc5", points: 100, diff: "MEDIO",
        title: "Función de la Placenta y Cordón Umbilical",
        text: "¿Cómo recibe el feto el oxígeno y los nutrientes necesarios para crecer?",
        options: [
            "Comiendo alimentos sólidos por la boca.",
            "A través de los vasos sanguíneos de la placenta y del cordón umbilical.",
            "Respirando aire con sus propios pulmones.",
            "Beber agua de la vejiga de la madre.",
            "Filtrando orina por los riñones."
        ],
        correct: 1,
        explain: "La placenta permite el intercambio de oxígeno y sustancias nutritivas entre la madre y el feto sin que sus sangres se mezclen directamente."
    },
    {
        id: "m3_q7", mission: 3, idx: 7, type: "img_label", points: 150, diff: "DIFÍCIL",
        title: "Identificación Visual: Las Fases del Parto",
        imgKey: "fases_parto",
        text: "Observa la ilustración de las 3 fases del parto y ordena sus etapas:",
        labels: [
            { id: 1, text: "Imagen superior (cuello del útero abriéndose):", correct: "Dilatación", choices: ["Dilatación", "Expulsión", "Alumbramiento"] },
            { id: 2, text: "Imagen central (bebé saliendo al exterior):", correct: "Expulsión", choices: ["Expulsión", "Dilatación", "Fecundación"] },
            { id: 3, text: "Imagen inferior (útero desprendiendo la placenta):", correct: "Alumbramiento", choices: ["Alumbramiento", "Expulsión", "Anidación"] }
        ],
        explain: "El orden biológico del nacimiento es: 1º Dilatación ➔ 2º Expulsión ➔ 3º Alumbramiento."
    },
    {
        id: "m3_q8", mission: 3, idx: 8, type: "mc5", points: 100, diff: "MEDIO",
        title: "Importancia de la Lactancia Materna",
        text: "¿Qué aporta la leche materna al recién nacido en sus primeros meses de vida?",
        options: [
            "Únicamente agua con azúcares.",
            "Nutrientes completos y defensas naturales (anticuerpos) contra enfermedades e infecciones.",
            "Aire oxigenado para los pulmones.",
            "Glóbulos rojos para las piernas.",
            "Jugos pancreáticos."
        ],
        correct: 1,
        explain: "La leche materna es el alimento ideal porque suministra nutrientes equilibrados e inmunoglobulinas protectoras."
    },
    {
        id: "m3_q9", mission: 3, idx: 9, type: "fill", points: 100, diff: "MEDIO",
        title: "Duración del Embarazo Humano",
        text: "Completa los datos de la gestación humana:",
        template: "El embarazo humano dura aproximadamente {1} meses (unas {2} semanas de gestación).",
        blanks: [
            { id: 1, correct: "9", choices: ["9", "3", "12"] },
            { id: 2, correct: "40", choices: ["40", "20", "60"] }
        ],
        explain: "La gestación promedio en la especie humana abarca 9 meses de calendario (40 semanas)."
    },
    {
        id: "m3_q10", mission: 3, idx: 10, type: "mc5", points: 150, diff: "DIFÍCIL",
        title: "Gemelos Univitelinos vs Mellizos Bivitelinos",
        text: "¿Por qué los hermanos gemelos idénticos tienen exactamente el mismo ADN?",
        options: [
            "Porque proceden de dos óvulos diferentes.",
            "Porque proceden de un único óvulo fecundado por un espermatozoide que se dividió en dos embriones.",
            "Porque uno nace en verano y otro en invierno.",
            "Porque los educan en el mismo colegio.",
            "Porque comen los mismos alimentos."
        ],
        correct: 1,
        explain: "Los gemelos idénticos (univitelinos) surgen del mismo cigoto original que se escinde en dos embriones gemelos."
    },

    // --- NIVEL 4: SALUD, MENSTRUACIÓN, HÁBITOS E IGUALDAD ---
    {
        id: "m4_q1", mission: 4, idx: 1, type: "mc5", points: 50, diff: "FÁCIL",
        title: "El Concepto de Menstruación",
        text: "¿Por qué se produce el sangrado menstrual en la mujer?",
        options: [
            "Por una herida en la vejiga.",
            "Por el desprendimiento de la mucosa uterina (endometrio) cuando el óvulo no ha sido fecundado.",
            "Porque el estómago se llena de agua.",
            "Por comer alimentos fríos.",
            "Porque se rompe una vena del brazo."
        ],
        correct: 1,
        explain: "Si no hay embarazo, la pared interna del útero preparada para acoger al bebé se desprende y se expulsa junto con el óvulo."
    },
    {
        id: "m4_q2", mission: 4, idx: 2, type: "mc5", points: 100, diff: "MEDIO",
        title: "Desmitificación de la Menstruación",
        text: "¿Es verdad que durante la menstruación no se debe hacer ejercicio ni ducharse?",
        options: [
            "SÍ, porque el agua corta la regla inmediatamente.",
            "NO, es un MITO FALSO. Ducharse a diario y hacer ejercicio moderado es totalmente sano y recomendable.",
            "SÍ, hay que quedarse en cama sin moverse 10 días.",
            "SÍ, la regla es una enfermedad grave.",
            "SÍ, porque se pierde la memoria."
        ],
        correct: 1,
        explain: "La menstruación es un proceso biológico natural. Mantener la higiene diaria mediante la ducha es saludable y necesario."
    },
    {
        id: "m4_q3", mission: 4, idx: 3, type: "fill", points: 100, diff: "MEDIO",
        title: "Importancia de la Higiene en la Pubertad",
        text: "Completa el texto sobre el cuidado corporal:",
        template: "En la pubertad aumenta la actividad de las glándulas {1}, por lo que la {2} diaria con agua y jabón neutro es esencial para prevenir infecciones y malos olores.",
        blanks: [
            { id: 1, correct: "sudoríparas", choices: ["sudoríparas", "salivales", "renales"] },
            { id: 2, correct: "ducha", choices: ["ducha", "vacuna", "comida"] }
        ],
        explain: "El aumento hormonal incrementa el sudor, requiriendo un cuidado especial de la higiene diaria."
    },
    {
        id: "m4_q4", mission: 4, idx: 4, type: "mc5", points: 150, diff: "DIFÍCIL",
        title: "Riesgos del Alcohol y Tabaco en la Gestación",
        text: "¿Por qué una mujer embarazada no debe consumir alcohol ni fumar?",
        options: [
            "Porque solo le produce tos a la madre.",
            "Porque el alcohol y la nicotina atraviesan la placenta y el cordón umbilical, pudiendo causar lesiones graves o malformaciones en el feto.",
            "Porque cambia el color del pelo del bebé.",
            "Porque no afecta en nada al embrión.",
            "Porque hace crecer más rápido los dientes."
        ],
        correct: 1,
        explain: "Las sustancias tóxicas del tabaco y alcohol pasan a la sangre fetal a través de la placenta afectando su desarrollo."
    },
    {
        id: "m4_q5", mission: 4, idx: 5, type: "match", points: 100, diff: "MEDIO",
        title: "Valores ODS 5: Igualdad de Género",
        text: "Relaciona cada principio con la actitud correcta en el colegio:",
        pairs: [
            { key: "Igualdad de Derechos", correct: "Niños y niñas tienen la misma capacidad de estudio y juego" },
            { key: "Corresponsabilidad", correct: "El cuidado del hogar y los bebés es tarea de hombres y mujeres" },
            { key: "Respeto a la Diversidad", correct: "Aceptar que cada persona tiene su propio ritmo corporal" }
        ],
        optionsList: [
            "Niños y niñas tienen la misma capacidad de estudio y juego",
            "El cuidado del hogar y los bebés es tarea de hombres y mujeres",
            "Aceptar que cada persona tiene su propio ritmo corporal"
        ],
        explain: "La igualdad de género (ODS 5) promueve la corresponsabilidad y la no discriminación."
    },
    {
        id: "m4_q6", mission: 4, idx: 6, type: "mc5", points: 50, diff: "FÁCIL",
        title: "Profesionales de la Salud Sexual y Reproductiva",
        text: "¿Qué profesional sanitario se encarga del seguimiento del embarazo, parto y atención al recién nacido?",
        options: [
            "El dentista.",
            "La matrona / matrón y el ginecólogo/a.",
            "El traumatólogo.",
            "El óptico.",
            "El veterinario."
        ],
        correct: 1,
        explain: "Los matrones/as y ginecólogos/as son los especialistas sanitarios del aparato reproductor y la maternidad."
    },
    {
        id: "m4_q7", mission: 4, idx: 7, type: "mc5", points: 100, diff: "MEDIO",
        title: "Búsqueda de Información Veraz",
        text: "Si un adolescente tiene dudas o inquietudes sobre los cambios en su cuerpo, ¿a dónde debe acudir?",
        options: [
            "Creer ciegamente cualquier rumor en redes sociales.",
            "Consultar a adultos de confianza: padres, profesores o profesionales médicos.",
            "Guardarse la duda y no hablar con nadie jamás.",
            "Buscar en foros anónimos de internet.",
            "Preguntar a un niño de 3 años."
        ],
        correct: 1,
        explain: "La información médica y veraz debe provenir de fuentes científicas y adultos de confianza."
    },
    {
        id: "m4_q8", mission: 4, idx: 8, type: "fill", points: 100, diff: "MEDIO",
        title: "Alimentación en el 'Estirón'",
        text: "Completa las pautas de alimentación saludable:",
        template: "Durante la pubertad es crucial consumir alimentos ricos en {1} para los huesos y {2} para los músculos, reduciendo refrescos azucarados.",
        blanks: [
            { id: 1, correct: "calcio", choices: ["calcio", "azúcar", "grasa"] },
            { id: 2, correct: "proteínas", choices: ["proteínas", "sal", "aceite"] }
        ],
        explain: "El crecimiento de los huesos y músculos requiere nutrientes esenciales como el calcio y las proteínas."
    },
    {
        id: "m4_q9", mission: 4, idx: 9, type: "mc5", points: 100, diff: "MEDIO",
        title: "Expresión de Emociones y Empatía",
        text: "¿Es verdad que los niños no deben llorar o mostrar vulnerabilidad?",
        options: [
            "SÍ, los chicos no deben llorar nunca.",
            "NO, es un estereotipo falso. Expresar emociones como la tristeza o el miedo es sano para todas las personas.",
            "SÍ, llorar es malo para los pulmones.",
            "SÍ, solo las niñas pueden sentir tristeza.",
            "SÍ, las emociones no existen."
        ],
        correct: 1,
        explain: "Romper con los estereotipos de género implica reconocer que sentir y comunicar emociones es saludable para todos."
    },
    {
        id: "m4_q10", mission: 4, idx: 10, type: "scheme", points: 150, diff: "DIFÍCIL",
        title: "Esquema Final: Compromiso con la Salud",
        text: "Completa el esquema del autocuidado en la adolescencia:",
        nodes: [
            { label: "Pilar 1 (Higiene):", correct: "Ducha y limpieza genital diaria", choices: ["Ducha y limpieza genital diaria", "No lavarse", "Usar colonia sin agua"] },
            { label: "Pilar 2 (Convivencia):", correct: "Respeto a la diversidad corporal", choices: ["Respeto a la diversidad corporal", "Burlarse de los demás", "Ignorar a los amigos"] }
        ],
        explain: "El autocuidado abarca tanto la higiene física como la convivencia empática con los demás."
    }
];

function startGame() {
    const nameInput = document.getElementById('student-name').value.trim();
    const classInput = document.getElementById('student-class').value.trim();
    if (!nameInput) { alert("⚠️ Por favor, escribe tu nombre antes de iniciar."); return; }
    studentData.name = nameInput; studentData.class = classInput || "6º de Primaria";
    document.getElementById('hdr-player-name').textContent = studentData.name;
    document.getElementById('res-student-name').textContent = studentData.name;
    document.getElementById('screen-register').classList.remove('active');
    document.getElementById('screen-game').classList.add('active');
    renderQuests();
}

function renderQuests() {
    const container = document.getElementById('quest-container'); container.innerHTML = '';
    const currentQuests = QUEST_DATA.filter(q => q.mission === currentMission);

    currentQuests.forEach((q) => {
        const card = document.createElement('div'); card.className = 'quest-card'; card.id = `card-${q.id}`;
        let diffClass = q.diff === "MEDIO" ? "diff-medium" : (q.diff === "DIFÍCIL" ? "diff-hard" : "diff-easy");

        let html = `
            <div class="quest-header">
                <span class="quest-number">MISIÓN ${q.mission} — DESAFÍO ${q.idx}/10</span>
                <span class="difficulty-tag ${diffClass}">${q.diff} (+${q.points} XP)</span>
            </div>
            <div class="quest-title">${q.title}</div>
            <div class="quest-body">${q.text}</div>
        `;

        if (q.imgKey && IMAGES[q.imgKey]) {
            html += `<div class="img-diagram-box"><img src="${IMAGES[q.imgKey]}" alt="${q.title}"></div>`;
        }

        if (q.type === 'mc5') {
            html += `<div class="options-list">`;
            q.options.forEach((opt, oIdx) => {
                html += `<button class="option-btn" id="btn-${q.id}-${oIdx}" onclick="selectMcOption('${q.id}', ${oIdx})"><span>⚡</span> <span>${opt}</span></button>`;
            });
            html += `</div>`;
        } else if (q.type === 'match') {
            html += `<div class="match-grid">`;
            q.pairs.forEach((pair, pIdx) => {
                let optsHtml = '<option value="">-- Selecciona Correspondencia --</option>';
                q.optionsList.forEach(optVal => optsHtml += `<option value="${optVal}">${optVal}</option>`);
                html += `<div style="font-weight:700; color:var(--cyber-cyan); display:flex; align-items:center;">${pair.key} ➔</div><div><select class="select-custom" id="sel-${q.id}-${pIdx}">${optsHtml}</select></div>`;
            });
            html += `</div>`;
        } else if (q.type === 'fill') {
            let fillHtml = q.template;
            q.blanks.forEach(b => {
                let opts = `<option value="">[ Selecciona... ]</option>`;
                b.choices.forEach(c => opts += `<option value="${c}">${c}</option>`);
                fillHtml = fillHtml.replace(`{${b.id}}`, `<select class="select-custom" style="width:auto; display:inline-block;" id="fill-${q.id}-${b.id}">${opts}</select>`);
            });
            html += `<div class="scheme-box"><div style="font-size:1.1rem; line-height:1.8;">${fillHtml}</div></div>`;
        } else if (q.type === 'scheme') {
            html += `<div class="scheme-box">`;
            q.nodes.forEach((node, nIdx) => {
                let opts = `<option value="">[ Completa el Nudo... ]</option>`;
                node.choices.forEach(c => opts += `<option value="${c}">${c}</option>`);
                html += `<div class="scheme-node"><strong>${node.label}</strong><select class="select-custom" style="width:auto;" id="scheme-${q.id}-${nIdx}">${opts}</select></div>`;
            });
            html += `</div>`;
        } else if (q.type === 'img_label') {
            html += `<div class="scheme-box">`;
            q.labels.forEach((lbl, lIdx) => {
                let opts = `<option value="">[ Selecciona Elemento... ]</option>`;
                lbl.choices.forEach(c => opts += `<option value="${c}">${c}</option>`);
                html += `<div class="scheme-node"><span>🏷️ <strong>${lbl.text}</strong></span><select class="select-custom" style="width:auto;" id="imglbl-${q.id}-${lIdx}">${opts}</select></div>`;
            });
            html += `</div>`;
        }

        html += `
            <div style="display:flex; justify-content:space-between; align-items:center; margin-top:10px;">
                <button class="cyber-btn" id="check-${q.id}" onclick="verifyQuest('${q.id}')">🔍 COMPROBAR Y ANALIZAR</button>
            </div>
            <div class="feedback-box" id="fb-${q.id}">
                <div class="maestra-msg" id="msg-${q.id}"></div>
                <div id="exp-${q.id}"></div>
            </div>
        `;
        card.innerHTML = html; container.appendChild(card);
    });
    updateProgressUI();
}

function selectMcOption(qId, oIdx) {
    const quest = QUEST_DATA.find(q => q.id === qId);
    quest.options.forEach((_, idx) => document.getElementById(`btn-${qId}-${idx}`).classList.remove('selected'));
    document.getElementById(`btn-${qId}-${oIdx}`).classList.add('selected');
    userAnswers[qId] = oIdx;
}

function verifyQuest(qId) {
    const quest = QUEST_DATA.find(q => q.id === qId);
    const fbBox = document.getElementById(`fb-${qId}`);
    const msgEl = document.getElementById(`msg-${qId}`);
    const expEl = document.getElementById(`exp-${qId}`);
    const checkBtn = document.getElementById(`check-${qId}`);
    let isCorrect = false;

    if (quest.type === 'mc5') {
        const selected = userAnswers[qId];
        if (selected === undefined) { alert("⚠️ Por favor, selecciona una opción antes de comprobar."); return; }
        isCorrect = (selected === quest.correct);
        quest.options.forEach((_, idx) => {
            const btn = document.getElementById(`btn-${qId}-${idx}`); btn.disabled = true;
            if (idx === quest.correct) btn.classList.add('correct-opt');
            else if (idx === selected) btn.classList.add('wrong-opt');
        });
    } else if (quest.type === 'match') {
        let allCorrect = true, allSelected = true;
        quest.pairs.forEach((pair, pIdx) => {
            const sel = document.getElementById(`sel-${qId}-${pIdx}`);
            if (!sel.value) allSelected = false; if (sel.value !== pair.correct) allCorrect = false;
            sel.disabled = true;
        });
        if (!allSelected) { alert("⚠️ Por favor, responde a todos los desplegables."); return; }
        isCorrect = allCorrect;
    } else if (quest.type === 'fill') {
        let allCorrect = true, allSelected = true;
        quest.blanks.forEach(b => {
            const sel = document.getElementById(`fill-${qId}-${b.id}`);
            if (!sel.value) allSelected = false; if (sel.value !== b.correct) allCorrect = false;
            sel.disabled = true;
        });
        if (!allSelected) { alert("⚠️ Por favor, completa todos los huecos del texto."); return; }
        isCorrect = allCorrect;
    } else if (quest.type === 'scheme') {
        let allCorrect = true, allSelected = true;
        quest.nodes.forEach((n, nIdx) => {
            const sel = document.getElementById(`scheme-${qId}-${nIdx}`);
            if (!sel.value) allSelected = false; if (sel.value !== n.correct) allCorrect = false;
            sel.disabled = true;
        });
        if (!allSelected) { alert("⚠️ Por favor, completa todos los nudos del esquema."); return; }
        isCorrect = allCorrect;
    } else if (quest.type === 'img_label') {
        let allCorrect = true, allSelected = true;
        quest.labels.forEach((lbl, lIdx) => {
            const sel = document.getElementById(`imglbl-${qId}-${lIdx}`);
            if (!sel.value) allSelected = false; if (sel.value !== lbl.correct) allCorrect = false;
            sel.disabled = true;
        });
        if (!allSelected) { alert("⚠️ Por favor, asigna el nombre a todas las etiquetas."); return; }
        isCorrect = allCorrect;
    }

    checkBtn.disabled = true; fbBox.style.display = 'flex';

    if (isCorrect) {
        playSfx('correct'); fbBox.className = 'feedback-box correct';
        msgEl.innerHTML = "🌟 ¡RESPUESTA CORRECTA! Maestra Mª Luz & NutriBot aplauden tu rigor científico.";
        if (!completedQuests.has(qId)) {
            completedQuests.add(qId); userXp += quest.points;
            document.getElementById('xp-val').textContent = userXp; updateRank();
        }
    } else {
        playSfx('wrong'); fbBox.className = 'feedback-box wrong';
        msgEl.innerHTML = "💡 ¡CASI! Revisa la explicación razonada para aprender del error.";
    }

    expEl.innerHTML = `<strong>Análisis Científico:</strong> ${quest.explain}`;
    updateProgressUI(); checkMissionCompletion();
}

function switchMission(mNum) {
    if (mNum > 1) {
        const prevMQuests = QUEST_DATA.filter(q => q.mission === (mNum - 1));
        const prevDone = prevMQuests.filter(q => completedQuests.has(q.id)).length;
        if (prevDone < 10) { alert(`🔒 Completa las 10 preguntas del Nivel ${mNum - 1} para desbloquear el Nivel ${mNum}.`); return; }
    }
    currentMission = mNum;
    for (let i = 1; i <= 4; i++) document.getElementById(`tab-m${i}`).classList.remove('active');
    document.getElementById(`tab-m${mNum}`).classList.add('active');
    renderQuests();
}

function updateRank() {
    const rankEl = document.getElementById('rank-val');
    if (userXp >= 3500) rankEl.textContent = "🥇 Máster Bio-Médico";
    else if (userXp >= 2400) rankEl.textContent = "🥈 Especialista Anatómico";
    else if (userXp >= 1000) rankEl.textContent = "🥉 Cadete Nutricional";
    else rankEl.textContent = "Recluta Bio-Cyber";
}

function updateProgressUI() {
    for (let m = 1; m <= 4; m++) {
        const mQuests = QUEST_DATA.filter(q => q.mission === m);
        const done = mQuests.filter(q => completedQuests.has(q.id)).length;
        document.getElementById(`badge-m${m}`).textContent = `${done}/10 completados`;
        const tabEl = document.getElementById(`tab-m${m}`);
        if (m === 1 || (m > 1 && QUEST_DATA.filter(q => q.mission === (m-1)).filter(q => completedQuests.has(q.id)).length === 10)) {
            tabEl.classList.add('unlocked');
        }
    }
    const percent = (completedQuests.size / QUEST_DATA.length) * 100;
    document.getElementById('overall-progress').style.width = `${percent}%`;
}

function checkMissionCompletion() {
    if (completedQuests.size === QUEST_DATA.length) { setTimeout(showFinalResults, 1200); }
}

function showFinalResults() {
    document.getElementById('screen-game').classList.remove('active');
    document.getElementById('screen-results').classList.add('active');
    document.getElementById('res-total-xp').textContent = `${userXp} XP`;
    document.getElementById('res-accuracy').textContent = `${completedQuests.size} / 40`;
    document.getElementById('res-final-rank').textContent = document.getElementById('rank-val').textContent;
}

function generatePDFReport() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();
    const pName = studentData.name || "Alumno/a";
    const pClass = studentData.class || "6º de Primaria";
    const scoreXp = userXp; const accuracy = completedQuests.size;
    const rank = document.getElementById('rank-val').textContent;
    const dateStr = new Date().toLocaleDateString('es-ES', { day: '2-digit', month: '2-digit', year: 'numeric' });

    doc.setFillColor(15, 23, 42); doc.rect(0, 0, 210, 38, 'F');
    doc.setFont("helvetica", "bold"); doc.setFontSize(18); doc.setTextColor(0, 243, 255);
    doc.text("BIO-CYBER 2050: INFORME DE EVALUACIÓN", 15, 18);
    doc.setFontSize(11); doc.setTextColor(255, 255, 255);
    doc.text("Tema 3: La Adolescencia y la Reproducción Humana (6º Primaria)", 15, 28);

    doc.setDrawColor(2, 132, 199); doc.setFillColor(240, 249, 255);
    doc.roundedRect(15, 46, 180, 42, 3, 3, 'FD');
    doc.setTextColor(15, 23, 42); doc.setFontSize(11);
    doc.text(`Estudiante: ${pName}`, 22, 56); doc.text(`Curso: ${pClass}`, 120, 56);
    doc.text(`Fecha de Evaluación: ${dateStr}`, 22, 66); doc.text(`Puntuación Obtenida: ${scoreXp} XP`, 120, 66);
    doc.setFont("helvetica", "bold"); doc.setTextColor(21, 128, 61);
    doc.text(`Desafíos Completados: ${accuracy} / 40 (${Math.round((accuracy/40)*100)}%)`, 22, 78);
    doc.setTextColor(126, 34, 206); doc.text(`Rango Académico: ${rank}`, 120, 78);

    doc.setFontSize(13); doc.setTextColor(15, 23, 42);
    doc.text("Resumen de Desempeño por Niveles de Logro:", 15, 102);

    const levelsInfo = [
        { name: "Nivel 1: Pubertad y Caracteres Sexuales", qCount: 10 },
        { name: "Nivel 2: Anatomía de los Aparatos Reproductores", qCount: 10 },
        { name: "Nivel 3: Fecundación, Gestación y Parto", qCount: 10 },
        { name: "Nivel 4: Salud, Menstruación e Igualdad ODS 5", qCount: 10 }
    ];

    let yPos = 112;
    levelsInfo.forEach((lvl, idx) => {
        const lvlQuests = QUEST_DATA.filter(q => q.mission === (idx+1));
        const lvlDone = lvlQuests.filter(q => completedQuests.has(q.id)).length;
        const pct = Math.round((lvlDone / lvl.qCount) * 100);
        doc.setFillColor(248, 250, 252); doc.setDrawColor(203, 213, 225);
        doc.roundedRect(15, yPos, 180, 18, 2, 2, 'FD');
        doc.setFont("helvetica", "bold"); doc.setFontSize(10); doc.setTextColor(15, 23, 42);
        doc.text(lvl.name, 22, yPos + 11);
        doc.setTextColor(pct >= 80 ? 21 : 180, pct >= 80 ? 128 : 50, 50);
        doc.text(`${lvlDone} / 10 (${pct}%)`, 165, yPos + 11);
        yPos += 24;
    });

    doc.setDrawColor(15, 23, 42); doc.rect(15, 220, 180, 45, 'S');
    doc.setFont("helvetica", "bold"); doc.setFontSize(10); doc.setTextColor(15, 23, 42);
    doc.text("VALIDACIÓN DOCENTE Y OBSERVACIONES:", 20, 230);
    doc.setFont("helvetica", "normal");
    doc.text("Firma del Profesor/a: _______________________    Sello del Centro:", 20, 255);

    doc.save(`Informe_BioCyber_Tema3_${pName.replace(/\s+/g, '_')}.pdf`);
}

function initAudio() {
    if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    if (audioCtx.state === 'suspended') audioCtx.resume();
}

function toggleAudio() {
    initAudio();
    const btn = document.getElementById('audio-toggle');
    if (!isAudioPlaying) { isAudioPlaying = true; startBGM(); btn.textContent = "🎵 MÚSICA ON"; }
    else { isAudioPlaying = false; stopBGM(); btn.textContent = "🔇 MÚSICA OFF"; }
}

function startBGM() {
    if (!audioCtx) return;
    if (bgmTimer) clearInterval(bgmTimer);
    const synthNotes = [220, 261.63, 329.63, 392.00, 440, 523.25];
    let noteIdx = 0;
    bgmTimer = setInterval(() => {
        if (!isAudioPlaying || !audioCtx) return;
        const osc = audioCtx.createOscillator(); const gain = audioCtx.createGain();
        osc.type = 'sine'; osc.frequency.setValueAtTime(synthNotes[noteIdx % synthNotes.length], audioCtx.currentTime);
        gain.gain.setValueAtTime(0.03, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.4);
        osc.connect(gain); gain.connect(audioCtx.destination);
        osc.start(); osc.stop(audioCtx.currentTime + 0.4); noteIdx++;
    }, 400);
}

function stopBGM() { if (bgmTimer) { clearInterval(bgmTimer); bgmTimer = null; } }

function playSfx(type) {
    if (!audioCtx) return;
    const osc = audioCtx.createOscillator(), gain = audioCtx.createGain();
    osc.connect(gain); gain.connect(audioCtx.destination);
    if (type === 'correct') {
        osc.type = 'triangle'; osc.frequency.setValueAtTime(523.25, audioCtx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(880, audioCtx.currentTime + 0.3);
        gain.gain.setValueAtTime(0.15, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
        osc.start(); osc.stop(audioCtx.currentTime + 0.3);
    } else if (type === 'wrong') {
        osc.type = 'sawtooth'; osc.frequency.setValueAtTime(220, audioCtx.currentTime);
        osc.frequency.linearRampToValueAtTime(110, audioCtx.currentTime + 0.3);
        gain.gain.setValueAtTime(0.15, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
        osc.start(); osc.stop(audioCtx.currentTime + 0.3);
    }
}
</script>
</body>
</html>

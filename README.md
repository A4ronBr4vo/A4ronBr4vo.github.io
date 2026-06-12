theme: Reloj epigenetico
title: Grupo03
description: DAAAAAAAA
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Reloj Epigenético Cerebral</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg:        #070B14;
    --surface:   #0D1525;
    --surface2:  #111E35;
    --border:    rgba(255,255,255,0.07);
    --teal:      #00E5C3;
    --teal-dim:  rgba(0,229,195,0.12);
    --teal-glow: rgba(0,229,195,0.25);
    --amber:     #F5A623;
    --amber-dim: rgba(245,166,35,0.12);
    --red:       #FF4D6D;
    --red-dim:   rgba(255,77,109,0.12);
    --text:      #E8EDF5;
    --muted:     #6B7A99;
    --mono:      'Space Mono', monospace;
    --sans:      'Space Grotesk', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
  }

  .wrapper { position: relative; z-index: 1; max-width: 1100px; margin: 0 auto; padding: 2rem 1.5rem 4rem; }

  /* ── HEADER ── */
  .hero { padding: 3rem 0 2.5rem; border-bottom: 1px solid var(--border); margin-bottom: 2rem; }
  .hero-eyebrow {
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: .18em;
    color: var(--teal);
    margin-bottom: 1rem;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .hero-eyebrow::before {
    content: '';
    display: inline-block;
    width: 24px;
    height: 1px;
    background: var(--teal);
  }
  .hero-title {
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 600;
    line-height: 1.1;
    letter-spacing: -.02em;
    margin-bottom: .75rem;
  }
  .hero-title span { color: var(--teal); }
  .hero-sub { font-size: 15px; color: var(--muted); max-width: 560px; line-height: 1.7; }
  .source-chip {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    margin-top: 1.2rem;
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 5px 12px;
  }
  .source-chip::before { content: '↗'; color: var(--teal); }

  /* ── MAIN GRID ── */
  .main-grid {
    display: grid;
    grid-template-columns: 1fr 1.05fr;
    gap: 16px;
    align-items: start;
  }

  /* ── PANEL BASE ── */
  .panel {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
  }
  .panel-head {
    padding: .75rem 1.2rem;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .panel-label {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: .14em;
    color: var(--muted);
  }
  .panel-body { padding: 1.2rem; }

  /* ── AGE SLIDER ── */
  .age-row {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: .9rem 1.2rem;
    background: var(--surface2);
    border-bottom: 1px solid var(--border);
  }
  .age-label { font-size: 12px; color: var(--muted); white-space: nowrap; }
  .age-val {
    font-family: var(--mono);
    font-size: 18px;
    font-weight: 700;
    color: var(--text);
    min-width: 52px;
    text-align: right;
  }
  input[type=range] {
    -webkit-appearance: none;
    appearance: none;
    flex: 1;
    height: 3px;
    border-radius: 2px;
    background: var(--border);
    outline: none;
    cursor: pointer;
  }
  input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 16px;
    height: 16px;
    border-radius: 50%;
    background: var(--teal);
    box-shadow: 0 0 0 3px var(--teal-glow);
    cursor: pointer;
    transition: box-shadow .2s;
  }
  input[type=range]:hover::-webkit-slider-thumb { box-shadow: 0 0 0 6px var(--teal-glow); }
  input[type=range]::-moz-range-thumb {
    width: 16px; height: 16px; border-radius: 50%;
    background: var(--teal); border: none;
    box-shadow: 0 0 0 3px var(--teal-glow); cursor: pointer;
  }

  /* ── GENE ROWS ── */
  .genes-section { padding: 1rem 1.2rem; }
  .section-eyebrow {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: .14em;
    color: var(--muted);
    margin-bottom: 1rem;
  }
  .gene-item { margin-bottom: 1.1rem; }
  .gene-item:last-child { margin-bottom: 0; }
  .gene-top {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    margin-bottom: 3px;
  }
  .gene-name {
    font-family: var(--mono);
    font-size: 13px;
    font-weight: 700;
    color: var(--text);
  }
  .gene-pct {
    font-family: var(--mono);
    font-size: 12px;
    transition: color .3s;
  }
  .gene-desc { font-size: 11px; color: var(--muted); margin-bottom: 6px; line-height: 1.45; }
  .gene-track {
    height: 6px;
    background: rgba(255,255,255,0.05);
    border-radius: 3px;
    overflow: hidden;
    margin-bottom: 5px;
  }
  .gene-fill {
    height: 100%;
    border-radius: 3px;
    transition: width .4s ease, background .4s ease;
  }
  .gene-slider { width: 100%; }

  /* ── RESULT PANEL ── */
  .result-hero {
    padding: 1.5rem 1.2rem 1rem;
    border-bottom: 1px solid var(--border);
  }
  .result-label-sm { font-size: 11px; color: var(--muted); margin-bottom: .5rem; letter-spacing: .04em; }
  .result-age-row { display: flex; align-items: flex-end; gap: 12px; margin-bottom: .8rem; }
  .result-age-num {
    font-family: var(--mono);
    font-size: 52px;
    font-weight: 700;
    line-height: 1;
    transition: color .4s;
  }
  .result-age-suffix { font-size: 18px; color: var(--muted); margin-bottom: 6px; }
  .status-chip {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 5px 14px;
    border-radius: 20px;
    font-size: 12px;
    font-weight: 500;
    border: 1px solid transparent;
    transition: all .4s;
  }
  .status-chip::before {
    content: '';
    width: 6px;
    height: 6px;
    border-radius: 50%;
    flex-shrink: 0;
  }
  .chip-sano    { background: rgba(0,229,195,.1);  border-color: rgba(0,229,195,.3);  color: #00E5C3; }
  .chip-sano::before { background: #00E5C3; box-shadow: 0 0 6px #00E5C3; }
  .chip-riesgo  { background: rgba(245,166,35,.1); border-color: rgba(245,166,35,.3); color: #F5A623; }
  .chip-riesgo::before { background: #F5A623; box-shadow: 0 0 6px #F5A623; }
  .chip-patol   { background: rgba(255,77,109,.1); border-color: rgba(255,77,109,.3); color: #FF4D6D; }
  .chip-patol::before { background: #FF4D6D; box-shadow: 0 0 6px #FF4D6D; }

  /* ── AGE BAR ── */
  .age-bar-wrap { padding: 1rem 1.2rem; border-bottom: 1px solid var(--border); }
  .age-bar-label {
    display: flex;
    justify-content: space-between;
    font-size: 11px;
    color: var(--muted);
    margin-bottom: 6px;
    font-family: var(--mono);
  }
  .age-bar-track {
    height: 10px;
    background: rgba(255,255,255,0.05);
    border-radius: 5px;
    position: relative;
    overflow: visible;
  }
  .age-bar-cron {
    position: absolute;
    top: 0; left: 0;
    height: 10px;
    border-radius: 5px;
    background: rgba(255,255,255,0.12);
    transition: width .5s ease;
  }
  .age-bar-bio {
    position: absolute;
    top: 2px; left: 0;
    height: 6px;
    border-radius: 3px;
    transition: width .5s ease, background .4s;
  }
  .age-bar-ticks {
    display: flex;
    justify-content: space-between;
    margin-top: 4px;
    font-family: var(--mono);
    font-size: 10px;
    color: rgba(255,255,255,0.2);
  }

  /* ── MARKERS GRID ── */
  .markers-wrap { padding: 1rem 1.2rem; border-bottom: 1px solid var(--border); }
  .markers-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  .marker-cell {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: .7rem .85rem;
  }
  .marker-lbl { font-size: 10px; color: var(--muted); margin-bottom: 3px; font-family: var(--mono); letter-spacing: .06em; }
  .marker-val { font-size: 15px; font-weight: 600; transition: color .4s; }
  .marker-sub { font-size: 10px; color: var(--muted); margin-top: 1px; }

  /* ── INTERPRETATION ── */
  .interp-wrap { padding: 1rem 1.2rem; }
  .interp-title { font-family: var(--mono); font-size: 10px; letter-spacing: .14em; color: var(--muted); margin-bottom: .6rem; }
  .interp-text { font-size: 13px; color: var(--muted); line-height: 1.7; transition: color .3s; }
  .interp-text.highlighted { color: var(--text); }
  .note-block {
    margin-top: .9rem;
    padding: .7rem .9rem;
    background: var(--surface2);
    border-left: 2px solid var(--teal);
    border-radius: 0 6px 6px 0;
    font-size: 11px;
    color: var(--muted);
    line-height: 1.6;
  }

  /* ── FOOTER ── */
  .footer {
    margin-top: 2.5rem;
    padding-top: 1.5rem;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 8px;
  }
  .footer-ref { font-family: var(--mono); font-size: 10px; color: var(--muted); line-height: 1.6; }
  .footer-tag {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--teal);
    background: var(--teal-dim);
    border: 1px solid rgba(0,229,195,.2);
    border-radius: 4px;
    padding: 4px 10px;
  }

  /* ── GLOW PULSE (status indicator dot) ── */
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.4} }
  .pulse { animation: pulse 2s ease-in-out infinite; }

  /* ── RESPONSIVE ── */
  @media (max-width: 720px) {
    .main-grid { grid-template-columns: 1fr; }
    .result-age-num { font-size: 40px; }
  }
</style>
</head>
<body>
<div class="wrapper">

  <!-- HERO -->
  <header class="hero">
    <div class="hero-eyebrow">SIMULADOR CIENTÍFICO · NEUROEPIGENÉTICA</div>
    <h1 class="hero-title">Reloj<br><span>Epigenético</span><br>Cerebral</h1>
    <p class="hero-sub">Ajusta los niveles de metilación de genes reportados en la literatura. El sistema estima la edad biológica del cerebro y el riesgo neurodegenerativo.</p>
    <div class="source-chip">Tecalco-Cruz et al. (2021) · TIP Rev. Esp. Cienc. Quím.-Biol., 24: 1–15</div>
  </header>

  <!-- MAIN -->
  <div class="main-grid">

    <!-- LEFT: inputs -->
    <div>
      <div class="panel">
        <div class="panel-head">
          <span class="panel-label">PARÁMETROS DE ENTRADA</span>
        </div>

        <!-- Age -->
        <div class="age-row">
          <span class="age-label">Edad cronológica</span>
          <input type="range" min="1" max="100" value="50" id="s-edad" oninput="update()">
          <span class="age-val" id="v-edad">50 a</span>
        </div>

        <!-- Genes -->
        <div class="genes-section">
          <div class="section-eyebrow">METILACIÓN DE ISLAS CpG (%) · GENES REPORTADOS</div>

          <div class="gene-item">
            <div class="gene-top">
              <span class="gene-name">PIPOX</span>
              <span class="gene-pct" id="pct-pipox">45%</span>
            </div>
            <div class="gene-desc">Alta correlación con edad cronológica en corteza cerebral humana</div>
            <div class="gene-track"><div class="gene-fill" id="b-pipox" style="width:45%"></div></div>
            <input type="range" class="gene-slider" min="0" max="100" value="45" id="s-pipox" oninput="update()">
          </div>

          <div class="gene-item">
            <div class="gene-top">
              <span class="gene-name">DPP8</span>
              <span class="gene-pct" id="pct-dpp8">38%</span>
            </div>
            <div class="gene-desc">Marcador epigenético de envejecimiento cerebral</div>
            <div class="gene-track"><div class="gene-fill" id="b-dpp8" style="width:38%"></div></div>
            <input type="range" class="gene-slider" min="0" max="100" value="38" id="s-dpp8" oninput="update()">
          </div>

          <div class="gene-item">
            <div class="gene-top">
              <span class="gene-name">PTGER3</span>
              <span class="gene-pct" id="pct-ptger3">30%</span>
            </div>
            <div class="gene-desc">Asociado a declive cognitivo durante el envejecimiento</div>
            <div class="gene-track"><div class="gene-fill" id="b-ptger3" style="width:30%"></div></div>
            <input type="range" class="gene-slider" min="0" max="100" value="30" id="s-ptger3" oninput="update()">
          </div>

          <div class="gene-item">
            <div class="gene-top">
              <span class="gene-name">BACE1</span>
              <span class="gene-pct" id="pct-bace1">20%</span>
            </div>
            <div class="gene-desc">Hipometilación → sobreexpresión → progresión de Alzheimer</div>
            <div class="gene-track"><div class="gene-fill" id="b-bace1" style="width:20%"></div></div>
            <input type="range" class="gene-slider" min="0" max="100" value="20" id="s-bace1" oninput="update()">
          </div>

          <div class="gene-item">
            <div class="gene-top">
              <span class="gene-name">APP</span>
              <span class="gene-pct" id="pct-app">18%</span>
            </div>
            <div class="gene-desc">Precursor de proteína amiloide — hipometilado en Alzheimer</div>
            <div class="gene-track"><div class="gene-fill" id="b-app" style="width:18%"></div></div>
            <input type="range" class="gene-slider" min="0" max="100" value="18" id="s-app" oninput="update()">
          </div>

        </div>
      </div>
    </div>

    <!-- RIGHT: results -->
    <div style="display:flex;flex-direction:column;gap:16px;">

      <div class="panel">
        <!-- Age result -->
        <div class="result-hero">
          <div class="result-label-sm">EDAD BIOLÓGICA ESTIMADA DEL CEREBRO</div>
          <div class="result-age-row">
            <span class="result-age-num" id="edad-bio">48</span>
            <span class="result-age-suffix">años</span>
          </div>
          <span class="status-chip chip-sano" id="status-chip">Envejecimiento sano</span>
        </div>

        <!-- Bar comparison -->
        <div class="age-bar-wrap">
          <div class="age-bar-label">
            <span>Comparación de edades</span>
            <span id="diff-label">−2 años vs cronológica</span>
          </div>
          <div class="age-bar-track">
            <div class="age-bar-cron" id="bar-cron" style="width:50%"></div>
            <div class="age-bar-bio"  id="bar-bio"  style="width:48%;background:#00E5C3"></div>
          </div>
          <div class="age-bar-ticks">
            <span>0</span><span>25</span><span>50</span><span>75</span><span>100</span>
          </div>
          <div style="display:flex;gap:16px;margin-top:8px;font-family:var(--mono);font-size:10px;color:var(--muted);">
            <span style="display:flex;align-items:center;gap:5px;"><span style="display:inline-block;width:12px;height:4px;background:rgba(255,255,255,0.18);border-radius:2px;"></span>Cronológica</span>
            <span style="display:flex;align-items:center;gap:5px;"><span id="legend-dot" style="display:inline-block;width:8px;height:8px;border-radius:50%;background:#00E5C3;box-shadow:0 0 6px #00E5C3;"></span>Biológica</span>
          </div>
        </div>

        <!-- Markers -->
        <div class="markers-wrap">
          <div class="panel-label" style="margin-bottom:10px;">MARCADORES MOLECULARES</div>
          <div class="markers-grid">
            <div class="marker-cell">
              <div class="marker-lbl">METILACIÓN GLOBAL</div>
              <div class="marker-val" id="m-global" style="color:#00E5C3;">30%</div>
              <div class="marker-sub">promedio islas CpG</div>
            </div>
            <div class="marker-cell">
              <div class="marker-lbl">H4K16ac</div>
              <div class="marker-val" id="m-h4k16" style="color:#00E5C3;">Alto</div>
              <div class="marker-sub">marca neuroprotectora</div>
            </div>
            <div class="marker-cell">
              <div class="marker-lbl">FACTOR REST</div>
              <div class="marker-val" id="m-rest" style="color:#00E5C3;">Presente</div>
              <div class="marker-sub">silenciador neuroprotector</div>
            </div>
            <div class="marker-cell">
              <div class="marker-lbl">RIESGO ALZHEIMER</div>
              <div class="marker-val" id="m-riesgo" style="color:#00E5C3;">Bajo</div>
              <div class="marker-sub">basado en BACE1 + APP</div>
            </div>
          </div>
        </div>

        <!-- Interpretation -->
        <div class="interp-wrap">
          <div class="interp-title">INTERPRETACIÓN CLÍNICA</div>
          <p class="interp-text highlighted" id="interp-text">
            Los niveles de metilación son moderados y consistentes con la edad cronológica. H4K16ac alto y REST presente indican neuroprotección activa. Riesgo neurodegenerativo bajo.
          </p>
          <div class="note-block" id="note-block">
            El reloj epigenético de Horvath (2012) correlaciona el perfil de metilación de islas CpG de distintos tejidos con la edad cronológica del individuo. Niveles equilibrados sugieren un epigenoma saludable.
          </div>
        </div>
      </div>

    </div>
  </div>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="footer-ref">
      Hernandez et al. (2011) Hum. Mol. Genet. 20(6):1164 &nbsp;·&nbsp;
      Li et al. (2019) Nat. Commun. 10:2246 &nbsp;·&nbsp;
      Nativio et al. (2018) Nat. Neurosci. &nbsp;·&nbsp;
      Horvath &amp; Raj (2018) Nat. Rev. Genet.
    </div>
    <div class="footer-tag">INGENIERÍA DE SOFTWARE · CASO APLICATIVO</div>
  </footer>

</div>

<script>
  function update() {
    const edad  = +document.getElementById('s-edad').value;
    const pipox = +document.getElementById('s-pipox').value;
    const dpp8  = +document.getElementById('s-dpp8').value;
    const ptger = +document.getElementById('s-ptger3').value;
    const bace1 = +document.getElementById('s-bace1').value;
    const app   = +document.getElementById('s-app').value;

    document.getElementById('v-edad').textContent = edad + ' a';

    const genes = [
      { id: 'pipox', v: pipox },
      { id: 'dpp8',  v: dpp8  },
      { id: 'ptger3',v: ptger },
      { id: 'bace1', v: bace1 },
      { id: 'app',   v: app   }
    ];

    genes.forEach(g => {
      const col = g.v < 40 ? '#00E5C3' : g.v < 70 ? '#F5A623' : '#FF4D6D';
      document.getElementById('pct-' + g.id).textContent = g.v + '%';
      document.getElementById('pct-' + g.id).style.color = col;
      document.getElementById('b-'   + g.id).style.width = g.v + '%';
      document.getElementById('b-'   + g.id).style.background = col;
    });

    const metGlobal = Math.round((pipox + dpp8 + ptger + bace1 + app) / 5);
    const alzRisk   = Math.round((bace1 + app) / 2);
    const edadBio   = Math.round(edad * (1 + (metGlobal - 30) / 150));
    const diff      = edadBio - edad;

    document.getElementById('edad-bio').textContent = edadBio;
    document.getElementById('bar-cron').style.width = Math.min(edad, 100)    + '%';
    document.getElementById('bar-bio' ).style.width = Math.min(edadBio, 100) + '%';

    const diffTxt = diff === 0 ? 'igual a cronológica'
                  : diff > 0  ? '+' + diff + ' años vs cronológica'
                  :              diff + ' años vs cronológica';
    document.getElementById('diff-label').textContent = diffTxt;

    const h4k16 = metGlobal < 40 ? 'Alto'     : metGlobal < 65 ? 'Moderado' : 'Bajo';
    const rest  = metGlobal < 50 ? 'Presente' : metGlobal < 70 ? 'Reducido' : 'Ausente';
    const riesgo = alzRisk < 30  ? 'Bajo'     : alzRisk  < 55  ? 'Moderado' : 'Alto';

    document.getElementById('m-global').textContent = metGlobal + '%';
    document.getElementById('m-h4k16').textContent  = h4k16;
    document.getElementById('m-rest').textContent   = rest;
    document.getElementById('m-riesgo').textContent = riesgo;

    let accentCol, chipClass, interp, nota, bioColor;

    if (diff <= 3 && metGlobal < 45) {
      accentCol = '#00E5C3';
      chipClass = 'status-chip chip-sano';
      document.getElementById('status-chip').textContent = 'Envejecimiento sano';
      interp = 'Los niveles de metilación son consistentes con la edad cronológica. H4K16ac alto y REST presente indican neuroprotección activa. Riesgo neurodegenerativo bajo.';
      nota   = 'El reloj epigenético de Horvath correlaciona metilación CpG con edad real. Niveles equilibrados sugieren epigenoma saludable.';
    } else if (diff <= 12 && metGlobal < 65) {
      accentCol = '#F5A623';
      chipClass = 'status-chip chip-riesgo';
      document.getElementById('status-chip').textContent = 'Envejecimiento moderado';
      interp = 'La edad biológica supera ligeramente a la cronológica. Algunos genes muestran hipometilación incipiente. Se recomienda monitoreo de BACE1 y APP.';
      nota   = 'Una divergencia leve puede asociarse con factores ambientales o de estilo de vida. El paper menciona dieta y actividad física como moduladores epigenéticos.';
    } else {
      accentCol = '#FF4D6D';
      chipClass = 'status-chip chip-patol';
      document.getElementById('status-chip').textContent = 'Envejecimiento acelerado';
      interp = 'La edad biológica supera significativamente a la cronológica. BACE1 y APP hipometilados indican riesgo de progresión hacia Alzheimer. H4K16ac reducido y REST ausente.';
      nota   = 'Levine et al. (2015): edad epigenética acelerada en corteza prefrontal se asocia con placas amiloides y deterioro cognitivo — citado en Tecalco-Cruz et al. (2021).';
    }

    document.getElementById('status-chip').className = chipClass;
    document.getElementById('edad-bio').style.color  = accentCol;
    document.getElementById('bar-bio').style.background = accentCol;
    document.getElementById('legend-dot').style.background  = accentCol;
    document.getElementById('legend-dot').style.boxShadow   = '0 0 8px ' + accentCol;
    document.getElementById('note-block').style.borderLeftColor = accentCol;

    const markerCols = metGlobal < 40 ? '#00E5C3' : metGlobal < 65 ? '#F5A623' : '#FF4D6D';
    ['m-global','m-h4k16','m-rest','m-riesgo'].forEach(id => {
      document.getElementById(id).style.color = markerCols;
    });

    document.getElementById('interp-text').textContent = interp;
    document.getElementById('note-block').textContent  = nota;
  }

  update();
</script>
</body>
</html>

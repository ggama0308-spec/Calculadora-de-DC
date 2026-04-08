# Calculadora-de-DC[index.html](https://github.com/user-attachments/files/26557037/index.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
<meta name="theme-color" content="#0d1117" />
<title>% Gordura — Durnin & Womersley</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0d1117;
    --surface: #161b22;
    --surface2: #1c2330;
    --border: rgba(255,255,255,0.08);
    --border2: rgba(255,255,255,0.15);
    --text: #e6edf3;
    --muted: #7d8590;
    --accent: #58a6ff;
    --accent-dim: rgba(88,166,255,0.12);
    --green: #3fb950;
    --green-dim: rgba(63,185,80,0.12);
    --yellow: #d29922;
    --yellow-dim: rgba(210,153,34,0.12);
    --red: #f85149;
    --red-dim: rgba(248,81,73,0.12);
    --mono: 'DM Mono', monospace;
    --sans: 'DM Sans', sans-serif;
    --radius: 10px;
  }

  html { background: var(--bg); }

  body {
    font-family: var(--sans);
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    padding: env(safe-area-inset-top, 0) 0 env(safe-area-inset-bottom, 0);
  }

  .header {
    padding: 2rem 1.25rem 1rem;
    border-bottom: 1px solid var(--border);
    background: var(--bg);
    position: sticky;
    top: 0;
    z-index: 10;
  }

  .header-label {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: 0.15em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 4px;
  }

  .header h1 {
    font-size: 18px;
    font-weight: 400;
    color: var(--text);
    line-height: 1.3;
  }

  .header h1 span {
    font-weight: 300;
    color: var(--muted);
  }

  .content { padding: 1.5rem 1.25rem 3rem; max-width: 500px; margin: 0 auto; }

  .section-label {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: 0.12em;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 10px;
  }

  .sex-toggle { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 28px; }

  .sex-btn {
    padding: 12px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    color: var(--muted);
    font-family: var(--sans);
    font-size: 14px;
    font-weight: 400;
    cursor: pointer;
    transition: all 0.15s;
    letter-spacing: 0.02em;
  }

  .sex-btn.active {
    background: var(--accent-dim);
    border-color: var(--accent);
    color: var(--accent);
    font-weight: 500;
  }

  .field { margin-bottom: 16px; }

  .field label {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    font-size: 13px;
    color: var(--muted);
    margin-bottom: 7px;
  }

  .field label span {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: 0.05em;
  }

  input[type="number"] {
    width: 100%;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 12px 14px;
    font-family: var(--mono);
    font-size: 16px;
    color: var(--text);
    outline: none;
    transition: border-color 0.15s;
    -webkit-appearance: none;
    appearance: none;
  }

  input[type="number"]:focus { border-color: var(--border2); }
  input[type="number"]::placeholder { color: var(--border2); }

  .dobras-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 28px; }

  .calc-btn {
    width: 100%;
    padding: 14px;
    background: var(--accent-dim);
    border: 1px solid var(--accent);
    border-radius: var(--radius);
    color: var(--accent);
    font-family: var(--sans);
    font-size: 15px;
    font-weight: 500;
    cursor: pointer;
    letter-spacing: 0.02em;
    transition: all 0.15s;
  }

  .calc-btn:active { transform: scale(0.98); opacity: 0.8; }

  .error {
    font-size: 12px;
    color: var(--red);
    margin-top: 10px;
    font-family: var(--mono);
    display: none;
  }

  .result { margin-top: 28px; display: none; }

  .metrics-row { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; margin-bottom: 12px; }

  .metric {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 14px 10px;
    text-align: center;
  }

  .metric-lbl { font-size: 10px; color: var(--muted); letter-spacing: 0.06em; text-transform: uppercase; margin-bottom: 6px; font-family: var(--mono); }
  .metric-val { font-family: var(--mono); font-size: 20px; font-weight: 500; color: var(--text); line-height: 1; }
  .metric-unit { font-size: 10px; color: var(--muted); margin-top: 3px; font-family: var(--mono); }

  .classification {
    border-radius: var(--radius);
    padding: 14px 16px;
    text-align: center;
    font-size: 15px;
    font-weight: 500;
    margin-bottom: 12px;
    letter-spacing: 0.03em;
  }

  .cls-atleta { background: var(--green-dim); color: var(--green); border: 1px solid rgba(63,185,80,0.25); }
  .cls-bom { background: var(--accent-dim); color: var(--accent); border: 1px solid rgba(88,166,255,0.25); }
  .cls-medio { background: var(--yellow-dim); color: var(--yellow); border: 1px solid rgba(210,153,34,0.25); }
  .cls-elevado { background: var(--red-dim); color: var(--red); border: 1px solid rgba(248,81,73,0.25); }

  .steps {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 14px 16px;
  }

  .steps-title {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: 0.1em;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 10px;
  }

  .step-line {
    display: flex;
    justify-content: space-between;
    font-size: 13px;
    padding: 4px 0;
    border-bottom: 1px solid var(--border);
  }

  .step-line:last-child { border-bottom: none; }
  .step-line .desc { color: var(--muted); }
  .step-line .val { font-family: var(--mono); color: var(--text); font-size: 12px; }

  .reset-btn {
    width: 100%;
    margin-top: 14px;
    padding: 11px;
    background: transparent;
    border: 1px solid var(--border);
    border-radius: var(--radius);
    color: var(--muted);
    font-family: var(--sans);
    font-size: 13px;
    cursor: pointer;
    transition: all 0.15s;
  }

  .reset-btn:active { opacity: 0.6; }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button { -webkit-appearance: none; margin: 0; }
  input[type=number] { -moz-appearance: textfield; }
</style>
</head>
<body>

<div class="header">
  <div class="header-label">Avaliação Corporal</div>
  <h1>% Gordura <span>— Durnin & Womersley (1974)</span></h1>
</div>

<div class="content">

  <div class="section-label">Sexo biológico</div>
  <div class="sex-toggle">
    <button class="sex-btn active" id="btn-m" onclick="setSexo('M')">Masculino</button>
    <button class="sex-btn" id="btn-f" onclick="setSexo('F')">Feminino</button>
  </div>

  <div class="field">
    <label>Idade <span>anos</span></label>
    <input type="number" id="idade" placeholder="25" inputmode="numeric" />
  </div>

  <div class="section-label" style="margin-top:20px;">Dobras cutâneas</div>
  <div class="dobras-grid">
    <div class="field">
      <label>Tríceps <span>mm</span></label>
      <input type="number" id="dc-tri" placeholder="10" inputmode="decimal" />
    </div>
    <div class="field">
      <label>Bíceps <span>mm</span></label>
      <input type="number" id="dc-bic" placeholder="5" inputmode="decimal" />
    </div>
    <div class="field">
      <label>Subescapular <span>mm</span></label>
      <input type="number" id="dc-sub" placeholder="15" inputmode="decimal" />
    </div>
    <div class="field">
      <label>Suprailíaca <span>mm</span></label>
      <input type="number" id="dc-sup" placeholder="15" inputmode="decimal" />
    </div>
  </div>

  <button class="calc-btn" onclick="calcular()">Calcular</button>
  <div class="error" id="err"></div>

  <div class="result" id="resultado">
    <div class="metrics-row">
      <div class="metric">
        <div class="metric-lbl">Soma</div>
        <div class="metric-val" id="r-soma">—</div>
        <div class="metric-unit">mm</div>
      </div>
      <div class="metric">
        <div class="metric-lbl">Densidade</div>
        <div class="metric-val" id="r-dc">—</div>
        <div class="metric-unit">g/cm³</div>
      </div>
      <div class="metric">
        <div class="metric-lbl">Gordura</div>
        <div class="metric-val" id="r-pg">—</div>
        <div class="metric-unit">%</div>
      </div>
    </div>

    <div class="classification" id="r-class"></div>

    <div class="steps">
      <div class="steps-title">Passo a passo</div>
      <div id="r-steps"></div>
    </div>

    <button class="reset-btn" onclick="resetar()">Limpar e recalcular</button>
  </div>

</div>

<script>
let sexo = 'M';

const K = {
  M: [
    {min:17,max:19,c:1.1620,m:0.0630},
    {min:20,max:29,c:1.1631,m:0.0632},
    {min:30,max:39,c:1.1422,m:0.0544},
    {min:40,max:49,c:1.1620,m:0.0700},
    {min:50,max:999,c:1.1715,m:0.0779}
  ],
  F: [
    {min:18,max:19,c:1.1549,m:0.0678},
    {min:20,max:29,c:1.1599,m:0.0717},
    {min:30,max:39,c:1.1423,m:0.0632},
    {min:40,max:49,c:1.1333,m:0.0612},
    {min:50,max:999,c:1.1339,m:0.0645}
  ]
};

function setSexo(s) {
  sexo = s;
  document.getElementById('btn-m').classList.toggle('active', s==='M');
  document.getElementById('btn-f').classList.toggle('active', s==='F');
}

function getK(idade) {
  return K[sexo].find(r => idade >= r.min && idade <= r.max);
}

function classificar(pg) {
  if (sexo === 'M') {
    if (pg <= 13) return ['Atleta', 'cls-atleta'];
    if (pg <= 17) return ['Bom / fitness', 'cls-bom'];
    if (pg <= 24) return ['Médio — saudável', 'cls-medio'];
    return ['Elevado — sobrepeso', 'cls-elevado'];
  } else {
    if (pg <= 20) return ['Atleta', 'cls-atleta'];
    if (pg <= 24) return ['Bom / fitness', 'cls-bom'];
    if (pg <= 31) return ['Médio — saudável', 'cls-medio'];
    return ['Elevado — sobrepeso', 'cls-elevado'];
  }
}

function calcular() {
  const err = document.getElementById('err');
  err.style.display = 'none';

  const idade = parseFloat(document.getElementById('idade').value);
  const tri = parseFloat(document.getElementById('dc-tri').value);
  const bic = parseFloat(document.getElementById('dc-bic').value);
  const sub = parseFloat(document.getElementById('dc-sub').value);
  const sup = parseFloat(document.getElementById('dc-sup').value);

  if ([idade,tri,bic,sub,sup].some(v => isNaN(v) || v <= 0)) {
    err.textContent = 'Preencha todos os campos.';
    err.style.display = 'block';
    return;
  }

  const k = getK(idade);
  if (!k) {
    err.textContent = 'Idade fora do intervalo da tabela.';
    err.style.display = 'block';
    return;
  }

  const S = tri + bic + sub + sup;
  const logS = Math.log10(S);
  const DC = k.c - (k.m * logS);
  const PG = ((4.95 / DC) - 4.50) * 100;
  const [cls, clsCss] = classificar(PG);

  document.getElementById('r-soma').textContent = S.toFixed(1);
  document.getElementById('r-dc').textContent = DC.toFixed(4);
  document.getElementById('r-pg').textContent = PG.toFixed(1);

  const clsEl = document.getElementById('r-class');
  clsEl.className = 'classification ' + clsCss;
  clsEl.textContent = cls;

  document.getElementById('r-steps').innerHTML = `
    <div class="step-line"><span class="desc">Soma (S)</span><span class="val">${tri} + ${bic} + ${sub} + ${sup} = ${S.toFixed(1)} mm</span></div>
    <div class="step-line"><span class="desc">log₁₀(${S.toFixed(1)})</span><span class="val">${logS.toFixed(4)}</span></div>
    <div class="step-line"><span class="desc">Constantes (c / m)</span><span class="val">${k.c} / ${k.m}</span></div>
    <div class="step-line"><span class="desc">DC = c − (m × log S)</span><span class="val">${DC.toFixed(4)} g/cm³</span></div>
    <div class="step-line"><span class="desc">%G = (4,95 ÷ DC − 4,50) × 100</span><span class="val">${PG.toFixed(1)}%</span></div>
  `;

  document.getElementById('resultado').style.display = 'block';
  document.getElementById('resultado').scrollIntoView({behavior:'smooth', block:'nearest'});
}

function resetar() {
  ['idade','dc-tri','dc-bic','dc-sub','dc-sup'].forEach(id => document.getElementById(id).value = '');
  document.getElementById('resultado').style.display = 'none';
  document.getElementById('err').style.display = 'none';
  window.scrollTo({top:0, behavior:'smooth'});
}
</script>
</body>
</html>

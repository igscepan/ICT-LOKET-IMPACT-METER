<!DOCTYPE html>
<html lang="nl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>ICT LOKET NOORDKADE — IMPACT DASHBOARD</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,wght@0,400;0,500;0,700;1,400&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --sand:#D0B292;--sl:#f4e6d7;--sm:#e3ceb5;--ink:#2b2b2b;--is:#5a4a3a;
  --w:#fdfaf6;--acc:#e63946;--grn:#2b7a2b;--amber:#f4a261;
  --card-bg:rgba(253,250,246,0.78);--shadow:5px 5px 0 var(--ink);
  --radius:14px;
}
html,body{width:100%;height:100%;overflow:hidden;font-family:'DM Sans',sans-serif;color:var(--ink)}
body{background:linear-gradient(135deg,#eecfa3 0%,#D0B292 45%,#c09870 100%);display:flex;flex-direction:column}
body::before{content:'';position:fixed;inset:0;background-image:radial-gradient(circle,rgba(43,43,43,0.05) 1.5px,transparent 1.5px);background-size:28px 28px;pointer-events:none;z-index:0}

header{position:relative;z-index:10;display:flex;align-items:center;justify-content:space-between;padding:0 20px;flex-shrink:0;background:rgba(253,250,246,0.5);backdrop-filter:blur(16px);border-bottom:2.5px solid var(--ink);box-shadow:0 3px 0 rgba(43,43,43,0.07);min-height:110px}
.h-left{display:flex;align-items:center;gap:14px}
#ictLogo{height:76px;width:auto;border-radius:8px}
.h-title p{font-size:clamp(0.95rem,1.6vw,1.15rem);color:var(--is);letter-spacing:.2em;text-transform:uppercase;font-weight:700;display:flex;align-items:center;gap:10px}
.live-pill{display:inline-flex;align-items:center;gap:5px;background:rgba(230,57,70,0.12);padding:3px 10px;border-radius:20px;border:1.5px solid var(--acc);color:var(--acc);font-size:.82em;letter-spacing:.08em;font-weight:700}
.pulse{width:8px;height:8px;border-radius:50%;background:#e63946;flex-shrink:0;animation:pulse-anim 2s infinite}
@keyframes pulse-anim{0%,100%{opacity:1;box-shadow:0 0 6px rgba(230,57,70,0.7)}50%{opacity:.4;box-shadow:0 0 12px rgba(230,57,70,0.9)}}

.time-container{text-align:center;background:rgba(253,250,246,0.85);padding:8px 18px;border-radius:14px;border:2.5px solid var(--ink);box-shadow:4px 4px 0 var(--ink)}
#clock{font-family:'Bebas Neue',sans-serif;font-size:clamp(1.55rem,2.2vw,1.7rem);letter-spacing:2px;color:var(--ink)}
#date{font-size:clamp(0.8rem,1.1vw,0.9rem);color:var(--is);letter-spacing:1px;margin-top:2px}

.h-right{display:flex;align-items:center;gap:20px}
.powered-by{font-family:'Bebas Neue',sans-serif;font-size:.7rem;letter-spacing:.18em;color:var(--ink);opacity:.75;margin-bottom:4px}
#kw1cLogo{height:72px;width:auto}

.banner{flex-shrink:0;background:linear-gradient(90deg,rgba(230,57,70,0.12),rgba(230,57,70,0.06),rgba(230,57,70,0.12));padding:7px 18px;text-align:center;border-bottom:2.5px solid var(--ink);border-top:2px solid var(--ink);font-family:'Bebas Neue',sans-serif;font-size:clamp(.9rem,1.5vw,1.15rem);color:var(--ink);letter-spacing:.12em;position:relative;z-index:1}
.grid{flex:1;display:grid;grid-template-columns:1fr 1fr;grid-template-rows:1fr 1fr;gap:8px;padding:8px 12px 6px;min-height:0;position:relative;z-index:1}
.card{background:var(--card-bg);backdrop-filter:blur(10px);border-radius:var(--radius);border:2.5px solid var(--ink);padding:10px 12px;box-shadow:var(--shadow);display:flex;flex-direction:column;gap:0;overflow:hidden;transition:transform .13s}
.card:hover{transform:translateY(-2px)}
.ct{font-family:'Bebas Neue',sans-serif;font-size:clamp(1rem,1.6vw,1.3rem);letter-spacing:.08em;display:flex;align-items:center;gap:7px;padding-bottom:6px;margin-bottom:6px;border-bottom:2px solid var(--sm)}
.dot{width:9px;height:9px;border-radius:50%;flex-shrink:0;animation:pulse-anim 2s infinite}
.month-top{display:flex;align-items:flex-end;justify-content:space-between;margin-bottom:6px}
.vbig{font-family:'Bebas Neue',sans-serif;font-size:clamp(2.8rem,5.5vw,4rem);line-height:1;color:var(--ink);cursor:pointer;user-select:none;text-shadow:3px 3px 0 rgba(43,43,43,0.12);transition:transform .08s,color .1s}
.vbig:active{transform:scale(.92);color:var(--acc)}
.goal-info{text-align:right}
.goal-target{font-family:'Bebas Neue',sans-serif;font-size:clamp(1.2rem,2vw,1.6rem);color:var(--acc)}
.goal-label{font-size:.65rem;color:var(--is);text-transform:uppercase;letter-spacing:.05em}
.progress-bar{height:10px;background:var(--sm);border-radius:50px;border:1.5px solid var(--ink);overflow:hidden;margin-bottom:8px}
.progress-fill{height:100%;width:0%;background:linear-gradient(90deg,var(--acc),#ff5a5f);border-radius:50px;transition:width .4s ease-out}
.chart-tabs{display:flex;gap:4px;margin-bottom:6px}
.chart-tab{flex:1;padding:4px 6px;text-align:center;font-size:clamp(.65rem,.95vw,.8rem);font-weight:700;color:var(--is);background:rgba(227,206,181,.35);border:1.5px solid var(--sm);border-radius:8px;cursor:pointer;transition:all .18s;letter-spacing:.03em}
.chart-tab.active{background:var(--ink);color:var(--w);border-color:var(--ink)}
.chart-wrap{flex:1;min-height:0;position:relative}
canvas.bar-chart{width:100%;height:100%;display:block}
.stat-row{display:flex;justify-content:space-between;align-items:center;padding:5px 8px;border-radius:9px;cursor:pointer;transition:background .12s,transform .1s;border-bottom:1px solid rgba(227,206,181,.5);flex:1}
.stat-row:last-child{border-bottom:none}
.stat-row:hover{background:rgba(43,43,43,.07);transform:translateX(3px)}
.stat-row:active{background:rgba(230,57,70,.08);transform:scale(.97)}
.stat-row.no-click{cursor:default;pointer-events:none}
.sl-label{font-size:clamp(.8rem,1.3vw,1rem);color:var(--is);text-transform:uppercase;letter-spacing:.04em;font-weight:500}
.sl-val{font-family:'Bebas Neue',sans-serif;font-size:clamp(1.1rem,1.9vw,1.5rem);line-height:1;color:var(--ink);transition:color .15s,transform .15s}
.sl-val.bump{color:var(--grn);transform:scale(1.18)}
.stag-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:6px;flex:1}
.stag-card{background:linear-gradient(135deg,rgba(43,110,43,0.08),rgba(230,57,70,0.04));padding:6px 8px;border-radius:8px;border:1.5px solid rgba(43,110,43,.35);transition:transform .1s,box-shadow .1s;text-align:center;display:flex;flex-direction:column;gap:4px;justify-content:center}
.stag-card:hover{transform:translateY(-2px);box-shadow:0 4px 12px rgba(43,110,43,.2)}
.stag-name-input{width:100%;border:none;background:rgba(255,255,255,.6);border-bottom:2px solid var(--grn);padding:3px 4px;text-align:center;font-weight:700;font-size:clamp(.75rem,1.1vw,.9rem);color:var(--ink);font-family:'DM Sans',sans-serif;transition:background .2s;outline:none}
.stag-name-input:focus{background:rgba(255,255,255,.9);border-bottom-color:var(--acc)}
.stag-count{font-family:'Bebas Neue',sans-serif;font-size:clamp(1.4rem,2.5vw,2rem);color:var(--grn);line-height:1}
.stag-btn{background:var(--grn);color:var(--w);border:none;border-radius:6px;padding:4px 8px;font-weight:700;font-size:.8rem;cursor:pointer;transition:background .2s,transform .1s;font-family:'DM Sans',sans-serif}
.stag-btn:hover{background:var(--acc);transform:scale(1.05)}
.stag-btn:active{transform:scale(.95)}
.ticker{flex-shrink:0;height:clamp(32px,4.2vh,36px);background:linear-gradient(90deg,rgba(230,57,70,.95),rgba(200,35,50,.95),rgba(230,57,70,.95));border-top:2.5px solid var(--ink);overflow:hidden;display:flex;align-items:center;box-shadow:0 -3px 12px rgba(230,57,70,.25)}
.ticker-label{font-family:'Bebas Neue',sans-serif;font-size:clamp(.75rem,1.1vw,.9rem);letter-spacing:.12em;color:var(--w);flex-shrink:0;padding:0 12px;text-transform:uppercase;font-weight:900;border-right:2px solid rgba(255,255,255,.28);background:rgba(0,0,0,.2);display:flex;align-items:center}
.ticker-track{flex:1;overflow:hidden;position:relative}
.ticker-inner{display:flex;gap:32px;white-space:nowrap;animation:ticker-scroll 30s linear infinite}
.ticker-item{font-size:clamp(.68rem,0.95vw,.82rem);color:rgba(255,255,255,.93);font-weight:600;flex-shrink:0}
@keyframes ticker-scroll{0%{transform:translateX(0)}100%{transform:translateX(-50%)}}
#milestone{position:fixed;inset:0;display:none;z-index:10001;background:rgba(0,0,0,.65);backdrop-filter:blur(8px);justify-content:center;align-items:center}
.milestone-box{background:linear-gradient(135deg,var(--acc),#ff5a5f);color:var(--w);padding:2.5rem 3rem;border-radius:20px;text-align:center;box-shadow:0 24px 60px rgba(230,57,70,.5);font-family:'Bebas Neue',sans-serif}
.tooltip{position:fixed;background:var(--ink);color:var(--w);padding:5px 10px;border-radius:6px;font-size:.72rem;pointer-events:none;z-index:1000;display:none;border:1px solid var(--acc);white-space:nowrap}
</style>
</head>
<body>

<header>
  <div class="h-left">
    <img id="ictLogo" src="https://cdn.phototourl.com/uploads/2026-03-16-381af662-8528-408d-9280-ba1a254f0c3c.png" alt="ICT Loket">
    <div class="h-title">
      <p><span class="pulse"></span> Impact Dashboard — <span class="live-pill"><span class="pulse"></span>LIVE</span> Overzicht</p>
    </div>
  </div>
  <div class="time-container">
    <div id="clock">00:00:00</div>
    <div id="date"></div>
  </div>
  <div class="h-right">
    <div style="display:flex;flex-direction:column;align-items:center;gap:2px">
      <span class="powered-by">✦ Powered by ✦</span>
      <img id="kw1cLogo" src="https://image2url.com/r2/default/images/1773139826689-3d65e996-e132-41ea-817f-026972b0d650.png" alt="KW1C">
    </div>
  </div>
</header>

<div class="banner">📈 IMPACT DASHBOARD — ICT LOKET NOORDKADE — ACTIEF SINDS 2020</div>

<div class="grid">
  <!-- CARD 1 -->
  <div class="card">
    <div class="ct"><span class="dot" style="background:var(--acc)"></span>Devices Refurbished — <span id="maandLabel" style="opacity:.7;font-size:.85em"></span></div>
    <div class="month-top">
      <div class="vbig" id="vn" onmousedown="startHold()" onmouseup="stopHold()" onmouseleave="stopHold()" ontouchstart="startHold()" ontouchend="stopHold()" ontouchcancel="stopHold()">0</div>
      <div class="goal-info">
        <div class="goal-target">🎯 40</div>
        <div class="goal-label">Maandelijks doel</div>
      </div>
    </div>
    <div class="progress-bar"><div class="progress-fill" id="pf"></div></div>
    <div class="chart-tabs">
      <div class="chart-tab active" onclick="switchChart('week',this)">Vandaag</div>
      <div class="chart-tab" onclick="switchChart('month',this)">Maand</div>
      <div class="chart-tab" onclick="switchChart('year',this)">Jaar</div>
    </div>
    <div class="chart-wrap"><canvas class="bar-chart" id="barChart"></canvas></div>
  </div>

  <!-- CARD 2 -->
  <div class="card">
    <div class="ct"><span class="dot" style="background:var(--amber)"></span>🌍 Totale Impact Vanaf 2020</div>
    <div class="stat-rows-wrap">
      <div class="stat-row" data-key="received" onclick="addStat('received',1)" onmouseenter="showTip(event,'Klik om +1 • ⌫ verwijderen')" onmouseleave="hideTip()"><div class="sl-label">💻 Apparaten Ontvangen</div><div class="sl-val" id="tR">747</div></div>
      <div class="stat-row" data-key="refurbished" onclick="addStat('refurbished',1)" onmouseenter="showTip(event,'Klik om +1 • ⌫ verwijderen')" onmouseleave="hideTip()"><div class="sl-label">🔧 Gereviseerd</div><div class="sl-val" id="tF">613</div></div>
      <div class="stat-row no-click"><div class="sl-label">🌲 CO₂ Bespaard</div><div class="sl-val" id="tC">153.250 kg</div></div>
      <div class="stat-row" data-key="partners" onclick="addStat('partners',1)" onmouseenter="showTip(event,'Klik om +1 • ⌫ verwijderen')" onmouseleave="hideTip()"><div class="sl-label">🤝 Partners</div><div class="sl-val" id="tP">38</div></div>
      <div class="stat-row" data-key="questions" onclick="addStat('questions',1)" onmouseenter="showTip(event,'Klik om +1 • ⌫ verwijderen')" onmouseleave="hideTip()"><div class="sl-label">❓ Vragen Beantwoord</div><div class="sl-val" id="tQ">545</div></div>
    </div>
  </div>

  <!-- CARD 3: 8 Stagiaires -->
  <div class="card">
    <div class="ct"><span class="dot" style="background:var(--grn)"></span>🎓 Stagiaires — Gereviseerde Apparaten</div>
    <div class="stag-grid" id="stag-grid"></div>
  </div>

  <!-- CARD 4 -->
  <div class="card">
    <div class="ct"><span class="dot" style="background:var(--amber)"></span>⚡ Vandaag</div>
    <div class="stat-rows-wrap">
      <div class="stat-row" data-key="received_today" onclick="addStat('received_today',1)" onmouseenter="showTip(event,'Klik om +1 toe te voegen')" onmouseleave="hideTip()"><div class="sl-label">💻 Apparaten Ontvangen</div><div class="sl-val" id="rT_today">0</div></div>
      <div class="stat-row" data-key="refurbished_today" onclick="addStat('refurbished_today',1)" onmouseenter="showTip(event,'Klik om +1 toe te voegen')" onmouseleave="hideTip()"><div class="sl-label">🔧 Gereviseerd</div><div class="sl-val" id="fT">0</div></div>
      <div class="stat-row no-click"><div class="sl-label">🌲 CO₂ Vandaag</div><div class="sl-val" id="cT">0 kg</div></div>
      <div class="stat-row" data-key="partners_today" onclick="addStat('partners_today',1)" onmouseenter="showTip(event,'Klik om +1 toe te voegen')" onmouseleave="hideTip()"><div class="sl-label">🤝 Partners</div><div class="sl-val" id="pT">0</div></div>
      <div class="stat-row" data-key="questions_today" onclick="addStat('questions_today',1)" onmouseenter="showTip(event,'Klik om +1 toe te voegen')" onmouseleave="hideTip()"><div class="sl-label">❓ Vragen</div><div class="sl-val" id="qT">0</div></div>
    </div>
  </div>
</div>

<div class="ticker">
  <div class="ticker-label">🔴 NIEUWS</div>
  <div class="ticker-track">
    <div class="ticker-inner" id="tickerInner">
      <span class="ticker-item">🎯 Doel: 1000 apparaten per jaar reviseren</span>
      <span class="ticker-item">🗓️ Actief since 2020</span>
      <span class="ticker-item">📍 Veghel, Noord-Brabant</span>
      <span class="ticker-item">🏫 Onderdeel van Koning Willem I College</span>
      <span class="ticker-item">♻️ Laptops een tweede leven geven</span>
      <span class="ticker-item">💚 250 kg CO₂ bespaard per laptop</span>
      <span class="ticker-item">🎓 Stagaires leren praktisch IT</span>
      <span class="ticker-item">✅ Erkend leerbedrijf</span>
      <!-- dupe -->
      <span class="ticker-item">🎯 Doel: 1000 apparaten per jaar reviseren</span>
      <span class="ticker-item">🗓️ Actief since 2020</span>
      <span class="ticker-item">📍 Veghel, Noord-Brabant</span>
      <span class="ticker-item">🏫 Onderdeel van Koning Willem I College</span>
      <span class="ticker-item">♻️ Laptops een tweede leven geven</span>
      <span class="ticker-item">💚 250 kg CO₂ bespaard per laptop</span>
      <span class="ticker-item">🎓 Stagaires leren praktisch IT</span>
      <span class="ticker-item">✅ Erkend leerbedrijf</span>
    </div>
  </div>
</div>

<div id="milestone" style="display:none;justify-content:center;align-items:center">
  <div class="milestone-box" onclick="this.parentElement.style.display='none'">
    <h2 id="ms-title">🎉 MIJLPAAL!</h2>
    <p id="ms-text"></p>
  </div>
</div>
<div class="tooltip" id="tooltip"></div>

<script>
const $ = id => document.getElementById(id);

let V = 0, tRv = 747, tFv = 613, tPv = 38, tQv = 545;
let rTv_today = 0, fTv_today = 0, cTv_today = 0, pTv_today = 0, qTv_today = 0;
let VG = 40, holding = false, holdInterval = null;
let stagaires = {s1:0,s2:0,s3:0,s4:0,s5:0,s6:0,s7:0,s8:0};
let weekData = [0,0,0,0,0,0,0];
let monthData = [0,0,0,0];
let yearData = [0,0,0,0,0,0,0,0,0,0,0,0];
let chartMode = 'week';
let focus = 'vn';
let lastDate = new Date().toDateString();

// Clock + Date
function updateClock(){
  const clock = $('clock');
  const dateEl = document.createElement('div');
  dateEl.id = 'date';
  dateEl.style.fontSize = '0.85rem';
  dateEl.style.color = 'var(--is)';
  $('clock').parentElement.appendChild(dateEl);

  setInterval(() => {
    const now = new Date();
    clock.textContent = now.toLocaleTimeString('nl-NL', {hour:'2-digit', minute:'2-digit', second:'2-digit'});
    dateEl.textContent = now.toLocaleDateString('nl-NL', {weekday:'long', day:'numeric', month:'long', year:'numeric'});
  }, 1000);
}

function createStagaireCards(){
  const grid = $('stag-grid');
  grid.innerHTML = '';
  for(let i = 1; i <= 8; i++){
    const id = `s${i}`;
    const card = document.createElement('div');
    card.className = 'stag-card';
    card.innerHTML = `
      <input type="text" class="stag-name-input" id="${id}-name" placeholder="Naam" onchange="saveStagaireNames()">
      <div class="stag-count" id="${id}-count">0</div>
      <button class="stag-btn" onclick="addStagaire('${id}')">+1</button>
    `;
    grid.appendChild(card);
  }
}

function addStagaire(id){
  stagaires[id]++;
  fTv_today++;
  tFv++;
  $('tF').textContent = tFv;
  $('fT').textContent = fTv_today;
  addV(1);
  upCO2();
  updateStagaireCounts();
  bump('tF');
  bump('fT');
  floatEmoji($(id+'-count'), '🔧');
  saveData();
}

function updateStagaireCounts(){
  for(let i = 1; i <= 8; i++){
    const el = $(`s${i}-count`);
    if(el) el.textContent = stagaires[`s${i}`] || 0;
  }
}

// Dag reset (automatisch)
function checkDayReset(){
  const today = new Date().toDateString();
  if(today !== lastDate){
    resetStagiairesOnly();
    lastDate = today;
  }
}

function resetStagiairesOnly(){
  for(let i = 1; i <= 8; i++) stagaires[`s${i}`] = 0;
  rTv_today = fTv_today = pTv_today = qTv_today = 0;
  weekData = [0,0,0,0,0,0,0];
  monthData = [0,0,0,0];
  updateStagaireCounts();
  $('rT_today').textContent = 0;
  $('fT').textContent = 0;
  $('pT').textContent = 0;
  $('qT').textContent = 0;
  drawChart();
  saveData();
}

// Dubbele spatie reset (met namen wissen)
let spacePressCount = 0;
let spaceTimeout = null;

document.addEventListener('keydown', e => {
  if(e.key === ' '){
    spacePressCount++;
    if(spacePressCount === 2){
      e.preventDefault();
      if(confirm("Wil je dit bestand resetten naar de huidige nummers?\n\n(Stagiaires tellers + namen gaan naar 0)")){
        // Volledige stagaire reset (namen + tellers)
        for(let i = 1; i <= 8; i++){
          stagaires[`s${i}`] = 0;
          const nameInput = $(`s${i}-name`);
          if(nameInput) nameInput.value = '';
        }
        resetStagiairesOnly();
        saveStagaireNames();
      }
      spacePressCount = 0;
    }
    clearTimeout(spaceTimeout);
    spaceTimeout = setTimeout(() => spacePressCount = 0, 400);
  }
});

// De rest van de functies (drawChart, addV, addStat, etc.) zijn hetzelfde als vorige werkende versie
// (ik heb ze hier niet volledig herhaald om ruimte te besparen, maar ze zijn identiek)

function drawChart(){ /* jouw drawChart */ 
  const canvas=$('barChart'); if(!canvas) return;
  const dpr=window.devicePixelRatio||1; const rect=canvas.getBoundingClientRect();
  canvas.width=rect.width*dpr; canvas.height=rect.height*dpr;
  const ctx=canvas.getContext('2d'); ctx.scale(dpr,dpr);
  const W=rect.width, H=rect.height; ctx.clearRect(0,0,W,H);

  let data,labels;
  if(chartMode==='week'){data=weekData;labels=['Ma','Di','Wo','Do','Vr','Za','Zo'];}
  else if(chartMode==='month'){data=monthData;labels=['Wk 1','Wk 2','Wk 3','Wk 4'];}
  else {data=yearData;labels=['Jan','Feb','Mrt','Apr','Mei','Jun','Jul','Aug','Sep','Okt','Nov','Dec'];}

  const maxVal=Math.max(...data,1);
  const padL=28,padR=8,padT=10,padB=28;
  const chartW=W-padL-padR; const chartH=H-padT-padB;
  const barCount=data.length; const gap=Math.max(4,chartW/(barCount*5));
  const barW=(chartW-gap*(barCount-1))/barCount;

  ctx.strokeStyle='rgba(90,74,58,0.12)';
  for(let i=0;i<=4;i++){const y=padT+chartH-(chartH/4)*i;ctx.beginPath();ctx.moveTo(padL,y);ctx.lineTo(W-padR,y);ctx.stroke();}

  const todayIdx=new Date().getDay()===0?6:new Date().getDay()-1;

  data.forEach((val,i)=>{
    const x=padL+i*(barW+gap); const barH=chartH*(val/maxVal); const y=padT+chartH-barH;
    const isToday=chartMode==='week' && i===todayIdx;
    const grad=ctx.createLinearGradient(x,y,x,padT+chartH);
    grad.addColorStop(0,isToday?'#e63946':'rgba(90,74,58,0.85)');
    grad.addColorStop(1,isToday?'rgba(230,57,70,0.5)':'rgba(90,74,58,0.25)');
    ctx.fillStyle=grad; ctx.beginPath(); ctx.roundRect(x,y,barW,barH,4); ctx.fill();

    if(val>0){
      ctx.fillStyle=isToday?'#e63946':'rgba(43,43,43,0.75)';
      ctx.font=`bold ${Math.min(10,barW*0.75)}px DM Sans`; ctx.textAlign='center';
      ctx.fillText(val,x+barW/2,y-3);
    }
    ctx.fillStyle='rgba(90,74,58,0.7)'; ctx.font=`bold 9px DM Sans`;
    ctx.fillText(labels[i],x+barW/2,H-6);
  });
}

function switchChart(mode,el){chartMode=mode;document.querySelectorAll('.chart-tab').forEach(t=>t.classList.remove('active'));el.classList.add('active');drawChart();}

function startHold(){if(holding)return;holding=true;addV(1);let speed=200;holdInterval=setInterval(()=>{addV(1);speed=Math.max(60,speed-15);clearInterval(holdInterval);holdInterval=setInterval(()=>addV(1),speed);},speed);}
function stopHold(){holding=false;if(holdInterval){clearInterval(holdInterval);holdInterval=null;}}

function addV(n){
  V=Math.max(0,Math.min(V+n,9999));
  $('vn').textContent=V;
  $('pf').style.width=Math.min(V/VG*100,100)+'%';
  const today=new Date(); const idx=today.getDay()===0?6:today.getDay()-1;
  if(n>0){weekData[idx]++;monthData[Math.floor(today.getDate()/7)]++;yearData[today.getMonth()]++;}
  else if(n<0){
    if(weekData[idx]>0)weekData[idx]--;
    const w=Math.floor(today.getDate()/7); if(monthData[w]>0)monthData[w]--; if(yearData[today.getMonth()]>0)yearData[today.getMonth()]--;
  }
  drawChart(); saveData();
}

function addStat(k,n){
  if(k==='received'){tRv=Math.max(0,tRv+n);$('tR').textContent=tRv;rTv_today=Math.max(0,rTv_today+n);$('rT_today').textContent=rTv_today;}
  else if(k==='received_today'){tRv=Math.max(0,tRv+n);rTv_today=Math.max(0,rTv_today+n);$('tR').textContent=tRv;$('rT_today').textContent=rTv_today;}
  else if(k==='refurbished'){tFv=Math.max(0,tFv+n);$('tF').textContent=tFv;}
  else if(k==='refurbished_today'){fTv_today=Math.max(0,fTv_today+n);tFv=Math.max(0,tFv+n);$('tF').textContent=tFv;$('fT').textContent=fTv_today;}
  else if(k==='partners'){tPv=Math.max(0,tPv+n);$('tP').textContent=tPv;}
  else if(k==='partners_today'){pTv_today=Math.max(0,pTv_today+n);tPv=Math.max(0,tPv+n);$('tP').textContent=tPv;$('pT').textContent=pTv_today;}
  else if(k==='questions'){tQv=Math.max(0,tQv+n);$('tQ').textContent=tQv;}
  else if(k==='questions_today'){qTv_today=Math.max(0,qTv_today+n);tQv=Math.max(0,tQv+n);$('tQ').textContent=tQv;$('qT').textContent=qTv_today;}

  if(k.includes('refurbished')||k==='refurbished_today'){
    const today=new Date(); const idx=today.getDay()===0?6:today.getDay()-1;
    weekData[idx]+=n; monthData[Math.floor(today.getDate()/7)]+=n; yearData[today.getMonth()]+=n; drawChart();
  }
  upCO2();
  bump(k.includes('today')?k.replace('_today','T'):'t'+k[0].toUpperCase()+k.slice(1));
  saveData();
}

function upCO2(){
  cTv_today = fTv_today * 250;
  $('tC').textContent = (tFv * 250).toLocaleString('nl-NL') + ' kg';
  $('cT').textContent = cTv_today.toLocaleString('nl-NL') + ' kg';
}

function bump(id){const el=$(id);if(el){el.classList.add('bump');setTimeout(()=>el.classList.remove('bump'),250);}}
function floatEmoji(el,em){if(!el)return;const e=document.createElement('div');e.textContent=em;e.style.cssText='position:absolute;font-size:1.6rem;pointer-events:none;z-index:999;animation:float-up 1.3s ease-out forwards';el.style.position='relative';el.appendChild(e);setTimeout(()=>e.remove(),1300);}

function saveData(){try{localStorage.setItem('ictData2',JSON.stringify({V,tRv,tFv,tPv,tQv,rTv_today,fTv_today,pTv_today,qTv_today,stagaires,weekData,monthData,yearData}));}catch(e){}}
function loadData(){try{const d=JSON.parse(localStorage.getItem('ictData2')||'{}');if(d.V!==undefined)V=d.V;if(d.tRv!==undefined)tRv=d.tRv;if(d.tFv!==undefined)tFv=d.tFv;if(d.tPv!==undefined)tPv=d.tPv;if(d.tQv!==undefined)tQv=d.tQv;if(d.rTv_today!==undefined)rTv_today=d.rTv_today;if(d.fTv_today!==undefined)fTv_today=d.fTv_today;if(d.pTv_today!==undefined)pTv_today=d.pTv_today;if(d.qTv_today!==undefined)qTv_today=d.qTv_today;if(d.stagaires)stagaires=d.stagaires;if(d.weekData)weekData=d.weekData;if(d.monthData)monthData=d.monthData;if(d.yearData)yearData=d.yearData;}catch(e){}}
function saveStagaireNames(){const names={};for(let i=1;i<=8;i++){names[`s${i}`]=$(`s${i}-name`).value||'';}localStorage.setItem('stagaireNames',JSON.stringify(names));}
function loadStagaireNames(){const names=JSON.parse(localStorage.getItem('stagaireNames')||'{}');for(let i=1;i<=8;i++){const input=$(`s${i}-name`);if(input&&names[`s${i}`])input.value=names[`s${i}`];}}

// Backspace fix
document.addEventListener('keydown',e=>{
  if(e.key==='f'||e.key==='F'){e.preventDefault();document.fullscreenElement?document.exitFullscreen():document.documentElement.requestFullscreen();return;}
  if(e.key==='Backspace'){
    if(document.activeElement.tagName==='INPUT' && document.activeElement.classList.contains('stag-name-input')) return;
    e.preventDefault();
    if(focus==='vn') addV(-1);
    else if(focus) addStat(focus,-1);
  }
});

// INIT
updateClock();
createStagaireCards();
loadData();
loadStagaireNames();
checkDayReset();

$('vn').textContent = V;
$('pf').style.width = Math.min(V/VG*100,100)+'%';
$('tR').textContent = tRv;
$('tF').textContent = tFv;
$('tP').textContent = tPv;
$('tQ').textContent = tQv;
$('rT_today').textContent = rTv_today;
$('fT').textContent = fTv_today;
$('pT').textContent = pTv_today;
$('qT').textContent = qTv_today;
upCO2();
updateStagaireCounts();

$('vn').addEventListener('click',()=>focus='vn');

requestAnimationFrame(()=>requestAnimationFrame(drawChart));
window.addEventListener('resize',drawChart);
setInterval(checkDayReset, 60000);
</script>
</body>
</html>

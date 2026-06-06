[listagem-mercadinho_4.html](https://github.com/user-attachments/files/28668173/listagem-mercadinho_4.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>ListaMercado</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

:root {
  --bg:       #f0f2f0;
  --surface:  #ffffff;
  --surface2: #f7f8f7;
  --bdr:      #dde3dd;
  --bdr2:     #c8d0c8;
  --green:    #2e7d32;
  --green-lt: #e8f5e9;
  --green-md: #4caf50;
  --green-btn:#388e3c;
  --text:     #1a1a1a;
  --text2:    #444;
  --muted:    #777;
  --faint:    #aaa;
  --red:      #c62828;
  --red-lt:   #ffebee;
  --yellow:   #f57f17;
  --yel-lt:   #fff8e1;
  --viena:    #6a1b9a;
  --mirella:  #bf360c;
  --montana:  #01579b;
  --flash:    #2e7d32;
  --viena-lt:   #f3e5f5;
  --mirella-lt: #fbe9e7;
  --montana-lt: #e1f5fe;
  --flash-lt:   #e8f5e9;
  --radius:   8px;
  --shadow:   0 1px 3px rgba(0,0,0,.10), 0 1px 2px rgba(0,0,0,.06);
  --shadow-md:0 4px 6px rgba(0,0,0,.07), 0 2px 4px rgba(0,0,0,.05);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { -webkit-text-size-adjust: 100%; }

body {
  font-family: 'Inter', system-ui, sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  max-width: 600px;
  margin: 0 auto;
  font-size: 14px;
  line-height: 1.4;
}

/* SYNC INDICATOR */
.sync-bar {
  height: 3px;
  background: var(--green-lt);
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 200;
  transition: background .3s;
}
.sync-bar.syncing { background: var(--green-md); animation: syncpulse 1s infinite; }
.sync-bar.error   { background: var(--red); }
@keyframes syncpulse { 0%,100%{opacity:1} 50%{opacity:.4} }

.sync-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: var(--green-md);
  display: inline-block;
  margin-left: 6px;
  vertical-align: middle;
}
.sync-dot.offline { background: var(--red); }
.sync-dot.syncing { background: var(--yellow); animation: syncpulse .8s infinite; }

/* HEADER */
.hdr {
  background: var(--green);
  padding: 14px 14px 11px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 3px;
  z-index: 50;
  box-shadow: var(--shadow-md);
}
.logo {
  font-size: 17px;
  font-weight: 700;
  color: #fff;
  display: flex;
  align-items: center;
  gap: 7px;
}
.wk {
  font-size: 11px;
  font-weight: 500;
  color: rgba(255,255,255,.75);
  background: rgba(255,255,255,.15);
  border-radius: 20px;
  padding: 3px 9px;
  display: flex;
  align-items: center;
  gap: 4px;
}

/* TABS */
.tabs {
  background: var(--surface);
  border-bottom: 1px solid var(--bdr);
  display: flex;
  overflow-x: auto;
  scrollbar-width: none;
  position: sticky;
  top: 52px;
  z-index: 40;
}
.tabs::-webkit-scrollbar { display: none; }
.tab {
  flex-shrink: 0;
  padding: 10px 14px;
  font-size: 13px;
  font-weight: 600;
  color: var(--muted);
  cursor: pointer;
  border-bottom: 2px solid transparent;
  white-space: nowrap;
  transition: color .15s, border-color .15s;
  user-select: none;
  display: flex;
  align-items: center;
  gap: 5px;
}
.tab:hover { color: var(--text2); }
.tab.active { color: var(--green); border-bottom-color: var(--green); }
.tab[data-l="viena"].active   { color: var(--viena);   border-bottom-color: var(--viena); }
.tab[data-l="mirella"].active { color: var(--mirella); border-bottom-color: var(--mirella); }
.tab[data-l="montana"].active { color: var(--montana); border-bottom-color: var(--montana); }
.tab[data-l="flash"].active   { color: var(--flash);   border-bottom-color: var(--flash); }
.tab[data-l="cons"].active    { color: var(--green);   border-bottom-color: var(--green); }
.tab[data-l="check"].active   { color: var(--yellow);  border-bottom-color: var(--yellow); }

.badge {
  font-size: 10px; font-weight: 700;
  background: var(--bdr); color: var(--muted);
  border-radius: 10px; padding: 1px 5px;
  min-width: 18px; text-align: center;
}
.tab.active .badge { background: var(--green-lt); color: var(--green); }
.tab[data-l="viena"].active .badge   { background: var(--viena-lt);   color: var(--viena); }
.tab[data-l="mirella"].active .badge { background: var(--mirella-lt); color: var(--mirella); }
.tab[data-l="montana"].active .badge { background: var(--montana-lt); color: var(--montana); }
.tab[data-l="flash"].active .badge   { background: var(--flash-lt);   color: var(--flash); }

/* MAIN */
.main { padding: 12px; }

/* INPUT SECTION */
.inp-box {
  background: var(--surface);
  border: 1px solid var(--bdr);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  margin-bottom: 10px;
  overflow: hidden;
}
.inp-top-bar { height: 4px; }
.inp-body { padding: 12px; }
.inp-label {
  font-size: 11px; font-weight: 700;
  letter-spacing: .6px; text-transform: uppercase;
  color: var(--muted); margin-bottom: 8px;
}
textarea.chat {
  width: 100%;
  background: var(--surface2);
  border: 1px solid var(--bdr);
  border-radius: 6px;
  padding: 9px 10px;
  color: var(--text);
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 14px; resize: none; min-height: 72px;
  outline: none; line-height: 1.5;
  transition: border-color .15s, box-shadow .15s;
}
textarea.chat:focus { border-color: var(--green-md); box-shadow: 0 0 0 3px rgba(76,175,80,.12); }
textarea.chat::placeholder { color: var(--faint); }
.hint { font-size: 11.5px; color: var(--muted); margin-top: 6px; line-height: 1.4; }
.hint b { color: var(--green); }

.btn-row { display: flex; gap: 6px; margin-top: 10px; }
.btn {
  display: flex; align-items: center; justify-content: center; gap: 5px;
  padding: 9px 14px; border-radius: 6px; border: none;
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 13px; font-weight: 600;
  cursor: pointer; transition: filter .12s, transform .1s;
}
.btn:active { transform: scale(.97); }
.btn-primary { flex: 1; background: var(--green-btn); color: #fff; }
.btn-primary:hover { filter: brightness(1.08); }

/* SECTION TITLE */
.sec-title {
  font-size: 11px; font-weight: 700; letter-spacing: .6px;
  text-transform: uppercase; color: var(--muted);
  margin-bottom: 7px; display: flex; align-items: center; justify-content: space-between;
}
.sec-count {
  background: var(--surface); border: 1px solid var(--bdr);
  border-radius: 6px; padding: 2px 7px; font-size: 11px; font-weight: 600; color: var(--text2);
}

/* ITEM CARD */
.icard {
  display: flex; align-items: center; gap: 10px;
  padding: 10px 12px;
  background: var(--surface); border: 1px solid var(--bdr);
  border-radius: var(--radius); margin-bottom: 5px;
  box-shadow: var(--shadow); animation: fadeIn .18s ease;
}
@keyframes fadeIn { from { opacity:0; transform:translateY(-4px); } to { opacity:1; transform:none; } }
.icat-dot { width: 7px; height: 7px; border-radius: 50%; flex-shrink: 0; }
.iinfo { flex: 1; min-width: 0; }
.iname { font-size: 14px; font-weight: 500; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.icat-label { font-size: 11px; color: var(--muted); margin-top: 1px; }
.iqty-wrap { text-align: right; flex-shrink: 0; }
.iqty { font-size: 17px; font-weight: 700; line-height: 1; }
.iunit { font-size: 11px; color: var(--muted); font-weight: 400; }
.btn-rm {
  width: 28px; height: 28px; border-radius: 6px;
  border: 1px solid var(--bdr); background: var(--surface2);
  color: var(--muted); cursor: pointer;
  display: flex; align-items: center; justify-content: center;
  font-size: 13px; flex-shrink: 0; transition: all .12s;
}
.btn-rm:hover { background: var(--red-lt); color: var(--red); border-color: #ffcdd2; }

.btn-limpar-tudo {
  width: 100%; margin-top: 10px; padding: 11px;
  border-radius: 6px; border: 1.5px dashed #ffcdd2;
  background: var(--red-lt); color: var(--red);
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 13px; font-weight: 600; cursor: pointer; transition: all .15s; text-align: center;
}
.btn-limpar-tudo:hover { background: #ffcdd2; border-color: var(--red); }

/* EMPTY */
.empty { text-align: center; padding: 32px 16px; color: var(--muted); }
.empty-icon { font-size: 32px; margin-bottom: 8px; }
.empty-text { font-size: 13px; line-height: 1.5; }

/* PREVIEW */
.preview-box {
  background: var(--green-lt); border: 1px solid #c8e6c9;
  border-radius: 6px; padding: 10px; margin-top: 10px;
}
.preview-title {
  font-size: 11px; font-weight: 700; letter-spacing: .5px;
  text-transform: uppercase; color: var(--green); margin-bottom: 8px;
}
.preview-item {
  display: flex; align-items: center; padding: 5px 0;
  border-bottom: 1px solid #c8e6c9; gap: 6px; font-size: 13px;
}
.preview-item:last-of-type { border-bottom: none; }
.prev-name { flex: 1; color: var(--text); }
.prev-qty  { font-weight: 700; color: var(--green); }
.prev-unit { color: var(--muted); font-size: 11px; }
.prev-rm {
  width: 20px; height: 20px; border-radius: 4px;
  border: 1px solid #a5d6a7; background: #fff; color: var(--muted);
  cursor: pointer; display: flex; align-items: center; justify-content: center;
  font-size: 11px; transition: all .12s;
}
.prev-rm:hover { background: var(--red-lt); color: var(--red); border-color: #ffcdd2; }
.preview-actions { display: flex; gap: 6px; margin-top: 8px; }
.btn-confirm {
  flex: 1; padding: 8px; background: var(--green-btn); color: #fff;
  border: none; border-radius: 6px;
  font-family: 'Inter', system-ui, sans-serif; font-size: 13px; font-weight: 600;
  cursor: pointer; transition: filter .12s;
}
.btn-confirm:hover { filter: brightness(1.08); }
.btn-cancel {
  padding: 8px 12px; background: var(--surface); color: var(--muted);
  border: 1px solid var(--bdr); border-radius: 6px;
  font-family: 'Inter', system-ui, sans-serif; font-size: 13px; font-weight: 600; cursor: pointer;
}

/* CONSOLIDADO */
.cons-header {
  background: var(--surface); border: 1px solid var(--bdr);
  border-radius: var(--radius); box-shadow: var(--shadow);
  padding: 11px 13px; margin-bottom: 10px;
  display: flex; align-items: center; justify-content: space-between; gap: 10px;
}
.cons-header-title { font-size: 14px; font-weight: 700; color: var(--text); }
.cons-header-sub { font-size: 11.5px; color: var(--muted); margin-top: 2px; }
.btn-atualizar {
  display: flex; align-items: center; gap: 5px;
  padding: 8px 13px; background: var(--green-btn); color: #fff;
  border: none; border-radius: 6px;
  font-family: 'Inter', system-ui, sans-serif; font-size: 13px; font-weight: 600;
  cursor: pointer; flex-shrink: 0; transition: filter .12s, transform .1s;
}
.btn-atualizar:hover { filter: brightness(1.08); }
.btn-atualizar:active { transform: scale(.96); }

.cat-group { margin-bottom: 12px; }
.cat-header {
  display: flex; align-items: center; gap: 6px;
  padding: 6px 0 5px; border-bottom: 1px solid var(--bdr); margin-bottom: 6px;
}
.cat-icon { font-size: 15px; }
.cat-name { font-size: 12px; font-weight: 700; color: var(--text2); flex: 1; text-transform: uppercase; letter-spacing: .4px; }
.cat-count { font-size: 11px; color: var(--muted); background: var(--surface2); border: 1px solid var(--bdr); border-radius: 5px; padding: 1px 6px; }

.citem {
  background: var(--surface); border: 1px solid var(--bdr);
  border-radius: var(--radius); padding: 9px 12px; margin-bottom: 5px;
  box-shadow: var(--shadow); animation: fadeIn .18s ease;
}
.ctop { display: flex; align-items: center; justify-content: space-between; gap: 8px; margin-bottom: 6px; }
.cname { font-size: 14px; font-weight: 500; flex: 1; }
.ctotal { font-size: 20px; font-weight: 700; color: var(--green); line-height: 1; }
.cunit  { font-size: 11px; color: var(--muted); font-weight: 400; }
.chips  { display: flex; gap: 4px; flex-wrap: wrap; }
.chip { font-size: 11px; font-weight: 600; padding: 2px 7px; border-radius: 4px; border: 1px solid; }
.chip[data-l="viena"]   { color: var(--viena);   border-color: #ce93d8; background: var(--viena-lt); }
.chip[data-l="mirella"] { color: var(--mirella); border-color: #ffab91; background: var(--mirella-lt); }
.chip[data-l="montana"] { color: var(--montana); border-color: #81d4fa; background: var(--montana-lt); }
.chip[data-l="flash"]   { color: var(--flash);   border-color: #a5d6a7; background: var(--flash-lt); }

.exp-bar { display: flex; gap: 6px; margin-top: 12px; padding-top: 12px; border-top: 1px solid var(--bdr); }
.btn-exp {
  flex: 1; padding: 9px; background: var(--surface); color: var(--text2);
  border: 1px solid var(--bdr2); border-radius: 6px;
  font-family: 'Inter', system-ui, sans-serif; font-size: 12.5px; font-weight: 600;
  cursor: pointer; text-align: center; transition: background .12s;
}
.btn-exp:hover { background: var(--surface2); }

/* CHECK MODE */
.check-header {
  background: var(--yel-lt); border: 1px solid #ffe082;
  border-radius: var(--radius); padding: 11px 13px; margin-bottom: 8px;
  display: flex; align-items: center; gap: 10px;
}
.check-header-icon { font-size: 24px; }
.check-header-text strong { display: block; font-size: 14px; font-weight: 700; color: var(--yellow); }
.check-header-text span { font-size: 12px; color: var(--muted); }
.progress-bar { height: 5px; background: var(--bdr); border-radius: 3px; margin-bottom: 10px; overflow: hidden; }
.progress-fill { height: 100%; background: var(--yellow); border-radius: 3px; transition: width .35s ease; }
.check-cat-hdr {
  font-size: 11px; font-weight: 700; letter-spacing: .5px; text-transform: uppercase;
  color: var(--muted); padding: 8px 0 4px; display: flex; align-items: center; gap: 5px;
}
.check-item {
  background: var(--surface); border: 1px solid var(--bdr);
  border-radius: var(--radius); padding: 11px 12px; margin-bottom: 5px;
  display: flex; align-items: center; gap: 11px; cursor: pointer;
  transition: background .15s, border-color .15s;
  user-select: none; -webkit-tap-highlight-color: transparent;
}
.check-item:active { transform: scale(.98); }
.check-item.got { background: var(--green-lt); border-color: #a5d6a7; }
.check-circle {
  width: 24px; height: 24px; border-radius: 50%;
  border: 2px solid var(--bdr2); background: var(--surface2);
  display: flex; align-items: center; justify-content: center;
  font-size: 13px; font-weight: 700; flex-shrink: 0; color: #fff; transition: all .15s;
}
.check-item.got .check-circle { background: var(--green-btn); border-color: var(--green-btn); }
.check-iname { font-size: 14px; font-weight: 500; flex: 1; transition: color .15s; }
.check-item.got .check-iname { text-decoration: line-through; color: var(--muted); }
.check-iqty { font-size: 16px; font-weight: 700; color: var(--yellow); flex-shrink: 0; }
.check-item.got .check-iqty { color: var(--muted); }
.check-iunit { font-size: 11px; color: var(--muted); }
.done-banner {
  background: var(--green-lt); border: 1px solid #a5d6a7;
  border-radius: var(--radius); text-align: center; padding: 20px; margin-top: 8px;
  font-size: 14px; color: var(--green); font-weight: 600;
}
.btn-reset {
  width: 100%; padding: 10px; margin-top: 10px; border-radius: 6px;
  border: 1px dashed var(--bdr2); background: transparent; color: var(--muted);
  font-family: 'Inter', system-ui, sans-serif; font-size: 12.5px; font-weight: 600;
  cursor: pointer; transition: all .12s;
}
.btn-reset:hover { border-color: var(--muted); color: var(--text2); background: var(--surface); }

/* TOAST */
.toast {
  position: fixed; bottom: 20px; left: 50%;
  transform: translateX(-50%) translateY(60px);
  background: var(--text); color: #fff;
  font-size: 13px; font-weight: 600; padding: 10px 18px;
  border-radius: 20px; z-index: 999;
  transition: transform .28s cubic-bezier(.34,1.56,.64,1);
  white-space: nowrap; pointer-events: none; box-shadow: var(--shadow-md);
}
.toast.show { transform: translateX(-50%) translateY(0); }
.toast.ok  { background: var(--green-btn); }
.toast.err { background: var(--red); }

/* LOADER */
.ldover {
  display: none; position: fixed; inset: 0;
  background: rgba(255,255,255,.8); z-index: 100;
  flex-direction: column; align-items: center; justify-content: center; gap: 12px;
}
.ldover.show { display: flex; }
.spinner {
  width: 36px; height: 36px; border: 3px solid var(--bdr);
  border-top-color: var(--green-btn); border-radius: 50%; animation: spin .7s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
.ld-text { font-size: 14px; font-weight: 600; color: var(--text2); }
</style>
</head>
<body>

<div class="sync-bar" id="syncBar"></div>

<div class="hdr">
  <div class="logo">🛒 ListaMercado</div>
  <div class="wk">
    <span id="wkBadge"></span>
    <span class="sync-dot" id="syncDot" title="Status da sincronização"></span>
  </div>
</div>

<div class="tabs">
  <div class="tab active" data-l="viena"   onclick="goTab('viena')">Viena <span class="badge" id="n-viena">0</span></div>
  <div class="tab"        data-l="mirella" onclick="goTab('mirella')">Mirella <span class="badge" id="n-mirella">0</span></div>
  <div class="tab"        data-l="montana" onclick="goTab('montana')">Montana <span class="badge" id="n-montana">0</span></div>
  <div class="tab"        data-l="flash"   onclick="goTab('flash')">Flash <span class="badge" id="n-flash">0</span></div>
  <div class="tab"        data-l="cons"    onclick="goTab('cons')">📦 Consolidado</div>
  <div class="tab"        data-l="check"   onclick="goTab('check')">✅ Compras</div>
</div>

<div class="main" id="main"></div>
<div class="toast" id="toast"></div>
<div class="ldover" id="loader">
  <div class="spinner"></div>
  <div class="ld-text">Carregando...</div>
</div>

<!-- Firebase SDK -->
<script type="module">
import { initializeApp } from 'https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js';
import { getFirestore, doc, onSnapshot, setDoc, getDoc }
  from 'https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js';

// ── FIREBASE CONFIG (suas chaves) ──
const firebaseConfig = {
  apiKey: "AIzaSyBUI2xQyLAPq1xg2JWgA9IMZ3Ht6idyZVo",
  authDomain: "listamercadinho.firebaseapp.com",
  projectId: "listamercadinho",
  storageBucket: "listamercadinho.firebasestorage.app",
  messagingSenderId: "30507783997",
  appId: "1:30507783997:web:9601531157a5b1cfebd754"
};

const fbApp = initializeApp(firebaseConfig);
const db    = getFirestore(fbApp);
const DOC   = doc(db, 'listamercado', 'dados');

// ── CATEGORIAS ──
const CATS = {
  "Bebidas":           { icon:"🥤", cor:"#38bdf8", kw:["refri","refrigerante","suco","agua","água","cerveja","energetico","energético","vinho","achocolatado","nescau","toddy","refresco","isoton","chá","cha","café pronto","bebida","leite","iogurte","yakult"] },
  "Laticínios":        { icon:"🧀", cor:"#fbbf24", kw:["queijo","manteiga","margarina","requeijão","requeijao","creme de leite","leite condensado","catupiry","cream cheese","ricota","muçarela","mussarela","parmesão","parmesao","iogurte","yakult","leite"] },
  "Padaria / Cereais": { icon:"🍞", cor:"#fb923c", kw:["pão","pao","bolo","biscoito","bolacha","macarrão","macarrao","arroz","feijão","feijao","lentilha","cereal","aveia","granola","farinha","tapioca","cuscuz","milho","polenta","massa","lasanha","espaguete"] },
  "Carnes e Proteínas":{ icon:"🥩", cor:"#f87171", kw:["carne","frango","peixe","atum","sardinha","salsicha","linguiça","linguica","presunto","peito de peru","bacon","mortadela","hamburguer","hamburger","filé","file","picanha","costela","camarão","ovo","ovos"] },
  "Hortifruti":        { icon:"🥦", cor:"#4ade80", kw:["alface","tomate","cebola","alho","batata","cenoura","pepino","abobrinha","brocolis","brócolis","couve","banana","maçã","maca","laranja","uva","morango","abacate","limão","limao","fruta","legume","verdura"] },
  "Congelados":        { icon:"❄️", cor:"#a78bfa", kw:["congelado","sorvete","pizza pronta","nugget","batata frita","empanado","lasanha congelada"] },
  "Limpeza":           { icon:"🧹", cor:"#e879f9", kw:["detergente","sabão","sabao","amaciante","desinfetante","alvejante","limpador","multiuso","esponja","papel toalha","papel higiênico","papel higienico","guardanapo","saco de lixo","vassoura","candida","veja","omo","ariel"] },
  "Higiene":           { icon:"🧴", cor:"#67e8f9", kw:["shampoo","condicionador","sabonete","creme dental","pasta de dente","fio dental","desodorante","absorvente","fralda","cotonete","algodão","alcool","álcool","gel alcool","lenço","curativo","band-aid"] },
  "Snacks e Doces":    { icon:"🍫", cor:"#fcd34d", kw:["chocolate","chips","salgadinho","pipoca","bala","chiclete","pirulito","amendoim","castanha","nozes","barrinha","doce","paçoca","pacoca","cocada","wafer","trident"] },
  "Mercearia":         { icon:"🏪", cor:"#94a3b8", kw:["azeite","oleo","óleo","vinagre","sal","açúcar","acucar","ketchup","mostarda","maionese","molho","pimenta","tempero","caldo","extrato de tomate","shoyu","fermento","canela","orégano","oregano","café","cafe","mel","farofa","geleia"] },
};
function getCat(nome) {
  const l = nome.toLowerCase();
  for (const [cat, d] of Object.entries(CATS)) {
    if (d.kw.some(k => l.includes(k))) return cat;
  }
  return "Mercearia";
}

// ── PARSER ──
const UNITS = ["kg","g","ml","l","lt","cx","pct","dz","un","gr","grama","gramas","lata","pacote","caixa","duzia","garrafa","litro","litros"];
function parseQty(t) { return parseFloat(t.replace(',','.')) || 0; }
function parseUnit(t) {
  const l = t.toLowerCase().replace('.','');
  const map = {lt:'L',litro:'L',litros:'L',l:'L',gr:'g',grama:'g',gramas:'g',pacote:'pct',caixa:'cx',duzia:'dz',garrafa:'un',lata:'un'};
  return map[l] || (UNITS.includes(l) ? l : null);
}
function capitalize(s) { return s.charAt(0).toUpperCase() + s.slice(1).toLowerCase(); }
function normalizeName(raw) {
  return raw.replace(/\b(\d+[,.]?\d*)\s*(kg|g|ml|l|lt|un|cx|pct|dz|gr|lata|pacote|caixa|garrafa|litro|litros)?\b/gi,'')
    .replace(/\s{2,}/g,' ').trim().split(' ').filter(Boolean).map(w=>capitalize(w)).join(' ');
}
function parseList(text) {
  const results = [];
  const chunks = text.split(/[,;\n]+/).map(c=>c.trim()).filter(Boolean);
  for (const chunk of chunks) {
    const tokens = chunk.trim().split(/\s+/);
    let qty=1, unit='un', nameParts=[], i=0;
    if (tokens[0] && /^\d+[,.]?\d*$/.test(tokens[0])) {
      qty = parseQty(tokens[0]); i=1;
      if (tokens[1]) { const u=parseUnit(tokens[1]); if(u){unit=u;i=2;} }
      nameParts = tokens.slice(i);
    } else {
      let qtyIdx=-1;
      for (let j=tokens.length-1;j>=0;j--) { if(/^\d+[,.]?\d*$/.test(tokens[j])){qtyIdx=j;break;} }
      if (qtyIdx>=0) {
        qty=parseQty(tokens[qtyIdx]);
        let afterIdx=qtyIdx+1;
        if(tokens[afterIdx]){const u=parseUnit(tokens[afterIdx]);if(u){unit=u;afterIdx++;}}
        const stuck=tokens[qtyIdx].match(/^(\d+[,.]?\d*)(kg|g|ml|l|lt|un|cx|pct|gr)$/i);
        if(stuck){qty=parseQty(stuck[1]);unit=parseUnit(stuck[2])||stuck[2];}
        nameParts=[...tokens.slice(0,qtyIdx),...tokens.slice(afterIdx)];
      } else {
        const si=tokens.findIndex(t=>/^\d+[,.]?\d*(kg|g|ml|l|lt|un|cx|pct|gr)$/i.test(t));
        if(si>=0){const stuck=tokens[si].match(/^(\d+[,.]?\d*)(kg|g|ml|l|lt|un|cx|pct|gr)$/i);qty=parseQty(stuck[1]);unit=parseUnit(stuck[2])||stuck[2];nameParts=tokens.filter((_,j)=>j!==si);}
        else{nameParts=tokens;}
      }
    }
    const rawName=nameParts.join(' ').replace(/^\-+|\-+$/g,'').trim();
    if(!rawName||rawName.length<2) continue;
    const nome=normalizeName(rawName)||capitalize(rawName);
    if(!nome||nome.length<2) continue;
    results.push({nome,qtd:qty||1,unidade:unit});
  }
  return results;
}

// ── CONSOLIDAÇÃO ──
function consolidarLocalmente() {
  const todos=[];
  LOJAS.forEach(loja=>{ estado[loja].forEach(item=>todos.push({...item,loja})); });
  if(!todos.length) return [];
  const grupos={};
  todos.forEach(item=>{
    const key=item.nome.toLowerCase().replace(/\s+/g,' ').trim()+'|'+item.unidade;
    if(!grupos[key]){grupos[key]={nome:item.nome,categoria:item.categoria||getCat(item.nome),unidade:item.unidade,total:0,lojas:{viena:0,mirella:0,montana:0,flash:0}};}
    grupos[key].total+=item.qtd;
    grupos[key].lojas[item.loja]=(grupos[key].lojas[item.loja]||0)+item.qtd;
  });
  return Object.values(grupos).sort((a,b)=>a.nome.localeCompare(b.nome));
}

// ── ESTADO ──
const LOJAS=['viena','mirella','montana','flash'];
const LNOMES={viena:'Viena',mirella:'Mirella',montana:'Montana',flash:'Flash'};
const LCORES={viena:'var(--viena)',mirella:'var(--mirella)',montana:'var(--montana)',flash:'var(--flash)'};

let estado={viena:[],mirella:[],montana:[],flash:[]};
let aba='viena';
let consolidado=[];
let checklist={};
let previewItems=[];
let draftTexts={viena:'',mirella:'',montana:'',flash:''};
let isSaving=false;
let unsubscribe=null;

// ── SYNC STATUS ──
function setSyncStatus(status) {
  const bar=document.getElementById('syncBar');
  const dot=document.getElementById('syncDot');
  if(!bar||!dot) return;
  bar.className='sync-bar '+(status==='syncing'?'syncing':status==='error'?'error':'');
  dot.className='sync-dot '+(status==='syncing'?'syncing':status==='error'?'offline':'');
  dot.title=status==='ok'?'Sincronizado':status==='syncing'?'Sincronizando...':'Sem conexão';
}

// ── FIREBASE SAVE ──
async function salvar() {
  if(isSaving) return;
  isSaving=true;
  setSyncStatus('syncing');
  try {
    await setDoc(DOC, { estado, consolidado, checklist, draftTexts, updatedAt: Date.now() });
    setSyncStatus('ok');
  } catch(e) {
    console.error('Erro ao salvar:', e);
    setSyncStatus('error');
    // fallback localStorage
    try { localStorage.setItem('lm4_backup', JSON.stringify({estado,consolidado,checklist,draftTexts})); } catch(_){}
  } finally {
    isSaving=false;
  }
}

// ── FIREBASE LISTEN (tempo real) ──
function iniciarSync() {
  setSyncStatus('syncing');
  showLoader(true);
  unsubscribe = onSnapshot(DOC, (snap) => {
    showLoader(false);
    if (snap.exists()) {
      const d = snap.data();
      LOJAS.forEach(l => {
        if (Array.isArray(d.estado?.[l])) estado[l] = d.estado[l];
        if (typeof d.draftTexts?.[l] === 'string') draftTexts[l] = d.draftTexts[l];
      });
      if (Array.isArray(d.consolidado)) consolidado = d.consolidado;
      if (d.checklist && typeof d.checklist === 'object') checklist = d.checklist;
    }
    setSyncStatus('ok');
    updateBadges();
    render();
  }, (error) => {
    console.error('Sync error:', error);
    setSyncStatus('error');
    showLoader(false);
    showToast('Erro de conexão — usando dados locais', true);
    // fallback
    try {
      const s = localStorage.getItem('lm4_backup');
      if (s) {
        const d = JSON.parse(s);
        LOJAS.forEach(l => {
          if (Array.isArray(d.estado?.[l])) estado[l] = d.estado[l];
          if (typeof d.draftTexts?.[l] === 'string') draftTexts[l] = d.draftTexts[l];
        });
        if (Array.isArray(d.consolidado)) consolidado = d.consolidado;
        if (d.checklist) checklist = d.checklist;
      }
    } catch(_) {}
    updateBadges();
    render();
  });
}

// ── TABS ──
function goTab(l) {
  if (LOJAS.includes(aba)) {
    const el=document.getElementById('chatInput');
    if(el){draftTexts[aba]=el.value;}
  }
  if (previewItems.length && LOJAS.includes(aba)) autoConfirmarPreview(aba);
  else if (LOJAS.includes(aba) && draftTexts[aba] !== (document.getElementById('chatInput')?.value||'')) salvar();
  aba=l;
  document.querySelectorAll('.tab').forEach(t=>t.classList.toggle('active',t.dataset.l===l));
  render();
}
function autoConfirmarPreview(loja) {
  previewItems.forEach(item=>{
    const idx=estado[loja].findIndex(e=>e.nome.toLowerCase().trim()===item.nome.toLowerCase().trim()&&e.unidade===item.unidade);
    if(idx>=0){estado[loja][idx].qtd+=item.qtd;}else{estado[loja].push({...item});}
  });
  previewItems=[];
  salvar();
  updateBadges();
}
function updateBadges() {
  LOJAS.forEach(l=>{const el=document.getElementById('n-'+l);if(el)el.textContent=estado[l].length;});
}

// ── RENDER ──
function render() {
  const m=document.getElementById('main');
  if(!m) return;
  if(aba==='cons'){renderCons(m);return;}
  if(aba==='check'){renderCheck(m);return;}
  renderLoja(m,aba);
}

function renderLoja(m,loja) {
  const items=estado[loja];
  const cor=LCORES[loja];
  let html=`
  <div class="inp-box">
    <div class="inp-top-bar" style="background:${cor}"></div>
    <div class="inp-body">
      <div class="inp-label">📝 Adicionar à lista — ${LNOMES[loja]}</div>
      <textarea class="chat" id="chatInput"
        placeholder="Ex: macarrão 3, arroz 2kg, refri 2L 6, feijão 1..."
        rows="3" onkeydown="handleKey(event)" oninput="saveDraft('${loja}')"></textarea>
      <div class="hint">Separe por vírgula. <b>Pode escrever do jeito que quiser!</b></div>
      <div class="btn-row">
        <button class="btn btn-primary" onclick="processarInput()">+ Adicionar à Lista</button>
      </div>
      ${previewItems.length?renderPreview(loja):''}
    </div>
  </div>
  <div class="sec-title">Itens da lista <span class="sec-count">${items.length} produto${items.length!==1?'s':''}</span></div>
  <div id="itemsList">
    ${items.length===0?`<div class="empty"><div class="empty-icon">📋</div><div class="empty-text">Nenhum item ainda.<br>Use o campo acima para adicionar produtos.</div></div>`
    :items.map((item,i)=>{
      const cat=CATS[item.categoria]||CATS['Mercearia'];
      return `<div class="icard">
        <div class="icat-dot" style="background:${cat.cor}"></div>
        <div class="iinfo"><div class="iname">${item.nome}</div><div class="icat-label">${cat.icon} ${item.categoria}</div></div>
        <div class="iqty-wrap"><div class="iqty" style="color:${cor}">${item.qtd}<span class="iunit"> ${item.unidade||'un'}</span></div></div>
        <button class="btn-rm" onclick="remItem('${loja}',${i})">✕</button>
      </div>`;
    }).join('')}
  </div>
  ${items.length>0?`<button class="btn-limpar-tudo" onclick="limparLoja('${loja}')">🗑 Limpar lista toda (${items.length} ${items.length===1?'item':'itens'})</button>`:''}`;

  m.innerHTML=html;
  const ta=document.getElementById('chatInput');
  if(ta&&draftTexts[loja]) ta.value=draftTexts[loja];
  if(previewItems.length) bindPreviewRm();
}

function renderPreview(loja) {
  return `<div class="preview-box">
    <div class="preview-title">✓ Confirmar itens interpretados</div>
    ${previewItems.map((it,i)=>`
    <div class="preview-item" id="prev-${i}">
      <span class="prev-name">${it.nome}</span>
      <span class="prev-qty">${it.qtd}</span>
      <span class="prev-unit">${it.unidade}</span>
      <button class="prev-rm" data-i="${i}">✕</button>
    </div>`).join('')}
    <div class="preview-actions">
      <button class="btn-confirm" onclick="confirmarPreview('${loja}')">✓ Confirmar todos</button>
      <button class="btn-cancel" onclick="cancelarPreview()">Cancelar</button>
    </div>
  </div>`;
}
function bindPreviewRm() {
  document.querySelectorAll('.prev-rm').forEach(btn=>{
    btn.onclick=()=>{previewItems.splice(parseInt(btn.dataset.i),1);render();};
  });
}

function renderCons(m) {
  const total=LOJAS.reduce((a,l)=>a+estado[l].length,0);
  const nLojas=LOJAS.filter(l=>estado[l].length>0).length;
  let html=`<div class="cons-header">
    <div><div class="cons-header-title">📦 Lista Consolidada</div><div class="cons-header-sub">${nLojas} loja(s) · ${total} itens cadastrados</div></div>
    <button class="btn-atualizar" onclick="gerarConsolidado()">↻ Atualizar</button>
  </div>`;
  if(!consolidado.length&&total===0){m.innerHTML=html+`<div class="empty"><div class="empty-icon">📦</div><div class="empty-text">Adicione itens nas lojas primeiro,<br>depois clique em Atualizar.</div></div>`;return;}
  if(!consolidado.length&&total>0){m.innerHTML=html+`<div class="empty"><div class="empty-icon">⚡</div><div class="empty-text">Clique em <b>Atualizar</b> para gerar<br>a lista consolidada.</div></div>`;return;}
  const byCat={};
  consolidado.forEach(it=>{if(!byCat[it.categoria])byCat[it.categoria]=[];byCat[it.categoria].push(it);});
  const catOrder=Object.keys(CATS);
  const cats=Object.keys(byCat).sort((a,b)=>(catOrder.indexOf(a)||99)-(catOrder.indexOf(b)||99));
  cats.forEach(cat=>{
    const cd=CATS[cat]||{icon:'🏪'};
    const items=byCat[cat];
    html+=`<div class="cat-group"><div class="cat-header"><div class="cat-icon">${cd.icon}</div><div class="cat-name">${cat}</div><div class="cat-count">${items.length} item${items.length!==1?'s':''}</div></div>
    ${items.map(it=>`<div class="citem"><div class="ctop"><div class="cname">${it.nome}</div><div><span class="ctotal">${it.total}</span><span class="cunit"> ${it.unidade}</span></div></div>
    <div class="chips">${LOJAS.filter(l=>it.lojas[l]>0).map(l=>`<div class="chip" data-l="${l}">${LNOMES[l]}: ${it.lojas[l]}</div>`).join('')}</div></div>`).join('')}</div>`;
  });
  html+=`<div class="exp-bar"><button class="btn-exp" onclick="copiarLista()">📋 Copiar</button><button class="btn-exp" onclick="abrirWhatsApp()">📱 WhatsApp</button></div>`;
  m.innerHTML=html;
}

function renderCheck(m) {
  if(!consolidado.length){m.innerHTML=`<div class="empty"><div class="empty-icon">🛒</div><div class="empty-text">Gere a lista consolidada primeiro<br>para usar o modo de compras.</div></div>`;return;}
  const total=consolidado.length;
  const done=consolidado.filter((_,i)=>checklist[i]).length;
  const pct=total?Math.round(done/total*100):0;
  const byCat={};
  consolidado.forEach((it,i)=>{if(!byCat[it.categoria])byCat[it.categoria]=[];byCat[it.categoria].push({...it,idx:i});});
  const catOrder=Object.keys(CATS);
  const cats=Object.keys(byCat).sort((a,b)=>(catOrder.indexOf(a)||99)-(catOrder.indexOf(b)||99));
  let html=`<div class="check-header"><div class="check-header-icon">🛒</div>
    <div class="check-header-text"><strong>Modo Compras</strong><span>Toque para marcar · ${done}/${total} (${pct}%)</span></div></div>
  <div class="progress-bar"><div class="progress-fill" style="width:${pct}%"></div></div>`;
  cats.forEach(cat=>{
    const cd=CATS[cat]||{icon:'🏪'};
    html+=`<div class="check-cat-hdr">${cd.icon} ${cat}</div>`;
    byCat[cat].forEach(it=>{
      const got=!!checklist[it.idx];
      html+=`<div class="check-item ${got?'got':''}" onclick="toggleCheck(${it.idx})">
        <div class="check-circle">${got?'✓':''}</div>
        <div class="check-iname">${it.nome}</div>
        <div><span class="check-iqty">${it.total}</span><span class="check-iunit"> ${it.unidade}</span></div>
      </div>`;
    });
  });
  if(done===total&&total>0) html+=`<div class="done-banner">🎉 Tudo comprado! Parabéns!</div>`;
  html+=`<button class="btn-reset" onclick="resetCheck()">↺ Reiniciar marcações</button>`;
  m.innerHTML=html;
}

// ── AÇÕES ──
function saveDraft(loja) {
  const el=document.getElementById('chatInput');
  if(el){draftTexts[loja]=el.value;}
}
function handleKey(e) { if(e.key==='Enter'&&(e.ctrlKey||e.metaKey)) processarInput(); }

function processarInput() {
  const el=document.getElementById('chatInput');
  if(!el) return;
  const txt=el.value.trim();
  if(!txt){showToast('Digite algo primeiro.',true);return;}
  const parsed=parseList(txt);
  if(!parsed.length){showToast('Não entendi a lista. Tente novamente.',true);return;}
  parsed.forEach(it=>{it.categoria=getCat(it.nome);});
  previewItems=parsed;
  render();
  setTimeout(()=>{const pb=document.querySelector('.preview-box');if(pb)pb.scrollIntoView({behavior:'smooth',block:'nearest'});},80);
}

function confirmarPreview(loja) {
  if(!previewItems.length) return;
  let novos=0,atualizados=0;
  previewItems.forEach(item=>{
    const idx=estado[loja].findIndex(e=>e.nome.toLowerCase().trim()===item.nome.toLowerCase().trim()&&e.unidade===item.unidade);
    if(idx>=0){estado[loja][idx].qtd+=item.qtd;atualizados++;}
    else{estado[loja].push({...item});novos++;}
  });
  previewItems=[];
  draftTexts[loja]='';
  salvar();
  updateBadges();
  render();
  const msg=novos&&atualizados?`✓ ${novos} novo(s) + ${atualizados} atualizado(s)`:novos?`✓ ${novos} item${novos!==1?'s':''} adicionado${novos!==1?'s':''}`:` ✓ ${atualizados} item${atualizados!==1?'s':''} atualizado${atualizados!==1?'s':''}`;
  showToast(msg);
}
function cancelarPreview() {
  previewItems=[];
  render();
  setTimeout(()=>{const el=document.getElementById('chatInput');if(el)el.focus();},50);
}
function remItem(loja,i) { estado[loja].splice(i,1); salvar(); updateBadges(); render(); }
function limparLoja(loja) {
  if(!estado[loja].length) return;
  if(!confirm(`Limpar toda a lista de ${LNOMES[loja]}?`)) return;
  estado[loja]=[];previewItems=[];
  salvar();updateBadges();render();
}
function gerarConsolidado() {
  const total=LOJAS.reduce((a,l)=>a+estado[l].length,0);
  if(!total){showToast('Adicione itens nas lojas primeiro.',true);return;}
  consolidado=consolidarLocalmente();
  checklist={};
  salvar();
  render();
  showToast(`✓ ${consolidado.length} produtos consolidados!`);
}
function toggleCheck(idx) {
  checklist[idx]=!checklist[idx];
  salvar();
  renderCheck(document.getElementById('main'));
}
function resetCheck() { checklist={}; salvar(); renderCheck(document.getElementById('main')); }

// ── EXPORTAR ──
function buildTexto() {
  const byCat={};
  consolidado.forEach(it=>{if(!byCat[it.categoria])byCat[it.categoria]=[];byCat[it.categoria].push(it);});
  const catOrder=Object.keys(CATS);
  const cats=Object.keys(byCat).sort((a,b)=>(catOrder.indexOf(a)||99)-(catOrder.indexOf(b)||99));
  let txt=`📦 LISTA CONSOLIDADA — ${getSemana()}\n\n`;
  cats.forEach(cat=>{
    const cd=CATS[cat]||{icon:'🏪'};
    txt+=`${cd.icon} ${cat.toUpperCase()}\n`;
    byCat[cat].forEach(it=>{
      const bd=LOJAS.filter(l=>it.lojas[l]>0).map(l=>`${LNOMES[l]}:${it.lojas[l]}`).join(' | ');
      txt+=`• ${it.nome} — ${it.total} ${it.unidade}  (${bd})\n`;
    });
    txt+='\n';
  });
  return txt;
}
function copiarLista() {
  navigator.clipboard.writeText(buildTexto()).then(()=>showToast('✓ Lista copiada!')).catch(()=>showToast('Erro ao copiar.',true));
}
function abrirWhatsApp() {
  const byCat={};
  consolidado.forEach(it=>{if(!byCat[it.categoria])byCat[it.categoria]=[];byCat[it.categoria].push(it);});
  const catOrder=Object.keys(CATS);
  const cats=Object.keys(byCat).sort((a,b)=>(catOrder.indexOf(a)||99)-(catOrder.indexOf(b)||99));
  let txt=`📦 *LISTA CONSOLIDADA* — ${getSemana()}\n\n`;
  cats.forEach(cat=>{
    const cd=CATS[cat]||{icon:'🏪'};
    txt+=`${cd.icon} *${cat}*\n`;
    byCat[cat].forEach(it=>{
      const bd=LOJAS.filter(l=>it.lojas[l]>0).map(l=>`${LNOMES[l]}: ${it.lojas[l]}`).join(' · ');
      txt+=`• ${it.nome}: *${it.total} ${it.unidade}*\n  _(${bd})_\n`;
    });
    txt+='\n';
  });
  window.open('https://wa.me/?text='+encodeURIComponent(txt),'_blank');
}

// ── UTILS ──
function getSemana() {
  const now=new Date();
  const jan1=new Date(now.getFullYear(),0,1);
  const wk=Math.ceil((((now-jan1)/86400000)+jan1.getDay()+1)/7);
  return `Semana ${wk}/${now.getFullYear()}`;
}
function showToast(msg,err=false) {
  const t=document.getElementById('toast');
  t.textContent=msg;
  t.className='toast '+(err?'err':'ok');
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2600);
}
function showLoader(show) { document.getElementById('loader').classList.toggle('show',show); }

// Expor funções globalmente (necessário para onclick no HTML)
window.goTab=goTab; window.processarInput=processarInput; window.confirmarPreview=confirmarPreview;
window.cancelarPreview=cancelarPreview; window.remItem=remItem; window.limparLoja=limparLoja;
window.gerarConsolidado=gerarConsolidado; window.toggleCheck=toggleCheck; window.resetCheck=resetCheck;
window.copiarLista=copiarLista; window.abrirWhatsApp=abrirWhatsApp;
window.handleKey=handleKey; window.saveDraft=saveDraft;

// ── INIT ──
document.getElementById('wkBadge').textContent=getSemana();
iniciarSync();
</script>
</body>
</html>

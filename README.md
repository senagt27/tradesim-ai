<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0,viewport-fit=cover"/>
<meta name="theme-color" content="#0F172A"/>
<meta name="mobile-web-app-capable" content="yes"/>
<meta name="apple-mobile-web-app-capable" content="yes"/>
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"/>
<meta name="apple-mobile-web-app-title" content="TradeSim AI"/>
<title>TradeSim AI</title>
<link rel="manifest" href="manifest.json"/>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;600&family=Inter:wght@400;600;700&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
:root{--bg:#F8FAFC;--card:#fff;--border:#E2E8F0;--text:#0F172A;--muted:#64748B;--green:#16A34A;--red:#DC2626;--nav:56px;--tabs:56px;}
html,body{height:100%;overflow:hidden;background:var(--bg);font-family:'Inter',sans-serif;color:var(--text);}
#app{height:100%;display:flex;flex-direction:column;}
.nav{height:var(--nav);display:flex;align-items:center;justify-content:space-between;padding:0 14px;background:var(--card);border-bottom:1px solid var(--border);flex-shrink:0;}
.brand{display:flex;align-items:center;gap:8px;}
.brand-icon{width:28px;height:28px;border-radius:7px;background:#0F172A;color:#fff;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;}
.brand-name{font-weight:700;font-size:15px;}.brand-name span{font-weight:400;color:var(--muted);}
.nav-r{display:flex;align-items:center;gap:6px;}
.ldot{width:7px;height:7px;border-radius:50%;background:var(--green);animation:pulse 2s infinite;}
.ltxt{font-size:10px;font-family:'DM Mono',monospace;color:var(--muted);}
.nbtn{padding:5px 8px;border-radius:7px;border:1.5px solid var(--border);background:var(--card);cursor:pointer;display:flex;align-items:center;gap:4px;font-size:11px;font-family:'DM Mono',monospace;font-weight:700;position:relative;}
.nbtn.on{border-color:#F59E0B;background:#FFFBEB;color:#D97706;}.nbtn.off{color:var(--muted);}
.nping{position:absolute;top:-3px;right:-3px;width:9px;height:9px;border-radius:50%;background:#EF4444;border:2px solid #fff;display:none;}
.nping.show{display:block;animation:ping 1.2s infinite;}
.wbtn{padding:5px 8px;border-radius:7px;border:1.5px solid var(--border);background:var(--card);cursor:pointer;font-size:11px;font-weight:700;font-family:'DM Mono',monospace;color:var(--muted);}
.wbtn.on{border-color:#2563EB;background:#EFF6FF;color:#2563EB;}
.tabs{height:var(--tabs);display:flex;background:var(--card);border-top:1px solid var(--border);flex-shrink:0;}
.tab{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:2px;cursor:pointer;border:none;background:none;color:var(--muted);font-size:10px;font-weight:600;font-family:inherit;}
.tab.active{color:var(--text);}
.ticon{font-size:18px;line-height:1;}
.scroll{flex:1;overflow-y:auto;overflow-x:hidden;-webkit-overflow-scrolling:touch;}
.ibar{background:var(--card);border-bottom:1px solid var(--border);}
.glbl{padding:6px 14px 3px;font-size:9px;font-weight:700;color:#94A3B8;text-transform:uppercase;letter-spacing:.1em;}
.pills{display:flex;gap:6px;padding:3px 14px 8px;overflow-x:auto;scrollbar-width:none;}
.pills::-webkit-scrollbar{display:none;}
.pill{flex-shrink:0;padding:6px 10px;border-radius:8px;border:1.5px solid var(--border);background:var(--card);cursor:pointer;min-width:66px;text-align:center;transition:all .15s;}
.pname{font-weight:700;font-size:11px;white-space:nowrap;}
.pchg{font-family:'DM Mono',monospace;font-size:10px;font-weight:600;margin-top:1px;}
.view{padding:12px 14px;display:flex;flex-direction:column;gap:10px;}
.empty{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:55vh;color:#CBD5E1;gap:8px;}
.ei{font-size:36px;}.et{font-family:'DM Mono',monospace;font-size:12px;text-align:center;line-height:1.6;}
.card{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:12px 14px;}
.clbl{font-size:9px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:.08em;margin-bottom:6px;}
.badge{padding:3px 9px;border-radius:999px;font-family:'DM Mono',monospace;font-size:11px;font-weight:700;display:inline-block;}
.ptag{padding:2px 7px;border-radius:5px;background:#EFF6FF;color:#2563EB;font-family:'DM Mono',monospace;font-size:10px;font-weight:700;}
.confrow{display:flex;align-items:center;gap:8px;}
.confbg{flex:1;height:5px;background:#F1F5F9;border-radius:4px;overflow:hidden;}
.conffill{height:100%;border-radius:4px;transition:width 1.2s ease;}
.confpct{font-family:'DM Mono',monospace;font-size:11px;font-weight:700;min-width:32px;}
.g2{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.pc{padding:10px 12px;border-radius:9px;}
.plbl{font-size:9px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:.07em;margin-bottom:3px;}
.pval{font-family:'DM Mono',monospace;font-size:16px;font-weight:700;}
.punit{font-size:9px;color:#94A3B8;margin-left:3px;}
.igrid{display:grid;grid-template-columns:1fr 1fr;gap:7px;}
.icard{padding:8px 10px;border-radius:8px;background:var(--card);border:1px solid var(--border);}
.iname{font-size:9px;color:#94A3B8;font-weight:600;text-transform:uppercase;letter-spacing:.06em;margin-bottom:2px;}
.ival{font-family:'DM Mono',monospace;font-size:11px;font-weight:700;margin-bottom:2px;}
.iint{font-size:10px;color:var(--muted);line-height:1.3;}
.li{display:flex;gap:5px;font-size:11px;color:#334155;line-height:1.5;margin-bottom:4px;}
.sbar{display:flex;align-items:center;gap:6px;padding:7px 10px;background:#F8FAFC;border:1px solid var(--border);border-radius:8px;flex-wrap:wrap;}
.sdot{width:6px;height:6px;border-radius:50%;flex-shrink:0;}
.stxt{font-family:'DM Mono',monospace;font-size:10px;color:#475569;font-weight:600;flex:1;}
.sbtn{padding:3px 8px;border-radius:5px;border:1.5px solid var(--border);background:var(--card);font-size:10px;font-weight:700;cursor:pointer;font-family:inherit;}
.stabs{display:flex;gap:0;background:#F1F5F9;border-radius:7px;padding:2px;width:fit-content;}
.stab{padding:5px 12px;border-radius:5px;border:none;font-size:11px;font-weight:400;cursor:pointer;background:transparent;color:var(--muted);font-family:inherit;}
.stab.active{background:#fff;color:var(--text);font-weight:700;box-shadow:0 1px 4px rgba(0,0,0,.07);}
.tcard{border-radius:10px;overflow:hidden;border:1px solid var(--border);background:var(--card);}
.thdr{padding:8px 12px;display:flex;justify-content:space-between;align-items:center;}
.tdir{font-family:'DM Mono',monospace;font-weight:800;font-size:11px;letter-spacing:.06em;}
.tsty{padding:2px 7px;border-radius:999px;background:var(--card);color:var(--muted);font-size:9px;font-weight:700;border:1px solid var(--border);}
.tlvls{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px;padding:8px 12px;}
.lvlbl{font-size:9px;font-weight:700;text-transform:uppercase;letter-spacing:.07em;margin-bottom:3px;}
.lvval{font-family:'DM Mono',monospace;font-size:12px;font-weight:700;}
.lvsub{font-family:'DM Mono',monospace;font-size:10px;color:#94A3B8;}
.ctxrow{display:flex;gap:5px;flex-wrap:wrap;padding:0 12px 8px;}
.ctxtag{padding:3px 7px;border-radius:5px;background:#F8FAFC;border:1px solid var(--border);font-size:10px;color:#475569;}
.tnote{padding:0 12px 10px;font-size:10px;color:var(--muted);font-style:italic;line-height:1.4;}
.warn{padding:8px 12px;border-radius:8px;background:#FFFBEB;border:1px solid #FDE68A;display:flex;gap:6px;align-items:flex-start;}
.warntxt{font-size:10px;color:#92400E;line-height:1.5;}
.hrow{display:flex;align-items:center;gap:7px;margin-bottom:5px;}
.hpass{font-family:'DM Mono',monospace;font-size:9px;color:#94A3B8;min-width:22px;}
.rbox{margin-top:8px;padding:7px 10px;border-radius:6px;background:#EFF6FF;border:1px solid #BFDBFE;font-size:10px;color:#334155;}
.rlbl{font-weight:700;color:#2563EB;margin-right:4px;}
.skel{border-radius:8px;background:linear-gradient(90deg,#F1F5F9 25%,#E2E8F0 50%,#F1F5F9 75%);background-size:200% 100%;animation:shimmer 1.4s infinite;}
.chat-w{display:flex;flex-direction:column;height:100%;}
.chat-msgs{flex:1;overflow-y:auto;padding:12px 14px;display:flex;flex-direction:column;gap:8px;-webkit-overflow-scrolling:touch;}
.msg{max-width:88%;padding:8px 12px;font-size:12px;line-height:1.55;}
.msg.user{align-self:flex-end;background:#0F172A;color:#fff;border-radius:14px 14px 4px 14px;}
.msg.ai{align-self:flex-start;background:var(--card);color:#334155;border:1px solid var(--border);border-radius:14px 14px 14px 4px;}
.mlbl{font-size:9px;font-weight:700;color:#94A3B8;text-transform:uppercase;letter-spacing:.08em;margin-bottom:3px;}
.qrow{display:flex;gap:5px;flex-wrap:wrap;padding:6px 14px;}
.qbtn{padding:4px 9px;border-radius:999px;border:1px solid var(--border);background:var(--card);color:#475569;font-size:10px;cursor:pointer;font-family:inherit;}
.cinrow{display:flex;gap:6px;padding:6px 10px 10px;border-top:1px solid var(--border);}
.cinput{flex:1;padding:9px 12px;border-radius:8px;border:1.5px solid var(--border);font-size:13px;color:var(--text);outline:none;font-family:inherit;background:#FAFAFA;}
.csend{padding:9px 14px;border-radius:8px;border:none;font-size:12px;font-weight:700;cursor:pointer;font-family:inherit;}
.widget{position:fixed;bottom:calc(var(--tabs)+10px);right:10px;width:228px;background:rgba(10,15,28,.95);backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);border-radius:14px;border:1px solid rgba(255,255,255,.1);box-shadow:0 10px 36px rgba(0,0,0,.45);z-index:200;display:none;animation:slideUp .2s ease;}
.widget.show{display:block;}
.wdrag{padding:8px 12px;display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid rgba(255,255,255,.07);}
.wtitle{font-family:'DM Mono',monospace;font-size:9px;color:rgba(255,255,255,.5);font-weight:700;letter-spacing:.08em;}
.wclose{background:none;border:none;color:rgba(255,255,255,.4);font-size:13px;cursor:pointer;line-height:1;padding:0 3px;}
.wpair{padding:8px 12px;}
.wpair:not(:last-of-type){border-bottom:1px solid rgba(255,255,255,.05);}
.wphdr{display:flex;justify-content:space-between;align-items:center;margin-bottom:6px;}
.wsym{font-weight:700;font-size:11px;color:#fff;}
.wsig{font-family:'DM Mono',monospace;font-size:9px;font-weight:700;padding:2px 6px;border-radius:999px;}
.wgrid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:5px;}
.wcl{font-size:8px;text-transform:uppercase;letter-spacing:.06em;font-weight:700;margin-bottom:2px;}
.wcv{font-family:'DM Mono',monospace;font-size:11px;font-weight:700;}
.wcs{font-family:'DM Mono',monospace;font-size:9px;opacity:.5;}
.wempty{font-size:10px;color:rgba(255,255,255,.28);text-align:center;padding:8px 0;}
.wselrow{display:flex;gap:5px;padding:6px 12px 10px;border-top:1px solid rgba(255,255,255,.06);}
.wsel{flex:1;padding:5px 7px;border-radius:6px;border:1px solid rgba(255,255,255,.1);background:rgba(255,255,255,.06);color:rgba(255,255,255,.7);font-size:10px;font-family:inherit;}
.toasts{position:fixed;top:calc(var(--nav)+8px);right:10px;z-index:9999;display:flex;flex-direction:column;gap:6px;max-width:calc(100vw - 20px);}
.toast{padding:10px 12px;border-radius:10px;background:#fff;box-shadow:0 4px 20px rgba(0,0,0,.18);animation:slideIn .25s ease;display:flex;gap:8px;align-items:flex-start;max-width:300px;}
.tdot{width:7px;height:7px;border-radius:50%;flex-shrink:0;margin-top:3px;}
.ttitle{font-weight:700;font-size:11px;margin-bottom:2px;}
.tbody{font-size:10px;color:#475569;line-height:1.4;}
.ttime{font-size:9px;color:#94A3B8;font-family:'DM Mono',monospace;margin-top:3px;}
.tx{background:none;border:none;color:#94A3B8;cursor:pointer;font-size:11px;padding:0;line-height:1;flex-shrink:0;}
.dots{display:flex;gap:4px;padding:8px 12px;}
.dot{width:6px;height:6px;border-radius:50%;background:#CBD5E1;animation:bounce .9s infinite;}
.dot:nth-child(2){animation-delay:.15s;}.dot:nth-child(3){animation-delay:.3s;}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.35}}
@keyframes ping{0%,100%{transform:scale(1);opacity:1}50%{transform:scale(1.8);opacity:.4}}
@keyframes shimmer{0%{background-position:200% 0}100%{background-position:-200% 0}}
@keyframes slideIn{from{opacity:0;transform:translateX(10px)}to{opacity:1;transform:translateX(0)}}
@keyframes slideUp{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}
@keyframes bounce{0%,80%,100%{transform:translateY(0)}40%{transform:translateY(-4px)}}
</style>
</head>
<body>
<div id="app">
  <div class="nav">
    <div class="brand"><div class="brand-icon">◈</div><span class="brand-name">TradeSim <span>AI</span></span></div>
    <div class="nav-r">
      <div class="ldot"></div><span class="ltxt">LIVE</span>
      <button class="nbtn off" id="nbtn">🔔 <span id="nlbl">OFF</span><span class="nping" id="nping"></span></button>
      <button class="wbtn" id="wbtn">⊞ WGT</button>
    </div>
  </div>
  <div id="toasts" class="toasts"></div>
  <div class="widget" id="widget">
    <div class="wdrag"><span class="wtitle">◈ TRADESIM WIDGET</span><button class="wclose" id="wclose">✕</button></div>
    <div class="wpair" id="wp0"><div class="wempty">— Select pair in app —</div></div>
    <div class="wpair" id="wp1"><div class="wempty">— Slot 2 below —</div></div>
    <div class="wselrow"><select class="wsel" id="wsel2"><option value="">Slot 2 pair…</option></select></div>
  </div>
  <div class="ibar" id="ibar"></div>
  <div class="scroll" id="scroll">
    <div id="aview"></div>
    <div id="cview" style="display:none"></div>
  </div>
  <div class="tabs">
    <button class="tab active" id="t1" onclick="switchTab('a')"><span class="ticon">📊</span><span>Analysis</span></button>
    <button class="tab" id="t2" onclick="switchTab('c')"><span class="ticon">💬</span><span>Ask AI</span></button>
  </div>
</div>
<script>
'use strict';
var INSTS=[
  {id:'gold',  name:'Gold',    sym:'XAU/USD',unit:'oz',   price:2341.50, chg:+0.82,col:'#B8960C',bg:'#FEFCE8'},
  {id:'silver',name:'Silver',  sym:'XAG/USD',unit:'oz',   price:29.84,   chg:-0.34,col:'#6B7280',bg:'#F9FAFB'},
  {id:'copper',name:'Copper',  sym:'HG1',    unit:'lb',   price:4.523,   chg:+1.21,col:'#B45309',bg:'#FFFBEB'},
  {id:'wti',   name:'WTI',     sym:'CL1',    unit:'bbl',  price:78.42,   chg:-0.67,col:'#1D4ED8',bg:'#EFF6FF'},
  {id:'brent', name:'Brent',   sym:'BRENT',  unit:'bbl',  price:82.17,   chg:-0.51,col:'#2563EB',bg:'#EFF6FF'},
  {id:'natgas',name:'Nat Gas', sym:'NG1',    unit:'MMBtu',price:2.184,   chg:+2.14,col:'#059669',bg:'#ECFDF5'},
  {id:'us30',  name:'US 30',   sym:'DJIA',   unit:'pts',  price:39127.80,chg:+0.43,col:'#7C3AED',bg:'#F5F3FF'},
  {id:'spx',   name:'S&P 500', sym:'SPX',    unit:'pts',  price:5248.49, chg:+0.57,col:'#0E7490',bg:'#ECFEFF'},
];
var GROUPS=[{l:'Metals',ids:['gold','silver','copper']},{l:'Energy',ids:['wti','brent','natgas']},{l:'Indices',ids:['us30','spx']}];
var TFS=['1H','4H','1D','1W'];
var IND={rsi:'RSI(14)',macd:'MACD',bb:'B.Bands',ema:'EMA X',vol:'Vol',obv:'OBV'};
var REFRESH=90000,MAXH=8;

// STATE
var S={sel:null,tf:'1D',tab:'a',sub:'o',nOn:false,wShow:false,w2:null,store:{},tim:{},toasts:[],loading:false,showH:false,chatH:[],chatM:[],chatL:false,tid:0};

function gInst(id){return INSTS.find(function(c){return c.id===id;})||null;}
function fT(ts){return new Date(ts).toLocaleTimeString([],{hour:'2-digit',minute:'2-digit',second:'2-digit'});}
function sCol(s){if(!s)return'#94A3B8';if(s.indexOf('BUY')>=0)return'#16A34A';if(s.indexOf('SELL')>=0)return'#DC2626';return'#D97706';}
function sBg(s){if(!s)return'#F1F5F9';if(s.indexOf('BUY')>=0)return'#DCFCE7';if(s.indexOf('SELL')>=0)return'#FFE4E6';return'#FEF9C3';}
function sTxt(s){if(!s)return'#64748B';if(s.indexOf('BUY')>=0)return'#15803D';if(s.indexOf('SELL')>=0)return'#B91C1C';return'#A16207';}
function sLbl(s){var m={STRONG_BUY:'Strong Buy',BUY:'Buy',HOLD:'Hold',SELL:'Sell',STRONG_SELL:'Strong Sell'};return(m[s]||s||'—');}
function fP(v,u){if(v===undefined||v===null)return'—';var n=+v;if(u==='pts')return n.toLocaleString(undefined,{minimumFractionDigits:2,maximumFractionDigits:2});if(n<10)return n.toFixed(4);return n.toFixed(2);}
function esc(s){var d=document.createElement('div');d.textContent=s||'';return d.innerHTML;}
function gKey(){return S.sel?S.sel+'-'+S.tf:null;}

// API
function doFetch(inst,tf,prev){
  var hasPrev=prev.length>0;
  var pc=hasPrev?'\n\nPREVIOUS:\n'+prev.map(function(a,i){return 'Pass '+(i+1)+': '+a.signal+', '+a.confidence+'%\n'+a.summary;}).join('\n---\n')+'\n\nRefine genuinely. Explain in refinementNote.':'';
  var prompt='Expert trading analyst AI.\nInstrument: '+inst.name+' ('+inst.sym+') | TF: '+tf+' | Price: ~'+inst.price+' '+inst.unit+' | Pass: '+(prev.length+1)+pc+'\n\nReturn ONLY valid JSON, no markdown:\n{"signal":"STRONG_BUY"|"BUY"|"HOLD"|"SELL"|"STRONG_SELL","confidence":<50-97>,"priceTarget":<n>,"stopLoss":<n>,"summary":"<2 sentences>","refinementNote":"'+(hasPrev?'<what changed>':'Initial pass.')+'","catalysts":["<c1>","<c2>","<c3>"],"risks":["<r1>","<r2>"],"indicators":{"rsi":{"value":<0-100>,"interpretation":"<t>"},"macd":{"value":"<t>","interpretation":"<t>"},"bb":{"value":"<t>","interpretation":"<t>"},"ema":{"value":"<t>","interpretation":"<t>"},"vol":{"value":"<t>","interpretation":"<t>"},"obv":{"value":"<t>","interpretation":"<t>"}},"dayTrades":[{"style":"Scalp"|"Day Trade"|"Momentum","direction":"LONG"|"SHORT","entryLow":<n>,"entryHigh":<n>,"stopLoss":<n>,"tp1":<n>,"tp2":<n>,"riskReward":<n>,"volumeContext":"<t>","volatilityContext":"<t>","timingContext":"<t>","note":"<1 sentence>"}]}\nProvide 2-3 dayTrades.';
  return fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1500,messages:[{role:'user',content:prompt}]})})
  .then(function(r){if(!r.ok)throw new Error('HTTP '+r.status);return r.json();})
  .then(function(d){
    var txt=(d.content||[]).map(function(b){return b.text||'';}).join('');
    var clean=txt.replace(/```json|```/g,'').trim();
    var p=JSON.parse(clean);
    p.timestamp=Date.now();p.pass=prev.length+1;
    return p;
  });
}

// LOOP
function runPass(key){
  if(!key||!S.sel)return;
  var ins=gInst(S.sel);if(!ins)return;
  if(!S.store[key])S.store[key]={current:null,history:[],prevSig:null};
  var st=S.store[key];
  S.loading=true;rAnalysis();
  return doFetch(ins,S.tf,st.history).then(function(result){
    var nh=st.history.concat([result]).slice(-MAXH);
    var old=st.prevSig;
    st.current=result;st.history=nh;st.prevSig=result.signal;
    if(old!==null&&old!==result.signal)showToast(ins.name+' changed',sLbl(old)+' → '+sLbl(result.signal)+' · '+result.confidence+'%',sCol(result.signal));
    else if(old===null)showToast(ins.name+' ready',sLbl(result.signal)+' · '+result.confidence+'% · Pass '+result.pass,sCol(result.signal));
    wRenderPair(0);
  }).catch(function(e){console.error(e);}).then(function(){S.loading=false;rAnalysis();});
}

function startLoop(key){
  stopLoop(key);
  if(!S.tim[key])S.tim[key]={};
  var t=S.tim[key];t.cd=REFRESH/1000;t.status='running';
  if(!S.store[key]||!S.store[key].current)runPass(key);
  t.iv=setInterval(function(){if(gKey()===key)runPass(key);},REFRESH);
  t.cdiv=setInterval(function(){t.cd=t.cd<=1?REFRESH/1000:t.cd-1;rStatusBar();},1000);
}
function stopLoop(key){if(!S.tim[key])return;clearInterval(S.tim[key].iv);clearInterval(S.tim[key].cdiv);S.tim[key]={};}
function pauseLoop(key){if(!S.tim[key])return;clearInterval(S.tim[key].iv);clearInterval(S.tim[key].cdiv);S.tim[key].status='paused';rStatusBar();}

// TOASTS
function showToast(title,body,color){
  if(!S.nOn)return;
  var id=++S.tid;S.toasts.push({id:id,title:title,body:body,color:color,ts:Date.now()});
  document.getElementById('nping').classList.add('show');
  rToasts();
  setTimeout(function(){dismissToast(id);},7000);
}
function dismissToast(id){S.toasts=S.toasts.filter(function(t){return t.id!==id;});rToasts();}
function rToasts(){
  document.getElementById('toasts').innerHTML=S.toasts.map(function(t){
    return '<div class="toast" style="border:1.5px solid '+t.color+'33"><div class="tdot" style="background:'+t.color+'"></div><div style="flex:1"><div style="display:flex;justify-content:space-between"><span class="ttitle">'+esc(t.title)+'</span><button class="tx" onclick="dismissToast('+t.id+')">✕</button></div><div class="tbody">'+esc(t.body)+'</div><div class="ttime">'+fT(t.ts)+'</div></div></div>';
  }).join('');
}

// WIDGET
function wRenderPair(idx){
  var pid=idx===0?S.sel:S.w2;
  var ins=pid?gInst(pid):null;
  var key=ins?ins.id+'-'+S.tf:null;
  var a=key&&S.store[key]?S.store[key].current:null;
  var el=document.getElementById('wp'+idx);if(!el)return;
  if(!ins){el.innerHTML='<div class="wempty">— '+(idx===0?'Select in app':'Pick pair below')+' —</div>';return;}
  var tr=a&&a.dayTrades&&a.dayTrades[0]?a.dayTrades[0]:null;
  var sig=a?a.signal:null;
  el.innerHTML='<div class="wphdr"><div><div class="wsym">'+esc(ins.sym)+'</div><div style="font-family:\'DM Mono\',monospace;font-size:9px;color:rgba(255,255,255,.35)">'+fP(ins.price,ins.unit)+' '+ins.unit+'</div></div>'+(sig?'<span class="wsig" style="background:'+(sig.indexOf('BUY')>=0?'rgba(74,222,128,.2)':sig.indexOf('SELL')>=0?'rgba(248,113,113,.2)':'rgba(252,211,77,.2)')+'%;color:'+(sig.indexOf('BUY')>=0?'#4ADE80':sig.indexOf('SELL')>=0?'#F87171':'#FCD34D')+'">'+sLbl(sig)+'</span>':'')+'</div>'+(tr?'<div class="wgrid"><div><div class="wcl" style="color:rgba(255,255,255,.35)">ENTRY</div><div class="wcv" style="color:#fff">'+fP(tr.entryLow,ins.unit)+'</div><div class="wcs">–'+fP(tr.entryHigh,ins.unit)+'</div></div><div><div class="wcl" style="color:rgba(248,113,113,.7)">SL</div><div class="wcv" style="color:#F87171">'+fP(tr.stopLoss,ins.unit)+'</div><div class="wcs">R:R '+tr.riskReward+'</div></div><div><div class="wcl" style="color:rgba(74,222,128,.7)">TP1/2</div><div class="wcv" style="color:#4ADE80">'+fP(tr.tp1,ins.unit)+'</div><div class="wcs" style="color:#86EFAC">'+fP(tr.tp2,ins.unit)+'</div></div></div>':'<div class="wempty">'+(a?'No setup yet':'Analysing…')+'</div>');
}

// RENDER IBAR
function rIbar(){
  document.getElementById('ibar').innerHTML=GROUPS.map(function(g){
    return '<div class="glbl">'+g.l+'</div><div class="pills">'+INSTS.filter(function(c){return g.ids.indexOf(c.id)>=0;}).map(function(c){
      var up=c.chg>=0,sel=S.sel===c.id;
      return '<div class="pill'+(sel?' sel':'')+'" style="border-color:'+(sel?c.col:'#E2E8F0')+';background:'+(sel?c.bg:'#fff')+'" onclick="selInst(\''+c.id+'\')"><div class="pname">'+esc(c.name)+'</div><div class="pchg" style="color:'+(up?'#16A34A':'#DC2626')+'">'+(up?'▲':'▼')+Math.abs(c.chg).toFixed(2)+'%</div></div>';
    }).join('')+'</div>';
  }).join('');
}

// RENDER STATUS BAR
function rStatusBar(){
  var el=document.getElementById('sbar');if(!el)return;
  var key=gKey(),t=key?S.tim[key]:null;
  var status=t&&t.status?t.status:'idle',cd=t&&t.cd?t.cd:0;
  var dc=status==='running'?'#16A34A':status==='paused'?'#D97706':'#94A3B8';
  var da=status==='running'?'animation:pulse 2s infinite':'';
  var hl=(key&&S.store[key]?S.store[key].history.length:0);
  el.innerHTML='<div class="sdot" style="background:'+dc+';'+da+'"></div><span class="stxt">'+(status==='running'?'LIVE · '+cd+'s':status==='paused'?'PAUSED':'IDLE')+(S.loading?' · analysing…':'')+'</span><button class="sbtn" onclick="forceRef()">↻</button>'+(status==='running'?'<button class="sbtn" style="color:#D97706" onclick="doPause()">⏸</button>':'<button class="sbtn" style="color:#16A34A;border-color:#DCFCE7;background:#F0FDF4" onclick="doResume()">▶</button>')+'<button class="sbtn" style="'+(S.showH?'color:#4338CA;border-color:#C7D2FE;background:#EEF2FF':'')+'" onclick="togH()">📜'+hl+'</button>';
}

// RENDER ANALYSIS
function rAnalysis(){
  var v=document.getElementById('aview');
  var ins=gInst(S.sel),key=gKey();
  var st=key?S.store[key]:null,cur=st?st.current:null,hist=st?st.history:[];
  if(!ins){v.innerHTML='<div class="empty"><div class="ei">◈</div><div class="et">Select an instrument above<br>to begin AI analysis</div></div>';return;}
  var ac=cur?sCol(cur.signal):'#94A3B8';
  var h='<div class="view">';
  // Header
  h+='<div style="display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:6px"><div><div style="display:flex;align-items:center;gap:7px;flex-wrap:wrap"><span style="font-weight:700;font-size:18px">'+esc(ins.name)+'</span>'+(cur?'<span class="badge" style="background:'+sBg(cur.signal)+';color:'+sTxt(cur.signal)+'">'+sLbl(cur.signal)+'</span>':'' )+(cur?'<span class="ptag">pass '+cur.pass+'</span>':'')+'</div><div style="font-family:\'DM Mono\',monospace;font-size:10px;color:#94A3B8;margin-top:2px">'+esc(ins.sym)+' · '+fP(ins.price,ins.unit)+' /'+ins.unit+'</div></div><div style="display:flex;gap:5px;flex-wrap:wrap">'+TFS.map(function(t){return'<button onclick="selTf(\''+t+'\')" style="padding:4px 8px;border-radius:6px;border:1.5px solid '+(t===S.tf?ins.col:'#E2E8F0')+';background:'+(t===S.tf?ins.bg:'#fff')+';color:'+(t===S.tf?ins.col:'#64748B')+';font-family:\'DM Mono\',monospace;font-size:10px;font-weight:700;cursor:pointer">'+t+'</button>';}).join('')+'</div></div>';
  h+='<div id="sbar" class="sbar"></div>';
  // History
  if(S.showH&&hist.length>0){
    h+='<div class="card"><div class="clbl">Signal Evolution</div>';
    hist.forEach(function(hh){h+='<div class="hrow"><span class="hpass">#'+hh.pass+'</span><span class="badge" style="font-size:10px;padding:2px 7px;background:'+sBg(hh.signal)+';color:'+sTxt(hh.signal)+'">'+sLbl(hh.signal)+'</span><div style="flex:1;height:3px;background:#F1F5F9;border-radius:2px;overflow:hidden"><div style="width:'+hh.confidence+'%;height:100%;background:'+sCol(hh.signal)+';border-radius:2px"></div></div><span style="font-family:\'DM Mono\',monospace;font-size:9px;color:#94A3B8">'+fT(hh.timestamp)+'</span></div>';});
    if(hist.length>1&&cur&&cur.refinementNote&&cur.refinementNote!=='Initial pass.')h+='<div class="rbox"><span class="rlbl">Refinement:</span>'+esc(cur.refinementNote)+'</div>';
    h+='</div>';
  }
  // Skeleton
  if(S.loading&&!cur)[5,3,6,3].forEach(function(hh,i){h+='<div class="skel" style="height:'+hh+'rem;animation-delay:'+(i*.1)+'s"></div>';});
  // Sub tabs
  if(cur){
    h+='<div class="stabs"><button class="stab'+(S.sub==='o'?' active':'')+'" onclick="setSub(\'o\')">📈 Overview</button><button class="stab'+(S.sub==='s'?' active':'')+'" onclick="setSub(\'s\')">⚡ Day Trading</button></div>';
    if(S.sub==='o'){
      h+='<div class="g2"><div class="pc" style="background:#F0FDF4"><div class="plbl">Swing Target</div><div class="pval" style="color:#16A34A">'+fP(cur.priceTarget,ins.unit)+'<span class="punit">/'+ins.unit+'</span></div></div><div class="pc" style="background:#FFF1F2"><div class="plbl">Swing Stop</div><div class="pval" style="color:#DC2626">'+fP(cur.stopLoss,ins.unit)+'<span class="punit">/'+ins.unit+'</span></div></div></div>';
      h+='<div class="card"><div class="clbl">AI Confidence — pass '+cur.pass+'</div><div class="confrow"><div class="confbg"><div class="conffill" style="width:'+cur.confidence+'%;background:linear-gradient(90deg,'+ac+'88,'+ac+')"></div></div><span class="confpct" style="color:'+ac+'">'+cur.confidence+'%</span></div></div>';
      h+='<div class="card"><div class="clbl">Market Outlook</div><p style="font-size:12px;color:#334155;line-height:1.6">'+esc(cur.summary)+'</p></div>';
      h+='<div><div class="clbl" style="margin-bottom:6px">Technical Indicators</div><div class="igrid">';
      Object.keys(cur.indicators||{}).forEach(function(k){var ind=cur.indicators[k];h+='<div class="icard"><div class="iname">'+(IND[k]||k)+'</div><div class="ival">'+(typeof ind.value==='number'?ind.value.toFixed(1):esc(ind.value))+'</div><div class="iint">'+esc(ind.interpretation)+'</div></div>';});
      h+='</div></div>';
      h+='<div class="g2"><div class="card"><div class="clbl">Catalysts</div>'+(cur.catalysts||[]).map(function(c){return'<div class="li"><span style="color:#16A34A">·</span>'+esc(c)+'</div>';}).join('')+'</div><div class="card"><div class="clbl">Risks</div>'+(cur.risks||[]).map(function(r){return'<div class="li"><span style="color:#DC2626">·</span>'+esc(r)+'</div>';}).join('')+'</div></div>';
    }
    if(S.sub==='s'){
      h+='<div class="warn"><span style="font-size:14px;flex-shrink:0">⚠️</span><p class="warntxt">AI-generated setups for informational purposes only. Not financial advice.</p></div>';
      if(cur.dayTrades&&cur.dayTrades.length>0){
        cur.dayTrades.forEach(function(tr){
          var isL=tr.direction==='LONG';
          h+='<div class="tcard"><div class="thdr" style="background:'+(isL?'#F0FDF4':'#FFF1F2')+'"><div style="display:flex;align-items:center;gap:6px"><span class="tdir" style="color:'+(isL?'#16A34A':'#DC2626')+'">'+(isL?'▲ LONG':'▼ SHORT')+'</span><span class="tsty">'+esc(tr.style)+'</span></div><div style="display:flex;gap:5px;align-items:center"><span style="font-size:9px;color:#64748B">R:R</span><span style="font-family:\'DM Mono\',monospace;font-size:11px;font-weight:700;color:'+(isL?'#16A34A':'#DC2626')+'">'+tr.riskReward+'</span></div></div><div class="tlvls"><div><div class="lvlbl" style="color:#64748B">Entry</div><div class="lvval">'+fP(tr.entryLow,ins.unit)+'</div><div class="lvsub">–'+fP(tr.entryHigh,ins.unit)+'</div></div><div><div class="lvlbl" style="color:#DC2626">Stop Loss</div><div class="lvval" style="color:#DC2626">'+fP(tr.stopLoss,ins.unit)+'</div><div class="lvsub">'+ins.unit+'</div></div><div><div class="lvlbl" style="color:#16A34A">TP1/TP2</div><div class="lvval" style="color:#16A34A">'+fP(tr.tp1,ins.unit)+'</div><div class="lvsub" style="color:#059669">'+fP(tr.tp2,ins.unit)+'</div></div></div><div class="ctxrow">'+(tr.volumeContext?'<span class="ctxtag">📊 '+esc(tr.volumeContext)+'</span>':'')+(tr.volatilityContext?'<span class="ctxtag">⚡ '+esc(tr.volatilityContext)+'</span>':'')+(tr.timingContext?'<span class="ctxtag">🕐 '+esc(tr.timingContext)+'</span>':'')+'</div>'+(tr.note?'<div class="tnote">'+esc(tr.note)+'</div>':'')+'</div>';
        });
      } else h+='<div style="text-align:center;padding:24px;color:#94A3B8;font-size:12px">No setups in this pass.</div>';
    }
  }
  h+='</div>';
  v.innerHTML=h;
  rStatusBar();
}

// RENDER CHAT
function rChat(){
  var v=document.getElementById('cview');
  var ins=gInst(S.sel);
  var Q=ins?['Best entry for '+ins.name+'?','Session timing?','Stop width?','Scalp or swing?']:['Best instrument?','Highest volatility?','Session tips?','Risk management?'];
  v.innerHTML='<div class="chat-w" style="height:calc(100vh - 112px - 56px)"><div class="chat-msgs" id="cmsgs">'+S.chatM.map(function(m){return'<div class="msg '+m.role+'">'+(m.role==='ai'?'<div class="mlbl">AI Analyst</div>':'')+esc(m.text)+'</div>';}).join('')+(S.chatL?'<div class="dots"><div class="dot"></div><div class="dot"></div><div class="dot"></div></div>':'')+'</div><div class="qrow">'+Q.map(function(q){return'<button class="qbtn" onclick="setCI('+JSON.stringify(q)+')">'+esc(q)+'</button>';}).join('')+'</div><div class="cinrow"><input class="cinput" id="ci" placeholder="Ask the AI analyst…" onkeydown="if(event.key===\'Enter\')sendC()"/><button class="csend" style="background:#0F172A;color:#fff" onclick="sendC()">Send</button></div></div>';
  setTimeout(function(){var m=document.getElementById('cmsgs');if(m)m.scrollTop=m.scrollHeight;},50);
}
function setCI(t){var e=document.getElementById('ci');if(e){e.value=t;e.focus();}}
function sendC(){
  var e=document.getElementById('ci');var txt=e&&e.value&&e.value.trim()?e.value.trim():'';
  if(!txt||S.chatL)return;e.value='';
  var ins=gInst(S.sel);
  S.chatM.push({role:'user',text:txt});S.chatH.push({role:'user',content:txt});S.chatL=true;rChat();
  var sys=ins?'Expert trader. '+ins.name+' ('+ins.sym+', ~'+ins.price+' '+ins.unit+'). Concise, actionable. Max 3 sentences.':'Expert commodity and index trader. Concise. Max 3 sentences.';
  fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:500,system:sys,messages:S.chatH})})
  .then(function(r){return r.json();}).then(function(d){
    var t=(d.content||[]).map(function(b){return b.text||'';}).join('')||'No response.';
    S.chatH.push({role:'assistant',content:t});S.chatM.push({role:'ai',text:t});
  }).catch(function(){S.chatM.push({role:'ai',text:'Connection error.'});}).then(function(){S.chatL=false;rChat();});
}

// ACTIONS
function selInst(id){if(S.sel===id)return;S.sel=id;S.showH=false;rIbar();rAnalysis();var k=gKey();if(k)startLoop(k);wRenderPair(0);}
function selTf(tf){if(S.tf===tf)return;var ok=gKey();if(ok)pauseLoop(ok);S.tf=tf;rAnalysis();var k=gKey();if(k)startLoop(k);}
function forceRef(){var k=gKey();if(k&&!S.loading)runPass(k);}
function doPause(){var k=gKey();if(k)pauseLoop(k);rStatusBar();}
function doResume(){var k=gKey();if(k&&S.sel)startLoop(k);}
function togH(){S.showH=!S.showH;rAnalysis();}
function setSub(t){S.sub=t;rAnalysis();}
function switchTab(tab){
  S.tab=tab;
  document.getElementById('aview').style.display=tab==='a'?'':'none';
  document.getElementById('cview').style.display=tab==='c'?'':'none';
  document.getElementById('scroll').style.overflow=tab==='a'?'auto':'hidden';
  document.getElementById('t1').className='tab'+(tab==='a'?' active':'');
  document.getElementById('t2').className='tab'+(tab==='c'?' active':'');
  if(tab==='a')rAnalysis();
  else{
    if(!S.chatM.length){var ins=gInst(S.sel);S.chatM=[{role:'ai',text:ins?'Analysis running for '+ins.name+'. Ask about entries, sessions, or risk.':'Select an instrument or ask a general trading question.'}];}
    rChat();
  }
}

// NOTIF TOGGLE
document.getElementById('nbtn').addEventListener('click',function(){
  S.nOn=!S.nOn;
  this.className='nbtn '+(S.nOn?'on':'off');
  document.getElementById('nlbl').textContent=S.nOn?'ON':'OFF';
  if(!S.nOn)document.getElementById('nping').classList.remove('show');
});

// WIDGET
document.getElementById('wbtn').addEventListener('click',function(){
  S.wShow=!S.wShow;
  document.getElementById('widget').classList.toggle('show',S.wShow);
  this.classList.toggle('on',S.wShow);
  if(S.wShow){wRenderPair(0);wRenderPair(1);}
});
document.getElementById('wclose').addEventListener('click',function(){
  S.wShow=false;
  document.getElementById('widget').classList.remove('show');
  document.getElementById('wbtn').classList.remove('on');
});
var wsel2=document.getElementById('wsel2');
INSTS.forEach(function(c){var o=document.createElement('option');o.value=c.id;o.textContent=c.sym;wsel2.appendChild(o);});
wsel2.addEventListener('change',function(e){
  S.w2=e.target.value||null;
  if(S.w2){var k2=S.w2+'-'+S.tf;if(!S.store[k2]||!S.store[k2].current){var i2=gInst(S.w2);if(i2){S.store[k2]={current:null,history:[],prevSig:null};doFetch(i2,S.tf,[]).then(function(r){S.store[k2].current=r;wRenderPair(1);}).catch(function(){});}}}
  wRenderPair(1);
});

// INIT
rIbar();rAnalysis();
if('serviceWorker' in navigator)navigator.serviceWorker.register('sw.js').catch(function(){});

// INSTALL BANNER
var dp;
window.addEventListener('beforeinstallprompt',function(e){
  e.preventDefault();dp=e;
  var b=document.createElement('div');b.id='ib';
  b.style.cssText='position:fixed;bottom:70px;left:50%;transform:translateX(-50%);background:#0F172A;color:#fff;padding:9px 16px;border-radius:999px;font-size:12px;z-index:9999;display:flex;gap:10px;align-items:center;box-shadow:0 4px 20px rgba(0,0,0,.35);white-space:nowrap;';
  b.innerHTML='<span>📲 Install TradeSim AI</span><button onclick="doInst()" style="padding:4px 10px;border-radius:999px;background:#2563EB;color:#fff;border:none;font-size:11px;font-weight:700;cursor:pointer;">Install</button><button onclick="this.parentNode.remove()" style="background:none;border:none;color:rgba(255,255,255,.45);cursor:pointer;font-size:14px;">✕</button>';
  document.body.appendChild(b);setTimeout(function(){b&&b.remove&&b.remove();},14000);
});
window.doInst=function(){dp&&dp.prompt();dp&&dp.userChoice&&dp.userChoice.then(function(){document.getElementById('ib')&&document.getElementById('ib').remove();dp=null;});};
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Data Nilai – Absensi & Nilai</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@500;600;700&family=Nunito:wght@400;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --papan:#2a6fdb; --papan-2:#3f86ee; --kapur:#e6f3ff;
  --kertas:#fffdf6; --garis:#cfe3fa; --tinta:#1c3a73; --abu:#5a6f93;
  --stabilo:#ffd84a; --merah:#ef5a4a; --laut:#2a6fdb; --biru:#2f64d6;
  --krem:#fffdf4; --judul:#1b52b5; --radius:20px;
}
*{box-sizing:border-box}
html,body{height:100%}
body{margin:0;font-family:Nunito,system-ui,sans-serif;color:var(--tinta);background:transparent;font-size:15px;line-height:1.5}
h1,h2,h3{font-family:Fredoka,Nunito,sans-serif;color:var(--judul);margin:0;line-height:1.15}
button,input,select,textarea{font:inherit;color:inherit}
button{cursor:pointer}
:focus-visible{outline:3px solid var(--biru);outline-offset:2px}



select,input[type=text],input[type=number],input[type=date],input[type=month],textarea{
  background:#fff;border:1.5px solid var(--garis);border-radius:8px;padding:8px 10px;min-height:38px;width:100%}
select{width:auto}
textarea{min-height:90px;resize:vertical}
.btn{background:var(--papan);color:#fff;border:0;border-radius:8px;padding:9px 14px;font-weight:600;min-height:38px}
.btn:hover{background:var(--papan-2)}
.btn.ghost{background:#fff;color:var(--papan);border:1.5px solid var(--papan)}
.btn.ghost:hover{background:var(--kapur)}
.btn.danger{background:#fff;color:var(--merah);border:1.5px solid var(--merah)}
.btn.sm{padding:4px 10px;min-height:30px;font-size:13px}
.btn:disabled{opacity:.5;cursor:default}

.panel{background:#fff;border:1.5px solid var(--garis);border-radius:var(--radius);padding:16px;margin-bottom:16px;box-shadow:0 3px 10px rgba(15,70,168,.07)}
.panel h2{font-size:19px;margin-bottom:10px}
.row{display:flex;gap:10px;flex-wrap:wrap;align-items:end}
.row>label{display:flex;flex-direction:column;gap:3px;font-size:13px;color:var(--abu);flex:1 1 150px}
.muted{color:var(--abu)}
.small{font-size:13px}

.stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:12px;margin-bottom:16px}
.stat{background:#fff;border:1.5px solid var(--garis);border-radius:var(--radius);padding:14px}
.stat b{display:block;font:700 30px Fredoka,sans-serif}
.stat span{color:var(--abu);font-size:13px}
.stat.hl{background:var(--stabilo);border-color:#e6c800}
.stat.hl span{color:#5d5200}

.tbl-wrap{overflow-x:auto;border:1.5px solid var(--garis);border-radius:var(--radius);background:#fff}
table{border-collapse:collapse;width:100%;min-width:560px}
th,td{padding:8px 10px;text-align:left;border-bottom:1px solid var(--garis);vertical-align:middle}
th{background:var(--kapur);font-weight:600;font-size:13px;position:sticky;top:0}
tr:last-child td{border-bottom:0}
td.num,th.num{text-align:center}
td input[type=number]{width:74px;text-align:center;padding:5px;min-height:32px}
td input.low{color:var(--merah);font-weight:700;border-color:var(--merah)}
.fin{font-weight:700}
.fin.low{color:var(--merah)}
.badge{display:inline-block;font-size:11px;padding:1px 7px;border-radius:99px;background:var(--stabilo);color:#4a4000;font-weight:600}
.badge.ok{background:#d6e8ff;color:#0f3f91}
.badge.warn{background:#fff0c2;color:#7a5800}
.badge.bad{background:#fde1de;color:#9c2217}
.tiny-in{width:56px!important;min-height:26px!important;padding:2px 4px!important;font-size:12px}

.stamps{display:flex;gap:6px}
.stamps button{width:44px;height:36px;border-radius:8px;border:1.5px solid var(--garis);background:#fff;font-weight:700;color:var(--abu)}
.stamps button.on[data-s=H]{background:var(--laut);border-color:var(--laut);color:#fff}
.stamps button.on[data-s=I]{background:#56c2ff;border-color:#2ea9f0;color:#04304f}
.stamps button.on[data-s=S]{background:var(--stabilo);border-color:#e6c800;color:#4a4000}
.stamps button.on[data-s=A]{background:var(--merah);border-color:var(--merah);color:#fff}

.tabs{display:inline-flex;border:1.5px solid var(--papan);border-radius:8px;overflow:hidden;margin-bottom:12px}
.tabs button{border:0;background:#fff;padding:7px 14px;color:var(--papan);font-weight:600}
.tabs button.on{background:var(--papan);color:#fff}
.empty{padding:26px;text-align:center;color:var(--abu);border:2px dashed var(--garis);border-radius:var(--radius);background:#fff}
.drop{display:block;border:2px dashed var(--papan-2);border-radius:var(--radius);background:var(--kapur);padding:20px;text-align:center;cursor:pointer}
.drop:hover,.drop.over{background:#d6e8ff;border-color:var(--papan)}
.drop b{display:block;font:700 17px Fredoka,sans-serif}
.drop input{display:none}
.scroll{max-height:320px;overflow:auto;border:1.5px solid var(--garis);border-radius:var(--radius)}
.scroll table{min-width:0}
.chips{display:flex;gap:6px;flex-wrap:wrap}
.chip{border:1.5px solid var(--garis);background:#fff;border-radius:99px;padding:5px 14px;font-weight:600;color:var(--abu)}
.chip:hover{border-color:var(--papan)}
.chip.on{background:var(--papan);border-color:var(--papan);color:#fff}
.chip:disabled{opacity:.4;cursor:default}
td .note-in{width:100%;min-width:160px;margin-top:4px;font-size:13px;text-align:left}
.grp{background:var(--papan);color:#fff;text-align:center;border-left:3px solid #fff;font-size:14px}
.grp .small{color:#cfe3ff;margin-top:2px}
.grp button{background:transparent;border:1px solid #9fc4f0;color:#fff;border-radius:6px;font-size:12px;padding:0 7px;margin-left:4px;min-height:22px}
.grp button:hover{background:var(--papan-2)}
td.tot{background:#fff8cf;font-weight:700;text-align:center}
td.tot.part{color:var(--abu);font-style:italic;font-weight:600}
td.tot.low{color:var(--merah)}
th.tot{background:var(--stabilo);color:#3d3500;text-align:center}
.stk1{position:sticky;left:0;z-index:2;background:#fff;width:46px;min-width:46px}
.stk2{position:sticky;left:46px;z-index:2;background:#fff;min-width:170px;box-shadow:1px 0 0 var(--garis)}
th.stk1,th.stk2{background:var(--kapur);z-index:3}
.steps{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px}
.steps span{font-size:13px;padding:3px 10px;border-radius:99px;background:var(--kapur)}
.steps span.on{background:var(--papan);color:#fff}
.note{background:#fffbe0;border-left:4px solid var(--stabilo);padding:10px 12px;border-radius:6px;font-size:13px;margin:10px 0}

#toast{position:fixed;left:50%;bottom:78px;transform:translateX(-50%);background:var(--papan);color:#fff;padding:9px 16px;border-radius:99px;font-size:14px;opacity:0;pointer-events:none;transition:opacity .2s;z-index:9}
#toast.show{opacity:1}

@media (prefers-reduced-motion:reduce){*{transition:none!important;animation:none!important}}
html{background:#cfe8ff}
#scene{position:fixed;inset:0;z-index:0;overflow:hidden;pointer-events:none}
#scene svg{position:absolute;inset:0;width:100%;height:100%;display:block}
.app{position:relative;z-index:1}
.empty-art{display:flex;justify-content:center;margin-bottom:8px}
.empty-art svg{width:86px;height:auto}
@keyframes bob{0%,100%{transform:translateY(0) rotate(-2deg)}50%{transform:translateY(-6px) rotate(2deg)}}
@keyframes bobsm{0%,100%{transform:translateY(0)}50%{transform:translateY(-4px)}}
@keyframes drift{to{transform:translateX(300px)}}
@keyframes cloudmove{to{transform:translateX(70px)}}
@keyframes spin{to{transform:rotate(360deg)}}
@keyframes twinkle{0%,100%{opacity:.25}50%{opacity:1}}
@keyframes rise{from{transform:translateY(0)}to{transform:translateY(-820px)}}
@keyframes rays{from{opacity:.05}to{opacity:.16}}
@media (prefers-reduced-motion:no-preference){
  .mascot svg{animation:bob 3.2s ease-in-out infinite}
  .bobsm{animation:bobsm 3.8s ease-in-out infinite}
  .drift{animation:drift 10s linear infinite}
  .drift.d2{animation-duration:15s;animation-direction:reverse}
  .drift.d3{animation-duration:22s}
  .cloud{animation:cloudmove 40s ease-in-out infinite alternate}
  .spin{animation:spin 80s linear infinite;transform-box:fill-box;transform-origin:center}
  .twinkle{animation:twinkle 3s ease-in-out infinite}
  .rise{animation:rise 10s linear infinite}
  .ray{animation:rays 7s ease-in-out infinite alternate}
}
.chk{width:18px;height:18px;min-height:0;accent-color:var(--papan);cursor:pointer;vertical-align:middle}

/* ===== Tema dongeng (Data Nilai) ===== */
.app{position:relative;z-index:1;min-height:100%;display:flex;flex-direction:column}
.site{position:sticky;top:0;z-index:20;background:var(--krem);box-shadow:0 4px 14px rgba(30,80,170,.12)}
.site-in{max-width:1180px;margin:0 auto;display:flex;align-items:center;gap:18px;padding:8px 20px}
.brand{display:flex;align-items:center;gap:8px;background:none;border:0;padding:0;text-align:left;font:700 25px Fredoka,sans-serif;color:var(--judul);line-height:1}
.brand .logo svg{width:46px;height:auto;display:block}
.brand small{display:block;font:600 11px Nunito,sans-serif;color:var(--abu);margin-top:4px;letter-spacing:.04em}
nav{display:flex;gap:4px;margin:0 auto}
nav button{background:none;border:0;padding:9px 16px;border-radius:99px;color:var(--judul);font-weight:700}
nav button:hover{background:var(--kapur)}
nav button.on{background:var(--stabilo);color:#4a3500}
.bgpick{display:flex;align-items:center;gap:6px;font-size:12px;color:var(--abu);font-weight:700}
.bgpick select{border-radius:99px;min-height:34px;padding:4px 12px}
.scallop{position:absolute;left:0;right:0;top:100%;width:100%;height:22px;display:block;pointer-events:none;margin-top:-1px}
main{flex:1;width:100%;max-width:1180px;margin:0 auto;padding:34px clamp(12px,3vw,28px) 24px}

#hero .hero{position:relative;border-radius:30px;overflow:hidden;min-height:340px;box-shadow:0 10px 30px rgba(30,80,170,.2);border:3px solid #fff}
#hero svg.art{position:absolute;inset:0;width:100%;height:100%;display:block}
.hero-text{position:relative;z-index:2;text-align:center;padding:34px 16px 70px;max-width:580px;margin:0 auto}
.hero h1{font-size:clamp(32px,5.2vw,52px);line-height:1.04;color:#1b52b5;text-shadow:0 2px 0 #fff}
.hero h1 span{display:block;color:#1796e8}
.hero p{margin:10px auto 16px;color:var(--tinta);font-weight:700;max-width:430px}
.pillbar{position:relative;z-index:3;display:flex;flex-wrap:wrap;gap:6px 0;justify-content:center;align-items:center;background:#fff;border-radius:99px;padding:10px 8px;margin:-34px auto 20px;max-width:max-content;box-shadow:0 6px 16px rgba(30,80,170,.18);font-size:13px;font-weight:700;color:var(--judul)}
.pillbar span{display:flex;align-items:center;gap:7px;padding:0 18px}
.pillbar span+span{border-left:2px solid #e3eefb}
.pillbar svg{width:24px;height:24px;flex:0 0 auto}

.topbar{display:flex;gap:12px;flex-wrap:wrap;align-items:center;margin-bottom:16px;padding:12px 18px;background:var(--krem);border:3px solid #fff;border-radius:26px;box-shadow:0 6px 18px rgba(30,80,170,.12)}
.topbar label{display:flex;flex-direction:column;font-size:12px;font-weight:700;color:var(--abu);gap:2px}
.topbar select{min-width:140px}
.title{margin-right:auto}
.title h1{font-size:28px}
.title p{margin:2px 0 0;color:var(--abu);font-weight:600}
.mascot{width:84px;flex:0 0 auto}
.mascot svg{width:100%;height:auto;display:block;overflow:visible}

#view{background:rgba(255,255,255,.62);border:3px solid rgba(255,255,255,.95);border-radius:30px;padding:16px;box-shadow:0 10px 30px rgba(30,80,170,.16);backdrop-filter:blur(5px);-webkit-backdrop-filter:blur(5px)}
html{background:#bfe3ff}
#scene{position:fixed;inset:0;z-index:0;overflow:hidden;pointer-events:none}
#scene svg{position:absolute;inset:0;width:100%;height:100%;display:block}

select,input[type=text],input[type=number],input[type=date],input[type=month],textarea{border-radius:14px;border-width:2px}
select{border-radius:99px;padding-left:14px}
.btn{background:var(--stabilo);color:#4a3500;border-radius:99px;padding:9px 20px;font-weight:700;min-height:40px;box-shadow:0 3px 0 #e0a800}
.btn:hover{background:#ffe27a}
.btn:active{transform:translateY(2px);box-shadow:0 1px 0 #e0a800}
.btn.ghost{background:#fff;color:var(--papan);border:2px solid var(--papan);box-shadow:none}
.btn.ghost:hover{background:var(--kapur)}
.btn.danger{background:#fff;color:var(--merah);border:2px solid var(--merah);box-shadow:none}
.btn.danger:hover{background:#fff1ef}
.btn.sm{padding:4px 12px;min-height:30px;font-size:13px;box-shadow:none}
.btn.sm:not(.ghost):not(.danger){box-shadow:0 2px 0 #e0a800}
.panel{background:var(--krem);border:3px solid #fff;border-radius:24px;box-shadow:0 6px 18px rgba(30,80,170,.12)}
.panel h2{color:var(--judul)}
.stat{border:3px solid #fff;border-radius:22px;box-shadow:0 6px 14px rgba(30,80,170,.12)}
.stat b{color:var(--judul)}
.stats .stat:nth-child(1){background:#fff0cf}
.stats .stat:nth-child(2){background:#e1f0ff}
.stats .stat:nth-child(3){background:#efe6ff}
.stat.hl{background:var(--stabilo)}
.tbl-wrap,.scroll{border:2px solid var(--garis);border-radius:20px}
th{color:var(--judul)}
.tabs{border-radius:99px}
.tabs button{padding:8px 18px}
.note{border-radius:14px}
.empty{border-radius:24px;background:var(--krem)}
tr.unset td{background:#fffbea}
.sect-title{text-align:center;font:700 26px Fredoka,sans-serif;color:var(--judul);margin:4px 0 14px}
.sect-title::before,.sect-title::after{content:'\2726';color:#ffc933;margin:0 10px;font-size:.65em;vertical-align:middle}
.tiles{display:grid;grid-template-columns:repeat(auto-fit,minmax(135px,1fr));gap:12px;margin-bottom:20px}
.tile{display:block;width:100%;border:3px solid #fff;border-radius:22px;padding:14px 10px;text-align:center;box-shadow:0 6px 14px rgba(30,80,170,.14);background:var(--bg,#fff);transition:transform .15s}
.tile:hover{transform:translateY(-4px)}
.tile svg{width:56px;height:56px;display:block;margin:0 auto}
.tile b{display:block;font:700 16px Fredoka,sans-serif;color:var(--judul);margin-top:6px}
.tile span{display:block;font-size:12px;color:var(--abu);font-weight:600;line-height:1.3;margin-top:2px}
.empty-art{display:flex;justify-content:center;margin-bottom:8px}
.empty-art svg{width:86px;height:auto}

.foot{position:relative;margin-top:46px;background:linear-gradient(180deg,#2a78e0,#1457c8);color:#e8f2ff;padding:26px 20px 18px}
.foot-wave{position:absolute;left:0;right:0;bottom:calc(100% - 1px);width:100%;height:38px;display:block}
.foot-in{max-width:1100px;margin:0 auto;display:grid;grid-template-columns:110px 1fr 110px;gap:18px;align-items:end}
.foot-art svg{width:100%;height:auto;display:block;margin-top:-62px}
.foot-cols{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;font-size:13px}
.foot-cols b{display:block;font:700 15px Fredoka,sans-serif;color:#ffe27a;margin-bottom:4px}
.foot-cols a,.foot-cols span{display:block;opacity:.94;line-height:1.7}
.foot-cols a{cursor:pointer}.foot-cols a:hover{text-decoration:underline}
.foot .copy{text-align:center;font-size:12px;opacity:.75;margin-top:14px}

@media (max-width:760px){
  .site-in{padding:6px 12px;gap:8px}
  .brand{font-size:21px}.brand .logo svg{width:38px}
  .brand small,.bgpick span{display:none}
  .bgpick{margin-left:auto}
  nav{position:fixed;left:0;right:0;bottom:0;margin:0;background:var(--krem);border-radius:22px 22px 0 0;box-shadow:0 -4px 16px rgba(30,80,170,.2);padding:6px;gap:0;justify-content:space-around;z-index:30}
  nav button{padding:8px 4px;font-size:12px;flex:1;border-radius:16px}
  main{padding-top:30px}
  .title h1{font-size:23px}
  .mascot{width:56px}
  #view{padding:10px;border-radius:22px}
  #hero .hero{min-height:320px}
  .hero-text{padding:22px 12px 64px}
  .pillbar{border-radius:24px;margin-top:-30px;padding:8px 4px}
  .pillbar span{padding:4px 10px;font-size:12px}
  .pillbar span+span{border-left:0}
  .foot{padding-bottom:96px}
  .foot-in{grid-template-columns:70px 1fr}
  .foot-art.r{display:none}
  .foot-cols{grid-template-columns:1fr}
  #toast{bottom:84px}
}
</style>
</head>
<body>
<div id="scene" aria-hidden="true"></div>
<div class="app">
  <header class="site">
    <div class="site-in">
      <button class="brand" id="brand" aria-label="Ke Beranda"></button>
      <nav id="nav">
        <button data-t="dashboard">Beranda</button>
        <button data-t="absensi">Absensi</button>
        <button data-t="nilai">Nilai</button>
        <button data-t="impor">Impor Form</button>
        <button data-t="data">Data</button>
      </nav>
      <label class="bgpick"><span>Latar</span><select id="gBg" aria-label="Latar"></select></label>
    </div>
    <svg class="scallop" viewBox="0 0 1200 30" preserveAspectRatio="none" aria-hidden="true"><path d="M0 0 H1200 V6 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 q-20 22 -40 0 Z" fill="#fffdf4"/></svg>
  </header>
  <main>
    <div id="hero"></div>
    <div class="topbar">
      <div id="mascot" class="mascot" aria-hidden="true"></div>
      <div class="title"><h1 id="pageTitle"></h1><p id="pageSub"></p></div>
      <label>Kelas <select id="gClass"></select></label>
      <label>Mata pelajaran <select id="gSubject"></select></label>
    </div>
    <div id="view"></div>
  </main>
  <footer class="foot" id="foot"></footer>
</div>
<div id="toast" role="status"></div>

<script>
/* ============ Util ============ */
const $=(s,r=document)=>r.querySelector(s);
const esc=s=>String(s??'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const uid=()=>Math.random().toString(36).slice(2,9);
const norm=s=>String(s||'').toLowerCase().replace(/[^a-z0-9 ]/g,' ').replace(/\s+/g,' ').trim();
const pad=n=>String(n).padStart(2,'0');
const today=()=>{const d=new Date();return d.getFullYear()+'-'+pad(d.getMonth()+1)+'-'+pad(d.getDate())};
const fmt=n=>n==null?'–':(Math.round(n*10)/10).toString().replace('.',',');
const JENIS=['Tugas','Catatan','Kuis','UH','PTS','PAS','Praktik','Sikap'];
const meetingsOf=(cid,subj,month)=>S.meetings.filter(m=>m.classId===cid&&m.subject===subj&&(!month||m.month===month));
const BULAN=['Januari','Februari','Maret','April','Mei','Juni','Juli','Agustus','September','Oktober','November','Desember'];
const monthLabel=m=>{const [y,mo]=String(m).split('-');return (BULAN[+mo-1]||m)+' '+y};
const compsOf=m=>S.assessments.filter(a=>a.meetingId===m.id);
const compLabel=(a,m)=>a.name&&a.name!==m.name?a.name:(a.type||'Tugas');
function meetingTotal(m,sid){
  let w=0,t=0,miss=0;
  compsOf(m).forEach(a=>{const v=S.scores[a.id]?.[sid];if(v!=null&&v!==''){w+=a.weight;t+=v*a.weight}else miss++});
  return {v:w?t/w:null,partial:miss>0&&w>0};
}
const noOf=(s,i)=>s.nis||String(i+1);
let toastT;
function toast(m){const t=$('#toast');t.textContent=m;t.classList.add('show');clearTimeout(toastT);toastT=setTimeout(()=>t.classList.remove('show'),2400)}
function download(name,text,type='text/csv'){const a=document.createElement('a');a.href=URL.createObjectURL(new Blob(['\ufeff'+text],{type}));a.download=name;a.click();setTimeout(()=>URL.revokeObjectURL(a.href),500)}
const csvCell=v=>{v=String(v??'');return /[",\n;]/.test(v)?'"'+v.replace(/"/g,'""')+'"':v};

/* ============ Penyimpanan (localStorage, dengan cadangan memori) ============ */
const KEY='kelasku.v1';
function seed(){
  const c1={id:'k7a',name:'VII A'},c2={id:'k8a',name:'VIII A'};
  const names=['Aditya Pratama','Bunga Lestari','Citra Maharani','Dimas Saputra','Eka Wulandari','Farhan Hakim','Gita Anjani','Hendra Wijaya','Indah Permata','Joko Santoso'];
  const students=names.map((n,i)=>({id:'s'+i,nis:String(i+1),name:n,classId:'k7a'}));
  ['Kartika Sari','Lutfi Ramadhan','Mega Putri'].forEach((n,i)=>students.push({id:'t'+i,nis:String(i+1),name:n,classId:'k8a'}));
  const meetings=[{id:'m1',classId:'k7a',subject:'Informatika',name:'Pertemuan 1'},{id:'m2',classId:'k7a',subject:'Informatika',name:'Pertemuan 2'}];
  const mk=(id,m,name,type,weight)=>({id,classId:'k7a',subject:'Informatika',meetingId:m,name,type,types:[type],weight,source:'manual',manual:{}});
  const as=[mk('a1','m1','Tugas Catatan','Catatan',70),mk('a2','m1','Kuis','Kuis',30),mk('a3','m2','Tugas Catatan','Catatan',70),mk('a4','m2','Kuis','Kuis',30)];
  const base=[88,76,92,64,80,71,95,58,84,78];
  const scores={a1:{},a2:{},a3:{},a4:{}};
  students.filter(s=>s.classId==='k7a').forEach((s,i)=>{
    scores.a1[s.id]=base[i];scores.a2[s.id]=Math.min(100,base[i]+((i*7)%11)-4);
    scores.a3[s.id]=Math.min(100,base[i]+((i*5)%9)-3);if(i<6)scores.a4[s.id]=Math.min(100,base[i]+((i*3)%7));
  });
  return {classes:[c1,c2],students,subjects:['Informatika','Matematika','IPA'],meetings,assessments:as,scores,notes:{},attendance:{},kkm:75,clientId:''};
}
function fixS(o){
  o.notes=o.notes||{};o.meetings=o.meetings||[];
  (o.assessments||[]).forEach(a=>{
    if(!a.types)a.types=[a.type||'Tugas'];
    if(!a.type)a.type=a.types[0];
    if(!(a.weight>0))a.weight=10;
    if(!a.meetingId){
      let m=o.meetings.find(x=>x.classId===a.classId&&x.subject===a.subject&&x.name===a.name);
      if(!m){m={id:'m'+Math.random().toString(36).slice(2,8),classId:a.classId,subject:a.subject,name:a.name};o.meetings.push(m)}
      a.meetingId=m.id;
    }
  });
  o.meetings.forEach(m=>{if(!m.month)m.month=today().slice(0,7)});
  o.bg=o.bg||'auto';
  return o;
}
function load(){try{const r=localStorage.getItem(KEY);if(r)return fixS(JSON.parse(r))}catch(e){}return fixS(seed())}
function save(){try{localStorage.setItem(KEY,JSON.stringify(S))}catch(e){}}
let S=load();

/* ============ Hitungan ============ */
const clsStudents=id=>S.students.filter(s=>s.classId===id).sort((a,b)=>{const x=parseFloat(a.nis),y=parseFloat(b.nis);if(!isNaN(x)&&!isNaN(y)&&x!==y)return x-y;return a.name.localeCompare(b.name)});
function finalGrade(cid,subj,sid,month){
  const ts=meetingsOf(cid,subj,month).map(m=>meetingTotal(m,sid).v).filter(v=>v!=null);
  return ts.length?ts.reduce((a,b)=>a+b,0)/ts.length:null;
}
function attStats(cid,sid,prefix=''){
  const c={H:0,I:0,S:0,A:0};
  for(const k in S.attendance){const [kc,d]=k.split('|');if(kc!==cid||!d.startsWith(prefix))continue;const v=S.attendance[k][sid];if(v)c[v]++}
  const tot=c.H+c.I+c.S+c.A;
  return {...c,tot,pct:tot?c.H/tot*100:null};
}

/* ============ State tampilan ============ */
const V={tab:'dashboard',classId:S.classes[0]?.id,subject:S.subjects[0],date:today(),month:today().slice(0,7),
  method:'api',imp:{link:'',name:'',type:'Kuis',weight:'',meetingId:'',csv:''},im:null,busy:false,err:''};

const TITLES={
  dashboard:['Beranda','Ringkasan kelas hari ini'],
  absensi:['Absensi','Catat kehadiran per tanggal dan lihat rekapnya'],
  nilai:['Nilai','Nilai dipisah per bulan; isi per pertemuan dan lihat nilai akhir'],
  impor:['Impor Google Form','Tarik nilai kuis langsung ke daftar nilai murid'],
  data:['Data & Pengaturan','Kelas, murid, mata pelajaran, dan cadangan']
};

function render(){
  $('#gClass').innerHTML=S.classes.map(c=>`<option value="${c.id}" ${c.id===V.classId?'selected':''}>${esc(c.name)}</option>`).join('');
  $('#gSubject').innerHTML=S.subjects.map(s=>`<option ${s===V.subject?'selected':''}>${esc(s)}</option>`).join('');
  document.querySelectorAll('#nav button').forEach(b=>b.classList.toggle('on',b.dataset.t===V.tab));
  $('#pageTitle').textContent=TITLES[V.tab][0];$('#pageSub').textContent=TITLES[V.tab][1];
  const needClass=['dashboard','absensi','nilai','impor'].includes(V.tab);
  $('#view').innerHTML=(needClass&&!V.classId)?`<div class="empty">Belum ada kelas. Tambahkan kelas dan murid di menu <b>Data & Pengaturan</b>.</div>`:VIEWS[V.tab]();
  decorate();
}
$('#nav').addEventListener('click',e=>{const b=e.target.closest('button');if(b){V.tab=b.dataset.t;render();scrollTo(0,0)}});
$('#gClass').addEventListener('change',e=>{V.classId=e.target.value;V.im=null;render()});
$('#gSubject').addEventListener('change',e=>{V.subject=e.target.value;V.im=null;render()});

/* ============ Tampilan ============ */
const VIEWS={
dashboard(){
  const st=clsStudents(V.classId),rec=S.attendance[V.classId+'|'+today()];
  const hadir=rec?st.filter(s=>rec[s.id]==='H').length:null,marked=rec?st.filter(s=>rec[s.id]).length:0;
  const fg=st.map(s=>finalGrade(V.classId,V.subject,s.id)).filter(v=>v!=null);
  const avg=fg.length?fg.reduce((a,b)=>a+b,0)/fg.length:null;
  const risk=st.map(s=>({s,a:attStats(V.classId,s.id),f:finalGrade(V.classId,V.subject,s.id)}))
    .filter(r=>(r.a.pct!=null&&r.a.pct<85)||(r.f!=null&&r.f<S.kkm));
  return `${tilesHTML()}
  <div class="stats">
    <div class="stat"><b>${st.length}</b><span>murid di kelas ini</span></div>
    <div class="stat"><b>${hadir==null?'–':hadir+'/'+st.length}</b><span>hadir hari ini${rec&&marked<st.length?` · ${st.length-marked} belum diabsen`:''}</span></div>
    <div class="stat"><b>${fmt(avg)}</b><span>rata-rata nilai akhir ${esc(V.subject)}</span></div>
    <div class="stat hl"><b>${risk.length}</b><span>murid perlu perhatian</span></div>
  </div>
  <div class="panel">
    <h2>Perlu perhatian</h2>
    ${risk.length?`<div class="tbl-wrap"><table><thead><tr><th>Nama</th><th class="num">Kehadiran</th><th class="num">Nilai akhir</th><th>Catatan</th></tr></thead><tbody>
    ${risk.map(r=>`<tr><td>${esc(r.s.name)}</td><td class="num">${r.a.pct==null?'–':fmt(r.a.pct)+'%'}</td><td class="num fin ${r.f!=null&&r.f<S.kkm?'low':''}">${fmt(r.f)}</td>
      <td>${r.a.pct!=null&&r.a.pct<85?'<span class="badge bad">Kehadiran rendah</span> ':''}${r.f!=null&&r.f<S.kkm?`<span class="badge warn">Di bawah KKM ${S.kkm}</span>`:''}</td></tr>`).join('')}
    </tbody></table></div>`:`<p class="muted">Tidak ada murid yang kehadirannya di bawah 85% atau nilainya di bawah KKM ${S.kkm}.</p>`}
  </div>
  <div class="row"><button class="btn" onclick="go('absensi')">Mulai absen hari ini</button><button class="btn ghost" onclick="go('nilai')">Buka daftar nilai</button><button class="btn ghost" onclick="go('impor')">Impor nilai kuis</button></div>`;
},

absensi(){
  const st=clsStudents(V.classId),key=V.classId+'|'+V.date,rec=S.attendance[key];
  const cnt={H:0,I:0,S:0,A:0};if(rec)st.forEach(s=>{if(rec[s.id])cnt[rec[s.id]]++});
  const marked=cnt.H+cnt.I+cnt.S+cnt.A;
  const rows=st.map((s,i)=>{const cur=rec?.[s.id]||'';return `<tr class="${cur?'':'unset'}"><td class="num muted" style="width:46px">${noOf(s,i)}</td><td>${esc(s.name)}</td>
    <td><div class="stamps">${['H','I','S','A'].map(x=>`<button data-s="${x}" class="${cur===x?'on':''}" onclick="setAtt('${s.id}','${x}')" aria-label="${{H:'Hadir',I:'Izin',S:'Sakit',A:'Alpa'}[x]}">${x}</button>`).join('')}</div></td></tr>`}).join('');
  const rk=st.map((s,i)=>({s,i,a:attStats(V.classId,s.id,V.month)}));
  return `
  <div class="panel">
    <div class="row">
      <label>Tanggal<input type="date" value="${V.date}" onchange="V.date=this.value;render()"></label>
      <span class="badge ${st.length&&marked===st.length?'ok':'warn'}" style="align-self:center">${marked} dari ${st.length} murid sudah diabsen</span>
      <button class="btn danger sm" onclick="clearAbsen()" ${rec?'':'disabled'}>Kosongkan absen tanggal ini</button>
    </div>
    <p class="muted small" style="margin:8px 0 0">Tidak ada yang terisi otomatis: ketuk status tiap murid (H = Hadir, I = Izin, S = Sakit, A = Alpa). Ketuk lagi untuk membatalkan. Setiap ketukan langsung tersimpan.</p>
    <div class="row" style="margin-top:10px;gap:6px"><span class="badge ok">Hadir ${cnt.H}</span><span class="badge" style="background:#d6efff;color:#0b4a7a">Izin ${cnt.I}</span><span class="badge">Sakit ${cnt.S}</span><span class="badge bad">Alpa ${cnt.A}</span><span class="badge warn">Belum diisi ${st.length-marked}</span></div>
  </div>
  ${st.length?`<div class="tbl-wrap"><table><thead><tr><th class="num">No</th><th>Murid</th><th>Status</th></tr></thead><tbody>${rows}</tbody></table></div>`:`<div class="empty">Kelas ini belum punya murid.</div>`}
  <div class="panel" style="margin-top:16px">
    <div class="row"><h2 style="margin-right:auto">Rekap bulanan</h2>
      <label style="flex:0 1 170px">Bulan<input type="month" value="${V.month}" onchange="V.month=this.value;render()"></label>
      <button class="btn ghost" onclick="exportAbsen()">Ekspor CSV</button></div>
    <div class="tbl-wrap" style="margin-top:10px"><table><thead><tr><th class="num">No</th><th>Murid</th><th class="num">H</th><th class="num">I</th><th class="num">S</th><th class="num">A</th><th class="num">% Hadir</th></tr></thead><tbody>
    ${rk.map(({s,a,i})=>`<tr><td class="num muted">${noOf(s,i)}</td><td>${esc(s.name)}</td><td class="num">${a.H}</td><td class="num">${a.I}</td><td class="num">${a.S}</td><td class="num">${a.A}</td>
      <td class="num fin ${a.pct!=null&&a.pct<85?'low':''}">${a.pct==null?'–':fmt(a.pct)+'%'}</td></tr>`).join('')}
    </tbody></table></div>
  </div>`;
},

nilai(){
  if(V.gAll)return nilaiRekap();
  const st=clsStudents(V.classId),allMs=meetingsOf(V.classId,V.subject),ms=meetingsOf(V.classId,V.subject,V.gMonth),nm=V.nm,nc=V.nc;
  const fgs=st.map(s=>finalGrade(V.classId,V.subject,s.id,V.gMonth));
  const ok=fgs.filter(v=>v!=null),avg=ok.length?ok.reduce((a,b)=>a+b,0)/ok.length:null;
  const mSel=ms.some(m=>m.id===nc.meetingId)?nc.meetingId:(ms[ms.length-1]?.id||'');
  const avgOf=vs=>{vs=vs.filter(v=>v!=null&&v!=='');return vs.length?fmt(vs.reduce((x,y)=>x+y,0)/vs.length):'–'};
  return `${monthBar()}
  <div class="panel"><h2>Atur pertemuan di ${monthLabel(V.gMonth)}</h2>
    <div class="row">
      <label style="flex:2 1 180px">Pertemuan baru<input type="text" value="${esc(nm.name)}" placeholder="Pertemuan ${ms.length+1}" oninput="V.nm.name=this.value"></label>
      ${allMs.length?`<label style="flex:0 1 auto;flex-direction:row;align-items:center;gap:6px;color:var(--tinta);padding-bottom:8px"><input type="checkbox" style="width:auto;min-height:0" ${nm.copy?'checked':''} onchange="V.nm.copy=this.checked"> Salin komponen dari pertemuan terakhir</label>`:''}
      <button class="btn" onclick="addMeeting()">Tambah pertemuan</button>
    </div>
    ${ms.length?`<div class="row" style="margin-top:14px">
      <label>Tambah komponen ke<select style="width:100%" onchange="V.nc.meetingId=this.value">${ms.map(m=>`<option value="${m.id}" ${m.id===mSel?'selected':''}>${esc(m.name)}</option>`).join('')}</select></label>
      <label>Jenis<select style="width:100%" onchange="V.nc.jenis=this.value">${JENIS.map(j=>`<option ${j===nc.jenis?'selected':''}>${j}</option>`).join('')}</select></label>
      <label>Nama (opsional)<input type="text" value="${esc(nc.name)}" oninput="V.nc.name=this.value" placeholder="mis. Tugas Catatan"></label>
      <label style="flex:0 1 110px">Bobot (%)<input type="number" min="1" max="100" value="${esc(nc.weight)}" oninput="V.nc.weight=this.value" placeholder="sisa"></label>
      <button class="btn" onclick="addComp()">Tambah komponen</button>
    </div>`:''}
    <p class="muted small" style="margin:10px 0 0">Tiap pertemuan punya komponen sendiri (misalnya Catatan 70% + Kuis 30%) dan totalnya dihitung terpisah dari pertemuan lain. Nilai akhir bulan ini = rata-rata total semua pertemuan di ${monthLabel(V.gMonth)}. Tiap bulan dihitung terpisah.</p>
  </div>
  ${ms.length?`
  <div class="row" style="margin-bottom:8px"><span class="muted small" style="margin-right:auto">KKM ${S.kkm}. Total miring berarti ada komponen yang belum terisi.</span>
    <button class="btn ghost sm" onclick="exportNilai()">Ekspor CSV</button></div>
  <div class="tbl-wrap"><table><thead>
    <tr><th class="stk1 num" rowspan="2">No</th><th class="stk2" rowspan="2">Murid</th>
    ${ms.map(m=>{const cs=compsOf(m),tw=cs.reduce((x,a)=>x+a.weight,0);
      return `<th class="grp" colspan="${cs.length+1}">${esc(m.name)}<button onclick="renameMeeting('${m.id}')">ubah nama</button><button onclick="delMeeting('${m.id}')" aria-label="Hapus ${esc(m.name)}">×</button>
        <div class="small">${cs.length?(tw===100?'bobot 100%':'<span class="badge warn">bobot '+tw+'%, idealnya 100%</span>'):'belum ada komponen'}</div></th>`}).join('')}
    <th class="num" rowspan="2">Nilai akhir<div class="small muted" style="font-weight:400">${monthLabel(V.gMonth)}</div></th></tr>
    <tr>${ms.map(m=>compsOf(m).map(a=>`<th class="num">${esc(compLabel(a,m))}<div class="small muted" style="font-weight:400">${esc(a.type)}${a.source==='google_form'?' <span class="badge">Form</span>':''}</div>
      <div style="display:flex;gap:3px;justify-content:center;align-items:center;margin-top:3px"><input class="tiny-in" type="number" min="1" max="100" value="${a.weight}" onchange="setW('${a.id}',this.value)" aria-label="Bobot ${esc(compLabel(a,m))}">%
      <button class="btn danger sm" style="padding:0 6px;min-height:24px" onclick="delAssess('${a.id}')" aria-label="Hapus ${esc(compLabel(a,m))}">×</button></div></th>`).join('')+`<th class="tot">Total</th>`).join('')}</tr>
  </thead><tbody>
    ${st.map((s,i)=>`<tr><td class="stk1 num muted">${noOf(s,i)}</td><td class="stk2">${esc(s.name)}</td>
      ${ms.map(m=>{const t=meetingTotal(m,s.id);
        return compsOf(m).map(a=>{const v=S.scores[a.id]?.[s.id];
          return `<td class="num"><input type="number" min="0" max="100" step="any" value="${v??''}" class="${v!=null&&v!==''&&v<S.kkm?'low':''}" onchange="setScore('${a.id}','${s.id}',this.value)" aria-label="${esc(s.name)} ${esc(compLabel(a,m))}"></td>`}).join('')
          +`<td class="tot ${t.partial?'part':''} ${t.v!=null&&t.v<S.kkm?'low':''}" ${t.partial?'title="Belum semua komponen terisi"':''}>${fmt(t.v)}</td>`}).join('')}
      <td class="num fin ${fgs[i]!=null&&fgs[i]<S.kkm?'low':''}">${fmt(fgs[i])}</td></tr>`).join('')}
    <tr><td class="stk1"></td><td class="stk2"><b>Rata-rata kelas</b></td>
      ${ms.map(m=>compsOf(m).map(a=>`<td class="num muted">${avgOf(st.map(s=>S.scores[a.id]?.[s.id]))}</td>`).join('')+`<td class="tot">${avgOf(st.map(s=>meetingTotal(m,s.id).v))}</td>`).join('')}
      <td class="num fin">${fmt(avg)}</td></tr>
  </tbody></table></div>
  <p class="muted small">Total pertemuan = rata-rata tertimbang dari komponen yang sudah terisi. Angka merah berarti di bawah KKM.</p>`
  :`<div class="empty">Belum ada pertemuan ${esc(V.subject)} pada ${monthLabel(V.gMonth)}. Buat pertemuan pertama di atas, lalu tambahkan komponennya.</div>`}`;
},

impor(){
  const p=V.imp,im=V.im;
  const stepOn=n=>(n===1&&!im)||(n===2&&im)?'on':'';
  return `
  <div class="steps"><span class="${stepOn(1)}">1. Ambil data form</span><span class="${stepOn(2)}">2. Cek & simpan</span></div>
  <div class="note">Nilai masuk ke <b>${esc(S.classes.find(c=>c.id===V.classId)?.name||'')}</b> · <b>${esc(V.subject)}</b> · bulan <input type="month" value="${V.gMonth}" style="width:165px;min-height:30px;padding:3px 8px;display:inline-block" onchange="if(this.value){V.gMonth=this.value;V.imp.meetingId='';render()}" aria-label="Bulan penilaian">. Ganti kelas atau mapel di bagian atas jika perlu.</div>
  ${im?importPreview():`
  <div class="panel">
    <div class="row">
      <label style="flex:3 1 260px">Link Google Form (mode Kuis)<input type="text" value="${esc(p.link)}" oninput="V.imp.link=this.value" placeholder="https://docs.google.com/forms/d/…/edit"></label>
      <label style="flex:1 1 170px">Masuk ke pertemuan<select style="width:100%" onchange="V.imp.meetingId=this.value">${(()=>{const ms=meetingsOf(V.classId,V.subject,V.gMonth),pm=p.meetingId||ms[ms.length-1]?.id||'__new__';return ms.map(m=>`<option value="${m.id}" ${m.id===pm?'selected':''}>${esc(m.name)}</option>`).join('')+`<option value="__new__" ${pm==='__new__'?'selected':''}>+ Pertemuan baru</option>`})()}</select></label>
      <label style="flex:2 1 160px">Nama komponen<input type="text" value="${esc(p.name)}" oninput="V.imp.name=this.value" placeholder="mis. Kuis Bab 2"></label>
      <label style="flex:0 1 120px">Jenis<select style="width:100%" onchange="V.imp.type=this.value">${JENIS.map(t=>`<option ${t===p.type?'selected':''}>${t}</option>`).join('')}</select></label>
      <label style="flex:0 1 90px">Bobot %<input type="number" value="${esc(p.weight)}" min="1" max="100" oninput="V.imp.weight=this.value" placeholder="sisa"></label>
    </div>
  </div>
  <div class="tabs" role="tablist">
    <button class="${V.method==='api'?'on':''}" onclick="V.method='api';render()">Google Forms API</button>
    <button class="${V.method==='csv'?'on':''}" onclick="V.method='csv';render()">Unggah CSV</button>
    <button class="${V.method==='demo'?'on':''}" onclick="V.method='demo';render()">Coba dengan data contoh</button>
  </div>
  ${V.err?`<div class="note" style="border-color:var(--merah);background:#fde8e6">${esc(V.err)}</div>`:''}
  ${V.method==='api'?`
  <div class="panel">
    <div class="row"><label style="flex:3 1 260px">OAuth Client ID (Google Cloud)<input type="text" value="${esc(S.clientId)}" oninput="S.clientId=this.value;save()" placeholder="xxxx.apps.googleusercontent.com"></label>
    <button class="btn" onclick="fetchAPI()" ${V.busy?'disabled':''}>${V.busy?'Mengambil…':'Hubungkan Google & ambil nilai'}</button></div>
    <p class="muted small" style="margin:10px 0 0">Akun Google yang dipakai harus pemilik atau editor form tersebut. Halaman ini harus dibuka lewat <b>https</b> atau <b>localhost</b>, dan alamatnya didaftarkan sebagai Authorized JavaScript origin di Google Cloud. Izin yang diminta hanya baca (form dan respons).</p>
  </div>`:''}
  ${V.method==='csv'?`
  <div class="panel">
    <p class="muted small" style="margin-top:0">Di Google Form buka tab <b>Respons → Tautkan ke Sheets</b>, unduh sebagai CSV, lalu unggah atau tempel di sini. Kolom <b>Skor/Score</b> terbaca otomatis, termasuk format "8 / 10".</p>
    <input type="file" accept=".csv,text/csv" onchange="readCSVFile(this.files[0])">
    <textarea style="margin-top:8px" placeholder="…atau tempel isi CSV di sini" oninput="V.imp.csv=this.value">${esc(p.csv)}</textarea>
    <div style="margin-top:8px"><button class="btn" onclick="loadCSV()">Baca CSV</button></div>
  </div>`:''}
  ${V.method==='demo'?`
  <div class="panel"><p style="margin-top:0">Membuat respons contoh dari murid di kelas ini (termasuk satu nama salah ketik dan satu murid tidak dikenal) untuk mencoba alur pencocokan.</p>
  <button class="btn" onclick="loadDemo()">Buat data contoh</button></div>`:''}
  `}`;
},

data(){
  const sel=V.classId;
  return `
  <div class="panel"><h2>Kelas</h2>
    <div class="row"><label>Nama kelas baru<input type="text" id="cName" placeholder="mis. IX B"></label><button class="btn" onclick="addClass()">Tambah kelas</button>
    ${S.classes.length?`<button class="btn danger" onclick="delClass()">Hapus kelas terpilih</button>`:''}</div>
  </div>
  <div class="panel"><h2>Murid ${sel?`di ${esc(S.classes.find(c=>c.id===sel)?.name)}`:''}</h2>
    ${sel?`<div class="row"><label style="flex:0 1 100px">No<input type="text" id="sNis" placeholder="otomatis"></label><label style="flex:2 1 200px">Nama<input type="text" id="sName"></label><button class="btn" onclick="addStudent()">Tambah murid</button></div>
    <div style="margin-top:14px">
      <label class="drop" ondragover="event.preventDefault();this.classList.add('over')" ondragleave="this.classList.remove('over')" ondrop="event.preventDefault();this.classList.remove('over');readStudentFile(event.dataTransfer.files[0])">
        <b>Unggah daftar murid dari file</b>
        <span class="muted small">Seret file ke sini atau klik untuk memilih. Mendukung Excel (.xlsx, .xls) dan CSV.</span>
        <input type="file" accept=".xlsx,.xls,.csv,.txt,.tsv" onchange="readStudentFile(this.files[0])">
      </label>
      <p class="muted small" style="margin:8px 0 0">Kolom yang dibaca: <b>No</b> (nomor) dan <b>Nama</b>, judul kolom boleh ada atau tidak. Jika tidak ada nomor, murid dinomori otomatis sesuai urutan. Murid masuk ke kelas yang sedang dipilih. <a href="#" onclick="downloadStudentTemplate();return false">Unduh templat CSV</a></p>
      ${stuPreviewHTML()}
    </div>
    <label class="muted small" style="display:block;margin-top:14px">Atau tempel banyak murid sekaligus, satu baris satu murid, format <b>No,Nama</b>
      <textarea id="bulk" placeholder="1,Aditya Pratama&#10;2,Bunga Lestari"></textarea></label>
    <div style="margin:8px 0 12px"><button class="btn ghost" onclick="bulkStudents()">Impor daftar</button></div>
    ${(()=>{const list=clsStudents(sel),selN=list.filter(s=>V.selStu[s.id]).length;return `<div class="row" style="margin-bottom:8px;align-items:center"><span class="muted small" style="margin-right:auto">${list.length} murid${selN?` · ${selN} dipilih`:''}</span>
      <button class="btn danger sm" onclick="delSelectedStu()" ${selN?'':'disabled'}>Hapus terpilih${selN?' ('+selN+')':''}</button>
      <button class="btn danger sm" onclick="delAllStu()" ${list.length?'':'disabled'}>Hapus semua murid kelas ini</button></div>
    <div class="tbl-wrap"><table><thead><tr><th class="num" style="width:44px"><input type="checkbox" class="chk" aria-label="Pilih semua murid" ${list.length&&selN===list.length?'checked':''} onchange="selectAllStu(this.checked)"></th><th class="num" style="width:50px">No</th><th>Nama</th><th></th></tr></thead><tbody>
    ${list.map((s,i)=>`<tr><td class="num"><input type="checkbox" class="chk" aria-label="Pilih ${esc(s.name)}" ${V.selStu[s.id]?'checked':''} onchange="toggleStu('${s.id}',this.checked)"></td><td class="num">${noOf(s,i)}</td><td>${esc(s.name)}</td><td style="text-align:right"><button class="btn danger sm" onclick="delStudent('${s.id}')">Hapus</button></td></tr>`).join('')||'<tr><td colspan="4" class="muted">Belum ada murid.</td></tr>'}
    </tbody></table></div>`})()}`:'<p class="muted">Tambahkan kelas terlebih dahulu.</p>'}
  </div>
  <div class="panel"><h2>Pengaturan</h2>
    <div class="row"><label style="flex:0 1 140px">KKM<input type="number" value="${S.kkm}" min="0" max="100" onchange="S.kkm=+this.value||75;save();render()"></label>
    <label>Tambah mata pelajaran<input type="text" id="mName" placeholder="mis. Bahasa Indonesia"></label><button class="btn" onclick="addSubject()">Tambah</button></div>
    <p class="muted small">Mapel: ${S.subjects.map(esc).join(', ')}</p>
  </div>
  <div class="panel"><h2>Cadangan data</h2>
    <div class="row"><button class="btn ghost" onclick="backup()">Unduh cadangan (.json)</button>
    <label style="flex:0 1 auto"><span class="btn ghost" style="display:inline-block">Pulihkan dari cadangan</span><input type="file" accept=".json" hidden onchange="restore(this.files[0])"></label>
    <button class="btn danger" onclick="resetAll()">Hapus semua data</button></div>
  </div>`;
}};

function importPreview(){
  const im=V.im,{rows,pick,missing}=computeMatches(),sts=clsStudents(V.classId);
  const matched=Object.keys(pick).length;
  return `
  <div class="panel">
    <div class="row">
      <label style="flex:2 1 220px">Kolom identitas murid<select style="width:100%" onchange="V.im.idQ=this.value;render()">${im.questions.map(q=>`<option value="${esc(q.id)}" ${q.id===im.idQ?'selected':''}>${esc(q.title)}</option>`).join('')}</select></label>
      <label style="flex:1 1 170px">Jika mengerjakan lebih dari sekali<select style="width:100%" onchange="V.im.policy=this.value;render()">
        <option value="max" ${im.policy==='max'?'selected':''}>Pakai nilai tertinggi</option><option value="last" ${im.policy==='last'?'selected':''}>Pakai yang terakhir</option><option value="first" ${im.policy==='first'?'selected':''}>Pakai yang pertama</option></select></label>
    </div>
    <p class="muted small" style="margin:10px 0 0">Skor diubah ke skala 0–100 (skor maksimum form: ${fmt(im.max)}). Pencocokan: nomor absen dulu, lalu nama.</p>
  </div>
  <div class="stats">
    <div class="stat"><b>${rows.length}</b><span>respons diterima</span></div>
    <div class="stat"><b>${matched}</b><span>murid cocok</span></div>
    <div class="stat hl"><b>${rows.filter(r=>!r.st).length}</b><span>perlu dicocokkan manual</span></div>
    <div class="stat"><b>${missing.length}</b><span>murid belum mengerjakan</span></div>
  </div>
  <div class="tbl-wrap"><table><thead><tr><th>Isian di form</th><th>Murid</th><th class="num">Nilai</th><th>Status</th></tr></thead><tbody>
  ${rows.map(r=>`<tr><td>${esc(r.raw)||'<span class="muted">(kosong)</span>'}</td>
    <td><select style="width:100%" onchange="assign(${r.i},this.value)"><option value="">– pilih murid –</option>${sts.map(s=>`<option value="${s.id}" ${r.st?.id===s.id?'selected':''}>${esc(s.name)}</option>`).join('')}</select></td>
    <td class="num">${r.score==null?'–':fmt(r.score)}</td>
    <td>${!r.st?'<span class="badge bad">Belum cocok</span>':r.how==='mirip'?'<span class="badge warn">Mirip, cek dulu</span>':'<span class="badge ok">Cocok ('+r.how+')</span>'}${r.st&&pick[r.st.id]&&pick[r.st.id].i!==r.i?' <span class="badge">Tidak dipakai</span>':''}</td></tr>`).join('')}
  </tbody></table></div>
  ${missing.length?`<p class="muted small">Belum mengerjakan (dibiarkan kosong, bukan nol): ${missing.map(m=>esc(m.name)).join(', ')}</p>`:''}
  <div class="row" style="margin-top:12px"><button class="btn" onclick="saveImport()" ${matched?'':'disabled'}>Simpan ${matched} nilai</button><button class="btn ghost" onclick="V.im=null;render()">Batal</button></div>`;
}

/* ============ Aksi: umum ============ */
function go(t){V.tab=t;render();scrollTo(0,0)}

function setAtt(sid,st){
  const key=V.classId+'|'+V.date;
  const rec=S.attendance[key]=S.attendance[key]||{};
  if(rec[sid]===st)delete rec[sid];else rec[sid]=st;
  if(!Object.keys(rec).length)delete S.attendance[key];
  save();render();
}
function clearAbsen(){
  const key=V.classId+'|'+V.date;if(!S.attendance[key])return;
  if(!confirm('Kosongkan semua absen pada tanggal ini?'))return;
  delete S.attendance[key];save();render();toast('Absen tanggal ini dikosongkan');
}
function exportAbsen(){
  const rows=[['No','Nama','Hadir','Izin','Sakit','Alpa','% Hadir']];
  clsStudents(V.classId).forEach((s,i)=>{const a=attStats(V.classId,s.id,V.month);rows.push([noOf(s,i),s.name,a.H,a.I,a.S,a.A,a.pct==null?'':fmt(a.pct)])});
  download(`rekap-absen-${V.month}.csv`,rows.map(r=>r.map(csvCell).join(',')).join('\n'));
}

function monthBar(){
  const shift=d=>{const [y,m]=V.gMonth.split('-').map(Number);const dt=new Date(y,m-1+d,1);return dt.getFullYear()+'-'+pad(dt.getMonth()+1)};
  return `<div class="tabs"><button class="on">Per bulan</button><button onclick="V.gAll=true;render()">Rekap semua bulan</button></div>
  <div class="row" style="margin-bottom:14px;align-items:center">
    <button class="btn ghost sm" onclick="V.gMonth='${shift(-1)}';render()" aria-label="Bulan sebelumnya">‹</button>
    <b style="font:700 21px 'Bricolage Grotesque',sans-serif;min-width:150px;text-align:center">${monthLabel(V.gMonth)}</b>
    <button class="btn ghost sm" onclick="V.gMonth='${shift(1)}';render()" aria-label="Bulan berikutnya">›</button>
    <input type="month" value="${V.gMonth}" style="width:170px" onchange="if(this.value){V.gMonth=this.value;render()}" aria-label="Pilih bulan">
  </div>`;
}
const meanOf=arr=>{const v=arr.filter(x=>x!=null);return v.length?v.reduce((a,b)=>a+b,0)/v.length:null};
function rekapData(){
  const st=clsStudents(V.classId),ml=meetingsOf(V.classId,V.subject),months=[...new Set(ml.map(m=>m.month))].sort();
  const grid=st.map((s,i)=>{const per=months.map(mo=>finalGrade(V.classId,V.subject,s.id,mo));return {s,i,per,avg:meanOf(per)}});
  return {months,grid,count:months.map(mo=>ml.filter(m=>m.month===mo).length),colAvg:months.map((mo,j)=>meanOf(grid.map(g=>g.per[j])))};
}
function nilaiRekap(){
  const tabs=`<div class="tabs"><button onclick="V.gAll=false;render()">Per bulan</button><button class="on">Rekap semua bulan</button></div>`;
  const {months,grid,count,colAvg}=rekapData();
  if(!months.length)return tabs+`<div class="empty">Belum ada pertemuan ${esc(V.subject)} di kelas ini.</div>`;
  return tabs+`<div class="row" style="margin-bottom:8px"><span class="muted small" style="margin-right:auto">Nilai akhir tiap bulan, dihitung terpisah. Rata-rata diambil dari bulan yang sudah ada nilainya. KKM ${S.kkm}.</span>
    <button class="btn ghost sm" onclick="exportRekap()">Ekspor CSV</button></div>
  <div class="tbl-wrap"><table><thead><tr><th class="stk1 num">No</th><th class="stk2">Murid</th>
    ${months.map((mo,j)=>`<th class="num"><button class="btn ghost sm" onclick="V.gMonth='${mo}';V.gAll=false;render()" title="Buka nilai bulan ini">${monthLabel(mo)}</button><div class="small muted" style="font-weight:400">${count[j]} pertemuan</div></th>`).join('')}
    <th class="num">Rata-rata</th></tr></thead><tbody>
    ${grid.map(({s,i,per,avg})=>`<tr><td class="stk1 num muted">${noOf(s,i)}</td><td class="stk2">${esc(s.name)}</td>${per.map(v=>`<td class="num fin ${v!=null&&v<S.kkm?'low':''}">${fmt(v)}</td>`).join('')}<td class="num fin ${avg!=null&&avg<S.kkm?'low':''}">${fmt(avg)}</td></tr>`).join('')}
    <tr><td class="stk1"></td><td class="stk2"><b>Rata-rata kelas</b></td>${colAvg.map(v=>`<td class="num muted">${fmt(v)}</td>`).join('')}<td class="num fin">${fmt(meanOf(grid.map(g=>g.avg)))}</td></tr>
  </tbody></table></div>`;
}
function exportRekap(){
  const {months,grid}=rekapData();
  const rows=[['No','Nama',...months.map(monthLabel),'Rata-rata']];
  grid.forEach(({s,i,per,avg})=>rows.push([noOf(s,i),s.name,...per.map(v=>v==null?'':fmt(v)),fmt(avg)]));
  download(`rekap-nilai-${V.subject}.csv`,rows.map(r=>r.map(csvCell).join(',')).join('\n'));
}

function addMeeting(){
  const all=meetingsOf(V.classId,V.subject),ms=meetingsOf(V.classId,V.subject,V.gMonth);
  const name=(V.nm.name||'').trim()||'Pertemuan '+(ms.length+1);
  const m={id:uid(),classId:V.classId,subject:V.subject,month:V.gMonth,name};S.meetings.push(m);
  const prev=ms[ms.length-1]||all[all.length-1];
  if(V.nm.copy&&prev)compsOf(prev).forEach(a=>{
    const c={id:uid(),classId:a.classId,subject:a.subject,meetingId:m.id,name:a.name,type:a.type,types:[a.type],weight:a.weight,source:'manual',manual:{}};
    S.assessments.push(c);S.scores[c.id]={};
  });
  V.nm.name='';V.nc.meetingId=m.id;save();render();
}
function addComp(){
  const ms=meetingsOf(V.classId,V.subject,V.gMonth);if(!ms.length)return;
  const m=ms.find(x=>x.id===V.nc.meetingId)||ms[ms.length-1];
  const used=compsOf(m).reduce((x,a)=>x+a.weight,0),typed=Math.round(+V.nc.weight);
  const w=typed>0?typed:(100-used>0?100-used:10);
  const a={id:uid(),classId:V.classId,subject:V.subject,meetingId:m.id,name:(V.nc.name||'').trim()||V.nc.jenis,type:V.nc.jenis,types:[V.nc.jenis],weight:w,source:'manual',manual:{}};
  S.assessments.push(a);S.scores[a.id]={};V.nc.name='';V.nc.weight='';V.nc.meetingId=m.id;save();render();
}
function renameMeeting(id){const m=S.meetings.find(x=>x.id===id);const n=prompt('Nama pertemuan',m.name);if(n&&n.trim()){m.name=n.trim();save();render()}}
function delMeeting(id){
  const m=S.meetings.find(x=>x.id===id);if(!confirm(`Hapus "${m.name}" beserta semua komponen dan nilainya?`))return;
  S.assessments.filter(a=>a.meetingId===id).forEach(a=>{delete S.scores[a.id];delete S.notes[a.id]});
  S.assessments=S.assessments.filter(a=>a.meetingId!==id);S.meetings=S.meetings.filter(x=>x.id!==id);save();render();
}
function setW(id,v){const a=S.assessments.find(x=>x.id===id);a.weight=Math.max(1,+v||1);save();render()}
function delAssess(id){const a=S.assessments.find(x=>x.id===id);if(!confirm(`Hapus penilaian "${a.name}" beserta semua nilainya?`))return;
  S.assessments=S.assessments.filter(x=>x.id!==id);delete S.scores[id];delete S.notes[id];save();render()}
function setScore(aid,sid,v){
  const a=S.assessments.find(x=>x.id===aid);S.scores[aid]=S.scores[aid]||{};
  if(v===''){delete S.scores[aid][sid]}else{S.scores[aid][sid]=Math.min(100,Math.max(0,+v))}
  a.manual=a.manual||{};a.manual[sid]=true;save();render();
}
function exportNilai(){
  const ms=meetingsOf(V.classId,V.subject,V.gMonth);
  const head=['No','Nama'];
  ms.forEach(m=>{compsOf(m).forEach(a=>head.push(`${m.name} - ${compLabel(a,m)} (${a.weight}%)`));head.push(`${m.name} - Total`)});
  head.push('Nilai akhir');
  const rows=[head];
  clsStudents(V.classId).forEach((s,i)=>{const r=[noOf(s,i),s.name];
    ms.forEach(m=>{compsOf(m).forEach(a=>r.push(S.scores[a.id]?.[s.id]??''));r.push(fmt(meetingTotal(m,s.id).v))});
    r.push(fmt(finalGrade(V.classId,V.subject,s.id,V.gMonth)));rows.push(r)});
  download(`nilai-${V.subject}-${V.gMonth}.csv`,rows.map(r=>r.map(csvCell).join(',')).join('\n'));
}

/* ============ Aksi: data ============ */
function addClass(){const n=$('#cName').value.trim();if(!n)return;const c={id:uid(),name:n};S.classes.push(c);V.classId=c.id;save();render()}
function delClass(){const c=S.classes.find(x=>x.id===V.classId);if(!confirm(`Hapus kelas ${c.name} beserta murid, absensi, dan nilainya?`))return;
  const aid=S.assessments.filter(a=>a.classId===c.id).map(a=>a.id);aid.forEach(i=>{delete S.scores[i];delete S.notes[i]});
  S.assessments=S.assessments.filter(a=>a.classId!==c.id);S.meetings=S.meetings.filter(m=>m.classId!==c.id);S.students=S.students.filter(s=>s.classId!==c.id);
  Object.keys(S.attendance).forEach(k=>{if(k.startsWith(c.id+'|'))delete S.attendance[k]});
  S.classes=S.classes.filter(x=>x.id!==c.id);V.classId=S.classes[0]?.id;save();render()}
function addStudent(){const n=$('#sName').value.trim();if(!n)return;S.students.push({id:uid(),nis:$('#sNis').value.trim()||String(clsStudents(V.classId).length+1),name:n,classId:V.classId});save();render()}
function bulkStudents(){
  const lines=$('#bulk').value.split('\n').map(l=>l.trim()).filter(Boolean);let n=0,cnt=clsStudents(V.classId).length;
  lines.forEach(l=>{const m=l.split(/[,;\t]/);const nis=m.length>1?m[0].trim():'';const name=(m.length>1?m.slice(1).join(' '):m[0]).trim();if(name){S.students.push({id:uid(),nis:nis||String(++cnt),name,classId:V.classId});n++}});
  save();render();toast(n+' murid ditambahkan');
}
function purgeStudents(ids){
  const set=new Set(ids);
  S.students=S.students.filter(s=>!set.has(s.id));
  for(const a in S.scores)ids.forEach(i=>{delete S.scores[a][i]});
  for(const a in S.notes)ids.forEach(i=>{delete S.notes[a][i]});
  for(const k in S.attendance)ids.forEach(i=>{delete S.attendance[k][i]});
  ids.forEach(i=>{delete V.selStu[i]});
  save();render();
}
function delStudent(id){
  const s=S.students.find(x=>x.id===id);
  if(!s||!confirm(`Hapus "${s.name}" beserta absensi dan nilainya?`))return;
  purgeStudents([id]);toast('Murid dihapus');
}
function toggleStu(id,on){if(on)V.selStu[id]=true;else delete V.selStu[id];render()}
function selectAllStu(on){clsStudents(V.classId).forEach(s=>{if(on)V.selStu[s.id]=true;else delete V.selStu[s.id]});render()}
function delSelectedStu(){
  const ids=clsStudents(V.classId).filter(s=>V.selStu[s.id]).map(s=>s.id);if(!ids.length)return;
  if(!confirm(`Hapus ${ids.length} murid terpilih beserta absensi dan nilainya? Tindakan ini tidak bisa dibatalkan.`))return;
  purgeStudents(ids);toast(ids.length+' murid dihapus');
}
function delAllStu(){
  const c=S.classes.find(x=>x.id===V.classId),ids=clsStudents(V.classId).map(s=>s.id);if(!ids.length)return;
  if(!confirm(`Hapus SEMUA ${ids.length} murid di kelas ${c.name} beserta absensi dan nilainya? Tindakan ini tidak bisa dibatalkan.`))return;
  purgeStudents(ids);toast('Semua murid di '+c.name+' dihapus');
}
function removeStuRow(i){V.stu.rows.splice(i,1);if(!V.stu.rows.length)V.stu=null;render()}
function addSubject(){const n=$('#mName').value.trim();if(!n||S.subjects.includes(n))return;S.subjects.push(n);V.subject=n;save();render()}
function backup(){download('data-nilai-cadangan.json',JSON.stringify(S),'application/json')}
function restore(f){if(!f)return;f.text().then(t=>{try{S=fixS(JSON.parse(t.replace(/^\ufeff/,'')));save();V.classId=S.classes[0]?.id;V.subject=S.subjects[0];render();toast('Data dipulihkan')}catch(e){toast('Berkas cadangan tidak valid')}})}
function resetAll(){if(!confirm('Hapus SEMUA data di browser ini? Tindakan ini tidak bisa dibatalkan.'))return;S={classes:[],students:[],subjects:['Informatika'],meetings:[],assessments:[],scores:{},notes:{},attendance:{},kkm:75,clientId:''};V.classId=undefined;V.subject='Informatika';save();render()}

/* ============ Impor Google Form ============ */
function formIdFromLink(l){const m=String(l).match(/\/forms\/d\/(?:e\/)?([\w-]{15,})/);return m?m[1]:''}

function getToken(clientId){
  return new Promise((res,rej)=>{
    const go=()=>{try{
      google.accounts.oauth2.initTokenClient({client_id:clientId,
        scope:'https://www.googleapis.com/auth/forms.body.readonly https://www.googleapis.com/auth/forms.responses.readonly',
        callback:r=>r.error?rej(new Error('Izin Google ditolak: '+r.error)):res(r.access_token)}).requestAccessToken();
    }catch(e){rej(e)}};
    if(window.google?.accounts?.oauth2)return go();
    const s=document.createElement('script');s.src='https://accounts.google.com/gsi/client';s.onload=go;
    s.onerror=()=>rej(new Error('Tidak bisa memuat layanan login Google. Periksa koneksi internet.'));document.head.appendChild(s);
  });
}
async function gfetch(url,token){
  const r=await fetch(url,{headers:{Authorization:'Bearer '+token}});
  if(!r.ok){let m='';try{m=(await r.json()).error.message}catch(e){}throw new Error(`Google menolak permintaan (${r.status}). ${m}`)}
  return r.json();
}
async function fetchAPI(){
  V.err='';const id=formIdFromLink(V.imp.link);
  if(!id){V.err='Link form tidak dikenali. Salin link dari bilah alamat saat membuka form di mode edit.';return render()}
  if(!S.clientId.trim()){V.err='Isi OAuth Client ID terlebih dahulu.';return render()}
  V.busy=true;render();
  try{
    const token=await getToken(S.clientId.trim());
    const form=await gfetch(`https://forms.googleapis.com/v1/forms/${id}`,token);
    const questions=[];let max=0;
    (form.items||[]).forEach(it=>{const q=it.questionItem?.question;if(!q)return;
      questions.push({id:q.questionId,title:it.title||'(tanpa judul)'});max+=q.grading?.pointValue||0});
    let resp=[],pt='';
    do{const d=await gfetch(`https://forms.googleapis.com/v1/forms/${id}/responses?pageSize=500${pt?'&pageToken='+pt:''}`,token);resp=resp.concat(d.responses||[]);pt=d.nextPageToken||''}while(pt);
    const responses=resp.map(r=>{const vals={};
      Object.entries(r.answers||{}).forEach(([qid,a])=>{vals[qid]=(a.textAnswers?.answers||[]).map(x=>x.value).join(', ')});
      if(r.respondentEmail)vals.__email=r.respondentEmail;
      return {vals,raw:r.totalScore,time:Date.parse(r.lastSubmittedTime||r.createTime)||0}}).sort((a,b)=>a.time-b.time);
    if(!max)max=100;
    responses.forEach(r=>r.score=r.raw==null?null:r.raw/max*100);
    if(responses.some(r=>r.vals.__email))questions.push({id:'__email',title:'Email responden'});
    startPreview({formId:id,title:form.info?.title||'',questions,responses,max});
  }catch(e){V.err=e.message}
  V.busy=false;render();
}

function parseCSV(t){
  const rows=[];let r=[],f='',q=false;
  for(let i=0;i<t.length;i++){const c=t[i];
    if(q){if(c==='"'){if(t[i+1]==='"'){f+='"';i++}else q=false}else f+=c}
    else if(c==='"')q=true;else if(c===','||c===';'){r.push(f);f=''}
    else if(c==='\n'){r.push(f);rows.push(r);r=[];f=''}else if(c!=='\r')f+=c}
  if(f!==''||r.length){r.push(f);rows.push(r)}
  return rows.filter(x=>x.some(v=>v.trim()!==''));
}
function readCSVFile(f){if(!f)return;f.text().then(t=>{V.imp.csv=t.replace(/^\ufeff/,'');loadCSV()})}
function loadCSV(){
  V.err='';const rows=parseCSV(V.imp.csv||'');
  if(rows.length<2){V.err='CSV kosong atau tidak terbaca.';return render()}
  const head=rows[0].map(h=>h.trim());
  let sc=head.findIndex(h=>/^(score|skor|nilai|poin|total)/i.test(h));
  if(sc<0){V.err='Kolom skor tidak ditemukan. Pastikan ada kolom bernama Skor/Score.';return render()}
  let max=0;const parsed=rows.slice(1).map((r,idx)=>{
    const cell=(r[sc]||'').trim(),m=cell.match(/(-?\d+(?:[.,]\d+)?)\s*\/\s*(\d+(?:[.,]\d+)?)/);
    let s=null,mx=null;
    if(m){s=+m[1].replace(',','.');mx=+m[2].replace(',','.')}else if(cell!==''&&!isNaN(+cell.replace(',','.'))){s=+cell.replace(',','.')}
    if(mx)max=Math.max(max,mx);
    const vals={};head.forEach((h,i)=>{vals[i]=(r[i]||'').trim()});
    return {vals,raw:s,time:idx}});
  if(!max)max=100;
  parsed.forEach(r=>r.score=r.raw==null?null:r.raw/max*100);
  const questions=head.map((h,i)=>({id:String(i),title:h||'(kolom '+(i+1)+')'})).filter((q,i)=>i!==sc);
  startPreview({formId:'',title:'',questions,responses:parsed,max});
  render();
}
function loadDemo(){
  const sts=clsStudents(V.classId);
  if(!sts.length){V.err='Kelas ini belum punya murid.';return render()}
  const responses=[];
  sts.forEach((s,i)=>{if(i%5===4)return;
    const sc=50+((i*13)%50);
    responses.push({vals:{nis:s.nis,nama:i%4===1?s.name.toLowerCase():s.name},raw:sc/10,time:i});
    if(i===2)responses.push({vals:{nis:s.nis,nama:s.name},raw:Math.min(10,sc/10+1.5),time:100+i})});
  responses.push({vals:{nis:'999999',nama:'Murid Tidak Dikenal'},raw:7,time:200});
  if(sts[0])responses.push({vals:{nis:'',nama:sts[0].name.split(' ')[0]+' P.'},raw:6,time:201});
  responses.forEach(r=>r.score=r.raw/10*100);
  startPreview({formId:'',title:'Kuis contoh',questions:[{id:'nis',title:'Nomor absen'},{id:'nama',title:'Nama lengkap'}],responses,max:10});
  render();
}
function startPreview(im){
  im.idQ=(im.questions.find(q=>/nomor|absen|\bnisn?\b|\bno\b/i.test(q.title))||im.questions.find(q=>/nama|name|email/i.test(q.title))||im.questions[0])?.id;
  im.policy='max';im.assign={};
  if(!V.imp.name)V.imp.name=im.title||'Kuis Google Form';
  V.im=im;
}
function assign(i,sid){V.im.assign[i]=sid||'';render()}

function computeMatches(){
  const im=V.im,sts=clsStudents(V.classId);
  const rows=im.responses.map((r,i)=>{
    const raw=String(r.vals[im.idQ]??'').trim();let st=null,how='';
    if(im.assign[i]){st=sts.find(s=>s.id===im.assign[i]);how='manual'}
    else if(raw){
      const rn=raw.replace(/^0+(?=\d)/,'');st=sts.find(s=>s.nis&&String(s.nis).replace(/^0+(?=\d)/,'')===rn);how=st?'No':'';
      if(!st){const n=norm(raw);
        st=sts.find(s=>norm(s.name)===n);if(st)how='nama';
        else if(n.length>=4){st=sts.find(s=>{const m=norm(s.name);return m.includes(n)||n.includes(m)});if(st)how='mirip'}}
    }
    return {i,raw,st,how,score:r.score};
  });
  const pick={};
  rows.forEach(r=>{if(!r.st||r.score==null)return;const p=pick[r.st.id];
    if(!p||(im.policy==='max'&&r.score>p.score)||im.policy==='last')pick[r.st.id]=r});
  return {rows,pick,missing:sts.filter(s=>!pick[s.id])};
}

function saveImport(){
  const im=V.im,p=V.imp,{pick}=computeMatches();
  let a=im.formId&&S.assessments.find(x=>x.formId===im.formId&&x.classId===V.classId&&x.subject===V.subject),m;
  if(a){m=S.meetings.find(x=>x.id===a.meetingId)}
  else{
    const ms=meetingsOf(V.classId,V.subject,V.gMonth);
    m=ms.find(x=>x.id===(p.meetingId||ms[ms.length-1]?.id));
    if(!m){m={id:uid(),classId:V.classId,subject:V.subject,month:V.gMonth,name:'Pertemuan '+(ms.length+1)};S.meetings.push(m)}
    const used=compsOf(m).reduce((x,c)=>x+c.weight,0),typed=Math.round(+p.weight);
    a={id:uid(),classId:V.classId,subject:V.subject,meetingId:m.id,name:(p.name||'').trim()||im.title||p.type,type:p.type,types:[p.type],
       weight:typed>0?typed:(100-used>0?100-used:10),source:'google_form',formId:im.formId||'',manual:{}};
    S.assessments.push(a);S.scores[a.id]={};
  }
  let n=0,skip=0;
  Object.entries(pick).forEach(([sid,r])=>{if(a.manual?.[sid]){skip++;return}S.scores[a.id][sid]=Math.round(r.score*10)/10;n++});
  a.syncedAt=Date.now();save();V.im=null;V.imp.name='';V.imp.meetingId='';V.tab='nilai';V.gAll=false;render();
  toast(`${n} nilai masuk ke ${m.name}: ${compLabel(a,m)}`+(skip?` (${skip} nilai yang diedit manual tidak ditimpa)`:''));
}

/* ============ Impor murid dari file ============ */
V.stu=null;V.selStu={};V.nm={name:'',copy:true};V.nc={meetingId:'',jenis:'Catatan',name:'',weight:''};V.gMonth=today().slice(0,7);V.gAll=false;
function loadXLSX(){
  return new Promise((res,rej)=>{
    if(window.XLSX)return res();
    const s=document.createElement('script');s.src='https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js';
    s.onload=res;s.onerror=()=>rej(new Error('Pembaca Excel gagal dimuat (butuh internet). Simpan file sebagai CSV lalu unggah lagi.'));
    document.head.appendChild(s);
  });
}
function gridToStudents(grid){
  grid=grid.map(r=>r.map(c=>String(c??'').trim())).filter(r=>r.some(Boolean));
  if(!grid.length)return [];
  const h=grid[0].map(x=>x.toLowerCase());
  let ni=h.findIndex(x=>/^(no\b|nomor|nis|nisn|absen)/.test(x)),nm=h.findIndex(x=>/nama|name/.test(x)),start=0;
  if(nm>=0){start=1}
  else if(grid[0].length>1){
    ni=0;nm=1;
    if(/^\d+$/.test(grid[0][1])&&!/^\d+$/.test(grid[0][0])){ni=1;nm=0}
  }else{ni=-1;nm=0}
  return grid.slice(start).map(r=>({nis:ni>=0?(r[ni]||''):'',name:r[nm]||''})).filter(r=>r.name);
}
async function readStudentFile(f){
  if(!f)return;
  try{
    const ext=(f.name.split('.').pop()||'').toLowerCase();let grid;
    if(ext==='xlsx'||ext==='xls'){
      await loadXLSX();
      const wb=XLSX.read(await f.arrayBuffer(),{type:'array'});
      grid=XLSX.utils.sheet_to_json(wb.Sheets[wb.SheetNames[0]],{header:1,raw:false,defval:''});
    }else{
      let t=(await f.text()).replace(/^\ufeff/,'');
      if(t.includes('\t'))t=t.replace(/\t/g,',');
      grid=parseCSV(t);
    }
    const rows=gridToStudents(grid);
    if(!rows.length){toast('Tidak ada nama murid yang terbaca di file ini');return}
    V.stu={file:f.name,rows};render();
  }catch(e){toast(e.message||'File tidak bisa dibaca')}
}
function stuCompute(){
  const seenN=new Set(clsStudents(V.classId).map(s=>norm(s.name)));
  return V.stu.rows.map(r=>{
    const dup=seenN.has(norm(r.name));
    if(!dup)seenN.add(norm(r.name));
    return {...r,dup};
  });
}
function stuPreviewHTML(){
  if(!V.stu)return '';
  const rows=stuCompute(),n=rows.filter(r=>!r.dup).length,d=rows.length-n;
  return `<div class="panel" style="margin:12px 0 0;background:var(--kertas)">
    <p style="margin:0 0 8px"><b>${esc(V.stu.file)}</b>: ${rows.length} baris terbaca, <b>${n}</b> murid baru${d?`, ${d} dilewati karena namanya sudah ada`:''}. Klik × untuk membuang nama yang tidak diinginkan sebelum ditambahkan.</p>
    <div class="scroll"><table><thead><tr><th class="num">No</th><th>Nama</th><th>Status</th><th></th></tr></thead><tbody>
    ${rows.map((r,i)=>`<tr><td>${esc(r.nis)||'<span class="muted">–</span>'}</td><td>${esc(r.name)}</td><td>${r.dup?'<span class="badge warn">Sudah ada</span>':'<span class="badge ok">Baru</span>'}</td><td style="text-align:right"><button class="btn danger sm" style="padding:0 8px;min-height:24px" onclick="removeStuRow(${i})" aria-label="Buang ${esc(r.name)} dari daftar">×</button></td></tr>`).join('')}
    </tbody></table></div>
    <div class="row" style="margin-top:10px"><button class="btn" onclick="saveStudentImport()" ${n?'':'disabled'}>Tambahkan ${n} murid</button><button class="btn ghost" onclick="V.stu=null;render()">Batal</button></div>
  </div>`;
}
function saveStudentImport(){
  const rows=stuCompute().filter(r=>!r.dup);
  let cnt=clsStudents(V.classId).length;rows.forEach(r=>S.students.push({id:uid(),nis:r.nis||String(++cnt),name:r.name,classId:V.classId}));
  V.stu=null;save();render();toast(rows.length+' murid ditambahkan');
}
function downloadStudentTemplate(){
  download('templat-murid.csv','No,Nama\n1,Aditya Pratama\n2,Bunga Lestari');
}

/* ============ Tema dongeng: karakter, latar, hero ============ */
const CH={
 owl:{w:90,h:100,g:`<ellipse cx="45" cy="60" rx="30" ry="33" fill="#b79af0"/>
  <path d="M22 36 L16 14 L36 28Z M68 36 L74 14 L54 28Z" fill="#9d7de0" stroke="#9d7de0" stroke-width="4" stroke-linejoin="round"/>
  <ellipse cx="45" cy="70" rx="19" ry="22" fill="#efe6ff"/>
  <path d="M37 64 q4 5 8 0 q4 5 8 0 M37 75 q4 5 8 0 q4 5 8 0" stroke="#cdb9f5" stroke-width="2.5" fill="none" stroke-linecap="round"/>
  <ellipse cx="14" cy="64" rx="8" ry="18" fill="#9d7de0" transform="rotate(12 14 64)"/><ellipse cx="76" cy="64" rx="8" ry="18" fill="#9d7de0" transform="rotate(-12 76 64)"/>
  <circle cx="32" cy="44" r="13" fill="#fff" stroke="#ff8fb8" stroke-width="4"/><circle cx="58" cy="44" r="13" fill="#fff" stroke="#ff8fb8" stroke-width="4"/><path d="M43 44 H47" stroke="#ff8fb8" stroke-width="4"/>
  <circle cx="33" cy="45" r="5.5" fill="#1a2b4d"/><circle cx="57" cy="45" r="5.5" fill="#1a2b4d"/><circle cx="35" cy="43" r="1.8" fill="#fff"/><circle cx="59" cy="43" r="1.8" fill="#fff"/>
  <path d="M45 52 L40 60 H50Z" fill="#ffb347" stroke="#ffb347" stroke-width="2" stroke-linejoin="round"/>
  <circle cx="22" cy="57" r="3.5" fill="#ff9fc0" opacity=".8"/><circle cx="68" cy="57" r="3.5" fill="#ff9fc0" opacity=".8"/>
  <path d="M36 92 V97 M40 92 V97 M50 92 V97 M54 92 V97" stroke="#ffb347" stroke-width="4" stroke-linecap="round"/>`},
 bunny:{w:90,h:120,g:`<ellipse cx="33" cy="24" rx="8" ry="22" fill="#fff" stroke="#dfe8f5" stroke-width="2.5" transform="rotate(-8 33 24)"/><ellipse cx="33" cy="26" rx="4" ry="15" fill="#ffc6d6" transform="rotate(-8 33 24)"/>
  <ellipse cx="57" cy="24" rx="8" ry="22" fill="#fff" stroke="#dfe8f5" stroke-width="2.5" transform="rotate(8 57 24)"/><ellipse cx="57" cy="26" rx="4" ry="15" fill="#ffc6d6" transform="rotate(8 57 24)"/>
  <ellipse cx="45" cy="96" rx="22" ry="24" fill="#fff" stroke="#dfe8f5" stroke-width="2.5"/>
  <circle cx="45" cy="58" r="23" fill="#fff" stroke="#dfe8f5" stroke-width="2.5"/>
  <circle cx="36" cy="56" r="9" fill="#fff" fill-opacity=".6" stroke="#f2a43a" stroke-width="3"/><circle cx="54" cy="56" r="9" fill="#fff" fill-opacity=".6" stroke="#f2a43a" stroke-width="3"/><path d="M44 56 H46" stroke="#f2a43a" stroke-width="3"/>
  <circle cx="36" cy="57" r="3.5" fill="#1a2b4d"/><circle cx="54" cy="57" r="3.5" fill="#1a2b4d"/><circle cx="37" cy="55.8" r="1.2" fill="#fff"/><circle cx="55" cy="55.8" r="1.2" fill="#fff"/>
  <ellipse cx="45" cy="66" rx="3.5" ry="2.6" fill="#ff8fa8"/><path d="M40 70 Q45 75 50 70" stroke="#1a2b4d" stroke-width="2.2" fill="none" stroke-linecap="round"/>
  <circle cx="29" cy="68" r="4" fill="#ffc6d6"/><circle cx="61" cy="68" r="4" fill="#ffc6d6"/>
  <path d="M36 80 L45 85 L36 90Z M54 80 L45 85 L54 90Z" fill="#ffd23f"/><circle cx="45" cy="85" r="3" fill="#ffb300"/>
  <rect x="26" y="94" width="38" height="24" rx="4" fill="#4a9bff"/><rect x="29" y="97" width="32" height="18" rx="2" fill="#fff"/><path d="M45 97 V115" stroke="#cfe0ff" stroke-width="2"/>
  <path d="M33 102 H42 M33 107 H42 M48 102 H57 M48 107 H57" stroke="#9db8e8" stroke-width="2" stroke-linecap="round"/>
  <circle cx="25" cy="98" r="5" fill="#fff" stroke="#dfe8f5" stroke-width="2"/><circle cx="65" cy="98" r="5" fill="#fff" stroke="#dfe8f5" stroke-width="2"/>`},
 dragon:{w:110,h:110,g:`<path d="M80 80 Q104 76 100 58 Q98 50 92 54" stroke="#62b6ff" stroke-width="10" stroke-linecap="round" fill="none"/>
  <path d="M70 52 Q98 26 102 54 Q92 50 86 60 Q84 52 70 64Z" fill="#9db8ff"/>
  <ellipse cx="52" cy="76" rx="30" ry="29" fill="#62b6ff"/><ellipse cx="52" cy="82" rx="19" ry="21" fill="#d9efff"/>
  <path d="M34 54 L38 44 L42 54Z M60 54 L65 44 L69 56Z" fill="#ffb347"/>
  <circle cx="50" cy="38" r="23" fill="#62b6ff"/>
  <path d="M36 20 L32 8 L44 16Z M62 20 L68 8 L56 16Z" fill="#ffd23f" stroke="#ffd23f" stroke-width="3" stroke-linejoin="round"/>
  <ellipse cx="50" cy="48" rx="12" ry="8" fill="#d9efff"/>
  <circle cx="42" cy="34" r="5" fill="#fff"/><circle cx="58" cy="34" r="5" fill="#fff"/><circle cx="43" cy="35" r="2.8" fill="#1a2b4d"/><circle cx="57" cy="35" r="2.8" fill="#1a2b4d"/><circle cx="44" cy="34" r="1" fill="#fff"/><circle cx="58" cy="34" r="1" fill="#fff"/>
  <circle cx="46" cy="47" r="1.4" fill="#4a7fc8"/><circle cx="54" cy="47" r="1.4" fill="#4a7fc8"/>
  <path d="M44 53 Q50 58 56 53" stroke="#1a2b4d" stroke-width="2.2" fill="none" stroke-linecap="round"/>
  <circle cx="33" cy="44" r="3.5" fill="#ff9fb3"/><circle cx="67" cy="44" r="3.5" fill="#ff9fb3"/>
  <rect x="34" y="82" width="36" height="22" rx="3" fill="#ff6b5e"/><rect x="37" y="85" width="30" height="16" rx="2" fill="#fff"/><path d="M52 85 V101" stroke="#cfe0ff" stroke-width="2"/>
  <circle cx="32" cy="90" r="6" fill="#62b6ff"/><circle cx="72" cy="90" r="6" fill="#62b6ff"/>
  <ellipse cx="40" cy="104" rx="9" ry="5" fill="#4a9de8"/><ellipse cx="64" cy="104" rx="9" ry="5" fill="#4a9de8"/>`},
 fox:{w:100,h:110,g:`<ellipse cx="82" cy="84" rx="12" ry="24" fill="#ff9a3d" transform="rotate(35 82 84)"/><ellipse cx="92" cy="100" rx="6" ry="9" fill="#fff" transform="rotate(35 92 100)"/>
  <ellipse cx="50" cy="88" rx="22" ry="22" fill="#ff9a3d"/><ellipse cx="50" cy="94" rx="13" ry="16" fill="#fff4e4"/>
  <path d="M24 38 L22 10 L42 28Z M76 38 L78 10 L58 28Z" fill="#ff9a3d" stroke="#ff9a3d" stroke-width="4" stroke-linejoin="round"/>
  <path d="M27 32 L26 18 L36 28Z M73 32 L74 18 L64 28Z" fill="#7a3b1e"/>
  <ellipse cx="50" cy="50" rx="28" ry="23" fill="#ff9a3d"/>
  <path d="M22 54 Q34 72 50 66 Q66 72 78 54 Q70 76 50 76 Q30 76 22 54Z" fill="#fff4e4"/>
  <circle cx="38" cy="46" r="4" fill="#1a2b4d"/><circle cx="62" cy="46" r="4" fill="#1a2b4d"/><circle cx="39.2" cy="44.8" r="1.3" fill="#fff"/><circle cx="63.2" cy="44.8" r="1.3" fill="#fff"/>
  <ellipse cx="50" cy="58" rx="4" ry="3" fill="#1a2b4d"/><path d="M44 63 Q50 69 56 63" stroke="#1a2b4d" stroke-width="2.2" fill="none" stroke-linecap="round"/>
  <circle cx="30" cy="56" r="3.5" fill="#ff8f7a" opacity=".8"/><circle cx="70" cy="56" r="3.5" fill="#ff8f7a" opacity=".8"/>
  <rect x="58" y="76" width="20" height="30" rx="4" fill="#3b6fd8"/><rect x="60" y="79" width="16" height="22" rx="2" fill="#bfe0ff"/><path d="M63 84 H73 M63 89 H73 M63 94 H69" stroke="#fff" stroke-width="2" stroke-linecap="round"/>
  <circle cx="60" cy="100" r="5" fill="#ff9a3d"/>`},
 monster:{w:90,h:100,g:`<ellipse cx="34" cy="94" rx="9" ry="5" fill="#ffb347"/><ellipse cx="58" cy="94" rx="9" ry="5" fill="#ffb347"/>
  <ellipse cx="45" cy="60" rx="30" ry="34" fill="#8f6be0"/>
  <path d="M22 32 L18 14 L34 26Z M68 32 L72 14 L56 26Z" fill="#ffd23f" stroke="#ffd23f" stroke-width="3" stroke-linejoin="round"/>
  <ellipse cx="45" cy="74" rx="20" ry="18" fill="#b79af0"/>
  <circle cx="34" cy="46" r="9" fill="#fff"/><circle cx="56" cy="46" r="9" fill="#fff"/><circle cx="35" cy="47" r="4.5" fill="#1a2b4d"/><circle cx="55" cy="47" r="4.5" fill="#1a2b4d"/><circle cx="36.5" cy="45" r="1.5" fill="#fff"/><circle cx="56.5" cy="45" r="1.5" fill="#fff"/>
  <path d="M30 58 Q45 78 60 58Z" fill="#4b2a8f"/><path d="M36 58 H42 V63 H36Z M48 58 H54 V63 H48Z" fill="#fff"/><ellipse cx="45" cy="68" rx="6" ry="3.5" fill="#ff7a9a"/>
  <ellipse cx="14" cy="64" rx="7" ry="13" fill="#8f6be0" transform="rotate(20 14 64)"/>
  <rect x="52" y="62" width="30" height="24" rx="4" fill="#243f9e"/><rect x="55" y="65" width="24" height="18" rx="2" fill="#dff0ff"/><path d="M58 70 H76 M58 75 H72 M58 80 H68" stroke="#4a9bff" stroke-width="2" stroke-linecap="round"/>
  <circle cx="52" cy="82" r="5" fill="#8f6be0"/>`},
 bird:{w:70,h:60,g:`<path d="M12 36 L0 30 L2 44Z" fill="#2f86e6"/>
  <ellipse cx="32" cy="36" rx="22" ry="17" fill="#4aa8ff"/><ellipse cx="34" cy="42" rx="13" ry="9" fill="#d9efff"/>
  <ellipse cx="26" cy="34" rx="10" ry="6" fill="#2f86e6" transform="rotate(-20 26 34)"/>
  <circle cx="50" cy="24" r="14" fill="#4aa8ff"/><path d="M61 22 L70 26 L61 30Z" fill="#ffb347"/>
  <circle cx="53" cy="21" r="3.2" fill="#1a2b4d"/><circle cx="54" cy="20" r="1.1" fill="#fff"/><circle cx="48" cy="29" r="3" fill="#ff9fb3" opacity=".8"/>
  <path d="M28 51 V57 M36 51 V57" stroke="#ffb347" stroke-width="3" stroke-linecap="round"/>`}
};
const chSvg=n=>`<svg viewBox="0 0 ${CH[n].w} ${CH[n].h}" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">${CH[n].g}</svg>`;
const ch=(n,cx,yb,w,cls='')=>{const c=CH[n],h=w*c.h/c.w;return `<g class="${cls}"><svg x="${cx-w/2}" y="${yb-h}" width="${w}" height="${h}" viewBox="0 0 ${c.w} ${c.h}">${c.g}</svg></g>`};

const ICON={
 logo:`<svg viewBox="0 0 64 56" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><path d="M32 14 Q20 6 4 10 V46 Q20 42 32 50Z" fill="#3b8cff"/><path d="M32 14 Q44 6 60 10 V46 Q44 42 32 50Z" fill="#2a6fdb"/><path d="M32 18 Q22 12 9 15 V41 Q22 38 32 44Z" fill="#fff"/><path d="M32 18 Q42 12 55 15 V41 Q42 38 32 44Z" fill="#eaf4ff"/><polygon points="32,0 35,7 42,8 37,13 38,20 32,16 26,20 27,13 22,8 29,7" fill="#ffd23f" stroke="#ffb300" stroke-width="1.5" stroke-linejoin="round"/></svg>`,
 check:`<svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><rect x="12" y="8" width="40" height="50" rx="7" fill="#fff" stroke="#6aaeff" stroke-width="4"/><rect x="22" y="4" width="20" height="12" rx="5" fill="#ffd23f" stroke="#e0a800" stroke-width="2"/><path d="M20 30 L28 38 L44 22" stroke="#2a6fdb" stroke-width="6" fill="none" stroke-linecap="round" stroke-linejoin="round"/><path d="M20 48 H44" stroke="#bcd7ff" stroke-width="4" stroke-linecap="round"/></svg>`,
 star:`<svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><polygon points="32,6 39.5,23 58,25 44,37.5 48,56 32,46.5 16,56 20,37.5 6,25 24.5,23" fill="#ffcf3f" stroke="#f2a900" stroke-width="4" stroke-linejoin="round"/><circle cx="26" cy="31" r="2.6" fill="#7a4b00"/><circle cx="38" cy="31" r="2.6" fill="#7a4b00"/><path d="M27 38 Q32 43 37 38" stroke="#7a4b00" stroke-width="2.6" fill="none" stroke-linecap="round"/></svg>`,
 cal:`<svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><rect x="7" y="12" width="50" height="46" rx="8" fill="#fff" stroke="#9a7df0" stroke-width="4"/><path d="M7 26 V20 Q7 12 15 12 H49 Q57 12 57 20 V26Z" fill="#9a7df0"/><path d="M20 6 V16 M44 6 V16" stroke="#6f55d0" stroke-width="5" stroke-linecap="round"/><g fill="#c8b8f8"><rect x="14" y="32" width="9" height="8" rx="2"/><rect x="27" y="32" width="9" height="8" rx="2"/><rect x="40" y="32" width="9" height="8" rx="2"/><rect x="14" y="44" width="9" height="8" rx="2"/></g><rect x="27" y="44" width="9" height="8" rx="2" fill="#ffd23f"/></svg>`,
 doc:`<svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><path d="M14 6 H38 L52 20 V56 Q52 60 48 60 H18 Q14 60 14 56Z" fill="#fff" stroke="#ff8fb0" stroke-width="4" stroke-linejoin="round"/><path d="M38 6 V20 H52" fill="#ffd6e2" stroke="#ff8fb0" stroke-width="4" stroke-linejoin="round"/><path d="M22 32 H44 M22 40 H44" stroke="#ffc2d3" stroke-width="4" stroke-linecap="round"/><circle cx="42" cy="48" r="10" fill="#3b8cff"/><path d="M42 43 V53 M37 48 L42 53 L47 48" stroke="#fff" stroke-width="3" fill="none" stroke-linecap="round" stroke-linejoin="round"/></svg>`,
 people:`<svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><circle cx="22" cy="22" r="10" fill="#ffd9b0"/><path d="M4 56 Q4 36 22 36 Q40 36 40 56Z" fill="#4a9bff"/><circle cx="44" cy="26" r="9" fill="#ffc9a0"/><path d="M28 58 Q28 40 44 40 Q60 40 60 58Z" fill="#ff8fb0"/><path d="M13 20 Q22 8 31 20 Q22 14 13 20Z" fill="#7a4a2b"/><circle cx="19" cy="23" r="1.6" fill="#1a2b4d"/><circle cx="25" cy="23" r="1.6" fill="#1a2b4d"/></svg>`,
 cloud:`<svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><g fill="#bfe0ff" stroke="#6aaeff" stroke-width="3"><circle cx="22" cy="38" r="12"/><circle cx="38" cy="30" r="16"/><circle cx="50" cy="40" r="10"/><rect x="14" y="38" width="42" height="12" rx="6" stroke="none"/></g><rect x="14" y="38" width="42" height="11" rx="5" fill="#bfe0ff"/><path d="M34 52 V36 M28 42 L34 36 L40 42" stroke="#2a6fdb" stroke-width="4" fill="none" stroke-linecap="round" stroke-linejoin="round"/></svg>`
};
const tilesHTML=()=>`<h2 class="sect-title">Mau mulai dari mana?</h2>
<div class="tiles">
 <button class="tile" style="--bg:#fff0cf" onclick="go('absensi')">${ICON.check}<b>Absensi</b><span>Catat kehadiran hari ini</span></button>
 <button class="tile" style="--bg:#e1f0ff" onclick="V.gAll=false;go('nilai')">${ICON.star}<b>Nilai</b><span>Isi nilai per pertemuan</span></button>
 <button class="tile" style="--bg:#efe6ff" onclick="V.gAll=true;go('nilai')">${ICON.cal}<b>Rekap Bulanan</b><span>Nilai tiap bulan terpisah</span></button>
 <button class="tile" style="--bg:#ffe6ee" onclick="go('impor')">${ICON.doc}<b>Impor Form</b><span>Tarik nilai dari Google Form</span></button>
 <button class="tile" style="--bg:#dff4ff" onclick="go('data')">${ICON.people}<b>Murid &amp; Kelas</b><span>Tambah, impor, atau hapus</span></button>
 <button class="tile" style="--bg:#fff4d6" onclick="go('data')">${ICON.cloud}<b>Cadangan</b><span>Simpan salinan data</span></button>
</div>`;

const wv=(y,amp,fill,op=1,cls='')=>`<g class="drift ${cls}"><path d="M-300 ${y} q75 ${-amp} 150 0${' t150 0'.repeat(11)} V820 H-300Z" fill="${fill}" opacity="${op}"/></g>`;
const cloud=(x,y,sc=1,fill='#fff',op=.92)=>`<g transform="translate(${x} ${y}) scale(${sc})"><g class="cloud" fill="${fill}" opacity="${op}"><circle cx="28" cy="34" r="20"/><circle cx="60" cy="22" r="26"/><circle cx="92" cy="34" r="20"/><ellipse cx="60" cy="42" rx="58" ry="14"/></g></g>`;
const grad=(id,stops)=>`<linearGradient id="${id}" x1="0" y1="0" x2="0" y2="1">${stops.map(([o,c])=>`<stop offset="${o}" stop-color="${c}"/>`).join('')}</linearGradient>`;
const stars=(n,maxY,seed=7)=>Array.from({length:n},(_,i)=>{const x=(i*263+seed*37)%1200,y=(i*149+seed*53)%maxY,r=1+((i*7)%3)*.6;return `<circle class="twinkle" style="animation-delay:-${(i%7)*.5}s" cx="${x}" cy="${y}" r="${r}" fill="#fff" opacity=".85"/>`}).join('');
const sparkle=(x,y,sc=1,fill='#ffe27a')=>`<path class="twinkle" style="animation-delay:-${(x%5)*.6}s" transform="translate(${x} ${y}) scale(${sc})" d="M0 -10 Q2 -2 10 0 Q2 2 0 10 Q-2 2 -10 0 Q-2 -2 0 -10Z" fill="${fill}"/>`;
const DAY={top:'#eaf4ff',rock:'#a3b4e6',castle:'#bdaaf0',roof:'#7a63d6',win:false};
const NIGHT={top:'#2a4396',rock:'#1a2c6e',castle:'#2c3f94',roof:'#4a5fc8',win:true};
const DUSK={top:'#8a78d6',rock:'#4a3a9a',castle:'#5b46b0',roof:'#3a2a82',win:false};
const island=(x,y,sc=1,c=DAY)=>`<g transform="translate(${x} ${y}) scale(${sc})"><g class="bobsm">
 <path d="M-70 0 Q-60 50 0 70 Q60 50 70 0Z" fill="${c.rock}"/><path d="M-14 40 V70 M0 44 V72 M14 40 V68" stroke="#fff" stroke-width="3" opacity=".55" stroke-linecap="round"/>
 <ellipse cx="0" cy="0" rx="72" ry="14" fill="${c.top}"/>
 <g fill="${c.castle}"><rect x="-28" y="-46" width="16" height="44"/><rect x="-10" y="-62" width="20" height="60"/><rect x="12" y="-40" width="16" height="38"/></g>
 <path d="M-30 -46 L-20 -64 L-10 -46Z M-12 -62 L0 -86 L12 -62Z M10 -40 L20 -58 L30 -40Z" fill="${c.roof}"/>
 ${c.win?`<g fill="#ffe27a"><rect x="-4" y="-48" width="8" height="12" rx="4"/><rect x="-23" y="-34" width="6" height="9" rx="3"/><rect x="17" y="-28" width="6" height="9" rx="3"/></g>`:`<rect x="-4" y="-48" width="8" height="12" rx="4" fill="#fff"/>`}
</g></g>`;
const balloon=(x,y,sc=1,a='#ff7a8a',b='#ffd23f')=>`<g transform="translate(${x} ${y}) scale(${sc})"><g class="bobsm"><ellipse cx="0" cy="0" rx="22" ry="26" fill="${a}"/><path d="M0 -26 Q-12 0 0 26 Q12 0 0 -26Z" fill="${b}"/><path d="M-12 22 L-6 34 M12 22 L6 34" stroke="#8a5a2b" stroke-width="2"/><rect x="-7" y="34" width="14" height="10" rx="2" fill="#a8693a"/></g></g>`;

const SCENES={
pagi:()=>`<defs>${grad('g',[[0,'#79c8ff'],[.55,'#bfe6ff'],[1,'#eef9ff']])}<radialGradient id="sg"><stop offset="0" stop-color="#fff6c8"/><stop offset="1" stop-color="#ffe27a" stop-opacity="0"/></radialGradient></defs>
 <rect width="1200" height="800" fill="url(#g)"/>
 <circle cx="990" cy="150" r="170" fill="url(#sg)"/><circle cx="990" cy="150" r="52" fill="#ffe27a"/>
 ${cloud(80,110,1.3)}${cloud(420,50,.9)}${cloud(740,270,1.1)}${cloud(230,340,.8,'#fff',.8)}${cloud(980,420,1,'#fff',.85)}
 ${island(300,480,1)}${island(830,430,.8)}${island(1090,590,.6)}${island(560,650,.7)}
 ${balloon(150,300,1)}${balloon(1100,300,.7,'#4a9bff','#fff')}
 ${ch('bird',640,240,58,'bobsm')}${sparkle(520,180,1)}${sparkle(880,300,1.2)}${sparkle(180,500,.9)}`,
awan:()=>`<defs>${grad('g',[[0,'#9fd8ff'],[.4,'#cfe0ff'],[.75,'#f1dcff'],[1,'#ffe6ef']])}</defs>
 <rect width="1200" height="800" fill="url(#g)"/>
 ${cloud(40,120,1.7)}${cloud(500,60,1.2)}${cloud(900,160,1.6)}${cloud(250,380,1.3,'#fff',.85)}${cloud(700,450,1.8,'#fff',.8)}${cloud(1000,600,1.4,'#fff',.85)}${cloud(100,640,1.5,'#fff',.85)}
 ${island(260,300,.7,{top:'#fdeaf5',rock:'#b9a8ea',castle:'#d6c4f8',roof:'#9a7df0',win:false})}${island(880,350,.65,{top:'#fdeaf5',rock:'#b9a8ea',castle:'#d6c4f8',roof:'#9a7df0',win:false})}
 ${balloon(560,260,.9,'#ff9fc0','#fff')}
 ${ch('bird',140,520,52,'bobsm')}
 ${[[120,220,1],[420,160,1.3],[760,120,1],[1010,320,1.2],[620,520,1.1],[330,600,.9],[900,560,1]].map(([x,y,k])=>sparkle(x,y,k,k>1.1?'#fff':'#ffe27a')).join('')}`,
pelangi:()=>`<defs>${grad('g',[[0,'#79c8ff'],[.6,'#c5e8ff'],[1,'#f2fbff']])}</defs>
 <rect width="1200" height="800" fill="url(#g)"/>
 ${[[560,'#ff7a6b'],[534,'#ffab5e'],[508,'#ffe066'],[482,'#8ad8ff'],[456,'#4f93ff'],[430,'#a58bff']].map(([r,c])=>`<path d="M${600-r} 700 A${r} ${r} 0 0 1 ${600+r} 700" fill="none" stroke="${c}" stroke-width="26" opacity=".6"/>`).join('')}
 ${cloud(20,560,1.5)}${cloud(1000,560,1.5)}${cloud(240,160,1)}${cloud(850,110,1.1)}${cloud(560,330,.8,'#fff',.8)}
 ${island(250,400,.6)}${island(960,370,.6)}${balloon(600,260,.9,'#ffab5e','#fff')}${balloon(110,300,.6)}
 ${ch('bird',420,200,50,'bobsm')}${sparkle(700,200,1)}${sparkle(160,160,1.2)}${sparkle(1080,220,1)}`,
senja:()=>`<defs>${grad('g',[[0,'#243fa8'],[.35,'#5a6bd8'],[.62,'#a68de8'],[.82,'#ff9fba'],[1,'#ffd0a0']])}<radialGradient id="sg"><stop offset="0" stop-color="#ffd08a"/><stop offset="1" stop-color="#ff9f6a" stop-opacity="0"/></radialGradient></defs>
 <rect width="1200" height="800" fill="url(#g)"/>${stars(24,300,3)}
 <circle cx="600" cy="620" r="240" fill="url(#sg)"/><circle cx="600" cy="620" r="96" fill="#ffb25e"/>
 ${cloud(120,260,1.3,'#ffc2d4',.75)}${cloud(900,330,1.1,'#ffc2d4',.7)}${cloud(520,150,.9,'#d8c6ff',.6)}
 ${island(250,520,1,DUSK)}${island(930,470,.85,DUSK)}${island(620,700,.6,DUSK)}
 <g fill="none" stroke="#3a2a82" stroke-width="3" stroke-linecap="round"><path d="M420 240 q12 -14 24 0 q12 -14 24 0"/><path d="M500 290 q9 -10 18 0 q9 -10 18 0"/></g>
 ${sparkle(700,220,1)}${sparkle(160,420,.9)}`,
malam:()=>`<defs>${grad('g',[[0,'#061642'],[.6,'#12307f'],[1,'#2449ad']])}<radialGradient id="mg"><stop offset="0" stop-color="#fff7d1" stop-opacity=".55"/><stop offset="1" stop-color="#fff7d1" stop-opacity="0"/></radialGradient></defs>
 <rect width="1200" height="800" fill="url(#g)"/>${stars(60,560,5)}
 <circle cx="190" cy="150" r="130" fill="url(#mg)"/><circle cx="190" cy="150" r="54" fill="#fff4c4"/>
 <g fill="#f1de9b"><circle cx="172" cy="136" r="9"/><circle cx="208" cy="168" r="12"/><circle cx="196" cy="128" r="5"/></g>
 <path d="M860 90 L760 150" stroke="#fff" stroke-width="3" stroke-linecap="round" opacity=".7"/>
 ${cloud(620,240,1,'#2d4cae',.5)}${cloud(980,170,.8,'#2d4cae',.45)}
 ${island(300,500,1,NIGHT)}${island(850,440,.8,NIGHT)}${island(1100,620,.6,NIGHT)}${island(560,680,.65,NIGHT)}
 ${sparkle(520,300,1.2,'#fff')}${sparkle(980,260,1,'#ffe27a')}${sparkle(120,420,1,'#fff')}`
};
const NAMA={pagi:'Langit Pagi',awan:'Taman Awan',pelangi:'Pelangi Ceria',senja:'Senja Ajaib',malam:'Malam Bintang'};
const AUTO={dashboard:'pagi',absensi:'awan',nilai:'pelangi',impor:'senja',data:'malam'};
const MASCOT={dashboard:'owl',absensi:'bunny',nilai:'dragon',impor:'monster',data:'fox'};
const EMPTYCH=['bird','owl','bunny','fox','monster','dragon'];

const tower=flip=>`<g transform="${flip?'translate(1200 0) scale(-1 1)':''}">
 <path d="M-10 262 Q30 330 110 318 Q170 306 205 270 V250 H-10Z" fill="#b4a0dc"/>
 <rect x="-10" y="244" width="215" height="16" rx="8" fill="#e8d9b8"/>
 <rect x="18" y="64" width="104" height="182" rx="6" fill="#c98a5b"/>
 <path d="M6 70 L70 -6 L134 70Z" fill="#7a4fc0"/><path d="M6 70 H134" stroke="#5f3aa0" stroke-width="5"/>
 <rect x="34" y="104" width="30" height="48" rx="15" fill="#6e3f22"/><rect x="76" y="104" width="30" height="48" rx="15" fill="#6e3f22"/>
 ${[0,1,2].map(k=>`<rect x="${38+k*8}" y="${116+(k%2)*4}" width="6" height="${28-(k%2)*4}" fill="${['#ff7a8a','#ffd23f','#4a9bff'][k]}"/><rect x="${80+k*8}" y="${118-(k%2)*2}" width="6" height="${26+(k%2)*3}" fill="${['#4a9bff','#ff7a8a','#ffd23f'][k]}"/>`).join('')}
 <rect x="52" y="178" width="36" height="68" rx="18" fill="#6e3f22"/>
 <rect x="130" y="228" width="40" height="8" rx="2" fill="#ff7a8a"/><rect x="134" y="220" width="34" height="8" rx="2" fill="#4a9bff"/><rect x="132" y="212" width="36" height="8" rx="2" fill="#ffd23f"/>
</g>`;
const heroArt=()=>`<svg class="art" viewBox="0 0 1200 340" preserveAspectRatio="xMidYMid slice" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
 <defs>${grad('hg',[[0,'#6fc3ff'],[.6,'#bfe6ff'],[1,'#e9f7ff']])}</defs>
 <rect width="1200" height="340" fill="url(#hg)"/>
 ${cloud(370,30,1.1)}${cloud(780,20,.9)}${cloud(560,215,.8,'#fff',.8)}${cloud(230,160,.7,'#fff',.7)}${cloud(900,215,.9)}
 ${island(430,260,.5)}${island(780,245,.5)}
 ${balloon(262,110,.7)}
 ${tower(0)}${tower(1)}
 ${ch('owl',138,246,64,'bobsm')}${ch('dragon',1062,246,120,'bobsm')}${ch('bird',945,92,52,'bobsm')}
 ${sparkle(330,60,1)}${sparkle(860,50,1.2)}${sparkle(600,300,.9)}</svg>`;
const heroHTML=()=>`<section class="hero">${heroArt()}<div class="hero-text"><h1>Absen &amp; Nilai<span>Jadi Lebih Ceria</span></h1><p>Catat kehadiran, isi nilai, dan lihat rekap tiap bulan dalam satu tempat.</p><button class="btn" onclick="go('absensi')">Mulai Absen</button></div></section>
<div class="pillbar"><span>${ICON.check}Absen diisi manual</span><span>${ICON.star}Nilai dihitung otomatis</span><span>${ICON.cal}Rekap tiap bulan</span><span>${ICON.doc}Impor Google Form</span></div>`;

const DECOR={scene:'',tab:'',hero:null};
function decorate(){
  const id=(S.bg&&S.bg!=='auto'&&SCENES[S.bg])?S.bg:AUTO[V.tab];
  if(DECOR.scene!==id){DECOR.scene=id;$('#scene').innerHTML=`<svg viewBox="0 0 1200 800" preserveAspectRatio="xMidYMax slice" xmlns="http://www.w3.org/2000/svg">${SCENES[id]()}</svg>`;document.body.dataset.bg=id}
  if(DECOR.tab!==V.tab){DECOR.tab=V.tab;$('#mascot').innerHTML=chSvg(MASCOT[V.tab])}
  const wantHero=V.tab==='dashboard';
  if(DECOR.hero!==wantHero){DECOR.hero=wantHero;$('#hero').innerHTML=wantHero?heroHTML():''}
  $('#gBg').value=(S.bg&&SCENES[S.bg])?S.bg:'auto';
  document.querySelectorAll('.empty').forEach((e,i)=>e.insertAdjacentHTML('afterbegin',`<div class="empty-art">${chSvg(EMPTYCH[i%EMPTYCH.length])}</div>`));
}
$('#brand').innerHTML=`<span class="logo">${ICON.logo}</span><span>Data Nilai<small>Absensi · Nilai · Rekap</small></span>`;
$('#brand').addEventListener('click',()=>go('dashboard'));
$('#foot').innerHTML=`<svg class="foot-wave" viewBox="0 0 1200 40" preserveAspectRatio="none" aria-hidden="true"><path d="M0 22 Q150 -6 300 22 T600 22 T900 22 T1200 22 V40 H0Z" fill="#2a78e0"/></svg>
 <div class="foot-in"><div class="foot-art l">${chSvg('monster')}</div>
  <div class="foot-cols"><div><b>Data Nilai</b><span>Absensi, nilai, dan rekap bulanan untuk kelas Anda.</span></div>
   <div><b>Menu</b><a onclick="go('absensi')">Absensi</a><a onclick="go('nilai')">Nilai</a><a onclick="go('impor')">Impor Form</a><a onclick="go('data')">Data</a></div>
   <div><b>Catatan</b><span>Data tersimpan di browser ini. Cadangkan lewat menu Data.</span></div></div>
  <div class="foot-art r">${chSvg('fox')}</div></div>
 <div class="copy">Data Nilai · dibuat dengan semangat belajar</div>`;
$('#gBg').innerHTML=`<option value="auto">Otomatis</option>`+Object.keys(NAMA).map(k=>`<option value="${k}">${NAMA[k]}</option>`).join('');
$('#gBg').addEventListener('change',e=>{S.bg=e.target.value;save();render()});

render();
</script>
</body>
</html>

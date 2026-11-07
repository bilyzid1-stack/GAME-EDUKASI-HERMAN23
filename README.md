Petualangan bangun datar · HTML
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Petualangan Bangun Datar - Matematika Kelas V</title>
<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@500;700;800&display=swap" rel="stylesheet">
<style>
:root{
  --hutan:#1f4d3a; --hutan-tua:#143327; --parchment:#fbf5e6; --kertas:#fffdf7;
  --oranye:#f08a24; --emas:#f4c542; --tinta:#2a2a2a; --biru:#2b6cb0;
  --radius:18px;
  color-scheme: light;
}
*{box-sizing:border-box}
html,body{margin:0;height:100%}
body{font-family:"Baloo 2","Trebuchet MS",system-ui,sans-serif;background:var(--parchment);color:var(--tinta);
  padding:env(safe-area-inset-top,0px) 0 env(safe-area-inset-bottom,0px);line-height:1.5}
header{background:var(--hutan);color:#fff;padding:14px 18px;display:flex;flex-wrap:wrap;gap:10px;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:5}
header h1{font-size:1.35rem;margin:0;font-weight:800;letter-spacing:.2px}
nav{display:flex;flex-wrap:wrap;gap:6px}
nav button{font:inherit;font-weight:700;border:2px solid transparent;background:rgba(255,255,255,.12);color:#fff;padding:6px 12px;border-radius:999px;cursor:pointer}
nav button.aktif{background:var(--emas);color:var(--hutan-tua)}
nav button:focus-visible,button:focus-visible,input:focus-visible{outline:3px solid var(--emas);outline-offset:2px}
main{max-width:980px;margin:0 auto;padding:18px}
.screen{display:none}
.screen.aktif{display:block}
.card{background:var(--kertas);border-radius:var(--radius);padding:18px;box-shadow:0 2px 0 rgba(31,77,58,.15);border:2px solid #e8dfc8}
h2{font-size:1.5rem;margin:.2rem 0 .6rem;color:var(--hutan)}
h3{margin:.2rem 0;font-size:1.15rem}
p{margin:.4rem 0}
.btn{font:inherit;font-weight:800;font-size:1.02rem;border:0;border-radius:999px;padding:10px 20px;background:var(--oranye);color:#fff;cursor:pointer;box-shadow:0 3px 0 #b8600f}
.btn:active{transform:translateY(2px);box-shadow:0 1px 0 #b8600f}
.btn.kedua{background:var(--hutan);box-shadow:0 3px 0 var(--hutan-tua)}
.btn:disabled{opacity:.45;cursor:not-allowed;transform:none}
input[type=text]{font:inherit;font-size:1.05rem;padding:9px 14px;border-radius:12px;border:2px solid #cdbf9c;background:#fff;min-width:0;width:100%;max-width:340px}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(230px,1fr));gap:14px}
.kartu-materi svg{width:100%;height:150px;display:block;background:#f3ecd6;border-radius:12px}
.kartu-materi ul{padding-left:1.1rem;margin:.4rem 0 0;font-size:.98rem}
.tag{display:inline-block;font-size:.85rem;background:#e6f2ea;color:var(--hutan);padding:2px 9px;border-radius:999px;margin:2px 3px 2px 0;font-weight:700}
.fig{fill:#bfe3cf;stroke:var(--hutan-tua);stroke-width:2.5;stroke-linejoin:round}
.sisi{stroke:var(--oranye);stroke-width:4.5;stroke-linecap:round}
.sudutdot{fill:var(--biru)}
.axis{stroke:var(--biru);stroke-width:1.6;stroke-dasharray:4 3}
.pilih{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:12px}
.pilih button{font:inherit;font-weight:700;border:2px solid #cdbf9c;background:#fff;border-radius:999px;padding:6px 12px;cursor:pointer}
.pilih button.aktif{background:var(--hutan);color:#fff;border-color:var(--hutan)}
.sim{display:grid;grid-template-columns:minmax(0,1fr) minmax(0,1fr);gap:18px;align-items:start}
@media (max-width:720px){.sim{grid-template-columns:1fr}}
.sim .gambar svg{width:100%;max-width:320px;height:auto;display:block;margin:auto;background:#f3ecd6;border-radius:14px;padding:8px}
.toggles{display:flex;flex-wrap:wrap;gap:12px;margin:10px 0}
.toggles label{font-weight:700;display:flex;gap:6px;align-items:center;cursor:pointer}
table{border-collapse:collapse;width:100%;font-size:1rem}
td,th{text-align:left;padding:6px 8px;border-bottom:1px dashed #d8ccb0}
th{width:48%;color:var(--hutan)}
.gamebox{position:relative}
#canvas{width:100%;height:auto;display:block;border-radius:14px;background:#2d6a4f;touch-action:manipulation;cursor:crosshair;border:3px solid var(--hutan-tua)}
.hud{display:flex;flex-wrap:wrap;gap:10px;align-items:center;justify-content:space-between;margin-bottom:10px}
.soal{font-size:1.15rem;font-weight:800;background:#fff3d6;border:2px dashed var(--oranye);padding:8px 14px;border-radius:14px;flex:1 1 360px}
.nyawa{font-size:1.4rem;letter-spacing:2px}
#gmsg{min-height:2.4em;margin:10px 0 0;font-weight:700;font-size:1.05rem}
.ok{color:#17663a}.salah{color:#b3261e}
.kuis-opsi{display:grid;gap:8px;margin-top:10px}
.kuis-opsi button{font:inherit;font-size:1.02rem;text-align:left;padding:10px 14px;border-radius:12px;border:2px solid #cdbf9c;background:#fff;cursor:pointer}
.kuis-opsi button:disabled{cursor:default}
.kuis-opsi button.benar{border-color:#17663a;background:#dcf5e4}
.kuis-opsi button.keliru{border-color:#b3261e;background:#fbe0de}
#kuisFeedback{min-height:2em;font-weight:700;margin-top:10px}
.progress{height:10px;background:#e8dfc8;border-radius:999px;overflow:hidden;margin:8px 0}
.progress span{display:block;height:100%;background:var(--oranye);width:0;transition:width .3s}
.sertifikat{background:#fffef8;border:10px double var(--emas);border-radius:12px;padding:28px 22px;text-align:center;position:relative;margin-top:14px;max-width:760px;margin-left:auto;margin-right:auto}
.sertifikat .judul{font-size:2rem;font-weight:800;color:var(--hutan);margin:0}
.sertifikat .nama{font-size:2.2rem;font-weight:800;color:var(--oranye);border-bottom:2px solid #d8ccb0;display:inline-block;padding:0 20px 2px;margin:8px 0}
.sertifikat .lencana{font-size:3.4rem;line-height:1}
.sertifikat .ttd{display:flex;justify-content:space-between;margin-top:22px;font-size:.98rem;gap:10px;flex-wrap:wrap}
.sertifikat .ttd div{min-width:150px}
.sertifikat small{color:#6b6250}
.kunci{background:#fff3d6;border-radius:14px;padding:14px;margin-top:12px}
.penutup{color:#6b6250;font-size:.9rem;text-align:center;margin:22px 0 6px}
.hero{background:linear-gradient(160deg,var(--hutan) 0%,var(--hutan-tua) 100%);color:#fff;border-radius:22px;padding:26px 22px;position:relative;overflow:hidden}
.hero h2{color:var(--emas);font-size:2rem;margin:0 0 6px}
.hero p{max-width:620px}
.langkah{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:10px;margin-top:16px}
.langkah div{background:rgba(255,255,255,.1);border-radius:14px;padding:12px}
.langkah b{color:var(--emas)}
@media print{
  body *{visibility:hidden}
  header,nav,.no-print{display:none!important}
  #sertifikatArea,#sertifikatArea *{visibility:visible}
  #sertifikatArea{position:absolute;left:0;top:0;width:100%}
  .sertifikat{box-shadow:none}
}
</style>
</head>
<body>
<header>
  <h1>🌳 Petualangan Bangun Datar</h1>
  <nav aria-label="Menu utama">
    <button data-tab="home" class="aktif">Beranda</button>
    <button data-tab="materi">1. Materi</button>
    <button data-tab="simulasi">2. Simulasi</button>
    <button data-tab="game">3. Berburu</button>
    <button data-tab="kuis">4. Kuis</button>
    <button data-tab="sertifikat">5. Sertifikat</button>
  </nav>
</header>
 
<main>
 
<!-- BERANDA -->
<section id="home" class="screen aktif">
  <div class="hero">
    <h2>Selamat datang, Pemburu Bangun Datar!</h2>
    <p>Hutan ajaib dijaga para monster yang membawa bangun datar di dadanya. Untuk melewati setiap rintangan, kamu harus menembak monster yang membawa bangun datar sesuai petunjuk. Kumpulkan ilmumu tentang <b>ciri-ciri bangun datar</b> dan raih sertifikat petualang!</p>
    <div class="langkah">
      <div><b>1. Materi</b><br>Pelajari bentuk dan ciri tiap bangun.</div>
      <div><b>2. Simulasi</b><br>Lihat sisi, sudut, dan garis simetri.</div>
      <div><b>3. Berburu</b><br>Tembak monster yang benar di 5 rintangan.</div>
      <div><b>4. Kuis</b><br>Jawab 10 soal pilihan ganda dan benar/salah.</div>
    </div>
  </div>
  <div class="card" style="margin-top:16px">
    <h3>Nama Petualang</h3>
    <p>Tulis namamu untuk dicantumkan di sertifikat.</p>
    <input type="text" id="namaInput" placeholder="Contoh: Budi Santoso" maxlength="40" aria-label="Nama petualang">
    <p style="margin-top:14px"><button class="btn" id="mulaiBtn">Mulai Petualangan ➜</button></p>
  </div>
</section>
 
<!-- MATERI -->
<section id="materi" class="screen">
  <h2>Materi: Ciri-Ciri Bangun Datar</h2>
  <p>Perhatikan gambar, lalu baca ciri-cirinya. Ingat: <b>sisi</b> adalah garis lurus pembatas bangun, <b>sudut</b> adalah titik sudut tempat dua sisi bertemu, dan <b>sumbu simetri lipat</b> adalah garis yang jika dilipat membuat dua bagian sama persis.</p>
  <div class="grid" id="gridMateri"></div>
</section>
 
<!-- SIMULASI -->
<section id="simulasi" class="screen">
  <h2>Simulasi: Periksa Sisi, Sudut, dan Simetri</h2>
  <p>Pilih sebuah bangun, lalu nyalakan pilihan di bawah untuk memeriksanya.</p>
  <div class="pilih" id="pilihSim" role="group" aria-label="Pilih bangun datar"></div>
  <div class="sim">
    <div class="card gambar" id="simGambar"></div>
    <div class="card">
      <h3 id="simNama"></h3>
      <div class="toggles">
        <label><input type="checkbox" id="tSisi"> Tandai sisi</label>
        <label><input type="checkbox" id="tSudut"> Tandai titik sudut</label>
        <label><input type="checkbox" id="tSimetri"> Tampilkan sumbu simetri lipat</label>
      </div>
      <table id="simTabel"></table>
      <div class="kunci" id="simCiri"></div>
    </div>
  </div>
</section>
 
<!-- GAME -->
<section id="game" class="screen">
  <h2>Berburu Bangun Datar</h2>
  <p>Klik monster untuk menembaknya. Tembak <b>semua monster yang membawa jawaban benar</b>. Setiap kali salah tembak, nyawamu berkurang satu.</p>
  <div class="card gamebox">
    <div class="hud">
      <div class="soal" id="gSoal"></div>
      <div class="nyawa" id="gNyawa" aria-label="Nyawa"></div>
    </div>
    <div class="hud" style="margin-bottom:6px">
      <span id="gInfo" style="font-weight:700"></span>
      <span>
        <button class="btn" id="gNext" disabled>Lanjut ➜</button>
        <button class="btn kedua" id="gUlang" style="display:none">Coba lagi</button>
        <button class="btn kedua no-print" id="gReset">Mulai dari awal</button>
      </span>
    </div>
    <canvas id="canvas" width="640" height="400" aria-label="Arena berburu bangun datar"></canvas>
    <div id="gmsg" role="status" aria-live="polite"></div>
  </div>
</section>
 
<!-- KUIS -->
<section id="kuis" class="screen">
  <h2>Kuis Bangun Datar</h2>
  <div class="card">
    <div id="kuisWrap"></div>
  </div>
</section>
 
<!-- SERTIFIKAT -->
<section id="sertifikat" class="screen">
  <h2>Sertifikat Petualang</h2>
  <div class="card" id="sertInfo"></div>
  <div id="sertifikatArea"></div>
  <p class="no-print" style="text-align:center;margin-top:14px" id="sertTombol"></p>
</section>
 
<p class="penutup">Media pembelajaran Matematika Kelas V · Bab Geometri · Dibuat oleh <b>Herman23</b></p>
</main>
 
<script>
/* ============ DATA BANGUN DATAR ============ */
const SHAPES = {
  persegi:{nama:"Persegi",pts:[[-1,-1],[1,-1],[1,1],[-1,1]],sisi:4,sejajar:2,sudut:"4 sudut siku-siku",simetri:4,axes:[0,45,90,135],
    ciri:"Empat sisinya sama panjang, empat sudutnya siku-siku (90°), dan sisi yang berhadapan saling sejajar."},
  persegi_panjang:{nama:"Persegi Panjang",pts:[[-1.35,-0.8],[1.35,-0.8],[1.35,0.8],[-1.35,0.8]],sisi:4,sejajar:2,sudut:"4 sudut siku-siku",simetri:2,axes:[0,90],
    ciri:"Sisi yang berhadapan sama panjang dan sejajar, serta empat sudutnya siku-siku."},
  segitiga_sama_sisi:{nama:"Segitiga Sama Sisi",pts:[[0,-1],[0.87,0.5],[-0.87,0.5]],sisi:3,sejajar:0,sudut:"3 sudut sama besar (60°)",simetri:3,axes:[90,30,150],
    ciri:"Ketiga sisinya sama panjang dan ketiga sudutnya sama besar, yaitu 60°."},
  segitiga_sama_kaki:{nama:"Segitiga Sama Kaki",pts:[[0,-1],[1,0.8],[-1,0.8]],sisi:3,sejajar:0,sudut:"2 sudut di alas sama besar",simetri:1,axes:[90],
    ciri:"Dua sisinya sama panjang (disebut kaki) dan dua sudut alasnya sama besar."},
  segitiga_siku:{nama:"Segitiga Siku-Siku",pts:[[-1,1],[1,1],[-1,-1]],sisi:3,sejajar:0,sudut:"1 sudut siku-siku (90°)",simetri:0,axes:[],
    ciri:"Memiliki tepat satu sudut siku-siku (90°). Sisi di depan sudut siku-siku disebut sisi miring."},
  jajar_genjang:{nama:"Jajar Genjang",pts:[[-0.6,-0.8],[1,-0.8],[0.6,0.8],[-1,0.8]],sisi:4,sejajar:2,sudut:"sudut berhadapan sama besar, tanpa siku-siku",simetri:0,axes:[],
    ciri:"Sisi yang berhadapan sama panjang dan sejajar. Tidak memiliki sumbu simetri lipat."},
  belah_ketupat:{nama:"Belah Ketupat",pts:[[0,-1],[0.7,0],[0,1],[-0.7,0]],sisi:4,sejajar:2,sudut:"sudut berhadapan sama besar",simetri:2,axes:[0,90],
    ciri:"Keempat sisinya sama panjang, sisi berhadapannya sejajar, dan memiliki 2 sumbu simetri lipat."},
  layang_layang:{nama:"Layang-Layang",pts:[[0,-1],[0.6,-0.2],[0,1],[-0.6,-0.2]],sisi:4,sejajar:0,sudut:"sepasang sudut berhadapan sama besar",simetri:1,axes:[90],
    ciri:"Dua pasang sisi berdekatan sama panjang. Memiliki 1 sumbu simetri lipat."},
  trapesium:{nama:"Trapesium",pts:[[-0.6,-0.8],[0.6,-0.8],[1,0.8],[-1,0.8]],sisi:4,sejajar:1,sudut:"2 sudut di alas sama besar",simetri:1,axes:[90],
    ciri:"Hanya memiliki sepasang sisi sejajar. Trapesium pada gambar ini memiliki 1 sumbu simetri lipat."},
  lingkaran:{nama:"Lingkaran",circle:true,sisi:0,sejajar:0,sudut:"tidak memiliki sudut",simetri:"tak terhingga",axes:[0,15,30,45,60,75,90,105,120,135,150,165],
    ciri:"Tidak memiliki sisi dan sudut. Bentuknya lengkung dan memiliki banyak sekali sumbu simetri lipat."}
};
const ORDER = Object.keys(SHAPES);
 
/* ============ UTIL ============ */
const $ = s => document.querySelector(s);
const $$ = s => [...document.querySelectorAll(s)];
function shuffle(a){for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]];}return a;}
 
function svgShape(id, o={}){
  const s = SHAPES[id], c = 50, k = 30;
  let g = "";
  if(s.circle){
    g += `<circle cx="50" cy="50" r="34" class="fig"/>`;
  } else {
    const pts = s.pts.map(p => [c+p[0]*k, c+p[1]*k]);
    g += `<polygon points="${pts.map(p=>p.join(",")).join(" ")}" class="fig"/>`;
    if(o.sisi){
      pts.forEach((p,i)=>{const q=pts[(i+1)%pts.length];
        g += `<line x1="${p[0]}" y1="${p[1]}" x2="${q[0]}" y2="${q[1]}" class="sisi"/>`;});
    }
    if(o.sudut){
      pts.forEach(p=>{ g += `<circle cx="${p[0]}" cy="${p[1]}" r="3.2" class="sudutdot"/>`; });
    }
  }
  if(o.simetri){
    s.axes.forEach(a=>{
      const r = a*Math.PI/180, dx = Math.cos(r)*42, dy = Math.sin(r)*42;
      g += `<line x1="${(50-dx).toFixed(1)}" y1="${(50-dy).toFixed(1)}" x2="${(50+dx).toFixed(1)}" y2="${(50+dy).toFixed(1)}" class="axis"/>`;
    });
  }
  return `<svg viewBox="0 0 100 100" role="img" aria-label="${s.nama}">${g}</svg>`;
}
 
/* ============ NAVIGASI ============ */
function showTab(id){
  $$(".screen").forEach(s => s.classList.toggle("aktif", s.id === id));
  $$("nav button").forEach(b => b.classList.toggle("aktif", b.dataset.tab === id));
  if(id === "sertifikat") renderSertifikat();
  if(id === "kuis" && !quiz.started) startKuis();
  window.scrollTo({top:0,behavior:"smooth"});
}
$$("nav button").forEach(b => b.addEventListener("click", () => showTab(b.dataset.tab)));
$("#mulaiBtn").addEventListener("click", () => showTab("materi"));
 
/* ============ MATERI ============ */
function renderMateri(){
  $("#gridMateri").innerHTML = ORDER.map(id => {
    const s = SHAPES[id];
    return `<div class="card kartu-materi">
      <h3>${s.nama}</h3>
      ${svgShape(id,{})}
      <div style="margin-top:8px">
        <span class="tag">${s.circle?0:s.sisi} sisi</span>
        <span class="tag">${s.simetri} simetri</span>
      </div>
      <ul><li>${s.ciri}</li><li><b>Sudut:</b> ${s.sudut}</li></ul>
    </div>`;
  }).join("");
}
 
/* ============ SIMULASI ============ */
let simId = "persegi";
function renderSim(){
  $("#pilihSim").innerHTML = ORDER.map(id =>
    `<button data-id="${id}" class="${id===simId?"aktif":""}">${SHAPES[id].nama}</button>`).join("");
  $$("#pilihSim button").forEach(b => b.addEventListener("click", () => { simId = b.dataset.id; renderSim(); }));
  const s = SHAPES[simId];
  $("#simNama").textContent = s.nama;
  $("#simGambar").innerHTML = svgShape(simId, {sisi:$("#tSisi").checked, sudut:$("#tSudut").checked, simetri:$("#tSimetri").checked});
  $("#simTabel").innerHTML = `
    <tr><th>Jumlah sisi</th><td>${s.circle?"0 (tidak ada)":s.sisi}</td></tr>
    <tr><th>Pasang sisi sejajar</th><td>${s.sejajar}</td></tr>
    <tr><th>Jumlah sudut / ciri sudut</th><td>${s.circle?"0 (tidak ada)":s.sudut}</td></tr>
    <tr><th>Sumbu simetri lipat</th><td>${s.simetri}</td></tr>`;
  $("#simCiri").innerHTML = `<b>Kesimpulan:</b> ${s.ciri}`;
}
["#tSisi","#tSudut","#tSimetri"].forEach(id => $(id).addEventListener("change", renderSim));
 
/* ============ GAME: BERBURU ============ */
const LV = [
  {q:"Tembak bangun yang memiliki 4 sisi sama panjang.", benar:["persegi","belah_ketupat"], salah:["persegi_panjang","layang_layang","trapesium"]},
  {q:"Tembak bangun yang TIDAK memiliki sudut siku-siku.", benar:["segitiga_sama_sisi","jajar_genjang","layang_layang"], salah:["persegi","persegi_panjang","segitiga_siku"]},
  {q:"Tembak bangun yang memiliki 3 sisi.", benar:["segitiga_sama_sisi","segitiga_sama_kaki","segitiga_siku"], salah:["persegi","belah_ketupat","trapesium"]},
  {q:"Tembak bangun yang memiliki 2 pasang sisi sejajar.", benar:["persegi","persegi_panjang","jajar_genjang"], salah:["trapesium","layang_layang","segitiga_siku"]},
  {q:"Tembak bangun yang tidak memiliki sisi dan sudut.", benar:["lingkaran"], salah:["persegi","segitiga_sama_sisi","belah_ketupat"]}
];
const NAMA_TOTAL = LV.length;
const G = {lvl:0, nyawa:3, mons:[], peluru:[], partikel:[], cleared:false, over:false, selesai:false, last:0, shake:0};
const cv = $("#canvas"), ctx = cv.getContext("2d");
const CW = cv.width, CH = cv.height, MW = 110, MH = 96;
 
function mulaiLevel(){
  const L = LV[G.lvl];
  G.nyawa = 3; G.peluru = []; G.partikel = []; G.cleared = false; G.over = false;
  const daftar = shuffle([...L.benar.map(id=>({id,ok:true})), ...L.salah.map(id=>({id,ok:false}))]);
  G.mons = daftar.map((o,i) => {
    const kol = i % 3, bar = Math.floor(i/3);
    return {id:o.id, ok:o.ok, dead:false,
      x: 20 + kol*205 + Math.random()*50,
      y: 70 + bar*150,
      vx: (Math.random()<.5?-1:1) * (0.035 + G.lvl*0.012) * (0.8+Math.random()*0.5),
      bob: Math.random()*6.28};
  });
  $("#gSoal").textContent = `Rintangan ${G.lvl+1}: ${L.q}`;
  $("#gInfo").textContent = `Rintangan ${G.lvl+1} dari ${NAMA_TOTAL}`;
  $("#gNext").disabled = true;
  $("#gUlang").style.display = "none";
  setMsg("Bidik dengan benar! Klik monster yang membawa jawaban.", "");
  updateNyawa();
}
function setMsg(t, cls){ const el=$("#gmsg"); el.textContent=t; el.className = cls || ""; }
function updateNyawa(){ $("#gNyawa").textContent = "❤️".repeat(G.nyawa) + "🖤".repeat(3-G.nyawa); }
 
function hit(m){
  if(m.dead || G.over || G.cleared) return;
  const nama = SHAPES[m.id].nama;
  if(m.ok){
    m.dead = true; explode(m.x+MW/2, m.y+MH/2, "#f4c542");
    const sisa = G.mons.filter(x=>x.ok && !x.dead).length;
    if(sisa === 0){
      G.cleared = true;
      const terakhir = G.lvl === NAMA_TOTAL-1;
      if(terakhir) G.selesai = true;
      setMsg(`Hebat! Rintangan terlewati. ${nama} memang jawaban yang benar.` + (terakhir ? " Kamu menyelesaikan seluruh hutan!" : ""), "ok");
      $("#gNext").disabled = false;
      $("#gNext").textContent = terakhir ? "Selesai ➜ Kuis" : "Lanjut ➜";
    } else {
      setMsg(`Tepat! ${nama} adalah jawaban yang benar. Sisa ${sisa} lagi.`, "ok");
    }
  } else {
    G.nyawa--; G.shake = 300; updateNyawa();
    const alasan = {persegi_panjang:"sisinya tidak semua sama panjang",
      segitiga_siku:"tidak sesuai dengan petunjuk rintangan ini",
      trapesium:"hanya memiliki sepasang sisi sejajar dan tidak sesuai petunjuk"}[m.id] || "tidak sesuai dengan petunjuk rintangan ini";
    if(G.nyawa <= 0){
      G.over = true;
      setMsg(`Nyawa habis! ${nama} ${alasan}. Coba lagi rintangan ini.`, "salah");
      $("#gUlang").style.display = "inline-block";
    } else {
      setMsg(`Salah! ${nama} ${alasan}. Coba lagi, sisa nyawa ${G.nyawa}.`, "salah");
    }
  }
}
 
function explode(x,y,warna){
  for(let i=0;i<18;i++){
    const a = Math.random()*6.28, v = 0.05+Math.random()*0.18;
    G.partikel.push({x,y,vx:Math.cos(a)*v,vy:Math.sin(a)*v,life:700,warna});
  }
}
 
function tembak(m){
  if(m.dead || G.over || G.cleared) return;
  G.peluru.push({m, x:CW/2, y:CH-30});
}
 
cv.addEventListener("pointerdown", e => {
  const r = cv.getBoundingClientRect();
  const x = (e.clientX - r.left) * (CW / r.width);
  const y = (e.clientY - r.top) * (CH / r.height);
  const m = [...G.mons].reverse().find(m => !m.dead && x>=m.x-4 && x<=m.x+MW+4 && y>=m.y-24 && y<=m.y+MH+4);
  if(m) tembak(m);
});
 
function drawPoly(id, cx, cy, k, fill, stroke){
  const s = SHAPES[id];
  ctx.beginPath();
  if(s.circle){ ctx.arc(cx, cy, k*1.15, 0, Math.PI*2); }
  else {
    s.pts.forEach((p,i)=>{ const X=cx+p[0]*k, Y=cy+p[1]*k; i?ctx.lineTo(X,Y):ctx.moveTo(X,Y); });
    ctx.closePath();
  }
  ctx.fillStyle = fill; ctx.fill();
  ctx.strokeStyle = stroke; ctx.lineWidth = 2.2; ctx.lineJoin="round"; ctx.stroke();
}
function rrect(x,y,w,h,r){
  ctx.beginPath();
  ctx.moveTo(x+r,y); ctx.lineTo(x+w-r,y); ctx.quadraticCurveTo(x+w,y,x+w,y+r);
  ctx.lineTo(x+w,y+h-r); ctx.quadraticCurveTo(x+w,y+h,x+w-r,y+h);
  ctx.lineTo(x+r,y+h); ctx.quadraticCurveTo(x,y+h,x,y+h-r);
  ctx.lineTo(x,y+r); ctx.quadraticCurveTo(x,y,x+r,y); ctx.closePath();
}
 
function update(dt){
  if(!G.cleared && !G.over){
    G.mons.forEach(m => {
      if(m.dead) return;
      m.x += m.vx * dt; m.bob += dt*0.004;
      if(m.x < 8){ m.x = 8; m.vx = Math.abs(m.vx); }
      if(m.x > CW-MW-8){ m.x = CW-MW-8; m.vx = -Math.abs(m.vx); }
    });
  }
  G.peluru = G.peluru.filter(b => {
    if(b.m.dead) return false;
    const tx = b.m.x+MW/2, ty = b.m.y+MH/2;
    const dx = tx-b.x, dy = ty-b.y, d = Math.hypot(dx,dy), step = dt*1.1;
    if(d <= step+10){ hit(b.m); return false; }
    b.x += dx/d*step; b.y += dy/d*step; return true;
  });
  G.partikel = G.partikel.filter(p => { p.life -= dt; p.x += p.vx*dt; p.y += p.vy*dt; p.vy += 0.0004*dt; return p.life > 0; });
  if(G.shake > 0) G.shake -= dt;
}
 
function draw(){
  ctx.save();
  if(G.shake > 0) ctx.translate((Math.random()-.5)*6, (Math.random()-.5)*6);
  const g = ctx.createLinearGradient(0,0,0,CH);
  g.addColorStop(0,"#9bd3e8"); g.addColorStop(0.6,"#c9efd0"); g.addColorStop(1,"#3f8f5c");
  ctx.fillStyle = g; ctx.fillRect(0,0,CW,CH);
  // pohon latar
  ctx.fillStyle = "rgba(20,51,39,.35)";
  for(let i=0;i<8;i++){ ctx.beginPath(); ctx.arc(40+i*85, 40+(i%2)*18, 34, 0, 6.28); ctx.fill(); }
  // monster
  G.mons.forEach(m => {
    if(m.dead) return;
    const yy = m.y + Math.sin(m.bob)*4;
    ctx.font = "34px serif"; ctx.textAlign = "center"; ctx.textBaseline = "alphabetic";
    ctx.fillText("👾", m.x+MW/2, yy-2);
    rrect(m.x, yy, MW, MH, 14);
    ctx.fillStyle = "#fffdf7"; ctx.fill();
    ctx.strokeStyle = "#143327"; ctx.lineWidth = 3; ctx.stroke();
    drawPoly(m.id, m.x+MW/2, yy+MH/2+2, 26, "#bfe3cf", "#143327");
  });
  // peluru
  G.peluru.forEach(b => {
    ctx.beginPath(); ctx.arc(b.x,b.y,6,0,6.28); ctx.fillStyle="#ffd54a"; ctx.fill();
    ctx.strokeStyle="rgba(255,255,255,.7)"; ctx.lineWidth=2; ctx.stroke();
  });
  // partikel
  G.partikel.forEach(p => {
    ctx.globalAlpha = Math.max(0, p.life/700);
    ctx.fillStyle = p.warna; ctx.beginPath(); ctx.arc(p.x,p.y,4,0,6.28); ctx.fill();
  });
  ctx.globalAlpha = 1;
  // pemburu
  ctx.font = "44px serif"; ctx.textAlign="center"; ctx.fillText("🧒", CW/2, CH-6);
  ctx.restore();
  // overlay status
  if(G.cleared || G.over){
    ctx.fillStyle = "rgba(0,0,0,.25)"; ctx.fillRect(0,0,CW,CH);
    ctx.fillStyle = "#fff"; ctx.font = "bold 30px sans-serif"; ctx.textAlign="center";
    ctx.fillText(G.cleared ? "Rintangan Terlewati!" : "Nyawa Habis", CW/2, 60);
  }
}
 
function frame(t){
  const dt = Math.min(50, t - (G.last || t)); G.last = t;
  update(dt); draw();
  requestAnimationFrame(frame);
}
 
$("#gNext").addEventListener("click", () => {
  if(G.selesai){ showTab("kuis"); return; }
  G.lvl++; mulaiLevel();
});
$("#gUlang").addEventListener("click", mulaiLevel);
$("#gReset").addEventListener("click", () => {
  G.lvl = 0; G.selesai = false; $("#gNext").textContent = "Lanjut ➜"; mulaiLevel();
});
 
/* ============ KUIS ============ */
const BANK = [
  {q:"Persegi memiliki berapa sisi?", o:["3","4","5","6"], a:1},
  {q:"Persegi panjang memiliki berapa sudut siku-siku?", o:["1","2","4","0"], a:2},
  {q:"Segitiga yang ketiga sisinya sama panjang disebut ...", o:["segitiga sama kaki","segitiga sama sisi","segitiga siku-siku","segitiga tumpul"], a:1},
  {q:"Lingkaran memiliki sisi dan sudut.", o:["Benar","Salah"], a:1},
  {q:"Jajar genjang memiliki 2 pasang sisi yang sejajar.", o:["Benar","Salah"], a:0},
  {q:"Trapesium memiliki berapa pasang sisi yang sejajar?", o:["0","1","2","3"], a:1},
  {q:"Berapa sumbu simetri lipat pada belah ketupat?", o:["1","2","3","4"], a:1},
  {q:"Bangun datar yang memiliki tepat satu sudut siku-siku adalah ...", o:["persegi","persegi panjang","segitiga siku-siku","jajar genjang"], a:2},
  {q:"Pada jajar genjang, sudut yang berhadapan ... ", o:["selalu berbeda besar","sama besar","selalu siku-siku","tidak ada"], a:1},
  {q:"Segitiga sama kaki memiliki berapa sisi yang sama panjang?", o:["1","2","3","0"], a:1}
];
const quiz = {started:false, i:0, skor:0, jawab:false, urut:[]};
const PASS = 60;
function startKuis(){
  quiz.started = true; quiz.i = 0; quiz.skor = 0; quiz.jawab = false;
  quiz.urut = shuffle([...BANK.keys()]);
  tampilSoal();
}
function tampilSoal(){
  const wrap = $("#kuisWrap");
  if(quiz.i >= quiz.urut.length){
    const lulus = quiz.skor >= PASS;
    wrap.innerHTML = `
      <h3>Hasil Kuis</h3>
      <p style="font-size:2rem;font-weight:800;color:${lulus?"#17663a":"#b3261e"}">${quiz.skor} / 100</p>
      <p>${lulus ? "Luar biasa! Kamu sudah lulus. Sertifikat sudah terbuka." : "Belum lulus. Minimal nilai "+PASS+". Ayo ulangi kuisnya!"}</p>
      <p style="margin-top:12px;display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn kedua" id="ulangKuis">Ulangi Kuis</button>
        <button class="btn" id="keSert">Lihat Sertifikat ➜</button>
      </p>`;
    $("#ulangKuis").addEventListener("click", startKuis);
    $("#keSert").addEventListener("click", () => showTab("sertifikat"));
    return;
  }
  const s = BANK[quiz.urut[quiz.i]];
  const benarSalah = s.o.length === 2;
  wrap.innerHTML = `
    <div style="display:flex;justify-content:space-between;font-weight:700"><span>Soal ${quiz.i+1} dari ${quiz.urut.length}</span><span>Skor: ${quiz.skor}</span></div>
    <div class="progress"><span style="width:${(quiz.i/quiz.urut.length*100)}%"></span></div>
    <h3 style="font-size:1.25rem;margin-top:12px">${benarSalah?"[Benar / Salah] ":""}${s.q}</h3>
    <div class="kuis-opsi">${s.o.map((t,i)=>`<button data-i="${i}">${String.fromCharCode(65+i)}. ${t}</button>`).join("")}</div>
    <div id="kuisFeedback"></div>
    <p style="margin-top:10px"><button class="btn" id="kuisNext" disabled>${quiz.i===quiz.urut.length-1?"Lihat Hasil":"Soal Berikutnya ➜"}</button></p>`;
  quiz.jawab = false;
  $$(".kuis-opsi button").forEach(b => b.addEventListener("click", () => jawab(parseInt(b.dataset.i,10))));
  $("#kuisNext").addEventListener("click", () => { quiz.i++; tampilSoal(); });
}
function jawab(idx){
  if(quiz.jawab) return;
  quiz.jawab = true;
  const s = BANK[quiz.urut[quiz.i]];
  const btn = $$(".kuis-opsi button");
  btn.forEach(b => b.disabled = true);
  btn[s.a].classList.add("benar");
  if(idx === s.a){ quiz.skor += 10; $("#kuisFeedback").innerHTML = `<span class="ok">Benar! +10 poin.</span>`; }
  else { btn[idx].classList.add("keliru"); $("#kuisFeedback").innerHTML = `<span class="salah">Belum tepat. Jawaban yang benar: ${s.o[s.a]}.</span>`; }
  $("#kuisNext").disabled = false;
}
 
/* ============ SERTIFIKAT ============ */
function renderSertifikat(){
  const nama = ($("#namaInput").value || "").trim();
  const kuisSelesai = quiz.started && quiz.i >= quiz.urut.length;
  const syarat = G.selesai && kuisSelesai && quiz.skor >= PASS;
  const info = $("#sertInfo");
  const area = $("#sertifikatArea");
  const tombol = $("#sertTombol");
  if(!syarat){
    info.innerHTML = `<h3>Sertifikat belum terbuka</h3>
      <p>Untuk mendapatkan sertifikat, kamu perlu:</p>
      <ul>
        <li>${G.selesai ? "✅" : "⬜"} Menyelesaikan semua rintangan di menu <b>Berburu</b></li>
        <li>${kuisSelesai && quiz.skor >= PASS ? "✅" : "⬜"} Mendapat nilai minimal ${PASS} di menu <b>Kuis</b> ${kuisSelesai ? `(nilaimu: ${quiz.skor})` : ""}</li>
      </ul>`;
    area.innerHTML = ""; tombol.innerHTML = "";
    return;
  }
  info.innerHTML = `<h3>Selamat! Sertifikatmu sudah siap.</h3><p>Periksa nama di bawah, lalu cetak atau simpan sebagai PDF.</p>`;
  const tgl = new Date().toLocaleDateString("id-ID",{day:"numeric",month:"long",year:"numeric"});
  area.innerHTML = `<div class="sertifikat" id="sertifikat">
    <div class="lencana">🏆</div>
    <p class="judul">SERTIFIKAT PENGHARGAAN</p>
    <p>Diberikan kepada</p>
    <div class="nama">${nama ? escapeHtml(nama) : "Petualang Hebat"}</div>
    <p>atas keberhasilan menyelesaikan<br><b>Petualangan Bangun Datar</b><br>Matematika Kelas V · Bab Geometri: Ciri-Ciri Bangun Datar</p>
    <p>Nilai kuis: <b>${quiz.skor}</b> · Semua rintangan berhasil dilewati</p>
    <div class="ttd">
      <div><small>${tgl}</small><br>Tanggal</div>
      <div><br>Dibuat oleh: <b>Herman23</b></div>
    </div>
  </div>`;
  tombol.innerHTML = `<button class="btn" id="cetakBtn">🖨️ Cetak / Simpan PDF</button>`;
  $("#cetakBtn").addEventListener("click", () => window.print());
}
function escapeHtml(s){ return s.replace(/[&<>"']/g, c => ({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c])); }
 
/* ============ INIT ============ */
renderMateri();
renderSim();
mulaiLevel();
requestAnimationFrame(frame);
</script>
</body>
</html>
 



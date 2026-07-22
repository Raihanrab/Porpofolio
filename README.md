<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Portofolio — Editor Visual</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@400;500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #0a0c0e;
    --bg-panel: #14171b;
    --bg-panel-2: #1a1e23;
    --teal: #3a9aa3;
    --teal-dim: #1f565c;
    --teal-glow: rgba(58,154,163,0.18);
    --orange: #e8873a;
    --orange-dim: #b5652a;
    --text: #edeae3;
    --text-muted: #8a8f94;
    --border: rgba(237,234,227,0.09);
    --font-display: 'Oswald', sans-serif;
    --font-body: 'Inter', sans-serif;
    --font-mono: 'JetBrains Mono', monospace;
  }

  *{ box-sizing: border-box; }
  html{ scroll-behavior: smooth; }
  body{
    margin:0;
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-body);
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
  }
  a{ color: inherit; }
  button{ font-family: inherit; cursor: pointer; }
  img{ max-width: 100%; display:block; }

  /* ---------- layout shells ---------- */
  .page{ min-height:100vh; overflow-x: hidden; }
  .wrap{ max-width: 1180px; margin: 0 auto; padding: 0 28px; }

  /* ---------- nav ---------- */
  .nav{
    position: sticky; top:0; z-index: 50;
    backdrop-filter: blur(10px);
    background: rgba(10,12,14,0.72);
    border-bottom: 1px solid var(--border);
  }
  .nav-inner{
    max-width: 1180px; margin:0 auto; padding: 16px 28px;
    display:flex; align-items:center; justify-content:space-between;
  }
  .logo{
    font-family: var(--font-display);
    font-weight:600; letter-spacing: 0.04em;
    font-size: 1.05rem; text-transform: uppercase;
    display:flex; align-items:center; gap:10px;
  }
  .logo .dot{
    width:9px; height:9px; border-radius:50%;
    background: var(--orange);
    box-shadow: 0 0 10px 2px var(--orange);
  }
  .nav-links{ display:flex; gap: 28px; list-style:none; margin:0; padding:0; }
  .nav-links a{
    text-decoration:none; color: var(--text-muted);
    font-family: var(--font-mono); font-size: 0.78rem;
    letter-spacing: 0.06em; text-transform: uppercase;
    transition: color .2s ease;
  }
  .nav-links a:hover{ color: var(--orange); }
  .nav-toggle{ display:none; background:none; border:1px solid var(--border); color:var(--text); padding:8px 10px; border-radius:6px; }

  /* ---------- hero ---------- */
  .hero{
    padding: 96px 28px 56px;
    max-width: 1180px; margin: 0 auto;
    position: relative;
  }
  .hero-eyebrow{
    font-family: var(--font-mono); font-size: 0.82rem;
    color: var(--teal); letter-spacing: 0.08em;
    display:flex; align-items:center; gap: 12px;
    margin-bottom: 22px;
  }
  .hero-eyebrow .rec{
    width:8px; height:8px; border-radius:50%; background:#e0503a;
    animation: pulse 2s ease-in-out infinite;
  }
  @media (prefers-reduced-motion: reduce){ .hero-eyebrow .rec{ animation:none; } }
  @keyframes pulse{ 0%,100%{ opacity:1; } 50%{ opacity:.25; } }

  .hero-name{
    font-family: var(--font-display);
    font-weight: 700;
    font-size: clamp(3rem, 9vw, 6.4rem);
    line-height: 0.94;
    text-transform: uppercase;
    letter-spacing: -0.01em;
    margin: 0;
    outline: none;
  }
  .hero-name:focus{ box-shadow: 0 0 0 2px var(--orange); border-radius:4px; }
  .hero-role{
    font-family: var(--font-display);
    font-weight: 400;
    font-size: clamp(1.1rem, 2.4vw, 1.6rem);
    color: var(--teal);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin: 10px 0 22px;
    outline:none;
  }
  .hero-bio{
    max-width: 560px; color: var(--text-muted);
    font-size: 1.02rem; margin-bottom: 34px;
    outline:none;
  }
  .hero-bio:focus, .hero-role:focus{ box-shadow: 0 0 0 2px var(--teal); border-radius:4px; }
  .edit-hint{
    font-family: var(--font-mono); font-size: 0.7rem; color: var(--text-muted);
    opacity: 0.55; margin-bottom: 28px;
  }
  .hero-cta{ display:flex; gap:14px; flex-wrap:wrap; }
  .btn{
    font-family: var(--font-mono); font-size: 0.8rem; letter-spacing: 0.04em;
    text-transform: uppercase; text-decoration:none;
    padding: 13px 22px; border-radius: 3px; border: 1px solid var(--border);
    transition: all .2s ease; display:inline-flex; align-items:center; gap:8px;
  }
  .btn-primary{ background: var(--orange); border-color: var(--orange); color: #17110a; font-weight:600; }
  .btn-primary:hover{ background: #f2984f; }
  .btn-ghost{ color: var(--text); }
  .btn-ghost:hover{ border-color: var(--teal); color: var(--teal); }

  /* ---------- timeline scrubber (signature element) ---------- */
  .scrubber{
    position: relative; height: 64px; margin: 20px 0 8px;
    border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
    background:
      repeating-linear-gradient(90deg, transparent 0 38px, var(--border) 38px 39px);
    overflow:hidden;
  }
  .scrubber-holes{
    position:absolute; left:0; right:0; top:8px; display:flex; gap:30px; padding: 0 20px;
  }
  .scrubber-holes.bottom{ top:auto; bottom:8px; }
  .scrubber-holes span{
    width:8px; height:8px; border-radius:2px; background: var(--bg-panel-2);
    border: 1px solid var(--border); flex-shrink:0;
  }
  .scrubber-track{
    position:absolute; left:0; right:0; top:50%; transform: translateY(-50%);
    height:2px; background: var(--border);
  }
  .scrubber-playhead{
    position:absolute; top:0; bottom:0; width:2px; background: var(--orange);
    box-shadow: 0 0 12px 2px var(--orange-dim);
    animation: scrub 14s linear infinite;
  }
  .scrubber-playhead::after{
    content:''; position:absolute; top:26px; left:-4px; width:10px; height:10px;
    background: var(--orange); transform: rotate(45deg);
  }
  @keyframes scrub{ 0%{ left:0%; } 100%{ left:100%; } }
  @media (prefers-reduced-motion: reduce){ .scrubber-playhead{ animation:none; left:22%; } }
  .scrubber-tc{
    position:absolute; right:20px; top:50%; transform: translateY(-50%);
    font-family: var(--font-mono); font-size: 0.78rem; color: var(--text-muted);
    background: var(--bg); padding: 2px 8px;
  }

  /* ---------- sections ---------- */
  .section{ padding: 84px 28px; max-width: 1180px; margin: 0 auto; }
  .section-head{
    display:flex; align-items:baseline; justify-content:space-between;
    gap: 20px; margin-bottom: 40px; flex-wrap:wrap;
  }
  .section-title{
    font-family: var(--font-display); text-transform: uppercase;
    font-size: clamp(1.7rem, 3.4vw, 2.6rem); font-weight:600; margin:0;
    letter-spacing: -0.01em;
  }
  .section-tag{
    font-family: var(--font-mono); font-size: 0.75rem; color: var(--teal);
    letter-spacing: 0.08em; text-transform:uppercase;
  }
  .filters{ display:flex; gap:10px; flex-wrap:wrap; margin-bottom: 28px; }
  .filter-btn{
    background: var(--bg-panel); border:1px solid var(--border); color: var(--text-muted);
    font-family: var(--font-mono); font-size: 0.72rem; letter-spacing: 0.05em;
    text-transform: uppercase; padding: 8px 14px; border-radius: 999px;
    transition: all .2s ease;
  }
  .filter-btn:hover{ color: var(--text); }
  .filter-btn.active{ background: var(--teal-dim); border-color: var(--teal); color: var(--text); }

  .grid{ display:grid; grid-template-columns: repeat(auto-fill, minmax(280px,1fr)); gap: 22px; }

  .card{
    background: var(--bg-panel); border: 1px solid var(--border); border-radius: 6px;
    overflow:hidden; position:relative; transition: transform .25s ease, border-color .25s ease;
  }
  .card:hover{ transform: translateY(-4px); border-color: var(--teal-dim); }
  .card-media{
    aspect-ratio: 16/9; background: var(--bg-panel-2); position:relative; overflow:hidden;
  }
  .card-media img{ width:100%; height:100%; object-fit: cover; }
  .card-media iframe{ width:100%; height:100%; border:0; }
  .card.photo .card-media{ aspect-ratio: 4/5; }
  .card-play{
    position:absolute; inset:0; display:flex; align-items:center; justify-content:center;
    background: linear-gradient(180deg, rgba(10,12,14,0) 40%, rgba(10,12,14,0.55));
    pointer-events:none;
  }
  .card-play svg{ width:44px; height:44px; opacity:0.9; filter: drop-shadow(0 2px 8px rgba(0,0,0,0.5)); }
  .card-body{ padding: 14px 16px 16px; }
  .card-title{ font-weight:600; font-size: 0.98rem; margin: 0 0 6px; }
  .card-meta{
    display:flex; align-items:center; justify-content:space-between;
    font-family: var(--font-mono); font-size: 0.68rem; color: var(--text-muted);
    text-transform: uppercase; letter-spacing: 0.05em;
  }
  .card-tag{ color: var(--orange); }
  .card-del{
    position:absolute; top:10px; right:10px; z-index:2;
    width:26px; height:26px; border-radius:50%; border:1px solid var(--border);
    background: rgba(10,12,14,0.65); color: var(--text); font-size: 0.85rem;
    display:flex; align-items:center; justify-content:center; opacity:0; transition: opacity .2s ease;
  }
  .card:hover .card-del{ opacity:1; }
  .card-del:hover{ border-color:#e0503a; color:#e0503a; }

  .empty{
    border: 1px dashed var(--border); border-radius: 6px; padding: 40px 24px;
    text-align:center; color: var(--text-muted); font-size: 0.94rem;
  }
  .empty strong{ color: var(--text); display:block; margin-bottom: 6px; font-family: var(--font-display); text-transform:uppercase; letter-spacing:0.02em; font-size:1.05rem; }

  /* ---------- tentang ---------- */
  .about-grid{ display:grid; grid-template-columns: 1fr 1fr; gap: 48px; align-items:start; }
  .about-text{ color: var(--text-muted); font-size: 1.02rem; outline:none; }
  .about-text:focus{ box-shadow: 0 0 0 2px var(--teal); border-radius:4px; }
  .stat-list{ display:flex; flex-direction:column; gap:0; }
  .stat-row{
    display:flex; justify-content:space-between; padding: 16px 0;
    border-bottom: 1px solid var(--border);
    font-family: var(--font-mono); font-size: 0.85rem;
  }
  .stat-row span:first-child{ color: var(--text-muted); text-transform:uppercase; letter-spacing:0.05em; font-size:0.72rem; padding-top:3px; }
  .stat-row span:last-child{ color: var(--text); font-size: 1.6rem; font-family: var(--font-display); }

  /* ---------- upload ---------- */
  .upload-grid{ display:grid; grid-template-columns: 1fr 1fr; gap: 28px; }
  .upload-panel{
    background: var(--bg-panel); border:1px solid var(--border); border-radius: 8px; padding: 26px;
  }
  .upload-panel h3{
    font-family: var(--font-display); text-transform: uppercase; letter-spacing:0.02em;
    font-size: 1.15rem; margin: 0 0 4px;
  }
  .upload-panel .sub{ color: var(--text-muted); font-size: 0.85rem; margin: 0 0 22px; }
  .field{ margin-bottom: 16px; }
  .field label{
    display:block; font-family: var(--font-mono); font-size: 0.68rem; letter-spacing:0.06em;
    text-transform: uppercase; color: var(--text-muted); margin-bottom: 8px;
  }
  .field input[type="text"], .field input[type="url"], .field select{
    width:100%; background: var(--bg); border:1px solid var(--border); color: var(--text);
    padding: 11px 12px; border-radius: 4px; font-size: 0.92rem; font-family: var(--font-body);
  }
  .field input:focus, .field select:focus{ outline:none; border-color: var(--teal); }
  .file-drop{
    border: 1px dashed var(--border); border-radius: 4px; padding: 22px; text-align:center;
    color: var(--text-muted); font-size: 0.85rem; position:relative; cursor:pointer;
    transition: border-color .2s ease;
  }
  .file-drop:hover{ border-color: var(--teal); }
  .file-drop input{ position:absolute; inset:0; opacity:0; cursor:pointer; }
  .file-drop.has-file{ border-style:solid; border-color: var(--orange); color: var(--text); }
  .btn-add{
    width:100%; background: var(--teal-dim); border: 1px solid var(--teal); color: var(--text);
    font-family: var(--font-mono); font-size: 0.8rem; letter-spacing:0.05em; text-transform:uppercase;
    padding: 13px; border-radius: 4px; margin-top: 6px; transition: background .2s ease;
  }
  .btn-add:hover{ background: var(--teal); }
  .form-msg{ font-family: var(--font-mono); font-size: 0.75rem; margin-top: 10px; min-height: 1em; }
  .form-msg.err{ color: #e0503a; }
  .form-msg.ok{ color: var(--teal); }

  footer{
    border-top: 1px solid var(--border); padding: 30px 28px;
    font-family: var(--font-mono); font-size: 0.72rem; color: var(--text-muted);
    text-align:center; letter-spacing: 0.04em;
  }

  @media (max-width: 760px){
    .nav-links{
      position:absolute; top:100%; left:0; right:0; flex-direction:column;
      background: var(--bg-panel); border-bottom: 1px solid var(--border);
      padding: 18px 28px; gap: 16px; display:none;
    }
    .nav-links.open{ display:flex; }
    .nav-toggle{ display:block; }
    .about-grid, .upload-grid{ grid-template-columns: 1fr; }
    .hero{ padding-top: 70px; }
  }
</style>
</head>
<body>
<div class="page">

  <header class="nav">
    <div class="nav-inner">
      <div class="logo"><span class="dot"></span> Cut&nbsp;/&nbsp;Frame</div>
      <button class="nav-toggle" id="navToggle" aria-label="Buka menu">☰</button>
      <ul class="nav-links" id="navLinks">
        <li><a href="#showreel">Showreel</a></li>
        <li><a href="#foto">Foto</a></li>
        <li><a href="#tentang">Tentang</a></li>
        <li><a href="#upload">Upload Karya</a></li>
      </ul>
    </div>
  </header>

  <section class="hero" id="top">
    <div class="hero-eyebrow"><span class="rec"></span> REC · <span class="tc" id="liveTc">00:00:00:00</span></div>
    <h1 class="hero-name" id="heroName" contenteditable="true" spellcheck="false">Nama Kamu</h1>
    <p class="hero-role" id="heroRole" contenteditable="true" spellcheck="false">Video &amp; Foto Editor</p>
    <p class="hero-bio" id="heroBio" contenteditable="true" spellcheck="false">Bercerita lewat gambar bergerak dan diam — dari color grading sinematik sampai retouch foto yang rapi dan natural.</p>
    <p class="edit-hint">Klik teks di atas untuk mengedit langsung</p>
    <div class="hero-cta">
      <a href="#showreel" class="btn btn-primary">▶ Lihat Showreel</a>
      <a href="#foto" class="btn btn-ghost">Lihat Foto</a>
    </div>
  </section>

  <div class="scrubber" aria-hidden="true">
    <div class="scrubber-holes"><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span></div>
    <div class="scrubber-holes bottom"><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span><span></span></div>
    <div class="scrubber-track"></div>
    <div class="scrubber-playhead"></div>
    <div class="scrubber-tc">TIMELINE</div>
  </div>

  <section class="section" id="showreel">
    <div class="section-head">
      <h2 class="section-title">Showreel</h2>
      <span class="section-tag" id="videoCount">0 video</span>
    </div>
    <div class="filters" id="videoFilters"></div>
    <div class="grid" id="videoGrid"></div>
  </section>

  <section class="section" id="foto">
    <div class="section-head">
      <h2 class="section-title">Galeri Foto</h2>
      <span class="section-tag" id="photoCount">0 foto</span>
    </div>
    <div class="filters" id="photoFilters"></div>
    <div class="grid" id="photoGrid"></div>
  </section>

  <section class="section" id="tentang">
    <div class="section-head">
      <h2 class="section-title">Tentang</h2>
      <span class="section-tag">Profil</span>
    </div>
    <div class="about-grid">
      <p class="about-text" id="aboutText" contenteditable="true" spellcheck="false">Saya editor visual yang senang merangkai potongan gambar jadi cerita yang enak ditonton. Fokus di editing video — pacing, transisi, color grading — dan editing foto — retouch, komposisi, dan warna. Klik di sini untuk menulis cerita kamu sendiri.</p>
      <div class="stat-list">
        <div class="stat-row"><span>Total Karya</span><span id="statTotal">0</span></div>
        <div class="stat-row"><span>Video</span><span id="statVideo">0</span></div>
        <div class="stat-row"><span>Foto</span><span id="statPhoto">0</span></div>
      </div>
    </div>
  </section>

  <section class="section" id="upload">
    <div class="section-head">
      <h2 class="section-title">Upload Karya</h2>
      <span class="section-tag">Tersimpan otomatis di browser ini</span>
    </div>
    <div class="upload-grid">

      <div class="upload-panel">
        <h3>Tambah Video</h3>
        <p class="sub">Tempel link YouTube atau Google Drive.</p>
        <form id="videoForm">
          <div class="field">
            <label for="vTitle">Judul</label>
            <input type="text" id="vTitle" placeholder="Contoh: Wedding Cinematic — Andi &amp; Rara" required>
          </div>
          <div class="field">
            <label for="vUrl">Link video (YouTube / Drive)</label>
            <input type="url" id="vUrl" placeholder="https://youtube.com/watch?v=..." required>
          </div>
          <div class="field">
            <label for="vCat">Kategori</label>
            <select id="vCat">
              <option>Showreel</option>
              <option>Musik</option>
              <option>Iklan</option>
              <option>Dokumenter</option>
              <option>Wedding</option>
              <option>Lainnya</option>
            </select>
          </div>
          <button type="submit" class="btn-add">Tambahkan Video</button>
          <div class="form-msg" id="videoMsg"></div>
        </form>
      </div>

      <div class="upload-panel">
        <h3>Tambah Foto</h3>
        <p class="sub">Unggah gambar dari perangkat kamu.</p>
        <form id="photoForm">
          <div class="field">
            <label>File foto</label>
            <div class="file-drop" id="fileDrop">
              <span id="fileDropLabel">Klik atau seret foto ke sini (JPG/PNG)</span>
              <input type="file" id="pFile" accept="image/*" required>
            </div>
          </div>
          <div class="field">
            <label for="pTitle">Judul</label>
            <input type="text" id="pTitle" placeholder="Contoh: Potret Golden Hour" required>
          </div>
          <div class="field">
            <label for="pCat">Kategori</label>
            <select id="pCat">
              <option>Potret</option>
              <option>Produk</option>
              <option>Editorial</option>
              <option>Landscape</option>
              <option>Lainnya</option>
            </select>
          </div>
          <button type="submit" class="btn-add">Tambahkan Foto</button>
          <div class="form-msg" id="photoMsg"></div>
        </form>
      </div>

    </div>
  </section>

  <footer>© <span id="year"></span> — Dibuat dengan Claude. Data tersimpan otomatis di browser kamu.</footer>
</div>

<script>
(function(){
  document.getElementById('year').textContent = new Date().getFullYear();

  // ---------- nav toggle ----------
  const navToggle = document.getElementById('navToggle');
  const navLinks = document.getElementById('navLinks');
  navToggle.addEventListener('click', () => navLinks.classList.toggle('open'));
  navLinks.querySelectorAll('a').forEach(a => a.addEventListener('click', () => navLinks.classList.remove('open')));

  // ---------- live timecode ----------
  const tcEl = document.getElementById('liveTc');
  const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  if(!reduceMotion){
    const start = performance.now();
    function pad(n,l){ return String(n).padStart(l,'0'); }
    function tick(now){
      const elapsed = (now - start)/1000;
      const h = Math.floor(elapsed/3600);
      const m = Math.floor((elapsed%3600)/60);
      const s = Math.floor(elapsed%60);
      const f = Math.floor((elapsed%1)*24);
      tcEl.textContent = pad(h,2)+':'+pad(m,2)+':'+pad(s,2)+':'+pad(f,2);
      requestAnimationFrame(tick);
    }
    requestAnimationFrame(tick);
  }

  // ---------- persistence helpers ----------
  const STORAGE_KEY = 'portfolio-items';
  const PROFILE_KEY = 'portfolio-profile';
  let items = [];
  let profile = {};

  async function loadAll(){
    try{
      const r = await window.storage.get(STORAGE_KEY, false);
      items = r && r.value ? JSON.parse(r.value) : [];
    }catch(e){ items = []; }
    try{
      const r2 = await window.storage.get(PROFILE_KEY, false);
      profile = r2 && r2.value ? JSON.parse(r2.value) : {};
    }catch(e){ profile = {}; }
    applyProfile();
    render();
  }

  async function saveItems(){
    try{ await window.storage.set(STORAGE_KEY, JSON.stringify(items), false); }
    catch(e){ console.error('Gagal menyimpan karya', e); }
  }
  async function saveProfile(){
    try{ await window.storage.set(PROFILE_KEY, JSON.stringify(profile), false); }
    catch(e){ console.error('Gagal menyimpan profil', e); }
  }

  function applyProfile(){
    if(profile.name) document.getElementById('heroName').textContent = profile.name;
    if(profile.role) document.getElementById('heroRole').textContent = profile.role;
    if(profile.bio) document.getElementById('heroBio').textContent = profile.bio;
    if(profile.about) document.getElementById('aboutText').textContent = profile.about;
  }

  ['heroName','heroRole','heroBio'].forEach(id => {
    const el = document.getElementById(id);
    el.addEventListener('blur', () => {
      const map = { heroName:'name', heroRole:'role', heroBio:'bio' };
      profile[map[id]] = el.textContent.trim();
      saveProfile();
    });
  });
  document.getElementById('aboutText').addEventListener('blur', function(){
    profile.about = this.textContent.trim();
    saveProfile();
  });

  // ---------- id gen ----------
  function uid(){ return Date.now().toString(36) + Math.random().toString(36).slice(2,7); }

  // ---------- video url parsing ----------
  function parseVideo(url){
    let m = url.match(/(?:youtube\.com\/(?:watch\?v=|embed\/|shorts\/)|youtu\.be\/)([\w-]{11})/);
    if(m) return { kind:'youtube', embed:'https://www.youtube.com/embed/'+m[1], thumb:'https://img.youtube.com/vi/'+m[1]+'/hqdefault.jpg' };
    m = url.match(/drive\.google\.com\/file\/d\/([\w-]+)/);
    if(m) return { kind:'drive', embed:'https://drive.google.com/file/d/'+m[1]+'/preview', thumb:null };
    return { kind:'link', embed:null, thumb:null, raw:url };
  }

  const playIcon = '<svg viewBox="0 0 24 24" fill="white"><circle cx="12" cy="12" r="11" fill="rgba(10,12,14,0.55)" stroke="white" stroke-width="1.2"/><path d="M10 8l6 4-6 4z"/></svg>';

  // ---------- filters state ----------
  let videoFilter = 'Semua';
  let photoFilter = 'Semua';

  function buildFilters(container, list, current, onPick){
    const cats = ['Semua', ...new Set(list.map(i => i.category))];
    container.innerHTML = '';
    cats.forEach(cat => {
      const b = document.createElement('button');
      b.className = 'filter-btn' + (cat === current ? ' active' : '');
      b.textContent = cat;
      b.addEventListener('click', () => onPick(cat));
      container.appendChild(b);
    });
  }

  function render(){
    const videos = items.filter(i => i.type === 'video');
    const photos = items.filter(i => i.type === 'photo');

    document.getElementById('videoCount').textContent = videos.length + ' video';
    document.getElementById('photoCount').textContent = photos.length + ' foto';
    document.getElementById('statTotal').textContent = items.length;
    document.getElementById('statVideo').textContent = videos.length;
    document.getElementById('statPhoto').textContent = photos.length;

    buildFilters(document.getElementById('videoFilters'), videos, videoFilter, (cat) => { videoFilter = cat; render(); });
    buildFilters(document.getElementById('photoFilters'), photos, photoFilter, (cat) => { photoFilter = cat; render(); });

    renderGrid('videoGrid', videos.filter(v => videoFilter === 'Semua' || v.category === videoFilter), 'video');
    renderGrid('photoGrid', photos.filter(p => photoFilter === 'Semua' || p.category === photoFilter), 'photo');
  }

  function renderGrid(gridId, list, type){
    const grid = document.getElementById(gridId);
    grid.innerHTML = '';
    if(list.length === 0){
      const empty = document.createElement('div');
      empty.className = 'empty';
      empty.innerHTML = type === 'video'
        ? '<strong>Belum ada video</strong>Tambahkan showreel pertamamu lewat form Upload Karya di bawah.'
        : '<strong>Belum ada foto</strong>Unggah foto pertamamu lewat form Upload Karya di bawah.';
      grid.appendChild(empty);
      return;
    }
    list.slice().reverse().forEach(item => {
      const card = document.createElement('div');
      card.className = 'card' + (type === 'photo' ? ' photo' : '');

      let mediaHtml = '';
      if(type === 'video'){
        if(item.embed){
          mediaHtml = '<iframe src="'+item.embed+'" allowfullscreen loading="lazy"></iframe>';
        } else {
          mediaHtml = '<div class="card-play" style="position:static;height:100%;background:linear-gradient(135deg,var(--bg-panel-2),var(--bg-panel));">'+playIcon+'</div>';
        }
      } else {
        mediaHtml = '<img src="'+item.image+'" alt="'+escapeHtml(item.title)+'" loading="lazy">';
      }

      card.innerHTML =
        '<button class="card-del" data-id="'+item.id+'" title="Hapus">✕</button>' +
        '<div class="card-media">'+mediaHtml+'</div>' +
        '<div class="card-body">' +
          '<p class="card-title">'+escapeHtml(item.title)+'</p>' +
          '<div class="card-meta"><span class="card-tag">'+escapeHtml(item.category)+'</span><span>'+timeAgo(item.createdAt)+'</span></div>' +
        '</div>';
      grid.appendChild(card);
    });

    grid.querySelectorAll('.card-del').forEach(btn => {
      btn.addEventListener('click', async () => {
        items = items.filter(i => i.id !== btn.dataset.id);
        await saveItems();
        render();
      });
    });
  }

  function escapeHtml(str){
    return str.replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
  }
  function timeAgo(ts){
    const diff = Date.now() - ts;
    const day = 86400000;
    if(diff < 3600000) return 'Baru saja';
    if(diff < day) return Math.floor(diff/3600000) + ' jam lalu';
    return Math.floor(diff/day) + ' hari lalu';
  }

  // ---------- video form ----------
  document.getElementById('videoForm').addEventListener('submit', async function(e){
    e.preventDefault();
    const msg = document.getElementById('videoMsg');
    const title = document.getElementById('vTitle').value.trim();
    const url = document.getElementById('vUrl').value.trim();
    const category = document.getElementById('vCat').value;
    if(!title || !url){ msg.textContent = 'Isi judul dan link dulu ya.'; msg.className = 'form-msg err'; return; }
    const parsed = parseVideo(url);
    items.push({ id: uid(), type:'video', title, category, embed: parsed.embed, thumb: parsed.thumb, kind: parsed.kind, createdAt: Date.now() });
    await saveItems();
    this.reset();
    msg.textContent = 'Video ditambahkan ke showreel.';
    msg.className = 'form-msg ok';
    render();
  });

  // ---------- photo form ----------
  const fileDrop = document.getElementById('fileDrop');
  const fileInput = document.getElementById('pFile');
  const fileLabel = document.getElementById('fileDropLabel');
  fileInput.addEventListener('change', () => {
    if(fileInput.files[0]){
      fileDrop.classList.add('has-file');
      fileLabel.textContent = fileInput.files[0].name;
    }
  });

  function resizeImage(file, maxDim){
    return new Promise((resolve, reject) => {
      const reader = new FileReader();
      reader.onload = (e) => {
        const img = new Image();
        img.onload = () => {
          let w = img.width, h = img.height;
          if(w > h && w > maxDim){ h = Math.round(h * maxDim / w); w = maxDim; }
          else if(h > maxDim){ w = Math.round(w * maxDim / h); h = maxDim; }
          const canvas = document.createElement('canvas');
          canvas.width = w; canvas.height = h;
          canvas.getContext('2d').drawImage(img, 0, 0, w, h);
          resolve(canvas.toDataURL('image/jpeg', 0.82));
        };
        img.onerror = reject;
        img.src = e.target.result;
      };
      reader.onerror = reject;
      reader.readAsDataURL(file);
    });
  }

  document.getElementById('photoForm').addEventListener('submit', async function(e){
    e.preventDefault();
    const msg = document.getElementById('photoMsg');
    const title = document.getElementById('pTitle').value.trim();
    const category = document.getElementById('pCat').value;
    const file = fileInput.files[0];
    if(!title || !file){ msg.textContent = 'Pilih foto dan isi judul dulu ya.'; msg.className = 'form-msg err'; return; }
    msg.textContent = 'Mengunggah...';
    msg.className = 'form-msg';
    try{
      const dataUrl = await resizeImage(file, 1400);
      items.push({ id: uid(), type:'photo', title, category, image: dataUrl, createdAt: Date.now() });
      await saveItems();
      this.reset();
      fileDrop.classList.remove('has-file');
      fileLabel.textContent = 'Klik atau seret foto ke sini (JPG/PNG)';
      msg.textContent = 'Foto ditambahkan ke galeri.';
      msg.className = 'form-msg ok';
      render();
    }catch(err){
      msg.textContent = 'Gagal memproses foto. Coba file lain.';
      msg.className = 'form-msg err';
    }
  });

  loadAll();
})();
</script>
</body>
</html>

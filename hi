<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
  <meta name="color-scheme" content="light dark">
  <title>Responsive Timer with Embedded Image</title>
  <style>
    :root{
      --bg:#0b0b0c;
      --card:#141518;
      --text:#e8eaf0;
      --muted:#9aa3b2;
      --border:#2a2e36;
      --accent:#4f8cff;
      --danger:#ff5d6c;
      --ok:#22c55e;
      --shadow:0 10px 28px rgba(0,0,0,.35);
      --radius:16px;
      --focus:#9dbdff;
      --pad:16px;
    }
    @media (prefers-color-scheme: light){
      :root{
        --bg:#f6f7fb; --card:#ffffff; --text:#0e1320; --muted:#5b6472; --border:#e7e9ee;
        --shadow:0 10px 24px rgba(16,24,40,.06);
        --focus:#2563eb;
      }
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Apple Color Emoji", "Segoe UI Emoji";
      background:var(--bg);
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
    }

    .wrap{
      max-width:900px;
      margin:0 auto;
      padding:clamp(12px,2.5vw,20px);
      display:grid;
      gap:clamp(10px,2vw,16px);
    }

    .card{
      background:var(--card);
      border:1px solid var(--border);
      border-radius:var(--radius);
      box-shadow:var(--shadow);
      padding:clamp(12px,2.5vw,18px);
    }

    h1{
      margin:0 0 8px 0;
      font-size:clamp(1.15rem, 1.5rem + 0.3vw, 1.5rem);
      line-height:1.2;
    }
    .sub{
      margin:0 0 10px 0;
      color:var(--muted);
      font-size:clamp(.9rem, .85rem + .2vw, 1rem);
    }

    .grid{
      display:grid;
      gap:12px;
      grid-template-columns: 1fr;
    }
    @media (min-width:720px){
      .grid.two{
        grid-template-columns: 1fr auto auto auto;
        align-items:end;
      }
    }

    label{
      display:block;
      font-weight:700;
      font-size:.95rem;
      margin-bottom:6px;
      color:var(--text);
    }

    input[type="text"],
    input[type="number"],
    select{
      width:100%;
      padding:12px 14px;
      background:transparent;
      color:var(--text);
      border:1px solid var(--border);
      border-radius:12px;
      font-size:1rem;
      outline:none;
    }
    input::placeholder{color:var(--muted)}
    input:focus, select:focus{border-color:var(--focus); box-shadow:0 0 0 3px color-mix(in oklab, var(--focus) 25%, transparent)}

    .row{
      display:flex;
      flex-wrap:wrap;
      gap:10px;
      align-items:center;
    }

    .btn{
      appearance:none;
      border:none;
      border-radius:12px;
      padding:12px 15px;
      font-weight:800;
      font-size:clamp(.95rem, .9rem + .2vw, 1rem);
      color:#fff; background:var(--accent);
      cursor:pointer;
      transition:transform .05s ease, opacity .2s ease, background .2s ease;
      touch-action:manipulation;
    }
    .btn:active{transform:translateY(1px)}
    .btn.alt{background:#6b7280}
    .btn.ok{background:var(--ok)}
    .btn.danger{background:var(--danger)}
    .btn:disabled{opacity:.6; cursor:not-allowed}

    .toolbar{
      display:flex; flex-wrap:wrap; gap:8px;
    }

    /* Image area */
    .img-wrap{
      width:100%;
      border:1px dashed var(--border);
      border-radius:14px;
      overflow:hidden;
      background:#0f1114;
      display:flex;align-items:center;justify-content:center;
      margin-bottom:8px;
    }
    @media (prefers-color-scheme: light){ .img-wrap{background:#fff} }

    .img-wrap.s{aspect-ratio:16/9; max-height:180px}
    .img-wrap.m{aspect-ratio:16/9; max-height:260px}
    .img-wrap.l{aspect-ratio:16/9; max-height:340px}
    .img-wrap img{width:100%; height:100%; object-fit:cover; display:block}

    @media (max-width:480px){
      .img-wrap.s{max-height:150px}
      .img-wrap.m{max-height:210px}
      .img-wrap.l{max-height:260px}
    }

    .time{
      font-variant-numeric:tabular-nums;
      font-weight:900;
      text-align:center;
      font-size:clamp(2.2rem, 8vw, 3.2rem);
      letter-spacing:.5px;
      margin:4px 0 2px 0;
    }
    .status{
      text-align:center; color:var(--muted);
      font-size:clamp(.95rem, .9rem + .2vw, 1rem);
      margin-bottom:6px;
    }
    .badges{display:flex;gap:8px;flex-wrap:wrap;justify-content:center}
    .badge{background:color-mix(in oklab, var(--accent) 7%, transparent); border:1px solid var(--border); padding:6px 10px; border-radius:999px; font-size:.92rem; color:var(--text)}

    /* Big touch targets for mobile footer actions */
    .actions{
      display:grid; gap:8px;
      grid-template-columns: repeat(3, 1fr);
    }
    .actions .btn{padding:14px 10px}
    @media (min-width:640px){
      .actions{grid-template-columns: repeat(6, auto)}
    }

    /* Reduce motion for users who prefer it */
    @media (prefers-reduced-motion: reduce){
      .btn{transition:none}
    }
  </style>
</head>
<body>
  <div class="wrap">
    <div class="card" role="region" aria-label="Timer with image">
      <h1>Timer with Embedded Image</h1>
      <p class="sub">Works on desktop, tablets, and phones. Settings and state are saved locally per browser.</p>

      <!-- Image controls -->
      <div class="grid two" aria-label="Image controls">
        <div>
          <label for="imgSrc">Image URL</label>
          <input id="imgSrc" type="text" inputmode="url" placeholder="https://example.com/image.jpg" aria-describedby="imgHelp"/>
          <small id="imgHelp" style="color:var(--muted);display:block;margin-top:6px">Paste a direct image link. The image will auto-scale.</small>
        </div>
        <div>
          <label for="imgSize">Size</label>
          <select id="imgSize" aria-label="Image size">
            <option value="s">Small</option>
            <option value="m" selected>Medium</option>
            <option value="l">Large</option>
          </select>
        </div>
        <div class="toolbar" style="align-self:end">
          <button id="applyImg" class="btn alt" aria-label="Apply image">Apply</button>
          <button id="clearImg" class="btn danger" aria-label="Clear image">Clear</button>
        </div>
      </div>

      <!-- Embedded image -->
      <div id="imgWrap" class="img-wrap m">
        <img id="heroImg" alt="Embedded illustration" />
      </div>

      <!-- Timer controls -->
      <div class="row" aria-label="Timer inputs">
        <div style="min-width:120px">
          <label for="min">Minutes</label>
          <input id="min" type="number" min="0" inputmode="numeric" value="5" aria-label="Minutes" />
        </div>
        <div style="min-width:120px">
          <label for="sec">Seconds</label>
          <input id="sec" type="number" min="0" max="59" inputmode="numeric" value="0" aria-label="Seconds" />
        </div>
        <div class="toolbar" style="margin-left:auto">
          <button id="start" class="btn ok">Start</button>
          <button id="pause" class="btn alt" disabled>Pause</button>
          <button id="resume" class="btn" disabled>Resume</button>
          <button id="finish" class="btn" disabled>Finish</button>
          <button id="reset" class="btn danger" disabled>Reset</button>
          <button id="plus1" class="btn alt" disabled>+1 min</button>
        </div>
      </div>

      <div class="time" id="display" aria-live="polite">05:00</div>
      <div class="status" id="status">Ready</div>

      <div class="badges" role="status" aria-live="polite">
        <span class="badge" id="startBadge">Start: —</span>
        <span class="badge" id="endBadge">End: —</span>
        <span class="badge" id="spentBadge">Spent: 0s</span>
      </div>
    </div>
  </div>

  <script>
    // Utility helpers
    const $ = id => document.getElementById(id);
    const pad = n => String(n).padStart(2,'0');
    const fmt = s => `${pad(Math.floor(s/60))}:${pad(s%60)}`;
    const when = d => new Date(d).toLocaleString(undefined,{hour12:false});
    const vibrate = pat => { try{ if(navigator.vibrate) navigator.vibrate(pat); }catch{} };

    // Elements
    const imgSrc = $('imgSrc'), imgSize = $('imgSize'), imgWrap = $('imgWrap'), heroImg = $('heroImg');
    const applyImg = $('applyImg'), clearImg = $('clearImg');
    const min = $('min'), sec = $('sec'), display = $('display'), statusEl = $('status');
    const startBtn = $('start'), pauseBtn = $('pause'), resumeBtn = $('resume'), finishBtn = $('finish'), resetBtn = $('reset'), plus1Btn = $('plus1');
    const startBadge = $('startBadge'), endBadge = $('endBadge'), spentBadge = $('spentBadge');

    // Timer state
    let total = 300, remain = 300, running=false, paused=false, interval=null;
    let startTime=null, endTime=null, pausedMs=0, pauseStart=null;

    // Local Storage
    const LS_STATE = 'timerImgStateV2';

    // Default image (your provided URL)
    const DEFAULT_IMG = "https://wallpapers.com/images/hd/pokemon-pictures-8zk4zk2ni8sq48yg.jpg";

    // Save and load
    function save(){
      try{
        const s = {
          total, remain, running, paused,
          startTime: startTime? startTime.toISOString(): null,
          endTime: endTime? endTime.toISOString(): null,
          pausedMs,
          img: imgSrc.value || '',
          size: imgSize.value || 'm'
        };
        localStorage.setItem(LS_STATE, JSON.stringify(s));
      }catch(e){
        console.warn('LocalStorage unavailable:', e);
      }
    }

    function load(){
      try{
        const raw = localStorage.getItem(LS_STATE);
        if(raw){
          try{
            const s = JSON.parse(raw);
            total = s.total ?? total;
            remain = s.remain ?? total;
            running = !!s.running; paused = !!s.paused;
            startTime = s.startTime? new Date(s.startTime): null;
            endTime = s.endTime? new Date(s.endTime): null;
            pausedMs = s.pausedMs || 0;
            imgSrc.value = s.img || DEFAULT_IMG;
            imgSize.value = s.size || 'm';
          }catch{
            imgSrc.value = DEFAULT_IMG;
            imgSize.value = 'm';
          }
        } else {
          imgSrc.value = DEFAULT_IMG;
          imgSize.value = 'm';
        }
      }catch{
        imgSrc.value = DEFAULT_IMG;
        imgSize.value = 'm';
      }
      min.value = Math.floor(total/60);
      sec.value = total%60;
      applyImage(false);
      refreshUIOnLoad();
    }

    function refreshUIOnLoad(){
      display.textContent = fmt(remain);
      spentBadge.textContent = 'Spent: ' + spentSeconds() + 's';
      if(running){
        statusEl.textContent = paused ? 'Paused' : 'Running';
        startBadge.textContent = startTime ? 'Start: ' + when(startTime) : 'Start: —';
        endBadge.textContent = endTime ? 'End: ' + when(endTime) : 'End: —';
        setControls({start:false, pause:!paused, resume:paused, finish:true, reset:paused, plus1:true});
        if(!paused && remain>0){
          interval = setInterval(tick, 1000);
        }
      } else {
        statusEl.textContent = endTime ? 'Finished' : 'Ready';
        setControls({start:true, pause:false, resume:false, finish:false, reset:false, plus1:false});
      }
    }

    function setControls(x){
      startBtn.disabled = !x.start;
      pauseBtn.disabled = !x.pause;
      resumeBtn.disabled = !x.resume;
      finishBtn.disabled = !x.finish;
      resetBtn.disabled = !x.reset;
      plus1Btn.disabled = !x.plus1;
    }

    function updateFromInputs(){
      const m = Math.max(0, parseInt(min.value||'0',10));
      const s = Math.max(0, Math.min(59, parseInt(sec.value||'0',10)));
      total = m*60 + s;
      remain = total;
      display.textContent = fmt(remain);
      spentBadge.textContent = 'Spent: 0s';
      save();
    }
    min.addEventListener('input', updateFromInputs, {passive:true});
    sec.addEventListener('input', updateFromInputs, {passive:true});

    function tick(){
      if(!running || paused) return;
      remain = Math.max(0, remain-1);
      display.textContent = fmt(remain);
      spentBadge.textContent = 'Spent: ' + spentSeconds() + 's';
      if(remain<=0){
        clearInterval(interval);
        running=false;
        endTime = new Date();
        statusEl.textContent = 'Time up';
        endBadge.textContent = 'End: ' + when(endTime);
        setControls({start:true, pause:false, resume:false, finish:false, reset:true, plus1:false});
        vibrate([120,40,120]); // gently alert on mobile
        save();
      } else {
        save();
      }
    }

    function spentSeconds(){
      if(!startTime) return 0;
      const end = endTime || new Date();
      return Math.max(0, Math.round((end - startTime - pausedMs)/1000));
    }

    // Timer actions
    startBtn.addEventListener('click', ()=>{
      if(running) return;
      if(remain<=0) updateFromInputs();
      running=true; paused=false;
      startTime = new Date(); endTime=null; pausedMs=0; pauseStart=null;
      startBadge.textContent = 'Start: ' + when(startTime);
      endBadge.textContent = 'End: —';
      statusEl.textContent = 'Running';
      setControls({start:false, pause:true, resume:false, finish:true, reset:false, plus1:true});
      interval = setInterval(tick, 1000);
      vibrate(30);
      save();
    });

    pauseBtn.addEventListener('click', ()=>{
      if(!running || paused) return;
      paused = true; pauseStart = new Date();
      statusEl.textContent = 'Paused';
      setControls({start:false, pause:false, resume:true, finish:true, reset:true, plus1:true});
      vibrate(15);
      save();
    });

    resumeBtn.addEventListener('click', ()=>{
      if(!running || !paused) return;
      paused = false; pausedMs += (new Date() - pauseStart);
      statusEl.textContent = 'Running';
      setControls({start:false, pause:true, resume:false, finish:true, reset:false, plus1:true});
      vibrate(20);
      save();
    });

    finishBtn.addEventListener('click', ()=>{
      if(interval) clearInterval(interval);
      running=false; paused=false;
      endTime = new Date();
      const spent = spentSeconds();
      remain = Math.max(0, total - spent);
      display.textContent = fmt(remain);
      statusEl.textContent = 'Finished';
      endBadge.textContent = 'End: ' + when(endTime);
      setControls({start:true, pause:false, resume:false, finish:false, reset:true, plus1:false});
      spentBadge.textContent = 'Spent: ' + spent + 's';
      vibrate([30,30,30]);
      save();
    });

    resetBtn.addEventListener('click', ()=>{
      if(interval) clearInterval(interval);
      running=false; paused=false; startTime=null; endTime=null; pausedMs=0; pauseStart=null;
      updateFromInputs();
      statusEl.textContent = 'Ready';
      startBadge.textContent = 'Start: —';
      endBadge.textContent = 'End: —';
      setControls({start:true, pause:false, resume:false, finish:false, reset:false, plus1:false});
      vibrate(10);
      save();
    });

    plus1Btn.addEventListener('click', ()=>{
      total += 60; remain += 60;
      display.textContent = fmt(remain);
      vibrate(8);
      save();
    });

    // Image handling with better mobile ergonomics
    function applyImage(showAlertOnError=true){
      const src = (imgSrc.value || '').trim();
      const size = imgSize.value || 'm';
      imgWrap.classList.remove('s','m','l');
      imgWrap.classList.add(size);

      if(!src){
        heroImg.removeAttribute('src');
        save();
        return;
      }
      heroImg.onload = ()=>{ save(); };
      heroImg.onerror = ()=>{
        if(showAlertOnError) alert('Failed to load image. Ensure it’s a direct, accessible image URL.');
      };
      heroImg.src = src;
      save();
    }
    applyImg.addEventListener('click', ()=>applyImage(true));
    clearImg.addEventListener('click', ()=>{
      imgSrc.value = '';
      applyImage(false);
    });
    imgSize.addEventListener('change', ()=>applyImage(false));
    imgSrc.addEventListener('keyup', e=>{ if(e.key==='Enter') applyImage(true); });

    // Improve number input on iOS/Android: prevent wheel-change on desktop
    ['min','sec'].forEach(id=>{
      const el = $(id);
      el.addEventListener('wheel', e=>e.target === document.activeElement && e.preventDefault(), {passive:false});
    });

    // Load last state
    load();
  </script>
</body>
</html>

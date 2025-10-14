<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Contador do Amor ❤️</title>
  <style>
    :root{--bg:#0f172a;--card:#0b1220;--accent:#ff6b81;--glass: rgba(255,255,255,0.04)}
    html,body{height:100%;margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,'Helvetica Neue',Arial}
    body{background:var(--bg);color:#e6eef8;display:flex;align-items:center;justify-content:center;padding:24px}
    .wrap{width:100%;max-width:980px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:16px;padding:20px;box-shadow:0 10px 30px rgba(2,6,23,0.6);position:relative;overflow:hidden}
    .bg-image{position:absolute;inset:0;background-size:cover;background-position:center;filter:blur(6px) saturate(0.9) brightness(0.45);z-index:0}
    .content{position:relative;z-index:2;display:grid;grid-template-columns:1fr 380px;gap:18px}
    header{display:flex;align-items:center;gap:12px}
    h1{margin:0;font-size:22px}
    p.lead{margin:4px 0 0;color:#cfe6ff90}
    .panel{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:12px;padding:16px}

    .counter{display:flex;gap:10px;flex-wrap:wrap}
    .tile{flex:1 1 120px;background:var(--glass);border-radius:10px;padding:12px;display:flex;flex-direction:column;align-items:center;justify-content:center;min-width:110px}
    .num{font-size:28px;font-weight:700;line-height:1;transition:all .25s ease;display:inline-block;min-width:56px;text-align:center}
    .label{font-size:12px;color:#cfe6ffb0;margin-top:6px;text-transform:uppercase;letter-spacing:0.06em}

    .controls{display:flex;flex-direction:column;gap:10px}
    input,input[type=file],button,select{width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:inherit}
    .small{padding:8px;font-size:13px}
    .row{display:flex;gap:8px}
    .row > *{flex:1}
    .muted{font-size:13px;color:#bcd9ff88}

    footer{margin-top:12px;font-size:13px;color:#aacbf877}

    @media (max-width:880px){.content{grid-template-columns:1fr;}.tile{flex:1 1 40%}}
  </style>
</head>
<body>
  <div class="wrap">
    <div id="bgImg" class="bg-image" aria-hidden="true"></div>
    <div class="content">
      <div>
        <header>
          <div style="width:56px;height:56px;border-radius:12px;background:linear-gradient(90deg,var(--accent),#ff9ab0);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:20px">❤</div>
          <div>
            <h1>Contador do Amor</h1>
            <p class="lead">Conte o tempo do relacionamento animado (inclui segundos). Salve para usar offline.</p>
          </div>
        </header>

        <section style="margin-top:14px" class="panel">
          <div class="counter" id="counter">
            <div class="tile"><div class="num" id="years">0</div><div class="label">anos</div></div>
            <div class="tile"><div class="num" id="months">0</div><div class="label">meses</div></div>
            <div class="tile"><div class="num" id="days">0</div><div class="label">dias</div></div>
            <div class="tile"><div class="num" id="hours">0</div><div class="label">horas</div></div>
            <div class="tile"><div class="num" id="minutes">0</div><div class="label">minutos</div></div>
            <div class="tile"><div class="num" id="seconds">0</div><div class="label">segundos</div></div>
          </div>

          <footer>
            <div id="sinceText">Escolha a data de início para começar a contagem.</div>
          </footer>
        </section>
      </div>

      <aside>
        <div class="panel controls">
          <label for="start">Data de início do relacionamento</label>
          <input id="start" type="date" />
          <div class="row">
            <input id="name" placeholder="Nome do casal (opcional)" />
            <button id="saveName" class="small">Salvar</button>
          </div>

          <label for="bgfile">Imagem de fundo (upload)</label>
          <input id="bgfile" type="file" accept="image/*" />
          <div class="row">
            <button id="removeBg" class="small">Remover fundo</button>
            <button id="downloadBtn" class="small">Baixar página</button>
          </div>

          <div style="margin-top:6px" class="muted">Sugestão: rode com <strong>Live Server</strong> no VSCode para ativar cache offline (service worker). Se abrir diretamente pelo arquivo (file://) o cache pode não funcionar.</div>
        </div>

        <div style="margin-top:12px" class="panel">
          <div class="muted">Limitações offline</div>
          <ul style="margin:8px 0 0 18px;color:#bcd9ffad">
            <li>Service worker funciona se a página for servida via HTTP(S) / localhost.</li>
            <li>Imagens muito grandes podem não caber no armazenamento local.</li>
            <li>Ao limpar dados do navegador, as configurações são perdidas.</li>
          </ul>
        </div>
      </aside>
    </div>
  </div>

  <script>
    function daysInMonth(y,m){return new Date(y,m+1,0).getDate();}

    function computeYMDHMS(from, to){
      let y = to.getFullYear() - from.getFullYear();
      let m = to.getMonth() - from.getMonth();
      let d = to.getDate() - from.getDate();
      let hh = to.getHours() - from.getHours();
      let mm = to.getMinutes() - from.getMinutes();
      let ss = to.getSeconds() - from.getSeconds();

      if (ss < 0){ ss += 60; mm -= 1; }
      if (mm < 0){ mm += 60; hh -= 1; }
      if (hh < 0){ hh += 24; d -= 1; }
      if (d < 0){
        const prevMonth = new Date(to.getFullYear(), to.getMonth()-1, 1);
        d += daysInMonth(prevMonth.getFullYear(), prevMonth.getMonth());
        m -= 1;
      }
      if (m < 0){ m += 12; y -= 1; }
      if (y < 0){ return {future:true}; }
      return {years:y, months:m, days:d, hours:hh, minutes:mm, seconds:ss};
    }

    const els = {years:document.getElementById('years'),months:document.getElementById('months'),days:document.getElementById('days'),hours:document.getElementById('hours'),minutes:document.getElementById('minutes'),seconds:document.getElementById('seconds'),sinceText:document.getElementById('sinceText')};
    const inputStart = document.getElementById('start');
    const bgFile = document.getElementById('bgfile');
    const bgImgDiv = document.getElementById('bgImg');
    const removeBgBtn = document.getElementById('removeBg');
    const nameInput = document.getElementById('name');
    const saveNameBtn = document.getElementById('saveName');
    const downloadBtn = document.getElementById('downloadBtn');

    function loadState(){
      const s = localStorage.getItem('love_start');
      if (s){ try{ inputStart.value = s; }catch(e){} }
      const bg = localStorage.getItem('love_bg');
      if (bg){ bgImgDiv.style.backgroundImage = `url(${bg})`; }
      const n = localStorage.getItem('love_name');
      if (n){ nameInput.value = n; updateTitle(n); }
    }

    function updateTitle(name){
      if (name) document.querySelector('h1').textContent = name + ' — Contador do Amor';
    }

    inputStart.addEventListener('change', ()=>{
      localStorage.setItem('love_start', inputStart.value);
      resetAndStart();
    });

    saveNameBtn.addEventListener('click', ()=>{ localStorage.setItem('love_name', nameInput.value || ''); updateTitle(nameInput.value); });

    bgFile.addEventListener('change', (e)=>{
      const f = e.target.files && e.target.files[0];
      if (!f) return;
      const reader = new FileReader();
      reader.onload = ()=>{
        const data = reader.result;
        try{ localStorage.setItem('love_bg', data); }
        catch(err){ alert('Não foi possível salvar a imagem localmente (arquivo grande). Use direto sem salvar ou reduza o tamanho.'); }
        bgImgDiv.style.backgroundImage = `url(${data})`;
      };
      reader.readAsDataURL(f);
    });

    removeBgBtn.addEventListener('click', ()=>{ localStorage.removeItem('love_bg'); bgImgDiv.style.backgroundImage = '' });

    downloadBtn.addEventListener('click', ()=>{
      const blob = new Blob([document.documentElement.outerHTML], {type:'text/html'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href = url; a.download = 'contador-do-amor.html'; document.body.appendChild(a); a.click(); a.remove(); setTimeout(()=>URL.revokeObjectURL(url), 1500);
    });

    let ticker = null;
    function resetAndStart(){
      if (ticker) clearInterval(ticker);
      const val = inputStart.value;
      if (!val){ els.sinceText.textContent = 'Escolha a data de início para começar a contagem.'; setTilesToZero(); return; }
      const start = new Date(val + 'T00:00:00');
      if (isNaN(start)) { els.sinceText.textContent = 'Data inválida'; return; }
      els.sinceText.textContent = `Contando desde ${start.toLocaleDateString()}`;

      function tick(){
        const now = new Date();
        const diff = computeYMDHMS(start, now);
        if (diff.future){ els.sinceText.textContent = 'A data escolhida está no futuro.'; setTilesToZero(); return; }
        animateTile(els.years, diff.years);
        animateTile(els.months, diff.months);
        animateTile(els.days, diff.days);
        animateTile(els.hours, diff.hours);
        animateTile(els.minutes, diff.minutes);
        animateTile(els.seconds, diff.seconds);
      }
      tick();
      ticker = setInterval(tick, 1000);
    }

    function setTilesToZero(){ ['years','months','days','hours','minutes','seconds'].forEach(id=>{document.getElementById(id).textContent='0'}); }

    function animateTile(el, value){
      if (el.textContent != String(value)){
        el.style.transform = 'translateY(-8px)';
        el.style.opacity = '0';
        setTimeout(()=>{ el.textContent = value; el.style.transform='translateY(0)'; el.style.opacity='1'; }, 160);
      }
    }

    loadState();
    resetAndStart();

    window.addEventListener('load', ()=>{ if (inputStart.value) resetAndStart(); });

    (function tryServiceWorker(){
      if (!('serviceWorker' in navigator)) return;
      const swCode = `self.addEventListener('install', e => { self.skipWaiting(); e.waitUntil(caches.open('love-cache-v1').then(c => c.addAll(['/', '/index.html'])) );});
      self.addEventListener('activate', e => { e.waitUntil(self.clients.claim()); });
      self.addEventListener('fetch', e => { e.respondWith(caches.match(e.request).then(r=>r||fetch(e.request))); });`;

      try{
        const blob = new Blob([swCode], {type: 'application/javascript'});
        const swUrl = URL.createObjectURL(blob);
        navigator.serviceWorker.register(swUrl).then(reg=>{
          console.log('Service worker (blob) registrado', reg);
        }).catch(err=>{
          console.warn('Não foi possível registrar service worker via blob:', err);
          navigator.serviceWorker.register('sw.js').then(r=>console.log('sw.js registrado')).catch(()=>{});
        });
      }catch(e){console.warn('SW não suportado:', e)}
    })();
  </script>
</body>
</html>

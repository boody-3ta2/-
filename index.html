<!--
// ============================================================
// هذا الملف صفحة HTML و Service Worker في الوقت نفسه (نفس المحتوى).
// عند تحميله كسكربت يعمل الجزء التالي فقط ويضيف ترويسات العزل
// (COOP/COEP) التي يحتاجها محاكي PSP، وعند فتحه كصفحة يظهر الموقع.
// ============================================================
self.addEventListener("install", function () { self.skipWaiting(); });
self.addEventListener("activate", function (e) { e.waitUntil(self.clients.claim()); });
self.addEventListener("fetch", function (e) {
  var r = e.request;
  if (r.cache === "only-if-cached" && r.mode !== "same-origin") return;
  var req = (r.mode === "no-cors") ? new Request(r, { credentials: "omit" }) : r;
  e.respondWith(
    fetch(req).then(function (res) {
      if (res.status === 0) return res;
      var h = new Headers(res.headers);
      h.set("Cross-Origin-Embedder-Policy", "credentialless");
      h.set("Cross-Origin-Opener-Policy", "same-origin");
      return new Response(res.body, { status: res.status, statusText: res.statusText, headers: h });
    }).catch(function (err) { console.error(err); })
  );
});
/*
-->
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#0f1220">
<title>مشغّل PSP</title>
<style>
  :root{--bg:#0f1220;--card:#181c30;--line:#2a3050;--acc:#5b8cff;--txt:#e8ebff;--mut:#8a93b8;--ok:#4ade80}
  *{box-sizing:border-box}
  html,body{margin:0;background:var(--bg);color:var(--txt);font-family:system-ui,"Segoe UI",Tahoma,sans-serif}
  .wrap{max-width:820px;margin:0 auto;padding:20px 14px}
  h1{font-size:24px;margin:6px 0 4px}
  p.sub{color:var(--mut);margin:0 0 16px;font-size:14px}
  .card{background:var(--card);border:1px solid var(--line);border-radius:16px;padding:18px}
  #status{padding:10px 12px;border-radius:10px;background:#00000030;font-size:14px;margin-bottom:14px}
  #status.ok{color:var(--ok)}
  #drop{border:2px dashed var(--line);border-radius:14px;padding:34px 14px;text-align:center;cursor:pointer;transition:.2s}
  #drop.over,#drop:hover{border-color:var(--acc);background:#1c2240}
  #drop b{display:block;font-size:17px;margin-bottom:6px}
  #drop span{color:var(--mut);font-size:13px}
  #fname{margin:12px 0 0;color:var(--acc);font-weight:600;min-height:22px;word-break:break-all;font-size:14px}
  button{background:var(--acc);color:#fff;border:0;border-radius:12px;padding:13px 28px;font-size:16px;font-weight:600;cursor:pointer;margin-top:12px;width:100%}
  button:disabled{opacity:.4;cursor:not-allowed}
  .warn{background:#3a2a14;border:1px solid #7a5522;color:#ffd9a0;border-radius:12px;padding:12px 14px;margin-top:14px;font-size:14px;line-height:1.8;display:none}
  .warn code{background:#00000040;padding:1px 6px;border-radius:6px;direction:ltr;display:inline-block}
  ul.tips{color:var(--mut);font-size:13.5px;line-height:1.9;padding-inline-start:20px;margin:16px 0 0}
  #stage{display:none;width:100%;height:100vh;height:100dvh}
  #game{width:100%;height:100%}
  body.playing .wrap{display:none}
  body.playing #stage{display:block}
</style>
</head>
<body>
<div class="wrap">
  <h1>🎮 مشغّل ألعاب PSP</h1>
  <p class="sub">ارفع ملف اللعبة (ISO / CSO / PBP) وابدأ اللعب مباشرة من المتصفح.</p>

  <div class="card">
    <div id="status">⏳ جارٍ فحص المتصفح...</div>

    <div id="drop">
      <b>اضغط لاختيار ملف اللعبة</b>
      <span>الملف يبقى على جهازك ولا يُرفع لأي خادم</span>
      <input id="file" type="file" hidden>
    </div>
    <div id="fname"></div>
    <button id="start" disabled>ابدأ اللعب ▶</button>

    <div class="warn" id="warn"></div>

    <ul class="tips">
      <li>الحفظ: من أزرار المحاكي اختر <b>Save State</b> و <b>Load State</b>، وتُحفظ داخل المتصفح لكل لعبة.</li>
      <li>على الهاتف تظهر أزرار اللمس تلقائيًا. الأفضل تدوير الشاشة أفقيًا.</li>
      <li>ملفات CSO أخف على ذاكرة الهاتف من ISO.</li>
    </ul>
  </div>
</div>

<div id="stage"><div id="game"></div></div>

<script>
(function(){
  var drop = document.getElementById('drop');
  var input = document.getElementById('file');
  var fname = document.getElementById('fname');
  var startBtn = document.getElementById('start');
  var warn = document.getElementById('warn');
  var statusEl = document.getElementById('status');
  var chosen = null, ready = false;

  function setStatus(t, ok){ statusEl.textContent = t; statusEl.className = ok ? 'ok' : ''; }
  function refresh(){ startBtn.disabled = !(ready && chosen); }

  function fail(msg){
    setStatus('❌ تعذّرت تهيئة المحاكي', false);
    warn.style.display = 'block';
    warn.innerHTML = msg || (
      'يحتاج محاكي PSP إلى تفعيل العزل في المتصفح، ولا يمكن ذلك من فتح الملف مباشرة من الجهاز. ' +
      'ارفع الملف على استضافة https (مثل GitHub Pages) <b>مرتين بنفس المحتوى</b>: ' +
      'مرة باسم <code>index.html</code> ومرة باسم <code>coi-sw.js</code>، ثم افتح رابط الموقع.'
    );
  }

  function reload(){
    var n = 0;
    try { n = +(sessionStorage.getItem('coi-tries') || 0); } catch(e){}
    if (n >= 3) { fail(); return; }
    try { sessionStorage.setItem('coi-tries', n + 1); } catch(e){}
    location.reload();
  }

  if (window.crossOriginIsolated) {
    ready = true;
    setStatus('✅ المحاكي جاهز، اختر لعبتك', true);
    try { sessionStorage.removeItem('coi-tries'); } catch(e){}
  } else if ('serviceWorker' in navigator && window.isSecureContext) {
    setStatus('⏳ جارٍ تهيئة المحاكي لأول مرة، قد تُعاد الصفحة تلقائيًا...', false);
    navigator.serviceWorker.register('coi-sw.js').then(function(reg){
      if (navigator.serviceWorker.controller) { fail(); return; }
      reg.addEventListener('updatefound', reload);
      if (reg.active) reload();
    }).catch(function(){ fail(); });
  } else {
    fail();
  }

  drop.addEventListener('click', function(){ input.click(); });
  input.addEventListener('change', function(){ pick(input.files[0]); });
  ['dragenter','dragover'].forEach(function(e){
    drop.addEventListener(e, function(ev){ ev.preventDefault(); drop.classList.add('over'); });
  });
  ['dragleave','drop'].forEach(function(e){
    drop.addEventListener(e, function(ev){ ev.preventDefault(); drop.classList.remove('over'); });
  });
  drop.addEventListener('drop', function(ev){ pick(ev.dataTransfer.files[0]); });

  function pick(f){
    if (!f) return;
    chosen = f;
    fname.textContent = f.name + '  (' + (f.size/1048576).toFixed(1) + ' MB)';
    refresh();
  }

  startBtn.addEventListener('click', function(){
    if (!chosen || !ready) return;
    document.body.classList.add('playing');

    window.EJS_player = '#game';
    window.EJS_core = 'psp';
    window.EJS_gameUrl = URL.createObjectURL(chosen);
    window.EJS_gameName = chosen.name.replace(/\.[^.]+$/, '');
    window.EJS_pathtodata = 'https://cdn.emulatorjs.org/stable/data/';
    window.EJS_threads = true;
    window.EJS_startOnLoaded = true;
    window.EJS_language = 'ar-AR';
    window.EJS_color = '#5b8cff';

    var s = document.createElement('script');
    s.src = window.EJS_pathtodata + 'loader.js';
    document.body.appendChild(s);
  });
})();
</script>
</body>
</html>
<!-- */

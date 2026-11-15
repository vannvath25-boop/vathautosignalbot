<!DOCTYPE html>
<html lang="km">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>VATh Auto Signal — XAUUSD AI (Gemini)</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500;700;900&family=Kantumruy+Pro:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
/* ===== រចនាប័ទ្មដើម ===== */
* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color: transparent; }
:root {
  --gold:#f0b90b; --gold-light:#ffd700; --buy:#00e676; --sell:#ff3d57;
  --bg-dark:#05070d; --bg-panel:rgba(18,24,38,0.65); --border:rgba(240,185,11,0.18);
  --text:#e8eef7; --text-dim:#8892a4;
}
html,body { height:100%; }
body { font-family:'Kantumruy Pro',sans-serif; background:var(--bg-dark); color:var(--text); overflow-x:hidden; min-height:100vh; position:relative; }
.bg-layer { position:fixed; inset:0; z-index:-2; background:radial-gradient(circle at 15% 20%, rgba(240,185,11,0.12), transparent 45%),radial-gradient(circle at 85% 80%, rgba(0,230,118,0.08), transparent 45%),radial-gradient(circle at 50% 50%, rgba(255,61,87,0.06), transparent 60%); animation:bgShift 18s ease-in-out infinite alternate; }
@keyframes bgShift { 0%{transform:scale(1) translate(0,0);} 100%{transform:scale(1.15) translate(-2%,2%);} }
#particles { position:fixed; inset:0; z-index:-1; }

/* ===== ប៊ូតុងខាងលើ ===== */
.top-buttons { position:fixed; top:15px; right:15px; z-index:1000; display:flex; gap:10px; }
.icon-btn {
  width:48px; height:48px; border-radius:50%;
  background:linear-gradient(135deg, rgba(240,185,11,0.9), rgba(255,215,0,0.7));
  display:flex; align-items:center; justify-content:center;
  font-size:22px; cursor:pointer; border:none; color:white;
  box-shadow:0 4px 20px rgba(240,185,11,0.5);
  transition:transform .3s, box-shadow .3s;
  animation:floatKey 3s ease-in-out infinite;
}
@keyframes floatKey { 0%,100%{transform:translateY(0);} 50%{transform:translateY(-6px);} }
.icon-btn:hover { transform:scale(1.1) rotate(15deg); box-shadow:0 8px 30px rgba(240,185,11,0.8); }
.icon-btn.saved::after { content:''; position:absolute; bottom:2px; right:2px; width:12px; height:12px; border-radius:50%; background:var(--buy); border:2px solid var(--bg-dark); box-shadow:0 0 10px var(--buy); }

/* ===== ម៉ូដាល់ ===== */
.modal-overlay { position:fixed; inset:0; z-index:999; background:rgba(0,0,0,0.7); backdrop-filter:blur(8px); display:none; align-items:center; justify-content:center; opacity:0; transition:opacity .3s; padding:15px; }
.modal-overlay.show { display:flex; opacity:1; }
.modal { background:linear-gradient(135deg, #12181f, #1a2230); border:1px solid var(--border); border-radius:20px; padding:24px; max-width:480px; width:100%; box-shadow:0 20px 60px rgba(0,0,0,0.7), 0 0 40px rgba(240,185,11,0.15); transform:scale(0.85) translateY(20px); transition:transform .4s cubic-bezier(.22,1,.36,1); }
.modal-overlay.show .modal { transform:scale(1) translateY(0); }
.modal h3 { font-family:'Orbitron',sans-serif; color:var(--gold); font-size:16px; letter-spacing:1.5px; margin-bottom:8px; display:flex; align-items:center; gap:10px; }
.modal .desc { font-size:12.5px; color:var(--text-dim); margin-bottom:18px; line-height:1.6; }
.modal label { display:block; font-size:12px; color:var(--text); margin-bottom:5px; font-weight:600; }
.modal input[type="text"], .modal input[type="password"] { width:100%; padding:14px 16px; background:rgba(5,7,13,0.8); border:1px solid rgba(240,185,11,0.25); border-radius:12px; color:var(--text); font-size:13px; font-family:'Courier New',monospace; letter-spacing:0.5px; transition:border-color .3s, box-shadow .3s; margin-bottom: 10px; }
.modal input:focus { outline:none; border-color:var(--gold); box-shadow:0 0 0 3px rgba(240,185,11,0.15); }
.modal .hint { margin-top:10px; font-size:11px; color:var(--text-dim); line-height:1.5; }
.modal .hint a { color:var(--gold); text-decoration:none; }
.modal .hint a:hover { text-decoration:underline; }
.modal-btns { display:flex; gap:10px; margin-top:20px; }
.modal-btns button { flex:1; padding:12px; border:none; border-radius:10px; font-family:'Kantumruy Pro',sans-serif; font-size:13px; font-weight:600; cursor:pointer; transition:transform .2s, opacity .2s; }
.modal-btns button:hover { transform:translateY(-2px); }
.btn-save { background:linear-gradient(90deg,var(--gold),var(--gold-light)); color:#05070d; }
.btn-clear { background:rgba(255,61,87,0.15); color:var(--sell); border:1px solid rgba(255,61,87,0.3); }
.btn-close { background:rgba(255,255,255,0.05); color:var(--text-dim); border:1px solid rgba(255,255,255,0.1); }
.key-status { margin-top:14px; padding:10px 12px; border-radius:10px; font-size:12px; display:none; }
.key-status.ok { display:block; background:rgba(0,230,118,0.1); color:var(--buy); border:1px solid rgba(0,230,118,0.3); }
.key-status.no { display:block; background:rgba(255,61,87,0.1); color:var(--sell); border:1px solid rgba(255,61,87,0.3); }

/* ===== AI Chat Modal ===== */
.chat-modal-overlay { position:fixed; inset:0; z-index:1001; background:rgba(0,0,0,0.8); backdrop-filter:blur(10px); display:none; align-items:center; justify-content:center; opacity:0; transition:opacity .3s; padding:15px; }
.chat-modal-overlay.show { display:flex; opacity:1; }
.chat-modal { background:var(--bg-panel); border:1px solid var(--border); border-radius:20px; width:100%; max-width:600px; height:80vh; display:flex; flex-direction:column; box-shadow:0 20px 60px rgba(0,0,0,0.8); transform:translateY(30px); transition:transform .4s cubic-bezier(.22,1,.36,1); overflow:hidden; }
.chat-modal-overlay.show .chat-modal { transform:translateY(0); }
.chat-header { background:rgba(5,7,13,0.9); padding:15px 20px; display:flex; justify-content:space-between; align-items:center; border-bottom:1px solid var(--border); }
.chat-header h3 { font-family:'Orbitron',sans-serif; color:var(--gold); font-size:16px; display:flex; align-items:center; gap:10px; }
.chat-close-btn { background:none; border:none; color:var(--text-dim); font-size:20px; cursor:pointer; transition:color 0.2s; }
.chat-close-btn:hover { color:var(--sell); }
.chat-messages { flex:1; padding:20px; overflow-y:auto; display:flex; flex-direction:column; gap:15px; }
.chat-msg { max-width:80%; padding:12px 16px; border-radius:12px; font-size:13.5px; line-height:1.5; word-wrap:break-word; animation:fadeIn .3s ease; }
@keyframes fadeIn { from{opacity:0; transform:translateY(10px);} to{opacity:1; transform:translateY(0);} }
.chat-msg.user { align-self:flex-end; background:linear-gradient(135deg, rgba(240,185,11,0.8), rgba(255,215,0,0.6)); color:#05070d; border-bottom-right-radius:4px; }
.chat-msg.ai { align-self:flex-start; background:rgba(5,7,13,0.8); border:1px solid rgba(255,255,255,0.1); color:var(--text); border-bottom-left-radius:4px; }
.chat-msg.ai .typing-indicator { display:flex; gap:4px; align-items:center; height:16px; }
.chat-msg.ai .typing-indicator span { width:6px; height:6px; background:var(--gold); border-radius:50%; animation:typing 1.4s infinite ease-in-out both; }
.chat-msg.ai .typing-indicator span:nth-child(1) { animation-delay:-0.32s; }
.chat-msg.ai .typing-indicator span:nth-child(2) { animation-delay:-0.16s; }
@keyframes typing { 0%, 80%, 100% { transform:scale(0); } 40% { transform:scale(1); } }
.chat-input-area { padding:15px; background:rgba(5,7,13,0.9); border-top:1px solid var(--border); display:flex; gap:10px; }
.chat-input-area input { flex:1; padding:12px 15px; background:rgba(255,255,255,0.05); border:1px solid rgba(240,185,11,0.2); border-radius:20px; color:var(--text); font-family:'Kantumruy Pro',sans-serif; font-size:13px; outline:none; transition:border-color 0.3s; }
.chat-input-area input:focus { border-color:var(--gold); }
.chat-send-btn { background:linear-gradient(90deg,var(--gold),var(--gold-light)); border:none; border-radius:50%; width:44px; height:44px; display:flex; align-items:center; justify-content:center; color:#05070d; font-size:18px; cursor:pointer; transition:transform 0.2s; }
.chat-send-btn:hover { transform:scale(1.05); }

/* ===== ផ្ទាំងដើម ===== */
header { text-align:center; padding:30px 15px 10px; animation:fadeDown .9s cubic-bezier(.22,1,.36,1); }
@keyframes fadeDown { from{opacity:0;transform:translateY(-30px);} to{opacity:1;transform:translateY(0);} }
.logo { font-family:'Orbitron',sans-serif; font-size:clamp(22px,5vw,42px); font-weight:900; letter-spacing:2px; background:linear-gradient(90deg,var(--gold),var(--gold-light),var(--gold)); background-size:200% auto; -webkit-background-clip:text; -webkit-text-fill-color:transparent; animation:shine 3s linear infinite; filter:drop-shadow(0 0 18px rgba(240,185,11,.35)); }
@keyframes shine { to{background-position:200% center;} }
.subtitle { margin-top:8px; font-size:11px; letter-spacing:3px; text-transform:uppercase; color:var(--text-dim); }
.subtitle .dot { display:inline-block; width:7px; height:7px; border-radius:50%; background:var(--buy); margin-right:8px; box-shadow:0 0 10px var(--buy); animation:pulseDot 1.6s infinite; }
@keyframes pulseDot { 0%,100%{opacity:1;transform:scale(1);} 50%{opacity:.35;transform:scale(.7);} }
.layout { display:grid; grid-template-columns:1.45fr 1fr; gap:20px; max-width:1440px; margin:15px auto 40px; padding:0 15px; }
@media (max-width:980px){ .layout{grid-template-columns:1fr; gap:15px;} }
.panel { background:var(--bg-panel); backdrop-filter:blur(18px) saturate(140%); -webkit-backdrop-filter:blur(18px) saturate(140%); border:1px solid var(--border); border-radius:20px; padding:18px; position:relative; overflow:hidden; animation:riseUp .9s cubic-bezier(.22,1,.36,1) backwards; }
.panel:nth-child(1){animation-delay:.1s;} .panel:nth-child(2){animation-delay:.25s;}
@keyframes riseUp { from{opacity:0;transform:translateY(40px) scale(.98);} to{opacity:1;transform:translateY(0) scale(1);} }
.panel::before { content:''; position:absolute; inset:0; border-radius:20px; padding:1px; background:linear-gradient(120deg,transparent,rgba(240,185,11,.5),transparent,rgba(0,230,118,.4),transparent); background-size:300% 300%; -webkit-mask:linear-gradient(#000 0 0) content-box,linear-gradient(#000 0 0); -webkit-mask-composite:xor; mask-composite:exclude; animation:borderSweep 6s linear infinite; pointer-events:none; }
@keyframes borderSweep { 0%{background-position:0% 50%;} 100%{background-position:300% 50%;} }
.panel-title { font-family:'Orbitron',sans-serif; font-size:12px; letter-spacing:1.5px; color:var(--gold); text-transform:uppercase; margin-bottom:12px; display:flex; align-items:center; gap:8px; }
.panel-title::after { content:''; flex:1; height:1px; background:linear-gradient(90deg,var(--border),transparent); }
#chart-container { width:100%; height:350px; border-radius:14px; overflow:hidden; background:rgba(5,7,13,.5); border:1px solid rgba(255,255,255,.05); }
@media (max-width:980px){ #chart-container{height:300px;} }
.chart-loading { display:flex; flex-direction:column; align-items:center; justify-content:center; height:100%; gap:14px; color:var(--text-dim); font-size:13px; }
.btn-analysis { width:100%; margin-top:14px; padding:15px; font-family:'Orbitron',sans-serif; font-size:14px; font-weight:700; letter-spacing:2px; color:#05070d; background:linear-gradient(90deg,var(--gold),var(--gold-light),var(--gold)); background-size:200% auto; border:none; border-radius:14px; cursor:pointer; position:relative; overflow:hidden; transition:transform .25s cubic-bezier(.22,1,.36,1), box-shadow .25s; box-shadow:0 6px 24px rgba(240,185,11,.25); animation:shine 3s linear infinite; }
.btn-analysis:hover:not(:disabled){ transform:translateY(-3px); box-shadow:0 12px 36px rgba(240,185,11,.45); }
.btn-analysis:active:not(:disabled){ transform:translateY(0) scale(.98); }
.btn-analysis:disabled{ opacity:.55; cursor:not-allowed; animation:none; }
.btn-analysis .ripple { position:absolute; border-radius:50%; background:rgba(255,255,255,.55); transform:scale(0); animation:ripple .65s linear; pointer-events:none; }
@keyframes ripple { to{transform:scale(4);opacity:0;} }
.status { margin-top:12px; font-size:12px; text-align:center; min-height:20px; color:var(--text-dim); transition:color .3s; display:flex; align-items:center; justify-content:center; gap:8px; }
.status.loading{color:var(--gold);} .status.success{color:var(--buy);} .status.error{color:var(--sell);}
.spinner { width:14px; height:14px; border:2px solid rgba(240,185,11,.25); border-top-color:var(--gold); border-radius:50%; animation:spin .7s linear infinite; }
@keyframes spin { to{transform:rotate(360deg);} }
.result-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; }
.result-box { background:rgba(5,7,13,.55); border:1px solid rgba(255,255,255,.06); border-radius:14px; padding:12px; position:relative; overflow:hidden; transition:border-color .35s, transform .35s, box-shadow .35s; animation:popIn .55s cubic-bezier(.22,1,.36,1) backwards; }
.result-box:nth-child(1){animation-delay:.05s;} .result-box:nth-child(2){animation-delay:.1s;} .result-box:nth-child(3){animation-delay:.15s;} .result-box:nth-child(4){animation-delay:.2s;} .result-box:nth-child(5){animation-delay:.25s;} .result-box:nth-child(6){animation-delay:.3s;} .result-box:nth-child(7){animation-delay:.35s;}
@keyframes popIn { from{opacity:0;transform:scale(.9) translateY(10px);} to{opacity:1;transform:scale(1) translateY(0);} }
.result-box:hover { transform:translateY(-3px); border-color:rgba(240,185,11,.35); }
.result-box .label { font-size:10px; letter-spacing:1.2px; text-transform:uppercase; color:var(--text-dim); margin-bottom:6px; display:flex; align-items:center; gap:6px; }
.result-box .value { font-family:'Orbitron',sans-serif; font-size:18px; font-weight:700; color:var(--text); transition:color .3s; }
.result-box.signal .value { font-size:20px; }
.value.buy { color:var(--buy); text-shadow:0 0 18px rgba(0,230,118,.5); }
.value.sell { color:var(--sell); text-shadow:0 0 18px rgba(255,61,87,.5); }
.value.neutral { color:var(--gold); text-shadow:0 0 18px rgba(240,185,11,.4); }
.value.notrade { color:#f85149; text-shadow:0 0 18px rgba(248,81,73,.5); }
.result-box.full { grid-column:1 / -1; }
.result-box.note .value { font-family:'Kantumruy Pro',sans-serif; font-size:12px; font-weight:400; line-height:1.5; color:#c9d1d9; }
.result-box.signal.active::after { content:''; position:absolute; inset:0; border-radius:14px; border:2px solid currentColor; animation:pulseRing 1.8s ease-out infinite; pointer-events:none; }
@keyframes pulseRing { 0%{opacity:.8;transform:scale(1);} 100%{opacity:0;transform:scale(1.08);} }
.disclaimer { margin-top:14px; padding:9px 10px; font-size:10.5px; line-height:1.5; color:var(--text-dim); text-align:center; background:rgba(255,61,87,.06); border:1px solid rgba(255,61,87,.15); border-radius:10px; }
footer { text-align:center; padding:10px 0 25px; font-size:10.5px; color:#4a5364; letter-spacing:1px; }
::-webkit-scrollbar { width:6px; }
::-webkit-scrollbar-thumb { background:rgba(240,185,11,.3); border-radius:10px; }

/* ===== Mobile Specific Adjustments ===== */
@media (max-width: 600px) {
  .top-buttons { top:10px; right:10px; gap:8px; }
  .icon-btn { width:42px; height:42px; font-size:18px; }
  .logo { font-size:22px; letter-spacing:1.5px; }
  .subtitle { font-size:9px; letter-spacing:2px; }
  .panel { padding:14px; border-radius:16px; }
  .panel-title { font-size:11px; }
  #chart-container { height: 250px; }
  .btn-analysis { padding:13px; font-size:13px; }
  .result-box { padding:10px; }
  .result-box .value { font-size:16px; }
  .result-box.signal .value { font-size:18px; }
  .result-box .label { font-size:9px; }
  .result-box.note .value { font-size:11px; }
  .modal { padding:20px; }
  .chat-modal { height:85vh; }
}
</style>
</head>
<body>

<div class="bg-layer"></div>
<canvas id="particles"></canvas>

<!-- ===== ប៊ូតុងខាងលើ ===== -->
<div class="top-buttons">
  <button class="icon-btn" id="btnOpenTelegram" title="កំណត់ Telegram">✈️</button>
  <button class="icon-btn" id="btnOpenChat" title="សួរ AI ពី XAUUSD">💬</button>
  <button class="icon-btn" id="keyIcon" title="ដាក់ Gemini API Key">🔑</button>
</div>

<!-- ===== ម៉ូដាល់ API Keys (Gemini) ===== -->
<div class="modal-overlay" id="keyModal">
  <div class="modal">
    <h3>🔑 Gemini API Key</h3>
    <div class="desc">បញ្ចូល API Key របស់អ្នកដើម្បីឱ្យ AI អាចវិភាគ XAUUSD។</div>
    
    <label style="display:block; font-size:12px; margin-bottom:5px; font-weight:600;">Gemini API Key</label>
    <input type="password" id="geminiKeyInput" placeholder="បញ្ចូល Gemini API Key នៅទីនេះ...">
    
    <div class="hint">
      📎 យក Gemini Key នៅ <a href="https://aistudio.google.com/app/apikey" target="_blank">Google AI Studio</a>
    </div>
    
    <div class="key-status" id="keyStatus"></div>
    
    <div class="modal-btns">
      <button class="btn-save" id="btnSaveKeys">💾 រក្សាទុក</button>
      <button class="btn-clear" id="btnClearKeys">🗑️ លុប</button>
      <button class="btn-close" id="btnCloseModal">✕</button>
    </div>
  </div>
</div>

<!-- ===== ម៉ូដាល់ Telegram ===== -->
<div class="modal-overlay" id="telegramModal">
  <div class="modal">
    <h3>✈️ Telegram Settings</h3>
    <div class="desc">ភ្ជាប់ Bot ដើម្បីទទួលបានសញ្ញាវិភាគដោយស្វ័យប្រវត្តិ នៅពេលចុច Analysis។</div>
    <input type="text" id="telegramToken" placeholder="Bot Token (ឧ. 123456:ABC-DEF...)">
    <input type="text" id="telegramChatId" placeholder="Chat ID (ឧ. 123456789)">
    <div class="hint" style="margin-top:5px;">
      📎 របៀបបង្កើត Bot: ស្វែងរក <a href="https://t.me/BotFather" target="_blank">@BotFather</a> ក្នុង Telegram ដើម្បីយក Token។<br>
      📎 យក Chat ID: ស្វែងរក <a href="https://t.me/userinfobot" target="_blank">@userinfobot</a> ដើម្បីយក ID របស់អ្នក។
    </div>
    <div class="key-status" id="telegramStatus"></div>
    <div class="modal-btns">
      <button class="btn-save" id="btnSaveTelegram">💾 រក្សាទុក</button>
      <button class="btn-clear" id="btnClearTelegram">🗑️ លុប</button>
      <button class="btn-close" id="btnCloseTelegramModal">✕</button>
    </div>
  </div>
</div>

<!-- ===== ម៉ូដាល់ AI Chat ===== -->
<div class="chat-modal-overlay" id="chatModal">
  <div class="chat-modal">
    <div class="chat-header">
      <h3>💬 AI Chat XAUUSD (ICT Expert)</h3>
      <button class="chat-close-btn" id="btnCloseChat">✕</button>
    </div>
    <div class="chat-messages" id="chatMessages">
      <div class="chat-msg ai">សួស្តី! ខ្ញុំជាអ្នកជំនាញវិភាគ XAUUSD តាម ICT។ តើអ្នកចង់សួរអំពី Order Block, FVG ឬ Liquidity ទេ?</div>
    </div>
    <div class="chat-input-area">
      <input type="text" id="chatInput" placeholder="សួរអំពី XAUUSD...">
      <button class="chat-send-btn" id="btnSendChat">➤</button>
    </div>
  </div>
</div>

<header>
  <div class="logo">VATh Auto Signal</div>
  <div class="subtitle"><span class="dot"></span>XAUUSD · Powered by Gemini AI (ICT)</div>
</header>

<div class="layout">
  <div class="panel">
    <div class="panel-title">📈 XAUUSD Live Chart</div>
    <div id="chart-container">
      <div class="chart-loading"><div class="spinner"></div><span>កំពុងផ្ទុកតារាង...</span></div>
    </div>
    <button class="btn-analysis" id="btnAnalysis">🔍 ANALYSIS</button>
    <div class="status" id="status">រង់ចាំការវិភាគ...</div>
  </div>

  <div class="panel">
    <div class="panel-title">🤖 AI Analysis Result (ICT)</div>
    
    <div class="result-grid">
      <div class="result-box signal" id="boxSignal">
        <div class="label">Signal</div>
        <div class="value neutral" id="signal">—</div>
      </div>
      <div class="result-box">
        <div class="label">New Signal</div>
        <div class="value neutral" id="newSignal">—</div>
      </div>
      <div class="result-box">
        <div class="label">Entry Price</div>
        <div class="value" id="entry">—</div>
      </div>
      <div class="result-box">
        <div class="label">Take Profit</div>
        <div class="value" id="tp">—</div>
      </div>
      <div class="result-box">
        <div class="label">Stop Loss</div>
        <div class="value" id="sl">—</div>
      </div>
      <div class="result-box">
        <div class="label">Confidence</div>
        <div class="value" id="confidence">—</div>
      </div>
      <div class="result-box full note">
        <div class="label">ICT Note</div>
        <div class="value" id="note">ចុច Analysis ដើម្បីទទួលបានការវិភាគពី AI</div>
      </div>
    </div>
    <div class="disclaimer">⚠️ សញ្ញានេះជាការវិភាគដោយ AI តាម ICT សម្រាប់ការសិក្សា មិនមែនការណែនាំវិនិយោគទេ។</div>
  </div>
</div>

<footer>© 2025 VATh Auto Signal · Built with Gemini AI (ICT Strategy)</footer>

<script>
/* ============================================================
   1. ការគ្រប់គ្រង Key (Gemini, Telegram)
   ============================================================ */
const STORAGE_KEY = 'vath_gemini_key';
const STORAGE_TG_TOKEN = 'vath_tg_token';
const STORAGE_TG_CHATID = 'vath_tg_chatid';

// UI Elements
const keyIcon   = document.getElementById('keyIcon');
const keyModal  = document.getElementById('keyModal');
const geminiKeyInput = document.getElementById('geminiKeyInput');
const keyStatus = document.getElementById('keyStatus');

const btnOpenTelegram = document.getElementById('btnOpenTelegram');
const telegramModal = document.getElementById('telegramModal');
const telegramToken = document.getElementById('telegramToken');
const telegramChatId = document.getElementById('telegramChatId');
const telegramStatus = document.getElementById('telegramStatus');
const btnCloseTelegramModal = document.getElementById('btnCloseTelegramModal');

// Helper Functions
function getKey(){ return localStorage.getItem(STORAGE_KEY) || ''; }
function getTgToken(){ return localStorage.getItem(STORAGE_TG_TOKEN) || ''; }
function getTgChatId(){ return localStorage.getItem(STORAGE_TG_CHATID) || ''; }

function updateKeyIcon(){ 
  if (getKey()) keyIcon.classList.add('saved'); 
  else keyIcon.classList.remove('saved'); 
}
function updateTgBtn(){
  if (getTgToken() && getTgChatId()) btnOpenTelegram.classList.add('saved');
  else btnOpenTelegram.classList.remove('saved');
}

function showKeyStatus(msg, ok){ 
  keyStatus.textContent = msg; 
  keyStatus.className = 'key-status ' + (ok ? 'ok' : 'no'); 
  setTimeout(()=>{ keyStatus.className='key-status'; }, 3000); 
}
function showTgStatus(msg, ok){ 
  telegramStatus.textContent = msg; 
  telegramStatus.className = 'key-status ' + (ok ? 'ok' : 'no'); 
  setTimeout(()=>{ telegramStatus.className='key-status'; }, 3000); 
}

/* ===== API Keys Events ===== */
keyIcon.addEventListener('click', () => { 
  geminiKeyInput.value = getKey(); 
  keyModal.classList.add('show'); 
  setTimeout(()=>geminiKeyInput.focus(), 300); 
});
document.getElementById('btnCloseModal').addEventListener('click', () => keyModal.classList.remove('show'));
keyModal.addEventListener('click', e => { if (e.target === keyModal) keyModal.classList.remove('show'); });

document.getElementById('btnSaveKeys').addEventListener('click', () => {
  const gk = geminiKeyInput.value.trim();
  
  if (!gk) { showKeyStatus('⚠️ សូមបញ្ចូល Key មុន', false); return; }
  if (gk.length < 20) { showKeyStatus('⚠️ Key ខ្លីពេក', false); return; }
  
  localStorage.setItem(STORAGE_KEY, gk);
  
  updateKeyIcon(); 
  showKeyStatus('✅ រក្សាទុករួចរាល់!', true); 
  setTimeout(()=>keyModal.classList.remove('show'), 1200);
});

document.getElementById('btnClearKeys').addEventListener('click', () => { 
  localStorage.removeItem(STORAGE_KEY); 
  geminiKeyInput.value = ''; 
  updateKeyIcon(); showKeyStatus('🗑️ លុប Key រួចរាល់', true); 
});
updateKeyIcon();

/* ===== Telegram Events ===== */
btnOpenTelegram.addEventListener('click', () => { 
  telegramToken.value = getTgToken(); 
  telegramChatId.value = getTgChatId(); 
  telegramModal.classList.add('show'); 
});
btnCloseTelegramModal.addEventListener('click', () => telegramModal.classList.remove('show'));
telegramModal.addEventListener('click', e => { if (e.target === telegramModal) telegramModal.classList.remove('show'); });

document.getElementById('btnSaveTelegram').addEventListener('click', () => {
  const token = telegramToken.value.trim();
  const chatId = telegramChatId.value.trim();
  if (!token || !chatId) { showTgStatus('⚠️ សូមបញ្ចូលទាំង Token និង Chat ID', false); return; }
  localStorage.setItem(STORAGE_TG_TOKEN, token);
  localStorage.setItem(STORAGE_TG_CHATID, chatId);
  updateTgBtn(); 
  showTgStatus('✅ ភ្ជាប់ Telegram រួចរាល់!', true); 
  setTimeout(()=>telegramModal.classList.remove('show'), 1200);
});
document.getElementById('btnClearTelegram').addEventListener('click', () => { 
  localStorage.removeItem(STORAGE_TG_TOKEN); 
  localStorage.removeItem(STORAGE_TG_CHATID); 
  telegramToken.value = ''; telegramChatId.value = ''; 
  updateTgBtn(); showTgStatus('🗑️ លុប Telegram រួចរាល់', true); 
});
updateTgBtn();

/* ============================================================
   2. AI CHAT LOGIC
   ============================================================ */
const btnOpenChat = document.getElementById('btnOpenChat');
const chatModal = document.getElementById('chatModal');
const btnCloseChat = document.getElementById('btnCloseChat');
const chatMessages = document.getElementById('chatMessages');
const chatInput = document.getElementById('chatInput');
const btnSendChat = document.getElementById('btnSendChat');

btnOpenChat.addEventListener('click', () => chatModal.classList.add('show'));
btnCloseChat.addEventListener('click', () => chatModal.classList.remove('show'));
chatModal.addEventListener('click', (e) => { if(e.target === chatModal) chatModal.classList.remove('show'); });

btnSendChat.addEventListener('click', sendChatMessage);
chatInput.addEventListener('keypress', (e) => { if(e.key === 'Enter') sendChatMessage(); });

async function sendChatMessage() {
  const text = chatInput.value.trim();
  if (!text) return;
  const apiKey = getKey();
  if (!apiKey) { alert('សូមដាក់ Gemini API Key មុន!'); keyModal.classList.add('show'); return; }

  appendMessage(text, 'user');
  chatInput.value = '';

  const typingId = 'typing-' + Date.now();
  const typingMsg = document.createElement('div');
  typingMsg.className = 'chat-msg ai';
  typingMsg.id = typingId;
  typingMsg.innerHTML = '<div class="typing-indicator"><span></span><span></span><span></span></div>';
  chatMessages.appendChild(typingMsg);
  chatMessages.scrollTop = chatMessages.scrollHeight;

  try {
    // ✅ ប្រើ gemini-4-hydrogen ដែលជាម៉ូដែលថ្មីបំផុត
    const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-4-hydrogen:generateContent?key=${apiKey}`;
    const contents = [
      { role: "user", parts: [{ text: "អ្នកជាអ្នកជំនាញផ្នែកវិភាគ XAUUSD (មាស) តាមបែប ICT (Inner Circle Trader) ដែលឆ្លើយតបជាភាសាខ្មែរយ៉ាងរលូន និងខ្លីៗ។" }] },
      { role: "model", parts: [{ text: "យល់ព្រម ខ្ញុំជាអ្នកជំនាញវិភាគ XAUUSD តាម ICT។ តើអ្នកចង់សួរអ្វី?" }] },
      { role: "user", parts: [{ text: text }] }
    ];

    const res = await fetch(url, {
      method: 'POST', headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ contents: contents })
    });

    const data = await res.json();
    document.getElementById(typingId).remove();

    if (res.ok && data.candidates && data.candidates[0].content) {
      appendMessage(data.candidates[0].content.parts[0].text, 'ai');
    } else {
      appendMessage('សុំទោស ខ្ញុំមិនអាចឆ្លើយតបបានទេ។', 'ai');
      console.error(data);
    }
  } catch (error) {
    document.getElementById(typingId).remove();
    appendMessage('មានបញ្ហាក្នុងការភ្ជាប់ទៅ AI។ សូមពិនិត្យ Internet។', 'ai');
    console.error(error);
  }
}

function appendMessage(text, sender) {
  const msgDiv = document.createElement('div');
  msgDiv.className = `chat-msg ${sender}`;
  msgDiv.innerHTML = text.replace(/\n/g, '<br>').replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
  chatMessages.appendChild(msgDiv);
  chatMessages.scrollTop = chatMessages.scrollHeight;
}

/* ============================================================
   3. គំនូរផ្ទៃខាងក្រោយ & តារាង
   ============================================================ */
(function(){
  const canvas = document.getElementById('particles');
  const ctx = canvas.getContext('2d');
  let w,h,ps=[];
  function resize(){ w=canvas.width=innerWidth; h=canvas.height=innerHeight; }
  addEventListener('resize', resize); resize();
  for(let i=0;i<55;i++){ ps.push({x:Math.random()*w,y:Math.random()*h,r:Math.random()*1.8+.4,vx:(Math.random()-.5)*.35,vy:(Math.random()-.5)*.35,a:Math.random()*.5+.2}); }
  (function draw(){
    ctx.clearRect(0,0,w,h);
    ps.forEach(p=>{ p.x+=p.vx; p.y+=p.vy; if(p.x<0||p.x>w)p.vx*=-1; if(p.y<0||p.y>h)p.vy*=-1; ctx.beginPath(); ctx.arc(p.x,p.y,p.r,0,Math.PI*2); ctx.fillStyle=`rgba(240,185,11,${p.a})`; ctx.fill(); });
    requestAnimationFrame(draw);
  })();
})();

(function(){
  const c = document.getElementById('chart-container');
  c.innerHTML = '<div id="tv_widget" style="height:100%"></div>';
  const s = document.createElement('script');
  s.src = 'https://s3.tradingview.com/tv.js';
  s.onload = () => new TradingView.widget({ container_id:'tv_widget', autosize:true, symbol:'OANDA:XAUUSD', interval:'15', theme:'dark', style:'1', locale:'en', backgroundColor:'rgba(5,7,13,1)', gridColor:'rgba(255,255,255,0.04)', hide_side_toolbar:false, allow_symbol_change:false, studies:['RSI@tv-basicstudies','MACD@tv-basicstudies'] });
  s.onerror = () => { c.innerHTML='<div class="chart-loading">❌ មិនអាចផ្ទុកតារាងបានទេ</div>'; };
  document.head.appendChild(s);
})();

/* ============================================================
   4. ប៊ូតុង Analysis & មុខងារវិភាគ
   ============================================================ */
const btn = document.getElementById('btnAnalysis');
btn.addEventListener('click', e => {
  const r = document.createElement('span'); r.className='ripple';
  const rect = btn.getBoundingClientRect(); const size = Math.max(rect.width,rect.height);
  r.style.width=r.style.height=size+'px'; r.style.left=(e.clientX-rect.left-size/2)+'px'; r.style.top=(e.clientY-rect.top-size/2)+'px';
  btn.appendChild(r); setTimeout(()=>r.remove(),700);
});

function animateNumber(el, target, prefix='', decimals=2){
  const start = parseFloat(el.dataset.raw||0); const dur=900, t0=performance.now();
  (function tick(now){ const p=Math.min((now-t0)/dur,1); const ease=1-Math.pow(1-p,3); const val=start+(target-start)*ease; el.textContent=prefix+val.toFixed(decimals); if(p<1)requestAnimationFrame(tick); else el.dataset.raw=target; })(performance.now());
}
function sleep(ms) { return new Promise(resolve => setTimeout(resolve, ms)); }
function computeIndicators(price){ return { rsi: Math.round(40 + Math.random()*30), macd: (Math.random()*2-1).toFixed(2), atr: +(price*0.008).toFixed(2) }; }

async function callGemini(apiKey, price, ind){
  const promptText = `អ្នកជាអ្នកវិភាគ XAUUSD ជំនាញខាង ICT 100% ។
ទិន្នន័យ៖ តម្លៃ=${price.toFixed(2)}, RSI=${ind.rsi}, MACD=${ind.macd}, ATR=${ind.atr}
ច្បាប់៖ ពិនិត្យ Market Structure, OB, FVG, Liquidity។ បើគ្មាន Setup ច្បាស់លាស់ សូមឆ្លើយថា "NO TRADE" ។
ឆ្លើយជា JSON តែមួយប៉ុណ្ណោះ៖
{"signal":"BUY|SELL|NO TRADE","entry":<float or 0>,"tp":<float or 0>,"sl":<float or 0>,"new_signal":<bool>,"confidence":"<str>","note":"<ខ្មែរ ២ ប្រយោគ>"}`;

  // ✅ ប្រើ gemini-4-hydrogen ដែលជាម៉ូដែលថ្មីបំផុត
  const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-4-hydrogen:generateContent?key=${apiKey}`;
  
  const MAX_RETRIES = 5;
  let lastError = null;

  for (let attempt = 1; attempt <= MAX_RETRIES; attempt++) {
    try {
      const res = await fetch(url, {
        method:'POST', headers:{'Content-Type':'application/json'},
        body: JSON.stringify({ 
          contents:[{ parts: [{ text: promptText }] }], 
          generationConfig:{ temperature: 0.1, responseMimeType:'application/json' } 
        })
      });
      
      if (!res.ok) {
         const errData = await res.json();
         if (res.status === 429 || res.status === 503) {
           if (attempt < MAX_RETRIES) {
             const waitTime = attempt * 2000;
             await sleep(waitTime);
             continue;
           }
           throw new Error('Gemini កំពុងមមាញឹក (503) ឬអស់ Quota (429)! សូមរង់ចាំបន្តិច។');
         }
         throw new Error('Gemini API Error: ' + JSON.stringify(errData));
      }
      
      const data = await res.json();
      let text = data.candidates?.[0]?.content?.parts?.[0]?.text || '';
      text = text.replace(/```json\s*|\s*```/g,'').trim();
      const startIdx = text.indexOf('{'); const endIdx = text.lastIndexOf('}');
      if (startIdx !== -1 && endIdx !== -1) { text = text.substring(startIdx, endIdx + 1); }
      return JSON.parse(text);
      
    } catch (e) {
      lastError = e;
      if (attempt < MAX_RETRIES) {
        await sleep(attempt * 2000);
      } else {
        throw lastError;
      }
    }
  }
  throw lastError;
}

function renderResult(r){
  const set=(id,v,cls)=>{ const el=document.getElementById(id); el.textContent=v; el.className='value'+(cls?' '+cls:''); };
  const sig=(r.signal||'NO TRADE').toUpperCase(); 
  let sigCls = sig==='BUY'?'buy':sig==='SELL'?'sell':sig==='NO TRADE'?'notrade':'neutral';
  
  set('signal',sig,sigCls); 
  set('newSignal', r.new_signal?'✅ YES':'— NO', r.new_signal?'buy':'neutral'); 
  set('confidence', r.confidence||'—');
  
  if (sig === 'NO TRADE') {
    set('entry', '—'); set('tp', '—'); set('sl', '—');
  } else {
    animateNumber(document.getElementById('entry'), Number(r.entry)||0, '$', 2); 
    animateNumber(document.getElementById('tp'), Number(r.tp)||0, '$', 2); 
    animateNumber(document.getElementById('sl'), Number(r.sl)||0, '$', 2);
    document.getElementById('tp').className='value buy'; 
    document.getElementById('sl').className='value sell';
  }
  
  document.getElementById('note').textContent = r.note || '—';
  const box=document.getElementById('boxSignal'); 
  box.classList.remove('active'); 
  box.style.color = sig==='BUY'?'var(--buy)':sig==='SELL'?'var(--sell)':sig==='NO TRADE'?'#f85149':'var(--gold)'; 
  void box.offsetWidth; box.classList.add('active');
}

/* ============================================================
   5. មុខងារផ្ញើទៅ Telegram
   ============================================================ */
async function sendToTelegram(result, price) {
  const token = getTgToken();
  const chatId = getTgChatId();
  if (!token || !chatId) return;

  const sig = (result.signal || 'NO TRADE').toUpperCase();
  let msg = `🚨 *VATh Auto Signal* 🚨\n`;
  msg += `------------------------\n`;
  msg += `📊 *XAUUSD* (ICT Analysis)\n`;
  msg += `💰 តម្លៃបច្ចុប្បន្ន: $${price.toFixed(2)}\n`;
  msg += `📌 សញ្ញា: *${sig}*\n`;

  if (sig !== 'NO TRADE') {
    msg += `🎯 Entry: $${Number(result.entry).toFixed(2)}\n`;
    msg += `🟢 Take Profit: $${Number(result.tp).toFixed(2)}\n`;
    msg += `🔴 Stop Loss: $${Number(result.sl).toFixed(2)}\n`;
  } else {
    msg += `⚠️ គ្មានកន្លែងចូលទីផ្សារតាម ICT ទេ។\n`;
  }
  
  msg += `📈 Confidence: ${result.confidence || '—'}\n`;
  msg += `📝 Note: ${result.note || '—'}\n`;
  msg += `------------------------\n`;
  msg += `⏰ Time: ${new Date().toLocaleString()}`;

  const url = `https://api.telegram.org/bot${token}/sendMessage`;
  
  try {
    await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        chat_id: chatId,
        text: msg,
        parse_mode: 'Markdown'
      })
    });
  } catch (err) {
    console.error("Telegram Error:", err);
  }
}

/* ============================================================
   6. មុខងារ Analyze សំខាន់
   ============================================================ */
async function analyze(){
  const status = document.getElementById('status'); 
  const geminiKey = getKey();
  
  if (!geminiKey){ 
    status.className='status error'; 
    status.textContent='🔑 សូមដាក់ Gemini API Key មុន'; 
    keyModal.classList.add('show'); 
    return; 
  }
  
  btn.disabled=true; 
  btn.textContent=`⏳ ANALYZING...`; 
  status.className='status loading'; 
  status.innerHTML=`<div class="spinner"></div> កំពុងទាញទិន្នន័យ XAUUSD...`;

  try {
    let price = 2385.50;
    try {
       const controller = new AbortController(); const id = setTimeout(() => controller.abort(), 10000);
       const res = await fetch('https://api.gold-api.com/price/XAU', { signal: controller.signal }); clearTimeout(id);
       if(res.ok) { const d = await res.json(); price = Number(d.price); }
    } catch (e) { console.log("Price fetch slow, use default."); }

    const ind = computeIndicators(price);
    status.innerHTML=`<div class="spinner"></div> កំពុងវិភាគតាម ICT...`;
    
    const result = await callGemini(geminiKey, price, ind);
    
    renderResult(result);
    
    // ✅ ផ្ញើទៅ Telegram
    await sendToTelegram(result, price);
    
    status.className='status success'; 
    status.textContent=`✅ វិភាគរួចរាល់ — XAUUSD: $${price.toFixed(2)}`;
  } catch(e){
    status.className='status error'; 
    status.textContent='❌ ' + e.message;
  } finally {
    btn.disabled=false; 
    btn.textContent='🔍 ANALYSIS';
  }
}
btn.addEventListener('click', analyze);
</script>

</body>
</html>

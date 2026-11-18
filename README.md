<!DOCTYPE html>
<html lang="km">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VATH AUTO SIGNAL — AI Gold Analysis</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Kantumruy+Pro:wght@400;600;700;800&family=Space+Grotesk:wght@500;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #05070f;
    --bg2: #0a0f1e;
    --glass: rgba(20, 27, 45, 0.55);
    --glass2: rgba(28, 37, 60, 0.7);
    --stroke: rgba(120, 160, 255, 0.12);
    --stroke2: rgba(120, 160, 255, 0.22);
    --accent: #22d3ee;
    --accent2: #a855f7;
    --accent3: #34d399;
    --buy: #22c55e;
    --sell: #f43f5e;
    --hold: #f59e0b;
    --text: #eef3ff;
    --muted: #8b97b8;
    --radius: 22px;
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  html { scroll-behavior:smooth; }
  body {
    font-family: 'Kantumruy Pro', 'Space Grotesk', system-ui, sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
    position: relative;
    -webkit-font-smoothing: antialiased;
  }

  .bg-layer {
    position: fixed; inset: 0; z-index: -2;
    background:
      radial-gradient(ellipse 80% 60% at 15% 5%, rgba(34,211,238,.18), transparent 55%),
      radial-gradient(ellipse 70% 55% at 85% 15%, rgba(168,85,247,.20), transparent 55%),
      radial-gradient(ellipse 90% 60% at 50% 100%, rgba(52,211,153,.12), transparent 55%),
      linear-gradient(180deg, var(--bg), var(--bg2));
    animation: bgShift 20s ease-in-out infinite alternate;
  }
  @keyframes bgShift {
    0% { filter: hue-rotate(0deg) brightness(1); }
    100% { filter: hue-rotate(25deg) brightness(1.1); }
  }
  .grid-layer {
    position: fixed; inset:0; z-index:-1; opacity:.35;
    background-image:
      linear-gradient(rgba(120,160,255,.05) 1px, transparent 1px),
      linear-gradient(90deg, rgba(120,160,255,.05) 1px, transparent 1px);
    background-size: 55px 55px;
    mask-image: radial-gradient(ellipse 90% 80% at 50% 40%, black 20%, transparent 80%);
    -webkit-mask-image: radial-gradient(ellipse 90% 80% at 50% 40%, black 20%, transparent 80%);
    animation: gridMove 30s linear infinite;
  }
  @keyframes gridMove {
    from { background-position: 0 0, 0 0; }
    to { background-position: 55px 55px, 55px 55px; }
  }
  .orb {
    position: fixed; border-radius:50%; filter: blur(60px);
    opacity:.45; z-index:-1; pointer-events:none;
    animation: float 18s ease-in-out infinite;
  }
  .orb.o1 { width:340px; height:340px; background: #22d3ee; top:-80px; left:-80px; }
  .orb.o2 { width:300px; height:300px; background: #a855f7; top:40%; right:-100px; animation-delay:-6s; }
  .orb.o3 { width:280px; height:280px; background: #34d399; bottom:-100px; left:30%; animation-delay:-12s; }
  @keyframes float {
    0%,100% { transform: translate(0,0) scale(1); }
    33% { transform: translate(40px,-30px) scale(1.12); }
    66% { transform: translate(-30px,30px) scale(.92); }
  }

  header {
    position: sticky; top:0; z-index: 50;
    display:flex; align-items:center; justify-content:space-between;
    padding: 16px 30px;
    background: rgba(5,7,15,.55);
    backdrop-filter: blur(22px) saturate(160%);
    -webkit-backdrop-filter: blur(22px) saturate(160%);
    border-bottom: 1px solid var(--stroke);
  }
  .logo {
    display:flex; align-items:center; gap:12px;
    font-family: 'Space Grotesk', sans-serif;
    font-size: 1.35rem; font-weight: 700; letter-spacing: 1.5px;
  }
  .logo-badge {
    width: 38px; height: 38px; border-radius: 12px;
    display:grid; place-items:center;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    box-shadow: 0 0 24px rgba(34,211,238,.5), inset 0 0 12px rgba(255,255,255,.25);
    font-size: 1.2rem;
    animation: badgePulse 3s ease-in-out infinite;
  }
  @keyframes badgePulse {
    0%,100% { box-shadow: 0 0 24px rgba(34,211,238,.5), inset 0 0 12px rgba(255,255,255,.25); }
    50% { box-shadow: 0 0 38px rgba(168,85,247,.7), inset 0 0 12px rgba(255,255,255,.35); }
  }
  .logo-text { display:flex; flex-direction:column; line-height:1.1; }
  .logo-text .brand {
    background: linear-gradient(90deg, #22d3ee, #a855f7, #34d399, #22d3ee);
    background-size: 300% 100%;
    -webkit-background-clip:text; background-clip:text; color:transparent;
    animation: brandShift 6s linear infinite;
    font-size:1.15rem;
  }
  @keyframes brandShift { to { background-position: 300% 0; } }
  .logo-text .tag {
    font-family:'Kantumruy Pro',sans-serif;
    font-size:.62rem; color: var(--muted); letter-spacing:2.5px; font-weight:600;
    text-transform:uppercase;
  }

  .header-actions { display:flex; gap:10px; align-items:center; }

  .btn {
    border:none; cursor:pointer; border-radius: 12px;
    padding: 10px 18px; font-weight:600; font-size:.9rem;
    font-family:'Kantumruy Pro',sans-serif;
    transition: all .25s cubic-bezier(.4,0,.2,1);
    color: var(--text);
    display:inline-flex; align-items:center; gap:8px;
    position:relative; overflow:hidden;
  }
  .btn-ghost {
    background: rgba(255,255,255,.04);
    border:1px solid var(--stroke);
    backdrop-filter: blur(10px);
  }
  .btn-ghost:hover {
    border-color: var(--accent);
    background: rgba(34,211,238,.08);
    box-shadow: 0 0 20px rgba(34,211,238,.2);
    transform: translateY(-2px);
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    color:#04101a; font-weight:800;
    box-shadow: 0 6px 24px rgba(34,211,238,.35);
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 10px 32px rgba(168,85,247,.45); }
  .btn-primary:disabled { opacity:.5; cursor:not-allowed; transform:none; }

  .btn-sm { padding: 7px 12px; font-size:.78rem; border-radius:9px; }
  .btn-danger {
    background: rgba(244,63,94,.14); color:#ff7a93;
    border:1px solid rgba(244,63,94,.35);
  }
  .btn-danger:hover { background: rgba(244,63,94,.24); transform:translateY(-1px); }

  main {
    max-width: 1180px; margin: 0 auto;
    padding: 36px 24px 80px;
    display:grid; gap:24px;
  }

  .hero { text-align:center; padding: 20px 0 8px; animation: fadeUp .7s ease both; }
  .hero h1 {
    font-size: clamp(1.6rem, 4vw, 2.4rem); font-weight: 800;
    background: linear-gradient(120deg, #eef3ff, #22d3ee 40%, #a855f7 70%, #34d399);
    background-size: 250% 100%;
    -webkit-background-clip:text; background-clip:text; color:transparent;
    animation: heroShift 8s linear infinite;
    margin-bottom: 10px; letter-spacing:.5px;
  }
  @keyframes heroShift { to { background-position: 250% 0; } }
  .hero p { color: var(--muted); font-size: .95rem; max-width: 560px; margin:0 auto; line-height:1.6; }

  .card {
    background: var(--glass);
    backdrop-filter: blur(24px) saturate(160%);
    -webkit-backdrop-filter: blur(24px) saturate(160%);
    border: 1px solid var(--stroke);
    border-radius: var(--radius);
    padding: 26px;
    position: relative;
    overflow: hidden;
    animation: fadeUp .7s ease both;
  }
  .card::before {
    content:''; position:absolute; inset:0; border-radius: inherit; padding:1px;
    background: linear-gradient(140deg, rgba(34,211,238,.4), transparent 40%, transparent 60%, rgba(168,85,247,.4));
    -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
    -webkit-mask-composite: xor; mask-composite: exclude;
    pointer-events:none; opacity:.7;
  }
  @keyframes fadeUp { from { opacity:0; transform: translateY(24px); } to { opacity:1; transform:none; } }

  .card-head { display:flex; align-items:center; gap:12px; margin-bottom:18px; }
  .card-head .icon-chip {
    width:34px; height:34px; border-radius:10px;
    display:grid; place-items:center; font-size:1rem;
    background: linear-gradient(135deg, rgba(34,211,238,.2), rgba(168,85,247,.2));
    border:1px solid var(--stroke2);
  }
  .card-head h2 {
    font-size:.9rem; color: var(--muted);
    text-transform: uppercase; letter-spacing:2.5px; font-weight:700;
    flex:1;
  }

  .upload-zone {
    border: 2px dashed var(--stroke2);
    border-radius: 18px;
    padding: 40px 24px;
    text-align:center;
    cursor:pointer;
    transition: all .35s cubic-bezier(.4,0,.2,1);
    position:relative; overflow:hidden;
    background: rgba(255,255,255,.015);
  }
  .upload-zone::after {
    content:''; position:absolute; inset:0;
    background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(34,211,238,.15), transparent 40%);
    opacity:0; transition: opacity .3s ease; pointer-events:none;
  }
  .upload-zone:hover::after { opacity:1; }
  .upload-zone:hover, .upload-zone.drag {
    border-color: var(--accent);
    background: rgba(34,211,238,.04);
    transform: translateY(-2px);
  }
  .upload-zone .up-icon {
    font-size: 2.6rem; margin-bottom: 12px; display:inline-block;
    animation: bob 2.5s ease-in-out infinite;
    filter: drop-shadow(0 0 14px rgba(34,211,238,.6));
  }
  @keyframes bob { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-8px)} }
  .upload-zone .up-title { font-weight:700; margin-bottom:6px; font-size:1rem; }
  .upload-zone p { color: var(--muted); font-size:.86rem; }

  #previewWrap { display:none; margin-top:18px; text-align:center; }
  #preview {
    max-width:100%; border-radius:14px; border:1px solid var(--stroke2);
    max-height:360px; object-fit:contain; display:block; margin:0 auto;
    box-shadow: 0 8px 40px rgba(0,0,0,.5);
  }
  .remove-img {
    margin-top:12px; background: rgba(244,63,94,.14); color:#ff7a93;
    border:1px solid rgba(244,63,94,.35);
  }
  .remove-img:hover { background: rgba(244,63,94,.24); transform:translateY(-2px); }

  .analysis-btn {
    width:100%; padding: 20px;
    font-family:'Kantumruy Pro',sans-serif;
    font-size: 1.05rem; font-weight: 800; letter-spacing: 3px;
    border-radius: 16px; border: none; cursor:pointer;
    background: linear-gradient(135deg, #22d3ee, #a855f7, #34d399, #22d3ee);
    background-size: 300% 100%;
    color:#04101a;
    animation: gradShift 5s linear infinite;
    transition: transform .25s ease, box-shadow .25s ease;
    position:relative; overflow:hidden;
    box-shadow: 0 8px 30px rgba(34,211,238,.3);
  }
  @keyframes gradShift { to { background-position: 300% 0; } }
  .analysis-btn::before {
    content:''; position:absolute; top:0; left:-100%; width:100%; height:100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,.5), transparent);
    transition: left .6s ease;
  }
  .analysis-btn:hover::before { left:100%; }
  .analysis-btn:hover { transform: translateY(-3px) scale(1.01); box-shadow: 0 14px 40px rgba(168,85,247,.45); }
  .analysis-btn:active { transform: translateY(-1px) scale(.99); }
  .analysis-btn:disabled {
    opacity:.55; cursor:not-allowed; transform:none;
    animation:none; background:#2a3350; color:var(--muted);
    box-shadow:none;
  }
  .analysis-btn:disabled::before { display:none; }

  .results { display:grid; grid-template-columns: repeat(auto-fit, minmax(160px,1fr)); gap:16px; }
  .result-box {
    background: var(--glass2);
    border:1px solid var(--stroke);
    border-radius:16px; padding:20px 18px;
    text-align:center; position:relative; overflow:hidden;
    transition: all .35s cubic-bezier(.4,0,.2,1);
  }
  .result-box::before {
    content:''; position:absolute; top:0; left:0; right:0; height:2px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    opacity:.4;
  }
  .result-box:hover { transform: translateY(-3px); border-color: var(--stroke2); }
  .result-box .label {
    font-size:.72rem; color: var(--muted);
    text-transform: uppercase; letter-spacing:2px;
    margin-bottom:10px; font-weight:700;
    display:flex; align-items:center; justify-content:center; gap:6px;
  }
  .result-box .value {
    font-family:'Space Grotesk',sans-serif;
    font-size:1.55rem; font-weight:700; color: var(--text);
    transition: all .4s ease; word-break:break-word;
  }

  .result-box.signal {
    grid-column: 1 / -1;
    padding: 30px 20px;
    background:
      radial-gradient(ellipse at 50% 120%, rgba(34,211,238,.12), transparent 70%),
      var(--glass2);
  }
  .result-box.signal .value {
    font-size: clamp(2.6rem, 8vw, 3.8rem);
    letter-spacing: 6px; font-weight: 800;
    transition: all .5s cubic-bezier(.34,1.56,.64,1);
  }
  .result-box.signal .label { letter-spacing:4px; font-size:.78rem; }

  .signal-buy  { color: var(--buy);  text-shadow: 0 0 30px rgba(34,197,94,.7), 0 0 60px rgba(34,197,94,.35); }
  .signal-sell { color: var(--sell); text-shadow: 0 0 30px rgba(244,63,94,.7), 0 0 60px rgba(244,63,94,.35); }
  .signal-hold { color: var(--hold); text-shadow: 0 0 30px rgba(245,158,11,.7), 0 0 60px rgba(245,158,11,.35); }

  .result-box.signal.buy  { border-color: rgba(34,197,94,.35);  box-shadow: 0 0 50px rgba(34,197,94,.15) inset; }
  .result-box.signal.sell { border-color: rgba(244,63,94,.35);  box-shadow: 0 0 50px rgba(244,63,94,.15) inset; }
  .result-box.signal.hold { border-color: rgba(245,158,11,.35); box-shadow: 0 0 50px rgba(245,158,11,.15) inset; }

  .reason {
    margin-top:18px; padding:18px 20px;
    background: rgba(10,15,30,.65);
    border-radius:14px;
    border-left:3px solid var(--accent);
    font-size:.92rem; line-height:1.7; color:#c8d3ee;
    white-space:pre-wrap;
    animation: fadeUp .5s ease both;
  }

  .tg-status {
    display:inline-flex; align-items:center; gap:6px;
    margin-top:12px; padding:8px 14px; border-radius:10px;
    font-size:.8rem; font-weight:600;
    transition: all .3s ease;
  }
  .tg-status.sending { background: rgba(34,211,238,.12); color: var(--accent); border:1px solid rgba(34,211,238,.3); }
  .tg-status.success { background: rgba(34,197,94,.14); color: #4ade80; border:1px solid rgba(34,197,94,.35); }
  .tg-status.error   { background: rgba(244,63,94,.14); color: #fb7185; border:1px solid rgba(244,63,94,.35); }
  .tg-status.hidden  { display:none; }

  .loader { display:none; text-align:center; padding: 30px 20px; }
  .loader.active { display:block; animation: fadeUp .4s ease; }
  .spinner {
    width:52px; height:52px; margin: 0 auto 16px;
    border:3px solid rgba(120,160,255,.15);
    border-top-color: var(--accent);
    border-right-color: var(--accent2);
    border-radius:50%;
    animation: spin 1s linear infinite;
    box-shadow: 0 0 24px rgba(34,211,238,.3);
  }
  @keyframes spin { to { transform: rotate(360deg); } }
  .loader p { color: var(--muted); font-size:.92rem; letter-spacing:.5px; }
  .progress-bar {
    width: 220px; height: 4px; margin: 14px auto 0;
    background: rgba(120,160,255,.12); border-radius: 4px; overflow:hidden;
  }
  .progress-fill {
    width: 40%; height:100%;
    background: linear-gradient(90deg, var(--accent), var(--accent2), var(--accent));
    background-size: 200% 100%;
    border-radius: 4px;
    animation: progressMove 1.6s ease-in-out infinite, gradShift 2s linear infinite;
  }
  @keyframes progressMove {
    0% { margin-left:-40%; } 100% { margin-left:100%; }
  }

  /* ===== History ===== */
  .history-head {
    display:flex; align-items:center; gap:12px; margin-bottom:18px;
  }
  .history-head .count-badge {
    background: linear-gradient(135deg, rgba(34,211,238,.22), rgba(168,85,247,.22));
    border:1px solid var(--stroke2);
    padding: 3px 10px; border-radius: 20px;
    font-size:.72rem; font-weight:700; color: var(--accent);
    font-family:'Space Grotesk',sans-serif;
  }
  .history-list { display:flex; flex-direction:column; gap:12px; max-height: 520px; overflow-y:auto; padding-right:6px; }
  .history-list::-webkit-scrollbar { width:6px; }
  .history-list::-webkit-scrollbar-track { background: transparent; }
  .history-list::-webkit-scrollbar-thumb { background: rgba(120,160,255,.2); border-radius:3px; }
  .history-list::-webkit-scrollbar-thumb:hover { background: rgba(120,160,255,.35); }

  .history-item {
    background: var(--glass2);
    border:1px solid var(--stroke);
    border-radius: 14px;
    padding: 16px 18px;
    display: grid;
    grid-template-columns: auto 1fr auto;
    gap: 14px; align-items: center;
    transition: all .3s cubic-bezier(.4,0,.2,1);
    animation: itemIn .4s ease both;
    position: relative;
    overflow: hidden;
  }
  @keyframes itemIn { from { opacity:0; transform: translateX(-12px); } to { opacity:1; transform:none; } }
  .history-item::before {
    content:''; position:absolute; left:0; top:0; bottom:0; width:3px;
  }
  .history-item.buy::before  { background: var(--buy);  box-shadow: 0 0 12px var(--buy); }
  .history-item.sell::before { background: var(--sell); box-shadow: 0 0 12px var(--sell); }
  .history-item.hold::before { background: var(--hold); box-shadow: 0 0 12px var(--hold); }
  .history-item:hover {
    border-color: var(--stroke2);
    transform: translateX(3px);
    background: rgba(28,37,60,.85);
  }

  .history-signal {
    font-family:'Space Grotesk',sans-serif;
    font-size:.85rem; font-weight:800;
    padding: 6px 12px; border-radius: 8px;
    letter-spacing:1px; white-space:nowrap;
  }
  .history-signal.buy  { background: rgba(34,197,94,.15); color:#4ade80; border:1px solid rgba(34,197,94,.3); }
  .history-signal.sell { background: rgba(244,63,94,.15); color:#fb7185; border:1px solid rgba(244,63,94,.3); }
  .history-signal.hold { background: rgba(245,158,11,.15); color:#fbbf24; border:1px solid rgba(245,158,11,.3); }

  .history-details { display:flex; flex-direction:column; gap:6px; min-width:0; }
  .history-prices {
    display:flex; gap:14px; flex-wrap:wrap;
    font-size:.8rem; color:#a8b4d4;
  }
  .history-prices span { display:flex; gap:4px; align-items:center; }
  .history-prices b { font-family:'Space Grotesk',sans-serif; color: var(--text); font-weight:700; }
  .history-time {
    font-size:.72rem; color: var(--muted);
    display:flex; align-items:center; gap:6px;
    margin-top:2px;
  }
  .history-reason {
    font-size:.76rem; color:#8b97b8; margin-top:4px;
    line-height:1.5;
    display: -webkit-box; -webkit-line-clamp:2; -webkit-box-orient:vertical;
    overflow: hidden;
  }

  .history-delete {
    background: transparent; border:1px solid transparent;
    color: var(--muted); cursor:pointer;
    width: 32px; height: 32px; border-radius: 8px;
    display:grid; place-items:center;
    transition: all .25s ease;
    font-size:.9rem; flex-shrink:0;
  }
  .history-delete:hover {
    background: rgba(244,63,94,.15);
    color: #fb7185;
    border-color: rgba(244,63,94,.3);
  }

  .empty-state {
    text-align:center; padding: 40px 20px;
    color: var(--muted);
  }
  .empty-state .icon { font-size: 2.6rem; opacity:.4; margin-bottom:12px; }
  .empty-state p { font-size:.9rem; }

  .modal-overlay {
    position:fixed; inset:0; z-index:100; padding:20px;
    display:none; align-items:flex-start; justify-content:center;
    background: rgba(3,6,15,.8);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    opacity:0; transition: opacity .3s ease;
    overflow-y:auto;
  }
  .modal-overlay.open { display:flex; opacity:1; }
  .modal {
    background: linear-gradient(160deg, rgba(24,32,52,.95), rgba(15,20,35,.95));
    border:1px solid var(--stroke2);
    border-radius: 20px;
    padding: 30px;
    width:100%; max-width: 520px;
    transform: translateY(24px) scale(.96);
    transition: transform .35s cubic-bezier(.34,1.56,.64,1);
    box-shadow: 0 30px 80px rgba(0,0,0,.6);
    position:relative;
    margin: auto;
  }
  .modal-overlay.open .modal { transform: none; }
  .modal::before {
    content:''; position:absolute; inset:0; border-radius:inherit; padding:1px;
    background: linear-gradient(140deg, rgba(34,211,238,.5), transparent 40%, transparent 60%, rgba(168,85,247,.5));
    -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
    -webkit-mask-composite: xor; mask-composite: exclude;
    pointer-events:none;
  }
  .modal h3 { margin-bottom:6px; font-size:1.2rem; font-weight:700; }
  .modal .sub { color: var(--muted); font-size:.85rem; margin-bottom:22px; line-height:1.6; }

  .settings-section {
    margin-bottom: 22px;
    padding-bottom: 22px;
    border-bottom: 1px solid var(--stroke);
  }
  .settings-section:last-of-type { border-bottom: none; }
  .section-title {
    display:flex; align-items:center; gap:8px;
    font-size:.78rem; color: var(--muted);
    margin-bottom:12px; font-weight:700;
    letter-spacing:1.5px; text-transform:uppercase;
  }
  .section-title .mini-chip {
    width:24px; height:24px; border-radius:7px;
    display:grid; place-items:center; font-size:.72rem;
    background: linear-gradient(135deg, rgba(34,211,238,.22), rgba(168,85,247,.22));
    border:1px solid var(--stroke2);
  }

  .lang-toggle {
    display:grid;
    grid-template-columns: 1fr 1fr;
    gap:10px;
    background: rgba(5,7,15,.7);
    border-radius: 14px;
    padding: 6px;
    border: 1px solid var(--stroke);
  }
  .lang-option {
    padding: 12px 14px;
    border-radius: 10px;
    border: none;
    background: transparent;
    color: var(--muted);
    font-family:'Kantumruy Pro',sans-serif;
    font-size:.92rem;
    font-weight:600;
    cursor:pointer;
    transition: all .3s cubic-bezier(.4,0,.2,1);
    display:flex; align-items:center; justify-content:center; gap:8px;
    position:relative;
  }
  .lang-option:hover { color: var(--text); }
  .lang-option.active {
    background: linear-gradient(135deg, rgba(34,211,238,.18), rgba(168,85,247,.18));
    color: var(--text);
    box-shadow: 0 4px 18px rgba(34,211,238,.18), inset 0 0 0 1px rgba(34,211,238,.35);
  }
  .lang-option.active::after {
    content:'✓';
    position:absolute; top:6px; right:10px;
    font-size:.75rem; color: var(--accent);
    font-weight:800;
  }
  .lang-option .flag { font-size:1.15rem; }

  .field { margin-bottom: 14px; }
  .field:last-child { margin-bottom: 0; }
  .field label {
    display:block; font-size:.72rem; color: var(--muted);
    margin-bottom:6px; font-weight:700; letter-spacing:1.2px; text-transform:uppercase;
  }
  .field input {
    width:100%; padding:13px 16px; border-radius:12px;
    border:1px solid var(--stroke); background: rgba(5,7,15,.7);
    color: var(--text); font-size:.92rem; outline:none;
    font-family:'Space Grotesk',sans-serif;
    transition: all .25s ease;
  }
  .field input:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(34,211,238,.15);
    background: rgba(5,7,15,.9);
  }
  .field input::placeholder { color:#4a5573; }
  .field .hint { font-size:.72rem; color:#5a6480; margin-top:6px; line-height:1.5; }

  .modal-actions { display:flex; gap:10px; justify-content:flex-end; margin-top:8px; }

  .toast {
    position:fixed; bottom:26px; left:50%;
    transform: translateX(-50%) translateY(140px);
    background: linear-gradient(135deg, rgba(24,32,52,.98), rgba(15,20,35,.98));
    border:1px solid var(--accent);
    padding: 15px 24px; border-radius: 14px;
    font-weight:600; font-size:.9rem;
    transition: transform .4s cubic-bezier(.34,1.56,.64,1);
    z-index:200;
    box-shadow: 0 12px 40px rgba(0,0,0,.5), 0 0 24px rgba(34,211,238,.25);
    max-width: calc(100vw - 40px);
    text-align:center;
  }
  .toast.show { transform: translateX(-50%) translateY(0); }

  .footer {
    text-align:center; padding: 20px;
    color: var(--muted); font-size:.78rem; letter-spacing:1px;
    opacity:.7;
  }
  .footer span {
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    -webkit-background-clip:text; background-clip:text; color:transparent;
    font-weight:700;
  }

  @media (max-width:640px){
    header { padding: 14px 16px; gap:10px; }
    .logo-text .brand { font-size: .98rem; }
    .logo-text .tag { font-size:.55rem; letter-spacing:2px; }
    .logo-badge { width:32px; height:32px; font-size:1rem; }
    .btn { padding: 8px 12px; font-size:.8rem; }
    main { padding: 24px 16px 60px; }
    .card { padding: 20px; }
    .analysis-btn { letter-spacing:2px; font-size:.95rem; padding:17px; }
    .result-box.signal .value { letter-spacing:4px; }
    .upload-zone { padding: 30px 16px; }
    .modal { padding: 24px 20px; }
    .history-item { grid-template-columns: auto 1fr auto; padding: 14px; gap:10px; }
    .history-prices { font-size:.74rem; gap:10px; }
    .history-signal { font-size:.75rem; padding: 5px 9px; }
  }
</style>
</head>
<body>

<div class="bg-layer"></div>
<div class="grid-layer"></div>
<div class="orb o1"></div>
<div class="orb o2"></div>
<div class="orb o3"></div>

<header>
  <div class="logo">
    <div class="logo-badge">⚡</div>
    <div class="logo-text">
      <span class="brand">VATH AUTO SIGNAL</span>
      <span class="tag" data-i18n="tagline">AI Gold Analysis</span>
    </div>
  </div>
  <div class="header-actions">
    <button class="btn btn-ghost" onclick="openSettings()">⚙️ <span data-i18n="settings">Settings</span></button>
  </div>
</header>

<main>
  <div class="hero">
    <h1 data-i18n="heroTitle">XAUUSD AI Trading Signal</h1>
    <p data-i18n="heroSub">Upload your gold chart and let Gemini AI analyze it instantly with a tight stop-loss.</p>
  </div>

  <div class="card" style="animation-delay:.05s">
    <div class="card-head">
      <div class="icon-chip">📈</div>
      <h2 data-i18n="uploadTitle">Upload Chart Screenshot</h2>
    </div>
    <div class="upload-zone" id="dropZone" onclick="document.getElementById('fileInput').click()">
      <div class="up-icon">📊</div>
      <div class="up-title" data-i18n="uploadHintTitle">Drop your chart here</div>
      <p data-i18n="uploadHint">Click or drag & drop your XAUUSD chart image</p>
    </div>
    <input type="file" id="fileInput" accept="image/*" hidden onchange="handleFile(event)">
    <div id="previewWrap">
      <img id="preview" alt="chart preview">
      <button class="btn remove-img" onclick="removeImage()">✕ <span data-i18n="remove">Remove</span></button>
    </div>
  </div>

  <button class="analysis-btn" id="analyzeBtn" onclick="runAnalysis()" data-i18n="analyze">⚡ ANALYSIS</button>

  <div class="loader" id="loader">
    <div class="spinner"></div>
    <p data-i18n="analyzing">Gemini AI is analyzing your chart...</p>
    <div class="progress-bar"><div class="progress-fill"></div></div>
  </div>

  <div class="card" id="resultsCard">
    <div class="card-head">
      <div class="icon-chip">🎯</div>
      <h2 data-i18n="resultTitle">Analysis Result</h2>
    </div>
    <div class="results">
      <div class="result-box signal" id="signalBox">
        <div class="label" data-i18n="signal">Signal</div>
        <div class="value" id="signalValue">—</div>
      </div>
      <div class="result-box">
        <div class="label">🎯 <span data-i18n="entry">Entry</span></div>
        <div class="value" id="entryValue">—</div>
      </div>
      <div class="result-box">
        <div class="label">💰 <span data-i18n="tp">TP</span></div>
        <div class="value" id="tpValue">—</div>
      </div>
      <div class="result-box">
        <div class="label">🛡️ <span data-i18n="sl">SL (Tight)</span></div>
        <div class="value" id="slValue">—</div>
      </div>
    </div>
    <div class="reason" id="reasonBox" style="display:none"></div>
    <div class="tg-status hidden" id="tgStatus"></div>
  </div>

  <div class="card" id="historyCard" style="animation-delay:.1s">
    <div class="history-head">
      <div class="card-head" style="margin-bottom:0; flex:1;">
        <div class="icon-chip">📜</div>
        <h2 data-i18n="historyTitle">Signal History</h2>
      </div>
      <span class="count-badge" id="historyCount">0</span>
      <button class="btn btn-danger btn-sm" id="clearHistoryBtn" onclick="clearHistory()" style="display:none">
        🗑️ <span data-i18n="clearAll">Clear All</span>
      </button>
    </div>
    <div class="history-list" id="historyList"></div>
    <div class="empty-state" id="historyEmpty">
      <div class="icon">📭</div>
      <p data-i18n="historyEmpty">No signals yet. Run your first analysis!</p>
    </div>
  </div>
</main>

<div class="footer">
  Built with <span>Gemini AI</span> · VATH AUTO SIGNAL © 2026
</div>

<div class="modal-overlay" id="settingsModal">
  <div class="modal">
    <h3 data-i18n="settingsTitle">Settings</h3>
    <p class="sub" data-i18n="settingsSub">Configure language, Gemini API key and Telegram bot. Stored locally in your browser.</p>

    <div class="settings-section">
      <div class="section-title">
        <div class="mini-chip">🌐</div>
        <span data-i18n="languageLabel">Language</span>
      </div>
      <div class="lang-toggle">
        <button class="lang-option" id="langKm" onclick="setLanguage('km')">
          <span class="flag">🇰🇭</span> ខ្មែរ
        </button>
        <button class="lang-option" id="langEn" onclick="setLanguage('en')">
          <span class="flag">🇬🇧</span> English
        </button>
      </div>
    </div>

    <div class="settings-section">
      <div class="section-title">
        <div class="mini-chip">🔑</div>
        <span data-i18n="apiKeyLabel">Gemini API Key</span>
      </div>
      <div class="field">
        <input type="password" id="apiKeyInput" placeholder="AIza...">
      </div>
    </div>

    <div class="settings-section">
      <div class="section-title">
        <div class="mini-chip">🤖</div>
        <span data-i18n="telegramLabel">Telegram Bot (Optional)</span>
      </div>
      <div class="field">
        <label data-i18n="botTokenLabel">Bot Token</label>
        <input type="password" id="botTokenInput" placeholder="123456789:ABCdefGHIjklMNOpqrsTUVwxyz">
        <div class="hint" data-i18n="botTokenHint">ទទួលបានពី @BotFather ក្នុង Telegram</div>
      </div>
      <div class="field">
        <label data-i18n="chatIdLabel">Chat ID</label>
        <input type="text" id="chatIdInput" placeholder="123456789">
        <div class="hint" data-i18n="chatIdHint">ទទួលបានពី @userinfobot ក្នុង Telegram</div>
      </div>
    </div>

    <div class="modal-actions">
      <button class="btn btn-ghost" onclick="closeSettings()" data-i18n="cancel">Cancel</button>
      <button class="btn btn-primary" onclick="saveSettings()" data-i18n="save">Save</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
/* ============ i18n ============ */
const i18n = {
  km: {
    tagline: "វិភាគមាស AI",
    heroTitle: "សញ្ញាជួញដូរ XAUUSD AI",
    heroSub: "ដាក់រូបភាពហ្គ្រាហ្វិកមាសរបស់អ្នក ហើយទុកឱ្យ Gemini AI វិភាគភ្លាមៗ តាមក្បួន ICT និង FVG",
    settings: "ការកំណត់",
    uploadTitle: "ដាក់រូបភាពហ្គ្រាហ្វិក",
    uploadHintTitle: "អូសរូបភាពមកទីនេះ",
    uploadHint: "ចុច ឬអូសរូបភាព XAUUSD មកដាក់",
    remove: "លុបចេញ",
    analyze: "⚡ វិភាគ",
    analyzing: "Gemini AI កំពុងវិភាគហ្គ្រាហ្វិករបស់អ្នក...",
    resultTitle: "លទ្ធផលវិភាគ",
    signal: "សញ្ញា",
    entry: "ចំណុចចូល",
    tp: "TP (យកចំណេញ)",
    sl: "SL (កាត់ខាត - តូច)",
    historyTitle: "ប្រវត្តិសញ្ញា (24ម៉ោង)",
    historyEmpty: "មិនទាន់មានសញ្ញាទេ។ ចាប់ផ្តើមវិភាគដំបូង!",
    clearAll: "សម្អាតទាំងអស់",
    confirmClear: "តើអ្នកចង់លុបប្រវត្តិទាំងអស់មែនទេ?",
    deleted: "បានលុប!",
    cleared: "បានសម្អាតប្រវត្តិទាំងអស់!",
    autoCleared: "ប្រវត្តិចាស់ជាង 24 ម៉ោង ត្រូវបានលុបដោយស្វ័យប្រវត្តិ!",
    settingsTitle: "ការកំណត់",
    settingsSub: "កំណត់ភាសា, Gemini API Key និង Telegram Bot។ រក្សាទុកក្នុង browser។",
    languageLabel: "ភាសា",
    apiKeyLabel: "Gemini API Key",
    telegramLabel: "Telegram Bot (ស្រេចចិត្ត)",
    botTokenLabel: "Bot Token",
    botTokenHint: "ទទួលបានពី @BotFather ក្នុង Telegram",
    chatIdLabel: "Chat ID",
    chatIdHint: "ទទួលបានពី @userinfobot ក្នុង Telegram",
    cancel: "បោះបង់",
    save: "រក្សាទុក",
    saved: "បានរក្សាទុក!",
    noKey: "សូមដាក់ Gemini API Key សិន (ចុច ⚙️ Settings)",
    noImage: "សូមដាក់រូបភាពហ្គ្រាហ្វិកសិន",
    error: "មានបញ្ហា: ",
    errorHighDemand: "ម៉ូដែល AI កំពុងមានអ្នកប្រើប្រាស់ច្រើន (High Demand)។ សូមរង់ចាំបន្តិច ហើយព្យាយាមម្តងទៀត។",
    tgSending: "កំពុងផ្ញើទៅ Telegram...",
    tgSuccess: "ផ្ញើទៅ Telegram បានជោគជ័យ!",
    tgError: "ផ្ញើទៅ Telegram បរាជ័យ: ",
    tgSignal: "សញ្ញា",
    tgEntry: "ចំណុចចូល",
    tgTp: "យកចំណេញ",
    tgSl: "កាត់ខាត",
    tgReason: "មូលហេតុ (ICT & FVG)"
  },
  en: {
    tagline: "AI Gold Analysis",
    heroTitle: "XAUUSD AI Trading Signal",
    heroSub: "Upload your gold chart and let Gemini AI analyze it using ICT & FVG concepts.",
    settings: "Settings",
    uploadTitle: "Upload Chart Screenshot",
    uploadHintTitle: "Drop your chart here",
    uploadHint: "Click or drag & drop your XAUUSD chart image",
    remove: "Remove",
    analyze: "⚡ ANALYSIS",
    analyzing: "Gemini AI is analyzing your chart...",
    resultTitle: "Analysis Result",
    signal: "Signal",
    entry: "Entry",
    tp: "TP",
    sl: "SL (Tight)",
    historyTitle: "Signal History (24h)",
    historyEmpty: "No signals yet. Run your first analysis!",
    clearAll: "Clear All",
    confirmClear: "Delete all history?",
    deleted: "Deleted!",
    cleared: "All history cleared!",
    autoCleared: "History older than 24h was auto-deleted!",
    settingsTitle: "Settings",
    settingsSub: "Configure language, Gemini API key and Telegram bot. Stored locally in your browser.",
    languageLabel: "Language",
    apiKeyLabel: "Gemini API Key",
    telegramLabel: "Telegram Bot (Optional)",
    botTokenLabel: "Bot Token",
    botTokenHint: "Get from @BotFather on Telegram",
    chatIdLabel: "Chat ID",
    chatIdHint: "Get from @userinfobot on Telegram",
    cancel: "Cancel",
    save: "Save",
    saved: "Saved!",
    noKey: "Please enter a Gemini API key first (⚙️ Settings)",
    noImage: "Please upload a chart image first",
    error: "Error: ",
    errorHighDemand: "The AI model is experiencing high demand. Please wait a moment and try again.",
    tgSending: "Sending to Telegram...",
    tgSuccess: "Sent to Telegram successfully!",
    tgError: "Telegram send failed: ",
    tgSignal: "Signal",
    tgEntry: "Entry",
    tgTp: "TP",
    tgSl: "SL",
    tgReason: "Reason (ICT & FVG)"
  }
};
let currentLang = localStorage.getItem('vas_lang') || 'km';

function setLanguage(lang) {
  currentLang = lang;
  localStorage.setItem('vas_lang', lang);
  document.documentElement.lang = lang;
  document.querySelectorAll('[data-i18n]').forEach(el => {
    const key = el.getAttribute('data-i18n');
    if (i18n[lang][key]) el.textContent = i18n[lang][key];
  });
  document.getElementById('langKm').classList.toggle('active', lang === 'km');
  document.getElementById('langEn').classList.toggle('active', lang === 'en');
  renderHistory();
}
function t(key) { return i18n[currentLang][key] || key; }

/* ============ Image Handling & Compression ============ */
let currentImageBase64 = null;

function compressImage(file, maxWidth = 1024) {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onload = (e) => {
      const img = new Image();
      img.onload = () => {
        let width = img.width;
        let height = img.height;
        if (width > maxWidth) {
          height = Math.round((height * maxWidth) / width);
          width = maxWidth;
        }
        const canvas = document.createElement('canvas');
        canvas.width = width;
        canvas.height = height;
        const ctx = canvas.getContext('2d');
        ctx.drawImage(img, 0, 0, width, height);
        const compressedDataUrl = canvas.toDataURL('image/jpeg', 0.8);
        resolve(compressedDataUrl);
      };
      img.onerror = (err) => reject(err);
      img.src = e.target.result;
    };
    reader.onerror = (err) => reject(err);
    reader.readAsDataURL(file);
  });
}

async function handleFile(e) {
  const file = e.target.files[0];
  if (!file) return;
  try {
    currentImageBase64 = await compressImage(file, 1024);
    document.getElementById('preview').src = currentImageBase64;
    document.getElementById('previewWrap').style.display = 'block';
    document.getElementById('dropZone').style.display = 'none';
  } catch (err) {
    showToast("Error processing image: " + err.message);
  }
}

function removeImage() {
  currentImageBase64 = null;
  document.getElementById('fileInput').value = '';
  document.getElementById('previewWrap').style.display = 'none';
  document.getElementById('dropZone').style.display = 'block';
  resetResults();
}
function resetResults() {
  const sigEl = document.getElementById('signalValue');
  sigEl.textContent = '—';
  sigEl.className = 'value';
  document.getElementById('signalBox').className = 'result-box signal';
  document.getElementById('entryValue').textContent = '—';
  document.getElementById('tpValue').textContent = '—';
  document.getElementById('slValue').textContent = '—';
  const rb = document.getElementById('reasonBox');
  rb.textContent = ''; rb.style.display = 'none';
  const tg = document.getElementById('tgStatus');
  tg.className = 'tg-status hidden';
  tg.textContent = '';
}
const dz = document.getElementById('dropZone');
['dragover','dragenter'].forEach(ev => dz.addEventListener(ev, e => { e.preventDefault(); dz.classList.add('drag'); }));
['dragleave','drop'].forEach(ev => dz.addEventListener(ev, e => { e.preventDefault(); dz.classList.remove('drag'); }));
dz.addEventListener('drop', async e => {
  const f = e.dataTransfer.files[0];
  if (f && f.type.startsWith('image/')) {
    try {
      currentImageBase64 = await compressImage(f, 1024);
      document.getElementById('preview').src = currentImageBase64;
      document.getElementById('previewWrap').style.display = 'block';
      dz.style.display = 'none';
    } catch (err) {
      showToast("Error processing image: " + err.message);
    }
  }
});
dz.addEventListener('mousemove', e => {
  const r = dz.getBoundingClientRect();
  dz.style.setProperty('--mx', ((e.clientX - r.left) / r.width * 100) + '%');
  dz.style.setProperty('--my', ((e.clientY - r.top) / r.height * 100) + '%');
});

/* ============ Settings ============ */
function openSettings() {
  document.getElementById('apiKeyInput').value = localStorage.getItem('vas_api_key') || '';
  document.getElementById('botTokenInput').value = localStorage.getItem('vas_bot_token') || '';
  document.getElementById('chatIdInput').value = localStorage.getItem('vas_chat_id') || '';
  document.getElementById('settingsModal').classList.add('open');
  document.body.style.overflow = 'hidden';
}
function closeSettings() {
  document.getElementById('settingsModal').classList.remove('open');
  document.body.style.overflow = '';
}
function saveSettings() {
  localStorage.setItem('vas_api_key', document.getElementById('apiKeyInput').value.trim());
  localStorage.setItem('vas_bot_token', document.getElementById('botTokenInput').value.trim());
  localStorage.setItem('vas_chat_id', document.getElementById('chatIdInput').value.trim());
  closeSettings();
  showToast(t('saved'));
}
document.getElementById('settingsModal').addEventListener('click', e => {
  if (e.target.id === 'settingsModal') closeSettings();
});

/* ============ Toast ============ */
let toastTimer;
function showToast(msg) {
  const el = document.getElementById('toast');
  el.textContent = msg;
  el.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => el.classList.remove('show'), 3200);
}

/* ============ History (Auto-Delete 24h) ============ */
const HISTORY_KEY = 'vas_history';
const MAX_HISTORY = 50;
const EXPIRY_TIME = 24 * 60 * 60 * 1000; // 24 ម៉ោងគិតជាមីលីវិនាទី

function loadHistory() {
  try {
    let arr = JSON.parse(localStorage.getItem(HISTORY_KEY) || '[]');
    const now = Date.now();
    const initialLength = arr.length;
    // ត្រងយកតែអ្វីដែលមិនទាន់ផុតកំណត់ 24 ម៉ោង
    arr = arr.filter(item => (now - item.time) < EXPIRY_TIME);
    
    // ប្រសិនបើមានការលុបដោយស្វ័យប្រវត្តិ សូមរក្សាទុកឡើងវិញ
    if (arr.length !== initialLength) {
      localStorage.setItem(HISTORY_KEY, JSON.stringify(arr));
      // បង្ហាញសារបើវាលុបពេលកំពុងបើក
      if (initialLength > 0) {
        setTimeout(() => showToast(t('autoCleared')), 500);
      }
    }
    return arr;
  }
  catch { return []; }
}
function saveHistory(arr) {
  localStorage.setItem(HISTORY_KEY, JSON.stringify(arr));
}
function addToHistory(result) {
  const arr = loadHistory();
  arr.unshift({
    id: Date.now() + '_' + Math.random().toString(36).slice(2,7),
    signal: (result.signal || 'HOLD').toUpperCase(),
    entry: result.entry || '—',
    tp: result.tp || '—',
    sl: result.sl || '—',
    reason: result.reason || '',
    time: Date.now()
  });
  if (arr.length > MAX_HISTORY) arr.length = MAX_HISTORY;
  saveHistory(arr);
  renderHistory();
}
function deleteHistoryItem(id, e) {
  if (e) e.stopPropagation();
  const arr = loadHistory().filter(x => x.id !== id);
  saveHistory(arr);
  renderHistory();
  showToast(t('deleted'));
}
function clearHistory() {
  if (!confirm(t('confirmClear'))) return;
  saveHistory([]);
  renderHistory();
  showToast(t('cleared'));
}

function formatTime(ts) {
  const d = new Date(ts);
  const now = new Date();
  const diffMs = now - d;
  
  // គណនាម៉ោងដែលនៅសល់រហូតដល់លុប (24 ម៉ោង)
  const remainMs = EXPIRY_TIME - diffMs;
  const remainHr = Math.floor(remainMs / 3600000);
  const remainMin = Math.floor((remainMs % 3600000) / 60000);

  const pad = n => String(n).padStart(2, '0');
  const timeStr = `${pad(d.getHours())}:${pad(d.getMinutes())}`;
  const dateStr = `${pad(d.getDate())}/${pad(d.getMonth()+1)}/${d.getFullYear()}`;

  let relative = '';
  if (currentLang === 'km') {
    if (remainHr > 0) relative = `នៅសល់ ${remainHr} ម៉ោង ${remainMin} នាទី`;
    else relative = `នៅសល់ ${remainMin} នាទី`;
  } else {
    if (remainHr > 0) relative = `${remainHr}h ${remainMin}m left`;
    else relative = `${remainMin}m left`;
  }
  return { timeStr, dateStr, relative };
}

function escapeHtml(s) {
  return String(s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
}

function renderHistory() {
  const arr = loadHistory();
  const list = document.getElementById('historyList');
  const empty = document.getElementById('historyEmpty');
  const badge = document.getElementById('historyCount');
  const clearBtn = document.getElementById('clearHistoryBtn');

  badge.textContent = arr.length;
  clearBtn.style.display = arr.length > 0 ? 'inline-flex' : 'none';

  if (arr.length === 0) {
    list.innerHTML = '';
    list.style.display = 'none';
    empty.style.display = 'block';
    return;
  }
  empty.style.display = 'none';
  list.style.display = 'flex';

  list.innerHTML = arr.map((item, idx) => {
    const cls = item.signal === 'BUY' ? 'buy' : item.signal === 'SELL' ? 'sell' : 'hold';
    const { timeStr, dateStr, relative } = formatTime(item.time);
    const reasonShort = item.reason ? escapeHtml(item.reason) : '';
    return `
      <div class="history-item ${cls}" style="animation-delay:${Math.min(idx*30,300)}ms">
        <div class="history-signal ${cls}">${item.signal}</div>
        <div class="history-details">
          <div class="history-prices">
            <span>🎯 <b>${escapeHtml(item.entry)}</b></span>
            <span>💰 <b>${escapeHtml(item.tp)}</b></span>
            <span>🛡️ <b>${escapeHtml(item.sl)}</b></span>
          </div>
          ${reasonShort ? `<div class="history-reason">${reasonShort}</div>` : ''}
          <div class="history-time">⏳ ${relative} · ${timeStr} ${dateStr}</div>
        </div>
        <button class="history-delete" onclick="deleteHistoryItem('${item.id}', event)" title="${t('remove')}">🗑️</button>
      </div>
    `;
  }).join('');
}

/* ============ Telegram ============ */
async function sendToTelegram(result) {
  const botToken = localStorage.getItem('vas_bot_token');
  const chatId = localStorage.getItem('vas_chat_id');
  const tg = document.getElementById('tgStatus');

  if (!botToken || !chatId) {
    tg.className = 'tg-status hidden';
    return;
  }

  tg.className = 'tg-status sending';
  tg.textContent = '📤 ' + t('tgSending');

  const sig = (result.signal || 'HOLD').toUpperCase();
  const emoji = sig === 'BUY' ? '🟢' : sig === 'SELL' ? '🔴' : '🟡';

  const caption =
`${emoji} <b>VATH AUTO SIGNAL</b>

<b>${t('tgSignal')}:</b> ${sig}
<b>${t('tgEntry')}:</b> ${result.entry || '—'}
<b>${t('tgTp')}:</b> ${result.tp || '—'}
<b>${t('tgSl')}:</b> ${result.sl || '—'}

<b>${t('tgReason')}:</b>
${result.reason || '—'}`;

  try {
    let resp;
    if (currentImageBase64) {
      const blob = await (await fetch(currentImageBase64)).blob();
      const form = new FormData();
      form.append('chat_id', chatId);
      form.append('caption', caption);
      form.append('parse_mode', 'HTML');
      form.append('photo', blob, 'chart.jpg');

      resp = await fetch(`https://api.telegram.org/bot${botToken}/sendPhoto`, {
        method: 'POST',
        body: form
      });
    } else {
      resp = await fetch(`https://api.telegram.org/bot${botToken}/sendMessage`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          chat_id: chatId,
          text: caption,
          parse_mode: 'HTML'
        })
      });
    }

    const data = await resp.json();
    if (!data.ok) throw new Error(data.description || 'Telegram API error');

    tg.className = 'tg-status success';
    tg.textContent = '✅ ' + t('tgSuccess');
  } catch (err) {
    tg.className = 'tg-status error';
    tg.textContent = '❌ ' + t('tgError') + err.message;
  }
}

/* ============ Analysis (ICT & FVG) ============ */
async function runAnalysis() {
  const apiKey = localStorage.getItem('vas_api_key');
  if (!apiKey) { showToast(t('noKey')); openSettings(); return; }
  if (!currentImageBase64) { showToast(t('noImage')); return; }

  const btn = document.getElementById('analyzeBtn');
  const loader = document.getElementById('loader');
  btn.disabled = true;
  loader.classList.add('active');
  resetResults();

  const models = ['gemini-3.8-flash', 'gemini-3.6-flash']; 
  let lastError = null;

  try {
    const base64Data = currentImageBase64.split(',')[1];
    const mimeType = currentImageBase64.substring(5, currentImageBase64.indexOf(';'));

    // 🚀 កែសម្រួល Prompt ឱ្យវិភាគតាម ICT និង FVG
    const prompt = `You are a professional XAUUSD (Gold) trader specializing in **Inner Circle Trader (ICT)** concepts and **Smart Money Concepts (SMC)**.
Analyze this chart image specifically looking for:
1. Market Structure (BOS / CHoCH)
2. Fair Value Gaps (FVG)
3. Order Blocks (OB)
4. Liquidity Pools

Based on these ICT principles, provide a trading signal. 
Respond ONLY with a valid JSON object (no markdown, no backticks) in this exact format:
{
  "signal": "BUY" | "SELL" | "HOLD",
  "entry": "price value",
  "tp": "take profit price",
  "sl": "stop loss price (must be VERY TIGHT, just below/above the FVG or OB)",
  "reason": "Explain the setup in ${currentLang === 'km' ? 'Khmer' : 'English'} (e.g., 'Price swept liquidity and tapped into 1H FVG...'). Max 3 sentences."
}
Rules:
- SL must be extremely tight, placed just past the FVG/Order Block invalidation level.
- TP should target the next liquidity pool or swing high/low.
- If there is no clear ICT setup, output "HOLD".
- Use realistic XAUUSD price levels based on the chart.`;

    let result = null;

    for (let i = 0; i < models.length; i++) {
      const currentModel = models[i];
      let retries = 3; 
      
      while (retries > 0) {
        try {
          const resp = await fetch(
            `https://generativelanguage.googleapis.com/v1beta/models/${currentModel}:generateContent?key=${apiKey}`,
            {
              method: 'POST',
              headers: { 'Content-Type': 'application/json' },
              body: JSON.stringify({
                contents: [{
                  parts: [
                    { text: prompt },
                    { inline_data: { mime_type: mimeType, data: base64Data } }
                  ]
                }],
                generationConfig: { temperature: 0.3, maxOutputTokens: 800 }
              })
            }
          );

          if (!resp.ok) {
            const err = await resp.json().catch(() => ({}));
            if (resp.status === 503) throw new Error('HIGH_DEMAND');
            throw new Error(err.error?.message || 'API request failed (' + resp.status + ')');
          }

          const data = await resp.json();
          let text = data.candidates?.[0]?.content?.parts?.[0]?.text || '';
          text = text.replace(/```json/gi, '').replace(/```/g, '').trim();

          try { result = JSON.parse(text); }
          catch {
            const m = text.match(/\{[\s\S]*\}/);
            if (m) result = JSON.parse(m[0]);
            else throw new Error('Invalid AI response format');
          }
          break; 

        } catch (err) {
          lastError = err;
          if (err.message === 'HIGH_DEMAND') {
            retries--;
            if (retries > 0) {
              await new Promise(r => setTimeout(r, 2000));
              continue;
            }
          }
          break;
        }
      }
      if (result) break; 
    }

    if (!result) throw lastError || new Error('Analysis failed after retries.');

    displayResult(result);
    addToHistory(result);
    await sendToTelegram(result);

  } catch (err) {
    if (err.message === 'HIGH_DEMAND') {
      showToast(t('error') + t('errorHighDemand'));
    } else {
      showToast(t('error') + err.message);
    }
  } finally {
    btn.disabled = false;
    loader.classList.remove('active');
  }
}

function displayResult(r) {
  const sig = (r.signal || 'HOLD').toUpperCase();
  const sigEl = document.getElementById('signalValue');
  const sigBox = document.getElementById('signalBox');

  sigEl.textContent = sig;
  sigBox.className = 'result-box signal ' + (sig === 'BUY' ? 'buy' : sig === 'SELL' ? 'sell' : 'hold');
  sigEl.className = 'value ' + (sig === 'BUY' ? 'signal-buy' : sig === 'SELL' ? 'signal-sell' : 'signal-hold');

  document.getElementById('entryValue').textContent = r.entry || '—';
  document.getElementById('tpValue').textContent = r.tp || '—';
  document.getElementById('slValue').textContent = r.sl || '—';

  const rb = document.getElementById('reasonBox');
  if (r.reason) { rb.textContent = r.reason; rb.style.display = 'block'; }
  else rb.style.display = 'none';

  document.getElementById('resultsCard').scrollIntoView({ behavior: 'smooth', block: 'center' });
}

/* ============ Init ============ */
setLanguage(currentLang);
renderHistory();

// ពិនិត្យមើលរាល់ ១ នាទីម្តង ដើម្បីលុបប្រវត្តិដែលផុត ២៤ ម៉ោងដោយស្វ័យប្រវត្តិ
setInterval(() => {
  const arrBefore = JSON.parse(localStorage.getItem(HISTORY_KEY) || '[]').length;
  const arrAfter = loadHistory().length;
  if (arrBefore !== arrAfter) {
    renderHistory(); // Update UI បើមានការលុប
  } else {
    renderHistory(); // Update ការរាប់ថយក្រោយ
  }
}, 60000);
</script>
</body>
</html>

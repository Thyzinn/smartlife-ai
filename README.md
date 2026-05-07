<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SmartLife AI</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,400&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #07080f;
  --bg2: #0d1120;
  --bg3: #131829;
  --surface: #161c2e;
  --surface2: #1c2438;
  --border: #232d45;
  --border2: #2a3652;
  --text: #e8eaf2;
  --text2: #8892a8;
  --text3: #525f7a;
  --accent: #4f8eff;
  --accent2: #6ba3ff;
  --green: #2dd4a0;
  --amber: #f5a623;
  --red: #ff5a5a;
  --purple: #9b7ff5;
  --font-head: 'Syne', sans-serif;
  --font-body: 'DM Sans', sans-serif;
  --r: 10px;
  --r-lg: 16px;
  --shadow: 0 4px 24px rgba(0,0,0,.4);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: var(--font-body);
  background: var(--bg);
  color: var(--text);
  line-height: 1.6;
  min-height: 100vh;
  font-size: 15px;
}

.hidden { display: none !important; }

/* ── SCROLLBAR ── */
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: var(--bg2); }
::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 3px; }

/* ── TOAST ── */
#toast {
  position: fixed; bottom: 24px; right: 24px; z-index: 9999;
  padding: 12px 20px; border-radius: var(--r);
  font-weight: 600; font-size: 0.88rem;
  background: var(--green); color: #06120e;
  transform: translateY(80px); opacity: 0;
  transition: all .3s cubic-bezier(.34,1.56,.64,1);
  pointer-events: none;
}
#toast.show { transform: translateY(0); opacity: 1; }
#toast.err { background: var(--red); color: #fff; }

/* ── FORMS ── */
input, select, textarea {
  width: 100%; padding: 11px 14px;
  border-radius: var(--r); border: 1px solid var(--border);
  background: var(--surface); color: var(--text);
  font-family: var(--font-body); font-size: 0.93rem;
  transition: border-color .2s, box-shadow .2s;
  -webkit-appearance: none;
}
input:focus, select:focus, textarea:focus {
  outline: none; border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(79,142,255,.12);
}
input::placeholder, textarea::placeholder { color: var(--text3); }
textarea { resize: vertical; min-height: 90px; }
label { display: block; font-size: 0.82rem; color: var(--text2); margin-bottom: 5px; font-weight: 500; }
.form-group { margin-bottom: 14px; }

/* ── BUTTONS ── */
.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: 6px;
  padding: 11px 20px; border-radius: var(--r); border: none;
  font-family: var(--font-head); font-weight: 700; font-size: 0.9rem;
  cursor: pointer; transition: all .18s; white-space: nowrap;
}
.btn-primary {
  background: linear-gradient(135deg, var(--accent), var(--accent2));
  color: #fff; width: 100%; padding: 13px;
}
.btn-primary:hover { filter: brightness(1.1); transform: translateY(-1px); box-shadow: 0 6px 20px rgba(79,142,255,.3); }
.btn-primary:active { transform: translateY(0); }
.btn-ghost { background: var(--surface2); color: var(--text2); border: 1px solid var(--border); }
.btn-ghost:hover { background: var(--border); color: var(--text); }
.btn-danger { background: rgba(255,90,90,.15); color: var(--red); border: 1px solid rgba(255,90,90,.2); padding: 6px 12px; font-size: 0.8rem; }
.btn-danger:hover { background: rgba(255,90,90,.25); }
.btn-success { background: rgba(45,212,160,.15); color: var(--green); border: 1px solid rgba(45,212,160,.2); padding: 6px 12px; font-size: 0.8rem; }
.btn-success:hover { background: rgba(45,212,160,.25); }
.btn-amber { background: rgba(245,166,35,.15); color: var(--amber); border: 1px solid rgba(245,166,35,.2); padding: 8px 16px; font-size: 0.85rem; }
.btn-amber:hover { background: rgba(245,166,35,.25); }
.btn-purple { background: rgba(155,127,245,.15); color: var(--purple); border: 1px solid rgba(155,127,245,.2); padding: 8px 16px; font-size: 0.85rem; }
.btn-logout { background: rgba(255,255,255,.12); color: #fff; padding: 7px 16px; font-size: 0.82rem; border: 1px solid rgba(255,255,255,.15); }
.btn-logout:hover { background: rgba(255,255,255,.2); }

/* ── CARD ── */
.card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--r-lg); padding: 24px;
  margin-bottom: 20px;
}
.card h2 {
  font-family: var(--font-head); font-size: 1.1rem; font-weight: 700;
  color: var(--text); margin-bottom: 4px;
}
.card-sub { font-size: 0.83rem; color: var(--text3); margin-bottom: 18px; }

/* ── LOGIN ── */
#loginPage {
  min-height: 100vh; display: flex; align-items: center; justify-content: center;
  padding: 20px;
  background: radial-gradient(ellipse 80% 60% at 50% -10%, rgba(79,142,255,.18) 0%, transparent 70%), var(--bg);
}
.login-box {
  width: 100%; max-width: 400px;
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: 20px; padding: 40px 36px;
  box-shadow: 0 20px 60px rgba(0,0,0,.5);
}
.login-logo {
  text-align: center; margin-bottom: 28px;
}
.login-logo h1 {
  font-family: var(--font-head); font-size: 2rem; font-weight: 800;
  background: linear-gradient(135deg, var(--accent2), var(--green));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  background-clip: text;
}
.login-logo p { font-size: 0.85rem; color: var(--text3); margin-top: 4px; }
.error-msg { color: var(--red); font-size: 0.83rem; min-height: 18px; margin-top: 4px; }
.login-divider { border: none; border-top: 1px solid var(--border); margin: 16px 0; }

/* ── APP HEADER ── */
#app { display: none; }
.app-header {
  position: sticky; top: 0; z-index: 100;
  background: rgba(7,8,15,.85); backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
  padding: 0 24px;
  display: flex; align-items: center; justify-content: space-between;
  height: 58px;
}
.app-logo {
  font-family: var(--font-head); font-weight: 800; font-size: 1.1rem;
  background: linear-gradient(135deg, var(--accent2), var(--green));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  background-clip: text;
}
.user-chip {
  display: flex; align-items: center; gap: 10px;
}
.user-avatar {
  width: 32px; height: 32px; border-radius: 50%;
  background: linear-gradient(135deg, var(--accent), var(--purple));
  display: flex; align-items: center; justify-content: center;
  font-family: var(--font-head); font-weight: 700; font-size: 0.85rem;
  flex-shrink: 0;
}
.user-name { font-size: 0.88rem; color: var(--text2); }

/* ── HERO BANNER ── */
.hero {
  padding: 32px 24px 24px;
  background: linear-gradient(135deg, rgba(79,142,255,.08) 0%, transparent 50%),
              linear-gradient(225deg, rgba(45,212,160,.06) 0%, transparent 50%);
  border-bottom: 1px solid var(--border);
}
.hero-inner { max-width: 860px; margin: auto; }
.quote-card {
  background: var(--surface); border: 1px solid var(--border2);
  border-radius: var(--r-lg); padding: 20px 24px;
  display: flex; gap: 16px; align-items: flex-start;
}
.quote-mark { font-size: 2rem; line-height: 1; color: var(--accent); opacity: .4; flex-shrink: 0; }
.quote-text { font-size: 0.93rem; color: var(--text2); font-style: italic; }
.quote-author { font-size: 0.78rem; color: var(--text3); margin-top: 6px; }

/* ── STATS BAR ── */
.stats-bar {
  display: flex; gap: 1px; background: var(--border);
  border-radius: var(--r-lg); overflow: hidden;
  margin-top: 16px;
}
.stat {
  flex: 1; background: var(--surface); padding: 14px 10px;
  text-align: center;
}
.stat-val { font-family: var(--font-head); font-size: 1.4rem; font-weight: 800; color: var(--accent2); }
.stat-lbl { font-size: 0.7rem; color: var(--text3); text-transform: uppercase; letter-spacing: .5px; margin-top: 2px; }

/* ── MAIN LAYOUT ── */
.main { max-width: 860px; margin: auto; padding: 24px 20px 60px; }

/* ── TABS ── */
.tabs { display: flex; gap: 4px; background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r-lg); padding: 5px; margin-bottom: 24px; overflow-x: auto; scrollbar-width: none; }
.tabs::-webkit-scrollbar { display: none; }
.tab {
  flex: 1; min-width: fit-content; padding: 9px 16px; border-radius: 8px;
  font-family: var(--font-head); font-weight: 600; font-size: 0.82rem;
  color: var(--text3); cursor: pointer; border: none; background: transparent;
  transition: all .18s; white-space: nowrap;
}
.tab:hover { color: var(--text2); background: var(--surface); }
.tab.active { background: var(--surface2); color: var(--text); border: 1px solid var(--border2); }
.tab-content { display: none; }
.tab-content.active { display: block; }

/* ── TABLE ── */
.table-wrap { overflow-x: auto; margin-top: 16px; }
table { width: 100%; border-collapse: separate; border-spacing: 0; }
th, td { padding: 11px 14px; text-align: left; border-bottom: 1px solid var(--border); }
th { font-family: var(--font-head); font-size: 0.76rem; text-transform: uppercase; letter-spacing: .5px; color: var(--text3); background: var(--bg2); }
th:first-child { border-radius: 8px 0 0 0; }
th:last-child { border-radius: 0 8px 0 0; }
td { font-size: 0.88rem; color: var(--text2); }
tr:hover td { background: var(--surface2); }
.empty-state { text-align: center; color: var(--text3); padding: 32px; font-style: italic; font-size: 0.88rem; }

/* ── INPUT ROW ── */
.input-row { display: flex; gap: 10px; flex-wrap: wrap; margin-bottom: 12px; }
.input-row input, .input-row select { flex: 1; min-width: 120px; }

/* ── HABITOS ── */
.habit-list { list-style: none; margin-top: 14px; display: flex; flex-direction: column; gap: 8px; }
.habit-item {
  display: flex; align-items: center; gap: 12px;
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 12px 14px;
  transition: border-color .2s;
}
.habit-item:hover { border-color: var(--border2); }
.habit-check {
  width: 22px; height: 22px; border-radius: 50%;
  border: 2px solid var(--border2); cursor: pointer; flex-shrink: 0;
  display: flex; align-items: center; justify-content: center;
  transition: all .2s;
}
.habit-check.done { background: var(--green); border-color: var(--green); }
.habit-check.done::after { content: "✓"; color: #06120e; font-size: 0.72rem; font-weight: 700; }
.habit-name { flex: 1; font-size: 0.9rem; }
.habit-streak { font-size: 0.78rem; color: var(--amber); font-weight: 600; }
.habit-del { cursor: pointer; color: var(--text3); font-size: 1.1rem; transition: color .2s; padding: 2px 4px; }
.habit-del:hover { color: var(--red); }
.progress-track { background: var(--bg2); border-radius: 100px; height: 6px; overflow: hidden; margin-top: 8px; }
.progress-fill { height: 100%; border-radius: 100px; background: linear-gradient(90deg, var(--green), var(--accent)); transition: width .6s cubic-bezier(.34,1.4,.64,1); }

/* ── NOTAS ── */
.notes-grid { display: grid; gap: 10px; margin-top: 14px; }
.note-item {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 14px 16px;
  border-left: 3px solid var(--accent); position: relative;
}
.note-title { font-weight: 600; font-size: 0.9rem; margin-bottom: 5px; }
.note-body { font-size: 0.85rem; color: var(--text2); white-space: pre-wrap; }
.note-date { font-size: 0.75rem; color: var(--text3); margin-top: 10px; }
.note-del { position: absolute; top: 12px; right: 12px; cursor: pointer; color: var(--text3); font-size: 1rem; transition: color .2s; }
.note-del:hover { color: var(--red); }

/* ── AI RESULT ── */
.ai-result {
  margin-top: 18px; padding: 22px;
  background: var(--bg2); border: 1px solid var(--border);
  border-left: 3px solid var(--green); border-radius: var(--r-lg);
}
.ai-result h3 { font-family: var(--font-head); color: var(--green); font-size: 1rem; margin-bottom: 6px; }
.ai-meta { font-size: 0.8rem; color: var(--text3); margin-bottom: 14px; }
.ai-body { font-size: 0.9rem; color: var(--text2); line-height: 1.8; white-space: pre-wrap; }
.ai-body strong { color: var(--text); }
.ai-body h4 { color: var(--accent2); font-family: var(--font-head); margin: 12px 0 4px; }
.ai-loading {
  display: flex; align-items: center; gap: 12px; margin-top: 18px;
  padding: 18px; color: var(--accent2); font-size: 0.9rem;
  background: var(--surface); border-radius: var(--r); border: 1px solid var(--border);
}
.ai-loading::before {
  content: ''; width: 18px; height: 18px; border-radius: 50%;
  border: 2px solid var(--border2); border-top-color: var(--accent);
  animation: spin .8s linear infinite; flex-shrink: 0;
}
@keyframes spin { to { transform: rotate(360deg); } }

/* ── POMODORO ── */
.pomo-card { text-align: center; padding: 36px 24px; }
.timer-ring-wrap { position: relative; width: 180px; height: 180px; margin: 0 auto 28px; }
.timer-ring { transform: rotate(-90deg); }
.timer-ring-bg { stroke: var(--border); fill: none; }
.timer-ring-fill { fill: none; stroke: var(--accent); stroke-linecap: round; transition: stroke-dashoffset .5s; }
.timer-number {
  position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%);
  font-family: var(--font-head); font-size: 2.6rem; font-weight: 800; color: var(--text);
}
.timer-label { font-size: 0.75rem; color: var(--text3); text-transform: uppercase; letter-spacing: .8px; margin-top: 6px; }
.pomo-btns { display: flex; gap: 10px; justify-content: center; }
.pomo-btns .btn { width: auto; }
.pomo-stats { display: flex; gap: 24px; justify-content: center; margin-top: 28px; padding-top: 24px; border-top: 1px solid var(--border); }
.pomo-stat-label { font-size: 0.78rem; color: var(--text3); text-transform: uppercase; }
.pomo-stat-val { font-family: var(--font-head); font-size: 1.4rem; font-weight: 700; color: var(--green); margin-top: 2px; }

/* ── RELATORIO ── */
.report-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(130px,1fr)); gap: 10px; margin-bottom: 20px; }
.report-card { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); padding: 16px; text-align: center; }
.report-val { font-family: var(--font-head); font-size: 1.5rem; font-weight: 800; color: var(--accent2); }
.report-lbl { font-size: 0.72rem; color: var(--text3); text-transform: uppercase; margin-top: 3px; }
.score-ring { position: relative; width: 110px; height: 110px; margin: 0 auto 12px; }
.score-ring svg { transform: rotate(-90deg); }
.score-num {
  position: absolute; inset: 0; display: flex; align-items: center; justify-content: center;
  font-family: var(--font-head); font-size: 1.8rem; font-weight: 800;
}
.report-section { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r-lg); padding: 18px; margin-bottom: 12px; }
.report-section h3 { font-family: var(--font-head); font-size: 0.78rem; text-transform: uppercase; color: var(--text3); letter-spacing: .5px; margin-bottom: 14px; }
.report-bar-row { margin-bottom: 10px; }
.report-bar-row-head { display: flex; justify-content: space-between; font-size: 0.83rem; margin-bottom: 5px; }
.report-bar-bg { background: var(--border); border-radius: 100px; height: 7px; overflow: hidden; }
.report-bar-fg { height: 100%; border-radius: 100px; transition: width .5s ease; }
.tip-box { background: var(--surface2); border: 1px solid var(--border2); border-left: 3px solid var(--amber); border-radius: var(--r); padding: 14px 16px; font-size: 0.88rem; color: var(--text2); margin-top: 16px; }
.tip-box strong { color: var(--amber); }
.task-row { display: flex; justify-content: space-between; padding: 7px 0; border-bottom: 1px solid var(--border); font-size: 0.87rem; }
.task-row:last-child { border-bottom: none; }

/* ── ADMIN PANEL ── */
#adminPanel { display: none; min-height: 100vh; padding: 24px 20px; }
.admin-wrap { max-width: 960px; margin: auto; }
.admin-hdr { display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 12px; margin-bottom: 24px; }
.admin-hdr h1 { font-family: var(--font-head); font-size: 1.4rem; color: var(--amber); }
.admin-hdr-btns { display: flex; gap: 8px; flex-wrap: wrap; }
.admin-stats { display: grid; grid-template-columns: repeat(auto-fit, minmax(130px,1fr)); gap: 10px; margin-bottom: 24px; }
.admin-stat { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r-lg); padding: 18px; text-align: center; }
.admin-stat .n { font-family: var(--font-head); font-size: 1.8rem; font-weight: 800; color: var(--amber); }
.admin-stat .l { font-size: 0.72rem; color: var(--text3); text-transform: uppercase; margin-top: 3px; }
.admin-user-card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r-lg); padding: 20px; margin-bottom: 14px; }
.admin-user-hdr { display: flex; justify-content: space-between; align-items: flex-start; gap: 8px; margin-bottom: 14px; flex-wrap: wrap; }
.admin-user-name { font-family: var(--font-head); font-size: 1rem; font-weight: 700; color: var(--accent2); }
.admin-user-meta { font-size: 0.78rem; color: var(--text3); margin-top: 2px; }
.admin-data-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(190px,1fr)); gap: 10px; }
.admin-data-block { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r); padding: 12px 14px; }
.admin-data-block h4 { font-size: 0.75rem; text-transform: uppercase; color: var(--text3); font-weight: 600; margin-bottom: 8px; }
.admin-data-block ul { list-style: none; }
.admin-data-block li { font-size: 0.82rem; padding: 3px 0; border-bottom: 1px solid var(--border); color: var(--text2); }
.admin-data-block li:last-child { border-bottom: none; }
.admin-empty { color: var(--text3); font-style: italic; font-size: 0.82rem; }
.admin-search { margin-bottom: 16px; }

/* ── ADMIN LOGIN ── */
#adminLogin {
  min-height: 100vh; display: none; align-items: center; justify-content: center; padding: 20px;
  background: radial-gradient(ellipse 80% 60% at 50% -10%, rgba(245,166,35,.12) 0%, transparent 70%), var(--bg);
}
#adminLogin.show { display: flex; }

/* ── RESPONSIVE ── */
@media (max-width: 580px) {
  .app-header { padding: 0 14px; }
  .main { padding: 16px 12px 60px; }
  .hero { padding: 20px 14px 16px; }
  .stats-bar { border-radius: var(--r); }
  .stat-val { font-size: 1.15rem; }
  .tab { font-size: 0.78rem; padding: 8px 10px; }
  .card { padding: 16px; }
  .pomo-card { padding: 24px 16px; }
  .timer-ring-wrap { width: 150px; height: 150px; }
  .timer-number { font-size: 2.1rem; }
  .login-box { padding: 28px 20px; }
}

/* ── BADGE ── */
.badge { display: inline-flex; align-items: center; padding: 2px 8px; border-radius: 100px; font-size: 0.72rem; font-weight: 600; }
.badge-green { background: rgba(45,212,160,.15); color: var(--green); }
.badge-amber { background: rgba(245,166,35,.15); color: var(--amber); }
.badge-red { background: rgba(255,90,90,.15); color: var(--red); }

/* ── STREAK FIRE ── */
.streak-badge { display: inline-flex; align-items: center; gap: 3px; font-size: 0.78rem; color: var(--amber); font-weight: 600; }

/* ── DIVIDER ── */
.divider { border: none; border-top: 1px solid var(--border); margin: 18px 0; }
</style>
</head>
<body>

<!-- TOAST -->
<div id="toast"></div>

<!-- ════════════════════════════════════════
     LOGIN
════════════════════════════════════════ -->
<div id="loginPage">
  <div class="login-box">
    <div class="login-logo">
      <h1>SmartLife AI</h1>
      <p>Organize seus estudos e sua vida com IA</p>
    </div>

    <div class="form-group">
      <label for="nome">Seu nome</label>
      <input id="nome" placeholder="Ex: João Silva" autocomplete="name">
    </div>
    <div class="form-group">
      <label for="idade">Idade</label>
      <input id="idade" type="number" placeholder="Ex: 20" min="1" max="120">
    </div>
    <div class="error-msg" id="loginError"></div>
    <button class="btn btn-primary" id="btnEntrar" style="margin-top:8px;">Entrar →</button>
    <hr class="login-divider">
    <button class="btn btn-amber" id="btnAdmin" style="width:100%;">Painel Admin</button>
  </div>
</div>

<!-- ════════════════════════════════════════
     ADMIN LOGIN
════════════════════════════════════════ -->
<div id="adminLogin">
  <div class="login-box">
    <div class="login-logo">
      <h1 style="background:linear-gradient(135deg,var(--amber),#ffd97d);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;">Admin</h1>
      <p>Painel de administração</p>
    </div>
    <div class="form-group">
      <label for="adminSenha">Senha</label>
      <input id="adminSenha" type="password" placeholder="Senha admin">
    </div>
    <div class="error-msg" id="adminError"></div>
    <button class="btn btn-amber" id="btnAdminLogin" style="width:100%; margin-top:8px;">Acessar →</button>
    <button class="btn btn-ghost" id="btnAdminVoltar" style="width:100%; margin-top:8px;">Voltar</button>
  </div>
</div>

<!-- ════════════════════════════════════════
     ADMIN PANEL
════════════════════════════════════════ -->
<div id="adminPanel">
  <div class="admin-wrap">
    <div class="admin-hdr">
      <h1>⚙ Painel Admin</h1>
      <div class="admin-hdr-btns">
        <button class="btn btn-success" id="btnExportAll">↓ Exportar Backup</button>
        <button class="btn btn-purple" id="btnImportAll">↑ Importar Backup</button>
        <button class="btn btn-ghost" id="btnBackAdmin">Voltar ao Login</button>
      </div>
      <input type="file" id="fileImport" accept=".json" style="display:none;">
    </div>
    <div class="admin-stats" id="adminStats"></div>
    <div class="admin-search">
      <input id="adminSearch" placeholder="Buscar usuário por nome...">
    </div>
    <div id="adminUsers"></div>
  </div>
</div>

<!-- ════════════════════════════════════════
     APP
════════════════════════════════════════ -->
<div id="app">

  <!-- Header -->
  <header class="app-header">
    <span class="app-logo">SmartLife AI</span>
    <div class="user-chip">
      <div class="user-avatar" id="userAvatar">?</div>
      <span class="user-name" id="userName"></span>
      <button class="btn btn-logout" id="btnLogout">Sair</button>
    </div>
  </header>

  <!-- Hero -->
  <div class="hero">
    <div class="hero-inner">
      <div class="quote-card">
        <div class="quote-mark">"</div>
        <div>
          <div class="quote-text" id="quoteText">Carregando...</div>
          <div class="quote-author" id="quoteAuthor"></div>
        </div>
      </div>
      <div class="stats-bar">
        <div class="stat"><div class="stat-val" id="statTarefas">0</div><div class="stat-lbl">Tarefas</div></div>
        <div class="stat"><div class="stat-val" id="statHabitos">0/0</div><div class="stat-lbl">Hábitos</div></div>
        <div class="stat"><div class="stat-val" id="statPomodoros">0</div><div class="stat-lbl">Pomodoros</div></div>
        <div class="stat"><div class="stat-val" id="statNotas">0</div><div class="stat-lbl">Notas</div></div>
      </div>
    </div>
  </div>

  <!-- Main -->
  <div class="main">

    <!-- Tabs -->
    <div class="tabs">
      <button class="tab active" data-tab="agenda">Agenda</button>
      <button class="tab" data-tab="habitos">Hábitos</button>
      <button class="tab" data-tab="estudos">IA Estudos</button>
      <button class="tab" data-tab="notas">Notas</button>
      <button class="tab" data-tab="pomodoro">Pomodoro</button>
      <button class="tab" data-tab="relatorio">Relatório</button>
    </div>

    <!-- ─── AGENDA ─── -->
    <div class="tab-content active" id="tab-agenda">
      <div class="card">
        <h2>Agenda</h2>
        <p class="card-sub">Organize suas tarefas e compromissos</p>
        <div class="input-row">
          <input id="tarefa" placeholder="Nome da tarefa">
          <input id="dia" type="date">
          <input id="hora" type="time">
        </div>
        <button class="btn btn-primary" id="btnAdd">+ Adicionar Tarefa</button>
        <div class="table-wrap" id="agendaWrap">
          <div class="empty-state" id="emptyAgenda">Nenhuma tarefa adicionada ainda.</div>
          <table id="tabelaAgenda" style="display:none;">
            <thead><tr><th>Tarefa</th><th>Data</th><th>Hora</th><th>Ação</th></tr></thead>
            <tbody id="agendaBody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ─── HÁBITOS ─── -->
    <div class="tab-content" id="tab-habitos">
      <div class="card">
        <h2>Rastreador de Hábitos</h2>
        <p class="card-sub">Construa sequências e monitore seu progresso diário</p>
        <div class="input-row">
          <input id="novoHabito" placeholder="Ex: Ler 30min, Meditar, Exercício...">
          <button class="btn btn-primary" id="btnAddHabito" style="width:auto; padding:11px 20px;">Adicionar</button>
        </div>
        <ul class="habit-list" id="habitList"></ul>
        <div class="empty-state hidden" id="emptyHabitos">Adicione hábitos para rastrear seu progresso.</div>
        <div style="margin-top:16px;">
          <div style="display:flex; justify-content:space-between; font-size:0.82rem; color:var(--text3); margin-bottom:5px;">
            <span>Progresso hoje</span><span id="habitPct">0%</span>
          </div>
          <div class="progress-track"><div class="progress-fill" id="habitBar" style="width:0%"></div></div>
        </div>
      </div>
    </div>

    <!-- ─── IA ESTUDOS ─── -->
    <div class="tab-content" id="tab-estudos">
      <div class="card">
        <h2>IA de Estudos Inteligente</h2>
        <p class="card-sub">Planos personalizados gerados por Claude AI</p>
        <div class="form-group">
          <label for="obj">O que você quer aprender?</label>
          <input id="obj" placeholder="Ex: programação, medicina, inglês, cálculo...">
        </div>
        <div class="input-row">
          <div class="form-group" style="flex:1;">
            <label for="nivel">Nível atual</label>
            <select id="nivel">
              <option value="iniciante">Iniciante</option>
              <option value="intermediário">Intermediário</option>
              <option value="avançado">Avançado</option>
            </select>
          </div>
          <div class="form-group" style="flex:1;">
            <label for="tempo">Tempo disponível</label>
            <select id="tempo">
              <option value="30 minutos por dia">30 min/dia</option>
              <option value="1 hora por dia">1h/dia</option>
              <option value="2 horas por dia">2h/dia</option>
              <option value="3 ou mais horas por dia">3h+/dia</option>
            </select>
          </div>
        </div>
        <button class="btn btn-primary" id="btnGerar">✦ Gerar Plano com IA</button>
        <div id="iaResult"></div>
      </div>
    </div>

    <!-- ─── NOTAS ─── -->
    <div class="tab-content" id="tab-notas">
      <div class="card">
        <h2>Notas Rápidas</h2>
        <p class="card-sub">Anote ideias, resumos e lembretes</p>
        <div class="form-group"><input id="notaTitulo" placeholder="Título da nota"></div>
        <div class="form-group"><textarea id="notaTexto" placeholder="Escreva aqui..."></textarea></div>
        <button class="btn btn-primary" id="btnAddNota">Salvar Nota</button>
        <div class="empty-state" id="emptyNotas" style="margin-top:16px;">Nenhuma nota salva ainda.</div>
        <div class="notes-grid" id="notesList"></div>
      </div>
    </div>

    <!-- ─── POMODORO ─── -->
    <div class="tab-content" id="tab-pomodoro">
      <div class="card pomo-card">
        <h2>Pomodoro Timer</h2>
        <p class="card-sub" style="margin-bottom:28px;">25 min de foco · 5 min de pausa</p>

        <div class="timer-ring-wrap">
          <svg class="timer-ring" width="180" height="180" viewBox="0 0 180 180">
            <circle class="timer-ring-bg" cx="90" cy="90" r="80" stroke-width="8"/>
            <circle class="timer-ring-fill" id="timerArc" cx="90" cy="90" r="80"
              stroke-width="8" stroke-dasharray="502.65" stroke-dashoffset="0"/>
          </svg>
          <div class="timer-number" id="timerDisplay">25:00</div>
        </div>
        <div class="timer-label" id="timerLabel">FOCO</div>

        <div class="pomo-btns" style="margin-top:20px;">
          <button class="btn btn-primary" id="btnStartTimer" style="width:120px;">Iniciar</button>
          <button class="btn btn-ghost" id="btnResetTimer" style="width:100px;">Resetar</button>
        </div>

        <div class="pomo-stats">
          <div>
            <div class="pomo-stat-label">Sessões hoje</div>
            <div class="pomo-stat-val" id="sessoes">0</div>
          </div>
          <div>
            <div class="pomo-stat-label">Tempo de foco</div>
            <div class="pomo-stat-val" id="tempoTotal">0h 0m</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ─── RELATÓRIO ─── -->
    <div class="tab-content" id="tab-relatorio">
      <div class="card">
        <h2>Relatório de Produtividade</h2>
        <p class="card-sub">Visão geral do seu desempenho</p>
        <div id="relatorioContent"></div>
      </div>
    </div>

  </div><!-- /main -->
</div><!-- /app -->

<script>
(function () {
"use strict";

// ═══════════════════════════════════════
// UTILS
// ═══════════════════════════════════════
const $ = id => document.getElementById(id);
const qs = sel => document.querySelector(sel);

function esc(s) {
  const d = document.createElement('div');
  d.textContent = s;
  return d.innerHTML;
}

function showToast(msg, isErr) {
  const t = $('toast');
  t.textContent = msg;
  t.className = 'show' + (isErr ? ' err' : '');
  clearTimeout(t._tid);
  t._tid = setTimeout(() => t.className = '', 3000);
}

function today() { return new Date().toISOString().split('T')[0]; }

function fmtDate(s) {
  if (!s) return '';
  const [y, m, d] = s.split('-');
  return `${d}/${m}/${y}`;
}

// ═══════════════════════════════════════
// STORAGE — por usuário, persistente
// ═══════════════════════════════════════
let currentUser = null;

function uKey(key) {
  if (!currentUser) return 'smartlife__' + key;
  const safe = currentUser.nome.toLowerCase().replace(/\s+/g, '_').replace(/[^a-z0-9_]/g, '');
  return `smartlife_u_${safe}_${key}`;
}

function getData(key, fallback) {
  try { const v = localStorage.getItem(uKey(key)); return v != null ? JSON.parse(v) : fallback; }
  catch { return fallback; }
}

function setData(key, val) {
  try { localStorage.setItem(uKey(key), JSON.stringify(val)); } catch(e) {}
}

// ─── Usuários registrados (lista global) ───
function getUsers() {
  try { const v = localStorage.getItem('smartlife_all_users'); return v ? JSON.parse(v) : []; }
  catch { return []; }
}

function saveUser(user) {
  const users = getUsers();
  const i = users.findIndex(u => u.nome.toLowerCase() === user.nome.toLowerCase());
  const now = new Date().toLocaleString('pt-BR');
  if (i >= 0) {
    users[i].idade = user.idade;
    users[i].ultimoAcesso = now;
  } else {
    users.push({ ...user, criadoEm: now, ultimoAcesso: now });
  }
  localStorage.setItem('smartlife_all_users', JSON.stringify(users));
}

// ─── Lê dados raw de qualquer usuário (para admin) ───
function getUserDataRaw(nome) {
  const safe = nome.toLowerCase().replace(/\s+/g, '_').replace(/[^a-z0-9_]/g, '');
  const prefix = `smartlife_u_${safe}_`;
  const read = key => {
    try { const v = localStorage.getItem(prefix + key); return v ? JSON.parse(v) : null; } catch { return null; }
  };
  return {
    agenda:   read('agenda')  || [],
    habitos:  read('habitos') || [],
    notas:    read('notas')   || [],
    sessoes:  read('sessoes') || 0,
  };
}

// ═══════════════════════════════════════
// FRASES MOTIVACIONAIS
// ═══════════════════════════════════════
const FRASES = [
  { t: "O sucesso é a soma de pequenos esforços repetidos dia após dia.", a: "Robert Collier" },
  { t: "A disciplina é a ponte entre metas e realizações.", a: "Jim Rohn" },
  { t: "A educação é a arma mais poderosa para mudar o mundo.", a: "Nelson Mandela" },
  { t: "Foco não é dizer sim ao que importa. É dizer não a centenas de outras boas ideias.", a: "Steve Jobs" },
  { t: "O melhor momento para plantar uma árvore foi 20 anos atrás. O segundo melhor é agora.", a: "Provérbio Chinês" },
  { t: "Você não precisa ser perfeito. Você só precisa começar.", a: "SmartLife" },
  { t: "Cada dia é uma nova chance de aprender algo novo.", a: "SmartLife" },
  { t: "O único lugar onde o sucesso vem antes do trabalho é no dicionário.", a: "Vidal Sassoon" },
];

function mostrarFrase() {
  const f = FRASES[Math.floor(Math.random() * FRASES.length)];
  $('quoteText').textContent = f.t;
  $('quoteAuthor').textContent = '— ' + f.a;
}

// ═══════════════════════════════════════
// STATS BAR
// ═══════════════════════════════════════
function updateStats() {
  const agenda  = getData('agenda', []);
  const habitos = getData('habitos', []);
  const notas   = getData('notas', []);
  const sessoes = getData('sessoes', 0);
  const t = today();
  const feitos = habitos.filter(h => h.ultimoDia === t).length;

  $('statTarefas').textContent  = agenda.length;
  $('statHabitos').textContent  = `${feitos}/${habitos.length}`;
  $('statPomodoros').textContent = sessoes;
  $('statNotas').textContent    = notas.length;
}

// ═══════════════════════════════════════
// LOGIN
// ═══════════════════════════════════════
function initApp(user) {
  currentUser = user;
  $('loginPage').classList.add('hidden');
  $('app').style.display = 'block';
  const ini = user.nome.trim().charAt(0).toUpperCase();
  $('userAvatar').textContent = ini;
  $('userName').textContent = user.nome;
  mostrarFrase();
  renderAgenda();
  renderHabitos();
  renderNotas();
  updateStats();
  updateTempoTotal();
  $('sessoes').textContent = getData('sessoes', 0);
}

function checkAutoLogin() {
  try {
    const raw = localStorage.getItem('smartlife_session');
    if (!raw) return false;
    const user = JSON.parse(raw);
    currentUser = user;
    initApp(user);
    return true;
  } catch { return false; }
}

$('btnEntrar').addEventListener('click', entrar);
$('idade').addEventListener('keypress', e => e.key === 'Enter' && entrar());
$('nome').addEventListener('keypress', e => e.key === 'Enter' && entrar());

function entrar() {
  const nome  = $('nome').value.trim();
  const idade = parseInt($('idade').value, 10);
  if (!nome) { $('loginError').textContent = 'Informe seu nome.'; return; }
  if (!idade || idade < 1 || idade > 120) { $('loginError').textContent = 'Informe uma idade válida.'; return; }
  $('loginError').textContent = '';
  const user = { nome, idade };
  saveUser(user);
  // Persistir sessão
  localStorage.setItem('smartlife_session', JSON.stringify(user));
  initApp(user);
  showToast(`Bem-vindo, ${nome}! 👋`);
}

$('btnLogout').addEventListener('click', () => {
  localStorage.removeItem('smartlife_session');
  currentUser = null;
  location.reload();
});

// ═══════════════════════════════════════
// TABS
// ═══════════════════════════════════════
document.querySelectorAll('.tab').forEach(tab => {
  tab.addEventListener('click', () => {
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
    tab.classList.add('active');
    $('tab-' + tab.dataset.tab).classList.add('active');
    if (tab.dataset.tab === 'relatorio') renderRelatorio();
  });
});

// ═══════════════════════════════════════
// AGENDA
// ═══════════════════════════════════════
function renderAgenda() {
  const agenda = getData('agenda', []);
  const tbody  = $('agendaBody');
  const empty  = $('emptyAgenda');
  const table  = $('tabelaAgenda');
  tbody.innerHTML = '';

  if (!agenda.length) {
    empty.style.display = 'block'; table.style.display = 'none'; return;
  }
  empty.style.display = 'none'; table.style.display = 'table';

  agenda.slice().sort((a,b) => (a.dia+a.hora).localeCompare(b.dia+b.hora)).forEach((item, i) => {
    const isHoje = item.dia === today();
    const tr = tbody.insertRow();
    tr.innerHTML = `
      <td>${esc(item.tarefa)} ${isHoje ? '<span class="badge badge-amber">Hoje</span>' : ''}</td>
      <td>${fmtDate(item.dia)}</td>
      <td>${item.hora}</td>
      <td><button class="btn btn-danger" data-idx="${i}">Remover</button></td>`;
  });

  tbody.querySelectorAll('[data-idx]').forEach(btn => {
    btn.addEventListener('click', () => {
      // Precisamos encontrar o index real no array não-ordenado
      const sorted = getData('agenda', []).slice().sort((a,b)=>(a.dia+a.hora).localeCompare(b.dia+b.hora));
      const item = sorted[parseInt(btn.dataset.idx)];
      const all = getData('agenda', []);
      const realIdx = all.findIndex(x => x.tarefa === item.tarefa && x.dia === item.dia && x.hora === item.hora);
      if (realIdx >= 0) { all.splice(realIdx, 1); setData('agenda', all); }
      renderAgenda(); updateStats(); showToast('Tarefa removida.');
    });
  });
}

$('btnAdd').addEventListener('click', addTarefa);
$('hora').addEventListener('keypress', e => e.key === 'Enter' && addTarefa());

function addTarefa() {
  const tarefa = $('tarefa').value.trim();
  const dia    = $('dia').value;
  const hora   = $('hora').value;
  if (!tarefa || !dia || !hora) { showToast('Preencha todos os campos!', true); return; }
  const agenda = getData('agenda', []);
  agenda.push({ tarefa, dia, hora });
  setData('agenda', agenda);
  renderAgenda(); updateStats();
  $('tarefa').value = ''; $('dia').value = ''; $('hora').value = '';
  $('tarefa').focus();
  showToast('Tarefa adicionada!');
}

// ═══════════════════════════════════════
// HÁBITOS
// ═══════════════════════════════════════
$('btnAddHabito').addEventListener('click', addHabito);
$('novoHabito').addEventListener('keypress', e => e.key === 'Enter' && addHabito());

function addHabito() {
  const nome = $('novoHabito').value.trim();
  if (!nome) { showToast('Digite o nome do hábito!', true); return; }
  const h = getData('habitos', []);
  h.push({ nome, streak: 0, ultimoDia: '' });
  setData('habitos', h);
  $('novoHabito').value = '';
  renderHabitos(); updateStats();
  showToast('Hábito adicionado!');
}

function renderHabitos() {
  const habitos = getData('habitos', []);
  const list  = $('habitList');
  const empty = $('emptyHabitos');
  list.innerHTML = '';
  const t = today();
  let feitos = 0;

  if (!habitos.length) { empty.classList.remove('hidden'); updateHabitProgress(0, 0); return; }
  empty.classList.add('hidden');

  habitos.forEach((h, i) => {
    const done = h.ultimoDia === t;
    if (done) feitos++;
    const li = document.createElement('li');
    li.className = 'habit-item';
    li.innerHTML = `
      <div class="habit-check ${done ? 'done' : ''}" data-i="${i}"></div>
      <span class="habit-name">${esc(h.nome)}</span>
      ${h.streak > 0 ? `<span class="streak-badge">🔥 ${h.streak}</span>` : ''}
      <span class="habit-del" data-d="${i}">×</span>`;
    list.appendChild(li);
  });

  list.querySelectorAll('.habit-check').forEach(el =>
    el.addEventListener('click', () => { toggleHabito(+el.dataset.i); }));
  list.querySelectorAll('.habit-del').forEach(el =>
    el.addEventListener('click', () => { deleteHabito(+el.dataset.d); }));

  updateHabitProgress(feitos, habitos.length);
}

function toggleHabito(i) {
  const h = getData('habitos', []);
  const item = h[i];
  const t = today();
  if (item.ultimoDia === t) {
    item.streak = Math.max(0, item.streak - 1);
    item.ultimoDia = '';
  } else {
    const yst = new Date(); yst.setDate(yst.getDate()-1);
    const ystStr = yst.toISOString().split('T')[0];
    item.streak = item.ultimoDia === ystStr ? item.streak + 1 : 1;
    item.ultimoDia = t;
  }
  setData('habitos', h); renderHabitos(); updateStats();
}

function deleteHabito(i) {
  const h = getData('habitos', []);
  h.splice(i, 1); setData('habitos', h);
  renderHabitos(); updateStats(); showToast('Hábito removido.');
}

function updateHabitProgress(done, total) {
  const pct = total > 0 ? Math.round((done/total)*100) : 0;
  $('habitPct').textContent = pct + '%';
  $('habitBar').style.width = pct + '%';
}

// ═══════════════════════════════════════
// NOTAS
// ═══════════════════════════════════════
$('btnAddNota').addEventListener('click', addNota);

function addNota() {
  const titulo = $('notaTitulo').value.trim();
  const texto  = $('notaTexto').value.trim();
  if (!titulo && !texto) { showToast('Escreva algo!', true); return; }
  const notas = getData('notas', []);
  notas.unshift({ titulo: titulo || 'Sem título', texto, data: new Date().toLocaleString('pt-BR') });
  setData('notas', notas);
  $('notaTitulo').value = ''; $('notaTexto').value = '';
  renderNotas(); updateStats(); showToast('Nota salva!');
}

function renderNotas() {
  const notas = getData('notas', []);
  const list  = $('notesList');
  const empty = $('emptyNotas');
  list.innerHTML = '';
  if (!notas.length) { empty.style.display = 'block'; return; }
  empty.style.display = 'none';
  notas.forEach((n, i) => {
    const div = document.createElement('div');
    div.className = 'note-item';
    div.innerHTML = `
      <span class="note-del" data-i="${i}">×</span>
      <div class="note-title">${esc(n.titulo)}</div>
      ${n.texto ? `<div class="note-body">${esc(n.texto)}</div>` : ''}
      <div class="note-date">${n.data}</div>`;
    list.appendChild(div);
  });
  list.querySelectorAll('.note-del').forEach(el => el.addEventListener('click', () => {
    const n = getData('notas', []); n.splice(+el.dataset.i, 1); setData('notas', n);
    renderNotas(); updateStats(); showToast('Nota removida.');
  }));
}

// ═══════════════════════════════════════
// IA DE ESTUDOS — Claude API Real
// ═══════════════════════════════════════
$('btnGerar').addEventListener('click', gerar);
$('obj').addEventListener('keypress', e => e.key === 'Enter' && gerar());

async function gerar() {
  const obj   = $('obj').value.trim();
  const nivel = $('nivel').value;
  const tempo = $('tempo').value;
  if (!obj) { showToast('Digite o que quer aprender!', true); return; }

  const res = $('iaResult');
  res.innerHTML = '<div class="ai-loading">Gerando seu plano de estudos personalizado com IA...</div>';
  $('btnGerar').disabled = true;

  const prompt = `Você é um especialista em educação e planejamento de estudos. Crie um plano de estudos detalhado para a seguinte situação:

- Área/Disciplina: ${obj}
- Nível atual: ${nivel}
- Tempo disponível: ${tempo}

Formate a resposta assim:
1. Uma breve introdução motivadora (2 linhas)
2. Lista de 6 a 8 tópicos numerados para estudar em ordem, cada um com uma breve descrição do que abordar
3. Uma dica de método de estudo específica para este conteúdo
4. Uma mensagem de encerramento motivadora

Responda em português brasileiro, de forma clara, prática e direta.`;

  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{ role: 'user', content: prompt }]
      })
    });

    if (!response.ok) throw new Error('API error ' + response.status);
    const data = await response.json();
    const text = data.content.map(b => b.text || '').join('');

    res.innerHTML = `
      <div class="ai-result">
        <h3>✦ Plano de Estudos: ${esc(obj.charAt(0).toUpperCase() + obj.slice(1))}</h3>
        <p class="ai-meta">Nível: <strong>${nivel}</strong> · Tempo: <strong>${tempo}</strong></p>
        <div class="ai-body">${esc(text)}</div>
        <div style="margin-top:14px; padding-top:14px; border-top:1px solid var(--border); font-size:0.8rem; color:var(--text3);">
          💡 Use o Pomodoro para manter o foco durante os estudos!
        </div>
      </div>`;
  } catch (err) {
    res.innerHTML = `<div class="ai-result" style="border-left-color:var(--red);">
      <h3 style="color:var(--red);">Erro ao gerar plano</h3>
      <p class="ai-body">${esc(err.message)}</p>
    </div>`;
  } finally {
    $('btnGerar').disabled = false;
  }
}

// ═══════════════════════════════════════
// POMODORO — com anel SVG animado
// ═══════════════════════════════════════
const POMO_FOCUS = 25 * 60;
const POMO_BREAK = 5  * 60;
const CIRCUMFERENCE = 2 * Math.PI * 80; // r=80

let timerInterval = null;
let timerSecs = POMO_FOCUS;
let isBreak   = false;

function updateTimerDisplay() {
  const m = String(Math.floor(timerSecs / 60)).padStart(2, '0');
  const s = String(timerSecs % 60).padStart(2, '0');
  $('timerDisplay').textContent = `${m}:${s}`;
  const total = isBreak ? POMO_BREAK : POMO_FOCUS;
  const offset = CIRCUMFERENCE * (1 - timerSecs / total);
  $('timerArc').style.strokeDashoffset = offset;
  $('timerArc').style.stroke = isBreak ? 'var(--green)' : 'var(--accent)';
  $('timerLabel').textContent = isBreak ? 'PAUSA' : 'FOCO';
}

function updateTempoTotal() {
  const min = getData('sessoes', 0) * 25;
  $('tempoTotal').textContent = `${Math.floor(min/60)}h ${min%60}m`;
}

$('btnStartTimer').addEventListener('click', function () {
  if (timerInterval) {
    clearInterval(timerInterval); timerInterval = null;
    this.textContent = 'Continuar'; return;
  }
  this.textContent = 'Pausar';
  timerInterval = setInterval(() => {
    timerSecs--;
    updateTimerDisplay();
    if (timerSecs <= 0) {
      clearInterval(timerInterval); timerInterval = null;
      if (!isBreak) {
        const s = getData('sessoes', 0) + 1;
        setData('sessoes', s);
        $('sessoes').textContent = s;
        updateStats(); updateTempoTotal();
        isBreak = true; timerSecs = POMO_BREAK;
        showToast('🎉 Sessão concluída! Descanse 5 minutos.');
        $('btnStartTimer').textContent = 'Iniciar Pausa';
      } else {
        isBreak = false; timerSecs = POMO_FOCUS;
        showToast('💪 Hora de focar novamente!');
        $('btnStartTimer').textContent = 'Iniciar';
      }
      updateTimerDisplay();
    }
  }, 1000);
});

$('btnResetTimer').addEventListener('click', () => {
  clearInterval(timerInterval); timerInterval = null;
  isBreak = false; timerSecs = POMO_FOCUS;
  updateTimerDisplay();
  $('btnStartTimer').textContent = 'Iniciar';
});

// ═══════════════════════════════════════
// RELATÓRIO
// ═══════════════════════════════════════
function renderRelatorio() {
  const agenda  = getData('agenda', []);
  const habitos = getData('habitos', []);
  const notas   = getData('notas', []);
  const sessoes = getData('sessoes', 0);
  const t = today();

  const tarefasHoje = agenda.filter(x => x.dia === t).length;
  const habitosFeitos = habitos.filter(h => h.ultimoDia === t).length;
  const maiorStreak = habitos.reduce((acc, h) => Math.max(acc, h.streak), 0);
  const tempoMin = sessoes * 25;

  let score = 0;
  if (habitos.length) score += (habitosFeitos / habitos.length) * 40;
  score += Math.min(sessoes * 10, 30);
  if (agenda.length) score += 15;
  if (notas.length)  score += 15;
  score = Math.round(Math.min(score, 100));

  const scoreColor = score >= 70 ? 'var(--green)' : score >= 40 ? 'var(--amber)' : 'var(--red)';
  const scoreMsg   = score >= 70 ? 'Excelente! 🚀' : score >= 40 ? 'Bom, continue assim! 💪' : 'Vamos melhorar! 📈';
  const scoreOff   = 2 * Math.PI * 40 * (1 - score/100);

  let html = `
    <div style="text-align:center; margin-bottom:24px;">
      <div class="score-ring">
        <svg width="110" height="110" viewBox="0 0 110 110">
          <circle cx="55" cy="55" r="40" fill="none" stroke="var(--border)" stroke-width="7"/>
          <circle cx="55" cy="55" r="40" fill="none" stroke="${scoreColor}" stroke-width="7"
            stroke-linecap="round" stroke-dasharray="${2*Math.PI*40}" stroke-dashoffset="${scoreOff}"/>
        </svg>
        <div class="score-num" style="color:${scoreColor};">${score}</div>
      </div>
      <p style="color:${scoreColor}; font-weight:700; margin:0;">${scoreMsg}</p>
      <p style="color:var(--text3); font-size:0.78rem; margin-top:4px;">Score de Produtividade</p>
    </div>

    <div class="report-grid">
      <div class="report-card"><div class="report-val">${agenda.length}</div><div class="report-lbl">Tarefas criadas</div></div>
      <div class="report-card"><div class="report-val">${tarefasHoje}</div><div class="report-lbl">Tarefas hoje</div></div>
      <div class="report-card"><div class="report-val">${sessoes}</div><div class="report-lbl">Pomodoros</div></div>
      <div class="report-card"><div class="report-val">${Math.floor(tempoMin/60)}h ${tempoMin%60}m</div><div class="report-lbl">Tempo foco</div></div>
      <div class="report-card"><div class="report-val">${notas.length}</div><div class="report-lbl">Notas salvas</div></div>
      <div class="report-card"><div class="report-val">${maiorStreak}d</div><div class="report-lbl">Maior sequência</div></div>
    </div>`;

  // Hábitos
  if (habitos.length) {
    html += `<div class="report-section"><h3>Hábitos de Hoje</h3>`;
    habitos.forEach(h => {
      const done = h.ultimoDia === t;
      const pct  = done ? 100 : 0;
      const c    = done ? 'var(--green)' : 'var(--text3)';
      html += `<div class="report-bar-row">
        <div class="report-bar-row-head">
          <span>${esc(h.nome)} <span class="streak-badge">🔥 ${h.streak}</span></span>
          <span style="color:${c};">${done ? 'Feito ✓' : 'Pendente'}</span>
        </div>
        <div class="report-bar-bg"><div class="report-bar-fg" style="width:${pct}%; background:${c};"></div></div>
      </div>`;
    });
    const pctG = Math.round((habitosFeitos/habitos.length)*100);
    html += `<p style="text-align:center; color:var(--text3); font-size:0.83rem; margin-top:12px;">
      Conclusão: <strong style="color:var(--accent2);">${pctG}%</strong> (${habitosFeitos}/${habitos.length})
    </p></div>`;
  }

  // Próximas tarefas
  const proximas = agenda.filter(x => x.dia >= t)
    .sort((a,b) => (a.dia+a.hora).localeCompare(b.dia+b.hora)).slice(0, 5);
  if (proximas.length) {
    html += `<div class="report-section"><h3>Próximas Tarefas</h3>`;
    proximas.forEach(x => {
      const isH = x.dia === t;
      html += `<div class="task-row">
        <span>${esc(x.tarefa)} ${isH ? '<span class="badge badge-amber">Hoje</span>' : ''}</span>
        <span style="color:var(--text3); font-size:0.82rem;">${fmtDate(x.dia)} ${x.hora}</span>
      </div>`;
    });
    html += `</div>`;
  }

  // Dica
  let dica;
  if (!habitos.length) dica = 'Adicione hábitos diários para acompanhar sua evolução!';
  else if (habitosFeitos < habitos.length) dica = `Você ainda tem <strong>${habitos.length - habitosFeitos} hábito(s) pendente(s)</strong> hoje. Complete todos!`;
  else if (sessoes < 2) dica = 'Tente fazer pelo menos <strong>2 sessões de Pomodoro</strong> por dia.';
  else dica = '<strong>Parabéns!</strong> Você está mandando muito bem! Continue assim.';

  html += `<div class="tip-box">${dica}</div>`;
  $('relatorioContent').innerHTML = html;
}

// ═══════════════════════════════════════
// ADMIN PANEL
// ═══════════════════════════════════════
const ADMIN_SENHA = 'admin123';

$('btnAdmin').addEventListener('click', () => {
  $('loginPage').classList.add('hidden');
  const al = $('adminLogin');
  al.style.display = 'flex'; al.classList.add('show');
  $('adminSenha').value = ''; $('adminError').textContent = '';
  $('adminSenha').focus();
});

$('btnAdminVoltar').addEventListener('click', () => {
  $('adminLogin').style.display = 'none';
  $('loginPage').classList.remove('hidden');
});

$('btnAdminLogin').addEventListener('click', acessarAdmin);
$('adminSenha').addEventListener('keypress', e => e.key === 'Enter' && acessarAdmin());

function acessarAdmin() {
  if ($('adminSenha').value !== ADMIN_SENHA) {
    $('adminError').textContent = 'Senha incorreta.'; return;
  }
  $('adminLogin').style.display = 'none';
  $('adminPanel').style.display = 'block';
  renderAdmin();
}

$('btnBackAdmin').addEventListener('click', () => {
  $('adminPanel').style.display = 'none';
  $('loginPage').classList.remove('hidden');
});

$('adminSearch').addEventListener('input', function () {
  renderAdmin(this.value.toLowerCase().trim());
});

function renderAdmin(filtro) {
  const users = getUsers();
  const cont  = $('adminUsers');
  const stats = $('adminStats');

  let totT = 0, totN = 0, totP = 0, totH = 0;
  users.forEach(u => {
    const d = getUserDataRaw(u.nome);
    totT += d.agenda.length; totN += d.notas.length;
    totP += d.sessoes;       totH += d.habitos.length;
  });

  stats.innerHTML = `
    <div class="admin-stat"><div class="n">${users.length}</div><div class="l">Usuários</div></div>
    <div class="admin-stat"><div class="n">${totT}</div><div class="l">Tarefas</div></div>
    <div class="admin-stat"><div class="n">${totH}</div><div class="l">Hábitos</div></div>
    <div class="admin-stat"><div class="n">${totN}</div><div class="l">Notas</div></div>
    <div class="admin-stat"><div class="n">${totP}</div><div class="l">Pomodoros</div></div>`;

  cont.innerHTML = '';
  const filtered = filtro ? users.filter(u => u.nome.toLowerCase().includes(filtro)) : users;

  if (!filtered.length) {
    cont.innerHTML = '<div class="empty-state">Nenhum usuário encontrado.</div>'; return;
  }

  filtered.forEach(user => {
    const d = getUserDataRaw(user.nome);
    const minFoco = d.sessoes * 25;

    const agendaItems = d.agenda.length
      ? d.agenda.slice(0,5).map(t => `<li>${esc(t.tarefa)} – ${fmtDate(t.dia)} ${t.hora}</li>`).join('') +
        (d.agenda.length > 5 ? `<li style="color:var(--text3)">+${d.agenda.length-5} mais</li>` : '')
      : '<li class="admin-empty">Nenhuma tarefa</li>';

    const habitosItems = d.habitos.length
      ? d.habitos.map(h => `<li>${esc(h.nome)} – 🔥 ${h.streak} dias</li>`).join('')
      : '<li class="admin-empty">Nenhum hábito</li>';

    const notasItems = d.notas.length
      ? d.notas.slice(0,5).map(n => `<li>${esc(n.titulo)} <span style="color:var(--text3)">(${n.data})</span></li>`).join('') +
        (d.notas.length > 5 ? `<li style="color:var(--text3)">+${d.notas.length-5} mais</li>` : '')
      : '<li class="admin-empty">Nenhuma nota</li>';

    const card = document.createElement('div');
    card.className = 'admin-user-card';
    card.innerHTML = `
      <div class="admin-user-hdr">
        <div>
          <div class="admin-user-name">${esc(user.nome)} <span style="color:var(--text3); font-size:0.85rem;">(${user.idade} anos)</span></div>
          <div class="admin-user-meta">Criado: ${user.criadoEm || 'N/A'} · Último acesso: ${user.ultimoAcesso || 'N/A'}</div>
        </div>
      </div>
      <div class="admin-data-grid">
        <div class="admin-data-block"><h4>Agenda (${d.agenda.length})</h4><ul>${agendaItems}</ul></div>
        <div class="admin-data-block"><h4>Hábitos (${d.habitos.length})</h4><ul>${habitosItems}</ul></div>
        <div class="admin-data-block"><h4>Notas (${d.notas.length})</h4><ul>${notasItems}</ul></div>
        <div class="admin-data-block"><h4>Pomodoro</h4><ul>
          <li>${d.sessoes} sessões</li>
          <li>${Math.floor(minFoco/60)}h ${minFoco%60}min de foco</li>
        </ul></div>
      </div>`;
    cont.appendChild(card);
  });
}

// ═══════════════════════════════════════
// BACKUP
// ═══════════════════════════════════════
$('btnExportAll').addEventListener('click', () => {
  const backup = {};
  for (let i = 0; i < localStorage.length; i++) {
    const k = localStorage.key(i);
    if (k.startsWith('smartlife_')) backup[k] = localStorage.getItem(k);
  }
  const blob = new Blob([JSON.stringify(backup, null, 2)], { type: 'application/json' });
  const url  = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url; a.download = `smartlife_backup_${today()}.json`;
  document.body.appendChild(a); a.click();
  document.body.removeChild(a); URL.revokeObjectURL(url);
  showToast('Backup exportado!');
});

$('btnImportAll').addEventListener('click', () => $('fileImport').click());

$('fileImport').addEventListener('change', function (e) {
  const file = e.target.files[0]; if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    try {
      const backup = JSON.parse(ev.target.result);
      let count = 0;
      for (const k in backup) {
        if (k.startsWith('smartlife_')) { localStorage.setItem(k, backup[k]); count++; }
      }
      showToast(`Backup restaurado! (${count} registros)`);
      renderAdmin();
    } catch { showToast('Arquivo inválido.', true); }
  };
  reader.readAsText(file);
  e.target.value = '';
});

// ═══════════════════════════════════════
// INIT
// ═══════════════════════════════════════
updateTimerDisplay();
if (!checkAutoLogin()) {
  $('loginPage').classList.remove('hidden');
}

})();
</script>
</body>
</html>

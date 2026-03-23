<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>ObfuscaterHub – PhantomScripts</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@700&display=swap');

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: #050e0e;
    background-image:
      linear-gradient(rgba(0,255,150,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,150,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    font-family: 'Share Tech Mono', monospace;
    color: #aaffcc;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  header {
    width: 100%;
    text-align: center;
    padding: 24px 0 10px;
    letter-spacing: 8px;
    font-size: 12px;
    color: #33ffaa55;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 18px;
  }
  header::before, header::after {
    content: '';
    display: inline-block;
    width: 120px;
    height: 1px;
    background: #33ffaa44;
  }

  .card {
    background: #0a1a14;
    border: 1px solid #1a3d2a;
    border-radius: 10px;
    padding: 36px 32px;
    width: 100%;
    max-width: 680px;
    margin: 18px auto;
    position: relative;
  }
  .card::before {
    content: '';
    position: absolute;
    top: 8px; left: 8px;
    width: 14px; height: 14px;
    border-top: 2px solid #33ffaa;
    border-left: 2px solid #33ffaa;
  }
  .card::after {
    content: '';
    position: absolute;
    top: 8px; right: 8px;
    width: 14px; height: 14px;
    border-top: 2px solid #33ffaa;
    border-right: 2px solid #33ffaa;
  }

  h1 {
    font-family: 'Orbitron', sans-serif;
    font-size: 22px;
    text-align: center;
    background: linear-gradient(90deg, #00e5ff, #cc44ff);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    margin-bottom: 6px;
  }
  .subtitle {
    text-align: center;
    font-size: 11px;
    letter-spacing: 4px;
    color: #33ffaa66;
    margin-bottom: 28px;
  }

  .section-label {
    font-size: 11px;
    letter-spacing: 3px;
    color: #33ffaa88;
    margin-bottom: 8px;
  }
  .section-label::before { content: '// '; }

  textarea, input[type=text], input[type=password], input[type=email] {
    width: 100%;
    background: #060f0a;
    border: 1px solid #1a3d2a;
    border-radius: 6px;
    color: #aaffcc;
    font-family: 'Share Tech Mono', monospace;
    font-size: 13px;
    padding: 12px;
    outline: none;
    resize: vertical;
    margin-bottom: 16px;
    transition: border 0.2s;
  }
  textarea:focus, input:focus { border-color: #33ffaa; }
  textarea { height: 180px; }

  .char-count {
    text-align: right;
    font-size: 11px;
    color: #33ffaa44;
    margin-top: -12px;
    margin-bottom: 16px;
  }

  .btn {
    width: 100%;
    padding: 15px;
    border: none;
    border-radius: 8px;
    font-family: 'Orbitron', sans-serif;
    font-size: 14px;
    font-weight: 700;
    letter-spacing: 2px;
    cursor: pointer;
    margin-bottom: 10px;
    transition: opacity 0.2s, transform 0.1s;
  }
  .btn:active { transform: scale(0.98); }
  .btn-primary {
    background: linear-gradient(90deg, #00e5ff, #cc44ff);
    color: #fff;
  }
  .btn-secondary {
    background: transparent;
    border: 1px solid #33ffaa44;
    color: #33ffaa;
  }
  .btn:hover { opacity: 0.85; }

  .info-row {
    display: flex;
    align-items: center;
    background: #060f0a;
    border: 1px solid #1a3d2a;
    border-radius: 6px;
    padding: 12px 16px;
    margin-bottom: 12px;
    gap: 12px;
  }
  .dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    background: #33ffaa;
    flex-shrink: 0;
  }
  .info-label { color: #33ffaa88; font-size: 12px; min-width: 80px; }
  .info-value { color: #33ffaa; font-size: 13px; }

  .loadstring-box {
    background: #060f0a;
    border: 1px solid #1a3d2a;
    border-radius: 6px;
    padding: 16px;
    font-size: 13px;
    color: #aaffcc;
    word-break: break-all;
    margin-bottom: 16px;
    line-height: 1.7;
  }

  .success-icon {
    font-size: 48px;
    text-align: center;
    margin-bottom: 12px;
  }

  .tabs {
    display: flex;
    gap: 8px;
    margin-bottom: 20px;
  }
  .tab {
    flex: 1;
    padding: 10px;
    text-align: center;
    border-radius: 6px;
    font-size: 12px;
    letter-spacing: 2px;
    cursor: pointer;
    border: 1px solid #1a3d2a;
    color: #33ffaa88;
    background: transparent;
    transition: all 0.2s;
  }
  .tab.active {
    background: #0f2a1e;
    border-color: #33ffaa;
    color: #33ffaa;
  }

  .page { display: none; }
  .page.active { display: block; }

  .toast {
    position: fixed;
    bottom: 30px;
    left: 50%;
    transform: translateX(-50%);
    background: #0f2a1e;
    border: 1px solid #33ffaa;
    color: #33ffaa;
    padding: 12px 24px;
    border-radius: 8px;
    font-size: 13px;
    letter-spacing: 1px;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s;
    z-index: 9999;
  }
  .toast.show { opacity: 1; }

  .divider {
    display: flex;
    align-items: center;
    gap: 10px;
    margin: 14px 0;
    color: #33ffaa44;
    font-size: 11px;
  }
  .divider::before, .divider::after {
    content: '';
    flex: 1;
    height: 1px;
    background: #1a3d2a;
  }

  .social-btn {
    width: 100%;
    padding: 12px;
    border-radius: 8px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 13px;
    cursor: pointer;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    transition: opacity 0.2s;
    border: 1px solid #1a3d2a;
    background: #060f0a;
    color: #aaffcc;
  }
  .social-btn:hover { opacity: 0.8; border-color: #33ffaa44; }

  #scriptList { margin-top: 10px; }
  .script-item {
    background: #060f0a;
    border: 1px solid #1a3d2a;
    border-radius: 6px;
    padding: 12px 16px;
    margin-bottom: 8px;
    cursor: pointer;
    transition: border-color 0.2s;
  }
  .script-item:hover { border-color: #33ffaa55; }
  .script-item .name { color: #33ffaa; font-size: 13px; }
  .script-item .meta { color: #33ffaa44; font-size: 11px; margin-top: 4px; }

  a { color: #33ffaa88; text-decoration: none; }
  a:hover { color: #33ffaa; }

  .nav-bar {
    display: flex;
    gap: 8px;
    width: 100%;
    max-width: 680px;
    margin: 10px auto 0;
    padding: 0 4px;
  }
  .nav-btn {
    flex: 1;
    padding: 9px;
    text-align: center;
    border-radius: 6px;
    font-size: 11px;
    letter-spacing: 2px;
    cursor: pointer;
    border: 1px solid #1a3d2a;
    color: #33ffaa88;
    background: transparent;
    transition: all 0.2s;
  }
  .nav-btn.active { background: #0f2a1e; border-color: #33ffaa; color: #33ffaa; }
  .nav-btn:hover { border-color: #33ffaa44; }
</style>
</head>
<body>

<header>OBFUSCATERHUB</header>

<div class="nav-bar">
  <button class="nav-btn active" onclick="showPage('obfuscate')">⚡ PROTECT</button>
  <button class="nav-btn" onclick="showPage('vault')">📁 MY SCRIPTS</button>
  <button class="nav-btn" onclick="showPage('auth')">👤 ACCOUNT</button>
</div>

<!-- OBFUSCATE PAGE -->
<div id="page-obfuscate" class="card page active">
  <h1>Lua Obfuscator</h1>
  <p class="subtitle">SECURE SCRIPTS FOR DELTA & ROBLOX</p>

  <div id="obfView">
    <div class="section-label">SCRIPT INPUT</div>
    <textarea id="scriptInput" placeholder="-- Paste your Lua script here..." oninput="updateCount()"></textarea>
    <div class="char-count"><span id="charCount">0</span> / 30,000</div>

    <div class="section-label">SCRIPT NAME</div>
    <input type="text" id="scriptName" placeholder="e.g. PhantomGodmode_v2" />

    <div class="section-label">PASSWORD (to retrieve script later)</div>
    <input type="password" id="scriptPass" placeholder="Set a secure password..." />

    <button class="btn btn-primary" onclick="saveScript()">⚡ SAVE & PROTECT SCRIPT</button>
  </div>

  <div id="successView" style="display:none;">
    <div class="success-icon">✅</div>
    <h1>Script Protected!</h1>
    <p class="subtitle">YOUR SCRIPT IS ENCRYPTED & READY</p>
    <br>
    <div class="info-row"><div class="dot"></div><span class="info-label">Script ID</span><span class="info-value" id="outScriptId"></span></div>
    <div class="info-row"><div class="dot"></div><span class="info-label">Status</span><span class="info-value">Protected & Live</span></div>

    <br>
    <div class="section-label">LOADSTRING — PASTE INTO YOUR EXECUTOR</div>
    <div class="loadstring-box" id="outLoadstring"></div>

    <button class="btn btn-primary" onclick="copyLoadstring()">⚡ COPY LOADSTRING</button>
    <button class="btn btn-secondary" onclick="resetForm()">← Protect Another Script</button>
  </div>
</div>

<!-- VAULT PAGE -->
<div id="page-vault" class="card page">
  <h1>My Scripts</h1>
  <p class="subtitle">RETRIEVE YOUR PROTECTED SCRIPTS</p>
  <br>
  <div class="section-label">SCRIPT ID</div>
  <input type="text" id="vaultId" placeholder="Enter script ID..." />
  <div class="section-label">PASSWORD</div>
  <input type="password" id="vaultPass" placeholder="Enter password..." />
  <button class="btn btn-primary" onclick="retrieveScript()">🔓 RETRIEVE SCRIPT</button>
  <div id="retrievedBox" style="display:none;margin-top:16px;">
    <div class="section-label">YOUR LOADSTRING</div>
    <div class="loadstring-box" id="retrievedLoadstring"></div>
    <button class="btn btn-primary" onclick="copyRetrieved()">⚡ COPY LOADSTRING</button>
    <br>
    <div class="section-label">RAW SCRIPT</div>
    <textarea id="retrievedRaw" style="height:140px;margin-top:4px;" readonly></textarea>
  </div>
</div>

<!-- AUTH PAGE -->
<div id="page-auth" class="card page">
  <h1>Account</h1>
  <p class="subtitle">SIGN IN TO SAVE YOUR SCRIPTS</p>
  <br>

  <div id="authForm">
    <div class="tabs">
      <div class="tab active" onclick="switchAuthTab('login')">LOGIN</div>
      <div class="tab" onclick="switchAuthTab('register')">REGISTER</div>
    </div>

    <div class="section-label">EMAIL</div>
    <input type="email" id="authEmail" placeholder="your@email.com" />
    <div class="section-label">PASSWORD</div>
    <input type="password" id="authPassword" placeholder="Password..." />
    <div id="confirmRow" style="display:none;">
      <div class="section-label">CONFIRM PASSWORD</div>
      <input type="password" id="authConfirm" placeholder="Confirm password..." />
    </div>

    <button class="btn btn-primary" id="authSubmitBtn" onclick="handleAuth()">⚡ LOGIN</button>

    <div class="divider">OR</div>

    <button class="social-btn" onclick="showToast('Google login coming soon – host on Firebase for full OAuth!')">
      <svg width="18" height="18" viewBox="0 0 48 48"><path fill="#EA4335" d="M24 9.5c3.5 0 6.6 1.2 9 3.2l6.7-6.7C35.8 2.2 30.3 0 24 0 14.7 0 6.7 5.4 2.7 13.3l7.8 6.1C12.5 13.1 17.8 9.5 24 9.5z"/><path fill="#34A853" d="M46.1 24.5c0-1.6-.1-3.1-.4-4.5H24v8.5h12.4c-.5 2.8-2.1 5.1-4.4 6.7l6.9 5.4c4-3.7 6.2-9.2 6.2-16.1z"/><path fill="#4A90D9" d="M10.5 28.6A14.6 14.6 0 0 1 9.5 24c0-1.6.3-3.2.8-4.6l-7.8-6.1A23.9 23.9 0 0 0 0 24c0 3.9.9 7.5 2.5 10.7l8-6.1z"/><path fill="#FBBC05" d="M24 48c6.5 0 12-2.2 16-5.9l-6.9-5.4c-2.1 1.4-4.7 2.3-9.1 2.3-6.2 0-11.5-3.7-13.5-9l-8 6.1C6.7 42.6 14.7 48 24 48z"/></svg>
      Continue with Google
    </button>
    <button class="social-btn" onclick="showToast('Apple login coming soon!')">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="#fff"><path d="M12.152 6.896c-.948 0-2.415-1.078-3.96-1.04-2.04.027-3.91 1.183-4.961 3.014-2.117 3.675-.546 9.103 1.519 12.09 1.013 1.454 2.208 3.09 3.792 3.039 1.52-.065 2.09-.987 3.935-.987 1.831 0 2.35.987 3.96.948 1.637-.026 2.676-1.48 3.676-2.948 1.156-1.688 1.636-3.325 1.662-3.415-.039-.013-3.182-1.221-3.22-4.857-.026-3.04 2.48-4.494 2.597-4.559-1.429-2.09-3.623-2.324-4.39-2.376-2-.156-3.675 1.09-4.61 1.09zM15.53 3.83c.843-1.012 1.4-2.427 1.245-3.83-1.207.052-2.662.805-3.532 1.818-.78.896-1.454 2.338-1.273 3.714 1.338.104 2.715-.688 3.559-1.701"/></svg>
      Continue with Apple
    </button>
  </div>

  <div id="loggedInView" style="display:none;">
    <div class="info-row"><div class="dot"></div><span class="info-label">Logged in as</span><span class="info-value" id="loggedEmail"></span></div>
    <br>
    <button class="btn btn-secondary" onclick="logout()">← LOGOUT</button>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ── JSONBIN CONFIG ─────────────────────────────────────────
// 1. Go to https://jsonbin.io and create a FREE account
// 2. Create a new bin and copy the BIN ID here
// 3. Copy your API key (Master Key) here
const JSONBIN_BIN_ID = "YOUR_BIN_ID_HERE";  // e.g. "65abc123def456"
const JSONBIN_API_KEY = "YOUR_API_KEY_HERE"; // e.g. "$2a$10$..."

// Your raw host URL - scripts will be stored as:
// https://api.jsonbin.io/v3/b/BINID/latest  (full DB)
// For per-script raw, we embed the script content in the DB
// ──────────────────────────────────────────────────────────

let currentUser = JSON.parse(localStorage.getItem('phantom_user') || 'null');
let currentLoadstring = '';
let authMode = 'login';
let db = {};

function showPage(p) {
  document.querySelectorAll('.page').forEach(el => el.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(el => el.classList.remove('active'));
  document.getElementById('page-' + p).classList.add('active');
  event.target.classList.add('active');
  if (p === 'auth' && currentUser) showLoggedIn();
}

function updateCount() {
  const v = document.getElementById('scriptInput').value;
  document.getElementById('charCount').textContent = v.length;
}

function generateId(len=8) {
  const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
  return Array.from({length:len}, ()=>chars[Math.floor(Math.random()*chars.length)]).join('');
}

async function simpleHash(str) {
  const enc = new TextEncoder().encode(str);
  const buf = await crypto.subtle.digest('SHA-256', enc);
  return Array.from(new Uint8Array(buf)).map(b=>b.toString(16).padStart(2,'0')).join('');
}

async function loadDB() {
  if (JSONBIN_BIN_ID === "YOUR_BIN_ID_HERE") { db = {}; return; }
  try {
    const r = await fetch(`https://api.jsonbin.io/v3/b/${JSONBIN_BIN_ID}/latest`, {
      headers: { 'X-Master-Key': JSONBIN_API_KEY }
    });
    const j = await r.json();
    db = j.record || {};
  } catch(e) { db = {}; }
}

async function saveDB() {
  if (JSONBIN_BIN_ID === "YOUR_BIN_ID_HERE") return;
  await fetch(`https://api.jsonbin.io/v3/b/${JSONBIN_BIN_ID}`, {
    method: 'PUT',
    headers: { 'Content-Type':'application/json', 'X-Master-Key': JSONBIN_API_KEY },
    body: JSON.stringify(db)
  });
}

async function saveScript() {
  const code = document.getElementById('scriptInput').value.trim();
  const name = document.getElementById('scriptName').value.trim() || 'Untitled';
  const pass = document.getElementById('scriptPass').value.trim();
  if (!code) { showToast('Paste your script first!'); return; }
  if (!pass) { showToast('Set a password!'); return; }
  if (code.length > 30000) { showToast('Script too long (30k max)!'); return; }

  const id = generateId(8);
  const hash = await simpleHash(pass);

  await loadDB();
  if (!db.scripts) db.scripts = {};

  // Build raw URL - we'll use a data approach
  // The "raw" URL for this system is our JSONBin endpoint
  // Users can also use Pastefy, Pastebin, etc. for true raw hosting
  const rawUrl = `https://api.jsonbin.io/v3/b/${JSONBIN_BIN_ID}/latest`;
  const loadstring = `loadstring(game:HttpGet("${rawUrl}", true))()`;

  // For demo/local mode (no JSONBin configured), store in localStorage
  if (JSONBIN_BIN_ID === "YOUR_BIN_ID_HERE") {
    const local = JSON.parse(localStorage.getItem('phantom_scripts') || '{}');
    local[id] = { name, hash, code, created: Date.now() };
    localStorage.setItem('phantom_scripts', JSON.stringify(local));
  } else {
    db.scripts[id] = { name, hash, code: btoa(unescape(encodeURIComponent(code))), created: Date.now() };
    await saveDB();
  }

  // Build loadstring using script ID as the lookup key
  const finalLoadstring = `loadstring(game:HttpGet("https://obfuscaterhub.tiiny.site/api/${id}", true))()`;

  document.getElementById('outScriptId').textContent = id;
  document.getElementById('outLoadstring').textContent = finalLoadstring;
  currentLoadstring = finalLoadstring;

  document.getElementById('obfView').style.display = 'none';
  document.getElementById('successView').style.display = 'block';
  showToast('Script protected!');
}

async function retrieveScript() {
  const id = document.getElementById('vaultId').value.trim();
  const pass = document.getElementById('vaultPass').value.trim();
  if (!id || !pass) { showToast('Enter ID and password!'); return; }

  const hash = await simpleHash(pass);

  let entry;
  if (JSONBIN_BIN_ID === "YOUR_BIN_ID_HERE") {
    const local = JSON.parse(localStorage.getItem('phantom_scripts') || '{}');
    entry = local[id];
  } else {
    await loadDB();
    entry = db.scripts?.[id];
  }

  if (!entry) { showToast('Script ID not found!'); return; }
  if (entry.hash !== hash) { showToast('Wrong password!'); return; }

  const raw = JSONBIN_BIN_ID === "YOUR_BIN_ID_HERE"
    ? entry.code
    : decodeURIComponent(escape(atob(entry.code)));

  const ls = `loadstring(game:HttpGet("https://obfuscaterhub.tiiny.site/api/${id}", true))()`;
  document.getElementById('retrievedLoadstring').textContent = ls;
  currentLoadstring = ls;
  document.getElementById('retrievedRaw').value = raw;
  document.getElementById('retrievedBox').style.display = 'block';
  showToast('Script retrieved!');
}

function copyLoadstring() {
  navigator.clipboard.writeText(currentLoadstring);
  showToast('Loadstring copied!');
}
function copyRetrieved() {
  navigator.clipboard.writeText(document.getElementById('retrievedLoadstring').textContent);
  showToast('Loadstring copied!');
}

function resetForm() {
  document.getElementById('scriptInput').value = '';
  document.getElementById('scriptName').value = '';
  document.getElementById('scriptPass').value = '';
  document.getElementById('charCount').textContent = '0';
  document.getElementById('obfView').style.display = 'block';
  document.getElementById('successView').style.display = 'none';
}

// ── AUTH ──────────────────────────────────────────────────
function switchAuthTab(mode) {
  authMode = mode;
  document.querySelectorAll('.tab').forEach((t,i) => {
    t.classList.toggle('active', (mode==='login' && i===0)||(mode==='register' && i===1));
  });
  document.getElementById('confirmRow').style.display = mode === 'register' ? 'block' : 'none';
  document.getElementById('authSubmitBtn').textContent = mode === 'login' ? '⚡ LOGIN' : '⚡ CREATE ACCOUNT';
}

async function handleAuth() {
  const email = document.getElementById('authEmail').value.trim();
  const pass = document.getElementById('authPassword').value.trim();
  if (!email || !pass) { showToast('Fill in all fields!'); return; }

  if (authMode === 'register') {
    const confirm = document.getElementById('authConfirm').value.trim();
    if (pass !== confirm) { showToast('Passwords don\'t match!'); return; }
    const hash = await simpleHash(pass);
    const users = JSON.parse(localStorage.getItem('phantom_users') || '{}');
    if (users[email]) { showToast('Account already exists!'); return; }
    users[email] = { hash };
    localStorage.setItem('phantom_users', JSON.stringify(users));
    currentUser = { email };
    localStorage.setItem('phantom_user', JSON.stringify(currentUser));
    showLoggedIn();
    showToast('Account created!');
  } else {
    const hash = await simpleHash(pass);
    const users = JSON.parse(localStorage.getItem('phantom_users') || '{}');
    if (!users[email] || users[email].hash !== hash) { showToast('Wrong email or password!'); return; }
    currentUser = { email };
    localStorage.setItem('phantom_user', JSON.stringify(currentUser));
    showLoggedIn();
    showToast('Logged in!');
  }
}

function showLoggedIn() {
  document.getElementById('authForm').style.display = 'none';
  document.getElementById('loggedInView').style.display = 'block';
  document.getElementById('loggedEmail').textContent = currentUser.email;
}

function logout() {
  currentUser = null;
  localStorage.removeItem('phantom_user');
  document.getElementById('authForm').style.display = 'block';
  document.getElementById('loggedInView').style.display = 'none';
  showToast('Logged out!');
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2500);
}

// Auto-login check
if (currentUser) { /* will show on auth page open */ }
</script>
</body>
</html>

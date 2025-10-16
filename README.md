<GVT>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>GVT140 — Investment Portal (Demo-Real)</title>
<style>
  :root{
    --bg:#f4f7fb; --card:#fff; --muted:#7a8696; --accent:#2d9cdb; --green:#27ae60; --danger:#e74c3c;
  }
  *{box-sizing:border-box}
  body{margin:0;font-family:Inter,Segoe UI,Arial,sans-serif;background:var(--bg);color:#1f2937}
  .wrap{max-width:1140px;margin:20px auto;padding:16px}
  header{display:flex;align-items:center;justify-content:space-between;gap:12px}
  .brand{display:flex;flex-direction:column}
  .brand h1{margin:0;font-size:1.5rem;color:#0f1724}
  .brand p{margin:0;font-size:0.85rem;color:var(--muted)}
  .nav{position:relative}
  .dots{width:46px;height:46px;border-radius:10px;background:var(--card);display:flex;align-items:center;justify-content:center;box-shadow:0 6px 18px rgba(15,23,36,.06);cursor:pointer;font-size:1.6rem}
  .menu{position:absolute;right:0;top:56px;background:var(--card);border-radius:12px;padding:8px;box-shadow:0 10px 30px rgba(15,23,36,.08);display:none;min-width:230px}
  .menu a{display:block;padding:10px;border-radius:8px;color:#0f1724;text-decoration:none;font-weight:600}
  .menu a:hover{background:#eef6ff}
  .grid{display:grid;grid-template-columns:1fr 380px;gap:18px;margin-top:18px}
  .card{background:var(--card);padding:18px;border-radius:12px;box-shadow:0 8px 28px rgba(15,23,36,.04)}
  .small{font-size:0.9rem;color:var(--muted)}
  .balance{display:flex;align-items:center;justify-content:space-between;gap:12px}
  .balance .left{display:flex;flex-direction:column}
  .balance .amount{font-size:1.45rem;font-weight:700;color:#0b1220}
  .controls button{margin-left:8px;padding:8px 12px;border-radius:8px;border:none;cursor:pointer}
  .btn-primary{background:var(--green);color:#fff}
  .btn-secondary{background:var(--accent);color:#fff}
  .btn-danger{background:var(--danger);color:#fff}
  /* plans */
  .plans{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px}
  .plan{padding:14px;border-radius:10px;background:linear-gradient(180deg,#ffffff,#fbfdff);box-shadow:0 8px 18px rgba(16,24,40,.04);border:1px solid #eef6ff}
  .plan h4{margin:4px 0}
  .plan .meta{font-size:.85rem;color:var(--muted);margin-bottom:8px}
  /* table */
  table{width:100%;border-collapse:collapse;margin-top:6px}
  th,td{padding:8px;text-align:left;border-bottom:1px solid #f1f5f9;font-size:.95rem}
  th{color:var(--muted);font-weight:700}
  .muted{color:var(--muted);font-size:.9rem}
  /* forms */
  input,select{width:100%;padding:10px;border-radius:8px;border:1px solid #e6eef6;margin:6px 0}
  .row{display:flex;gap:10px}
  .col{flex:1}
  .invest-card{display:flex;align-items:center;justify-content:space-between;gap:12px}
  .tiny{font-size:.85rem;color:var(--muted)}
  .list{max-height:300px;overflow:auto}
  .center{text-align:center}
  footer{margin-top:18px;color:var(--muted);font-size:.85rem;text-align:center}
  .badge{display:inline-block;padding:6px 8px;border-radius:8px;background:#eef6ff;color:var(--accent);font-weight:700}
  .link-like{color:var(--accent);cursor:pointer;text-decoration:underline}
  @media(max-width:980px){.grid{grid-template-columns:1fr}.nav{position:static}.menu{right:unset;top:unset}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div class="brand">
      <h1>GVT140 Investment Portal</h1>
      <p class="small">Real-like demo • Username+Password free login • Replace payment links to go live</p>
    </div>

    <div class="nav">
      <div class="dots" id="dotsBtn" title="Menu">⋯</div>
      <div class="menu" id="menu">
        <a href="#" data-view="home">Home</a>
        <a href="#" data-view="plans">Plans</a>
        <a href="#" data-view="dashboard">Dashboard</a>
        <a href="#" data-view="about">About</a>
        <a href="#" data-view="contact">Contact</a>
        <a href="#" data-view="settings">Settings</a>
      </div>
    </div>
  </header>

  <div class="grid">
    <!-- left main -->
    <div>
      <!-- HOME -->
      <div id="view-home" class="card" style="display:block">
        <h3>Welcome to GVT140</h3>
        <p class="small">Professional investment interface. Use the Sign up / Login on the right to create a demo account (username & password), or press "Auto Login" to enter immediately.</p>
        <hr>

        <div style="display:flex;gap:12px;flex-wrap:wrap">
          <div style="flex:1" class="card">
            <h4 class="small">Quick Invest</h4>
            <div class="row">
              <div class="col"><input id="quickAmount" type="number" placeholder="Amount PKR"></div>
              <div style="width:160px"><select id="quickPlan"></select></div>
              <div><button class="btn-primary" onclick="quickInvest()">Invest</button></div>
            </div>
            <p class="tiny muted" style="margin-top:8px">Select plan and amount (system will check min/max & balance).</p>
          </div>

          <div style="width:320px" class="card">
            <h4 class="small">Current Offers</h4>
            <p class="tiny">Limited-time demo bonus: +2% extra on any deposit done within demo session (visual only).</p>
            <div style="margin-top:8px"><span class="badge">Demo Bonus</span> <span class="tiny muted">Valid in demo only</span></div>
          </div>
        </div>

        <hr>
        <h4>Featured Plans</h4>
        <div class="plans" id="plansList"></div>
      </div>

      <!-- PLANS -->
      <div id="view-plans" class="card" style="display:none">
        <h3>All Plans</h3>
        <p class="small">Detailed plan table — shows min/max, duration and percentage return.</p>
        <div id="plansTableWrapper" style="margin-top:12px"></div>
      </div>

      <!-- DASHBOARD -->
      <div id="view-dashboard" class="card" style="display:none">
        <div class="balance">
          <div class="left">
            <div class="small">Account</div>
            <div class="amount" id="userLabel">Guest</div>
            <div class="tiny muted" id="joinedLabel"></div>
          </div>
          <div class="controls">
            <div class="tiny muted" id="balanceLabel">Balance: PKR 0</div>
            <button class="btn-primary" onclick="openDeposit()">Deposit</button>
            <button class="btn-secondary" onclick="openWithdraw()">Withdraw</button>
            <button class="btn-danger" onclick="logout()" title="Logout" style="margin-left:8px;padding:8px 10px">Logout</button>
          </div>
        </div>

        <div style="margin-top:14px">
          <h4>Active Investments</h4>
          <div class="list card" id="activeInvestments">
            <p class="tiny muted center">No active investments yet</p>
          </div>
        </div>

        <div style="margin-top:14px">
          <h4>History</h4>
          <div class="list card" id="historyList">
            <p class="tiny muted center">No history yet</p>
          </div>
        </div>
      </div>

      <!-- ABOUT -->
      <div id="view-about" class="card" style="display:none">
        <h3>About GVT140</h3>
        <p class="small"><strong>Founder & CEO:</strong> Muhammad Nazim</p>
        <p>Founded 2020. GVT140 provides tailored investment plans for Pakistani investors. This demo reproduces a real portal experience — to accept real payments and perform real transfers you'd add a backend + merchant gateways (JazzCash / Easypaisa / Bank API).</p>
      </div>

      <!-- CONTACT -->
      <div id="view-contact" class="card" style="display:none">
        <h3>Contact</h3>
        <p class="small">support@gvt140.com • +92 300 1234567</p>
        <p class="small">For production/payment setup contact above or your payment provider.</p>
      </div>

      <!-- SETTINGS -->
      <div id="view-settings" class="card" style="display:none">
        <h3>Settings & Demo Controls</h3>
        <p class="small">Demo time multiplier: controls how fast "days" pass for investment accrual (use to demo earnings).</p>
        <div class="row">
          <div class="col">
            <label class="tiny">Demo speed (seconds per demo-day):</label>
            <input id="demoSpeed" type="number" value="86400" />
            <div class="tiny muted">Set lower to accelerate accrual (e.g., 1 => 1 sec = 1 day)</div>
          </div>
          <div style="width:180px">
            <label class="tiny">Auto-cleanup local data</label>
            <select id="cleanup" onchange="setCleanup(this.value)">
              <option value="never">Never</option>
              <option value="reset">Reset on reload</option>
            </select>
            <div class="tiny muted" style="margin-top:6px">Demo-only: reset clears demo data (except settings)</div>
          </div>
        </div>
      </div>
    </div>

    <!-- right sidebar -->
    <div>
      <div class="card">
        <h4>Sign up / Login (Free)</h4>
        <div id="authArea">
          <div id="loggedOut">
            <div class="tiny muted">Use any username (no email required) + password — data saved in your browser only.</div>
            <input id="signupUser" placeholder="Username (e.g. nazim123)" />
            <input id="signupPass" placeholder="Password" type="password" />
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn-primary" style="flex:1" onclick="signup()">Sign Up</button>
              <button class="btn-secondary" style="flex:1" onclick="login()">Login</button>
            </div>
            <div style="margin-top:8px" class="tiny muted">Or use Auto Login to create a guest session instantly.</div>
            <div style="margin-top:8px"><button onclick="autoLogin()">Auto Login</button></div>
          </div>

          <div id="loggedIn" style="display:none">
            <div class="tiny">Signed in as</div>
            <div style="font-weight:700" id="signedInUser">—</div>
            <div class="tiny" id="signedSince"></div>
            <div style="margin-top:8px">
              <button onclick="switchView('dashboard')" style="padding:8px 12px;margin-right:8px">Open Dashboard</button>
              <button onclick="logout()" style="padding:8px 12px">Logout</button>
            </div>
          </div>
        </div>
      </div>

      <div style="height:12px"></div>

      <div class="card">
        <h4>Deposit / Withdraw</h4>
        <div class="tiny muted">Use demo deposit to credit your balance instantly. External links open payment providers' pages.</div>
        <input id="dwAmount" placeholder="Amount PKR" type="number" />
        <div style="margin-top:8px">
          <button class="btn-primary" style="width:48%" onclick="deposit('JazzCash')">Deposit JazzCash</button>
          <button class="btn-primary" style="width:48%" onclick="deposit('Easypaisa')">Deposit Easypaisa</button>
        </div>
        <div style="margin-top:8px">
          <button class="btn-secondary" style="width:48%" onclick="withdraw('JazzCash')">Withdraw JazzCash</button>
          <button class="btn-secondary" style="width:48%" onclick="withdraw('Easypaisa')">Withdraw Easypaisa</button>
        </div>
        <div style="margin-top:10px">
          <button style="width:100%" onclick="openBankInstructions()">Bank Transfer Instructions</button>
        </div>
      </div>

      <div style="height:12px"></div>

      <div class="card">
        <h4>Quick Calculator</h4>
        <input id="calcAmt" placeholder="Amount PKR" type="number" />
        <select id="calcPlan"></select>
        <div style="margin-top:8px"><button class="btn-primary" onclick="quickCalc()">Calculate</button></div>
        <p class="tiny muted" id="calcResult"></p>
      </div>

      <div style="height:12px"></div>

      <div class="card">
        <h4>Helpful Links</h4>
        <p class="tiny"><a href="https://www.jazzcash.com.pk/" target="_blank" rel="noreferrer">JazzCash</a></p>
        <p class="tiny"><a href="https://www.easypaisa.com.pk/" target="_blank" rel="noreferrer">Easypaisa</a></p>
        <p class="tiny"><a href="#" onclick="alert('Contact support@gvt140.com for merchant setup')">Merchant setup</a></p>
      </div>
    </div>
  </div>

  <footer class="small">© 2020–2025 GVT140 — Demo Portal • Owner: Khan Enterprises • Data stored locally in your browser.</footer>
</div>

<script>
/* ============================
   Full single-file demo app
   ============================ */

/* --------- Config / Plans ---------- */
const PLANS = [
  { id:'starter',  name:'Starter',   min:300,    max:10000,   pct:5,   days:7,   desc:'Low risk, short term' },
  { id:'silver',   name:'Silver',    min:10001,  max:50000,   pct:10,  days:14,  desc:'Moderate returns' },
  { id:'gold',     name:'Gold',      min:50001,  max:250000,  pct:15,  days:21,  desc:'Medium-high return' },
  { id:'platinum', name:'Platinum',  min:250001, max:1000000, pct:22,  days:30,  desc:'High return' },
  { id:'weekly',   name:'Weekly',    min:500,    max:20000,   pct:3,   days:3,   desc:'Very short term' },
  { id:'monthly',  name:'Monthly',   min:2000,   max:100000,  pct:12,  days:30,  desc:'Monthly payout' },
  { id:'flex',     name:'Flex',      min:300,    max:200000,  pct:8,   days:10,  desc:'Flexible plan' },
  { id:'diamond',  name:'Diamond',   min:1000001,max:5000000, pct:30,  days:45,  desc:'VIP plan (demo)' }
];

/* Demo speed (seconds per demo-day). Lower => faster accrual for demo */
let demoSpeed = Number(localStorage.getItem('gvt_demo_speed')) || 86400;
document.getElementById('demoSpeed').value = demoSpeed;

/* ---------- Utility helpers ---------- */
function uidFrom(user){ return 'gvt_u_'+btoa(user).replace(/=/g,''); }
function now(){ return Date.now(); }
function saveUser(user, obj){ localStorage.setItem(uidFrom(user), JSON.stringify(obj)); }
function loadUser(user){ return JSON.parse(localStorage.getItem(uidFrom(user)) || 'null'); }
function ensureUser(user){
  let u = loadUser(user);
  if(!u){
    u = { user, balance:0, createdAt: now(), investments:[], history:[] };
    saveUser(user, u);
  }
  return u;
}

/* ---------- UI initial population ---------- */
const plansList = document.getElementById('plansList');
const plansTableWrapper = document.getElementById('plansTableWrapper');
const quickPlan = document.getElementById('quickPlan');
const calcPlan = document.getElementById('calcPlan');

function renderPlans(){
  plansList.innerHTML = '';
  let tbl = `<table><tr><th>Plan</th><th>Range (PKR)</th><th>Return</th><th>Duration</th><th></th></tr>`;
  PLANS.forEach(p=>{
    const el = document.createElement('div');
    el.className = 'plan';
    el.innerHTML = `<h4>${p.name}</h4><div class="meta">${p.desc}</div><div class="tiny">PKR ${p.min.toLocaleString()} - ${p.max.toLocaleString()}</div><div style="margin-top:8px"><strong>${p.pct}%</strong> total over ${p.days} days</div><div style="margin-top:10px"><button class="btn-primary" onclick="promptInvest('${p.id}')">Invest</button></div>`;
    plansList.appendChild(el);

    tbl += `<tr><td>${p.name}</td><td>PKR ${p.min.toLocaleString()} - ${p.max.toLocaleString()}</td><td>${p.pct}%</td><td>${p.days}</td><td><button onclick="promptInvest('${p.id}')">Invest</button></td></tr>`;

    const opt = document.createElement('option'); opt.value = p.id; opt.text = p.name; quickPlan.appendChild(opt);
    const opt2 = document.createElement('option'); opt2.value = p.id; opt2.text = p.name; calcPlan.appendChild(opt2);
  });
  tbl += '</table>';
  plansTableWrapper.innerHTML = tbl;
}
renderPlans();

/* ---------- Authentication (username+password demo) ---------- */
let CURRENT_USER = localStorage.getItem('gvt_current_user') || null;

function signup(){
  const user = (document.getElementById('signupUser').value||'').trim();
  const pass = (document.getElementById('signupPass').value||'').trim();
  if(!user || !pass) return alert('Enter username and password');
  // store user record and password (demo only)
  ensureUser(user);
  localStorage.setItem(uidFrom(user)+'_pwd', pass);
  alert('Signup created (demo). You can now Login.');
  document.getElementById('signupUser').value=''; document.getElementById('signupPass').value='';
}

function login(){
  const user = (document.getElementById('signupUser').value||'').trim();
  const pass = (document.getElementById('signupPass').value||'').trim();
  if(!user || !pass) return alert('Enter username and password to login');
  const stored = localStorage.getItem(uidFrom(user)+'_pwd');
  if(!stored) return alert('User not found. Please Sign up first or use Auto Login.');
  if(stored !== pass) return alert('Incorrect password');
  CURRENT_USER = user;
  localStorage.setItem('gvt_current_user', CURRENT_USER);
  showLoggedIn();
  refreshDashboard();
}

function autoLogin(){
  const guest = 'guest_demo';
  ensureUser(guest);
  localStorage.setItem(uidFrom(guest)+'_pwd','guest'); // demo password
  CURRENT_USER = guest;
  localStorage.setItem('gvt_current_user', CURRENT_USER);
  showLoggedIn();
  refreshDashboard();
}

function logout(){
  CURRENT_USER = null;
  localStorage.removeItem('gvt_current_user');
  document.getElementById('loggedIn').style.display='none';
  document.getElementById('loggedOut').style.display='block';
  switchView('home');
  // clear sensitive inputs
  document.getElementById('signupUser').value=''; document.getElementById('signupPass').value='';
}

function showLoggedIn(){
  if(!CURRENT_USER) return;
  document.getElementById('loggedOut').style.display='none';
  document.getElementById('loggedIn').style.display='block';
  document.getElementById('signedInUser').innerText = CURRENT_USER;
  const u = ensureUser(CURRENT_USER);
  document.getElementById('signedSince').innerText = 'Member since: ' + new Date(u.createdAt).toLocaleString();
}

/* Restore current on load */
if(localStorage.getItem('gvt_current_user')){
  CURRENT_USER = localStorage.getItem('gvt_current_user');
  showLoggedIn();
  refreshDashboard();
}

/* ---------- Deposit / Withdraw (demo) ---------- */
function deposit(method){
  if(!ensureLogin()) return;
  const amt = Number(document.getElementById('dwAmount').value) || 0;
  if(amt <= 0) return alert('Enter valid amount');
  // open provider site in new tab for realism (user can follow real instructions)
  if(method === 'JazzCash') window.open('https://www.jazzcash.com.pk/','_blank');
  else if(method === 'Easypaisa') window.open('https://www.easypaisa.com.pk/','_blank');
  // credit instantly (demo)
  const u = ensureUser(CURRENT_USER);
  u.balance = (u.balance||0) + amt;
  u.history.push({type:'deposit', method, amount:amt, at:now()});
  saveUser(CURRENT_USER, u);
  refreshDashboard();
  alert(`Demo deposit of PKR ${amt} credited.`);
}

function withdraw(method){
  if(!ensureLogin()) return;
  const amt = Number(document.getElementById('dwAmount').value) || 0;
  const u = ensureUser(CURRENT_USER);
  if(amt <= 0 || amt > (u.balance||0)) return alert('Invalid withdrawal amount');
  // open provider site for instructions
  if(method === 'JazzCash') window.open('https://www.jazzcash.com.pk/','_blank');
  else if(method === 'Easypaisa') window.open('https://www.easypaisa.com.pk/','_blank');
  // deduct (demo)
  u.balance -= amt;
  u.history.push({type:'withdraw', method, amount:amt, at:now()});
  saveUser(CURRENT_USER, u);
  refreshDashboard();
  alert(`Demo withdrawal PKR ${amt} processed (demo).`);
}

function openBankInstructions(){
  const html = `Bank Transfer Instructions:\n\nAccount Name: GVT140 Investments (Demo)\nBank: Example Bank\nAccount #: 1234567890\nIBAN: PK00EXAMPL0001234567890\n\nNote: This is demo text — replace with real bank details for production.`;
  alert(html);
}

/* ---------- Invest flow ---------- */
function promptInvest(planId){
  if(!ensureLogin()) return;
  const p = PLANS.find(x=>x.id===planId);
  if(!p) return alert('Plan not found');
  const s = prompt(`Invest in ${p.name} — ${p.pct}% after ${p.days} days.\nEnter amount PKR (min ${p.min}):`);
  if(!s) return;
  const amt = Number(s);
  if(i

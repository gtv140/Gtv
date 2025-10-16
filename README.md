<!GVT>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>GVT140 — Investment Portal (Demo-Real)</title>
<style>
  :root{
    --bg:#f4f7fb; --card:#fff; --muted:#7a8696; --accent:#2d9cdb; --green:#27ae60;
  }
  *{box-sizing:border-box}
  body{margin:0;font-family:Inter,Segoe UI,Arial,sans-serif;background:var(--bg);color:#1f2937}
  .wrap{max-width:1100px;margin:24px auto;padding:18px}
  header{display:flex;align-items:center;justify-content:space-between;gap:12px}
  .brand{display:flex;flex-direction:column}
  .brand h1{margin:0;font-size:1.4rem;color:#0f1724}
  .brand p{margin:0;font-size:0.85rem;color:var(--muted)}
  .nav{position:relative}
  .dots{width:44px;height:44px;border-radius:8px;background:var(--card);display:flex;align-items:center;justify-content:center;box-shadow:0 6px 18px rgba(15,23,36,.06);cursor:pointer}
  .menu{position:absolute;right:0;top:52px;background:var(--card);border-radius:10px;padding:8px;box-shadow:0 8px 24px rgba(15,23,36,.08);display:none;min-width:200px}
  .menu a{display:block;padding:10px;border-radius:8px;color:#0f1724;text-decoration:none}
  .menu a:hover{background:#eef6ff}
  .grid{display:grid;grid-template-columns:1fr 340px;gap:18px;margin-top:18px}
  .card{background:var(--card);padding:18px;border-radius:12px;box-shadow:0 8px 22px rgba(15,23,36,.04)}
  .small{font-size:0.9rem;color:var(--muted)}
  .balance{display:flex;align-items:center;justify-content:space-between;gap:12px}
  .balance .left{display:flex;flex-direction:column}
  .balance .amount{font-size:1.45rem;font-weight:700;color:#0b1220}
  .controls button{margin-left:8px;padding:8px 12px;border-radius:8px;border:none;cursor:pointer}
  .btn-primary{background:var(--green);color:#fff}
  .btn-secondary{background:var(--accent);color:#fff}
  /* plans */
  .plans{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px}
  .plan{padding:14px;border-radius:10px;background:linear-gradient(180deg,#ffffff,#fbfdff);box-shadow:0 8px 18px rgba(16,24,40,.04);border:1px solid #eef6ff}
  .plan h4{margin:4px 0}
  .plan .meta{font-size:.85rem;color:var(--muted);margin-bottom:8px}
  /* table */
  table{width:100%;border-collapse:collapse;margin-top:6px}
  th,td{padding:8px;text-align:left;border-bottom:1px solid #f1f5f9;font-size:.95rem}
  th{color:var(--muted);font-weight:600}
  .muted{color:var(--muted);font-size:.9rem}
  /* forms */
  input,select{width:100%;padding:10px;border-radius:8px;border:1px solid #e6eef6;margin:6px 0}
  .row{display:flex;gap:10px}
  .col{flex:1}
  .invest-card{display:flex;align-items:center;justify-content:space-between;gap:12px}
  .tiny{font-size:.85rem;color:var(--muted)}
  .list{max-height:260px;overflow:auto}
  .center{text-align:center}
  footer{margin-top:18px;color:var(--muted);font-size:.85rem;text-align:center}
  @media(max-width:980px){.grid{grid-template-columns:1fr}.nav{position:static}.menu{right:unset;top:unset}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div class="brand">
      <h1>GVT140 Investment Portal</h1>
      <p class="small">Demo-Real mode — Login free (demo) • Replace payments to go live</p>
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
      <!-- HOME / PLANS / DASHBOARD views -->
      <div id="view-home" class="card" style="display:block">
        <h3>Welcome to GVT140</h3>
        <p class="small">Choose a plan, deposit funds and start earning. This demo stores data locally in your browser. To make it fully real you will need payment & backend integration (I can help with that).</p>
        <hr>
        <h4>Quick actions</h4>
        <div class="row" style="margin-top:8px">
          <div class="col">
            <input id="quickAmount" type="number" placeholder="Amount PKR">
          </div>
          <div style="width:160px">
            <select id="quickPlan">
              <!-- will be populated -->
            </select>
          </div>
          <div>
            <button class="btn-primary" onclick="quickInvest()">Invest</button>
          </div>
        </div>
        <hr>
        <h4>Featured plans</h4>
        <div class="plans" id="plansList"></div>
      </div>

      <div id="view-plans" class="card" style="display:none">
        <h3>All Plans</h3>
        <p class="small">Detailed list — check min/max, duration and returns.</p>
        <div id="plansTableWrapper" style="margin-top:12px"></div>
      </div>

      <div id="view-dashboard" class="card" style="display:none">
        <div class="balance">
          <div class="left">
            <div class="small">Account</div>
            <div class="amount" id="userLabel">Guest</div>
          </div>
          <div class="controls">
            <span class="small muted" id="balanceLabel">Balance: PKR 0</span>
            <button class="btn-primary" onclick="openDeposit()">Deposit</button>
            <button class="btn-secondary" onclick="openWithdraw()">Withdraw</button>
            <button onclick="logout()" style="margin-left:8px;border-radius:8px;padding:8px 10px">Logout</button>
          </div>
        </div>

        <div style="margin-top:12px">
          <h4>Active Investments</h4>
          <div class="list card" id="activeInvestments">
            <p class="tiny muted center">No active investments yet</p>
          </div>
        </div>

        <div style="margin-top:12px">
          <h4>History</h4>
          <div class="list card" id="historyList">
            <p class="tiny muted center">No history yet</p>
          </div>
        </div>
      </div>

      <div id="view-about" class="card" style="display:none">
        <h3>About GVT140</h3>
        <p class="small">Founder & CEO: <strong>Muhammad Nazim</strong></p>
        <p>Founded 2020. GVT140 provides tailored investment plans for Pakistani investors. This demo reproduces a real portal experience — to accept real payments and perform real transfers you'd add a backend + merchant gateways (JazzCash / Easypaisa).</p>
      </div>

      <div id="view-contact" class="card" style="display:none">
        <h3>Contact</h3>
        <p class="small">support@gvt140.com • +92 300 1234567</p>
        <p class="small">For payment setup or backend support, contact the above.</p>
      </div>

      <div id="view-settings" class="card" style="display:none">
        <h3>Settings & Demo Controls</h3>
        <p class="small">Demo time multiplier: controls how fast "days" pass for investment accrual (useful to demo earnings).</p>
        <div class="row">
          <div class="col">
            <label class="tiny">Demo speed (1 = real days, 86400 = 1 sec per day)</label>
            <input id="demoSpeed" type="number" value="86400" />
          </div>
          <div style="width:180px">
            <label class="tiny">Auto-cleanup local data</label>
            <select id="cleanup" onchange="setCleanup(this.value)">
              <option value="never">Never</option>
              <option value="reset">Reset on reload</option>
            </select>
          </div>
        </div>
        <p class="tiny muted">*Keep demo speed high to watch profits increase quickly. For real deployment set to 1 (no acceleration) and remove demo-only logic.</p>
      </div>

    </div>

    <!-- right sidebar -->
    <div>
      <div class="card">
        <h4>Account (Free Demo Login)</h4>
        <div id="authArea">
          <div id="loggedOut">
            <div class="tiny muted">Quick demo login — creates a free demo account in your browser</div>
            <input id="demoEmail" placeholder="Email (demo) e.g. you@mail.com" />
            <div class="row">
              <div class="col"><input id="demoPass" placeholder="Password (demo)" type="password" /></div>
              <div style="width:110px"><button class="btn-primary" onclick="signupDemo()">Signup</button></div>
            </div>
            <div class="row" style="margin-top:6px">
              <div class="col"><input id="loginEmail" placeholder="Email to login" /></div>
              <div style="width:110px"><button class="btn-secondary" onclick="loginDemo()">Login</button></div>
            </div>
            <div class="tiny muted" style="margin-top:8px">Or press <strong>Auto Login</strong> to enter without creating an account</div>
            <div style="margin-top:8px"><button onclick="autoLogin()">Auto Login</button></div>
          </div>

          <div id="loggedIn" style="display:none">
            <div class="tiny">Signed in as</div>
            <div style="font-weight:700" id="signedInEmail">—</div>
            <div class="tiny" id="signedSince"></div>
            <div style="margin-top:8px">
              <button onclick="logout()" style="padding:8px 12px">Logout</button>
            </div>
          </div>
        </div>
      </div>

      <div style="height:12px"></div>

      <div class="card">
        <h4>Deposit / Withdraw</h4>
        <div class="tiny muted">Use JazzCash or Easypaisa (demo). Deposits update your demo balance instantly.</div>
        <input id="dwAmount" placeholder="Amount PKR" type="number" />
        <div style="margin-top:8px">
          <button class="btn-primary" style="width:48%" onclick="deposit('JazzCash')">Deposit JazzCash</button>
          <button class="btn-primary" style="width:48%" onclick="deposit('Easypaisa')">Deposit Easypaisa</button>
        </div>
        <div style="margin-top:8px">
          <button class="btn-secondary" style="width:48%" onclick="withdraw('JazzCash')">Withdraw JazzCash</button>
          <button class="btn-secondary" style="width:48%" onclick="withdraw('Easypaisa')">Withdraw Easypaisa</button>
        </div>
      </div>

      <div style="height:12px"></div>

      <div class="card">
        <h4>Quick Calculator</h4>
        <input id="calcAmt" placeholder="Amount PKR" type="number" />
        <select id="calcPlan"></select>
        <div style="margin-top:8px"><button onclick="quickCalc()">Calculate</button></div>
        <p class="tiny muted" id="calcResult"></p>
      </div>

    </div>
  </div>

  <footer class="small">GVT140 Demo Portal — Data stored locally in your browser. For production you need a backend, merchant accounts and SSL.</footer>
</div>

<script>
/* -----------------------------
   Demo "real-like" client app
   ----------------------------- */

/* ---------- Configuration ---------- */
const PLANS = [
  { id:'starter',    name:'Starter',  min:300,    max:10000,   pct:5,    days:7,   desc:'Low risk, short term' },
  { id:'silver',     name:'Silver',   min:10001,  max:50000,   pct:10,   days:14,  desc:'Moderate' },
  { id:'gold',       name:'Gold',     min:50001,  max:250000,  pct:15,   days:21,  desc:'Medium-High' },
  { id:'platinum',   name:'Platinum', min:250001, max:1000000, pct:22,   days:30,  desc:'High return' },
  { id:'diamond',    name:'Diamond',  min:1000001,max:5000000, pct:30,   days:45,  desc:'VIP plan (demo)' },
  { id:'weekly',     name:'Weekly',   min:500,    max:20000,   pct:3,    days:3,   desc:'Very short term' },
  { id:'monthly',    name:'Monthly',  min:2000,   max:100000,  pct:12,   days:30,  desc:'Monthly payout' },
  { id:'flex',       name:'Flex',     min:300,    max:200000,  pct:8,    days:10,  desc:'Flexible plan' }
];

// demo speed controls (1 = real seconds per second; 86400 => 1 second equals 1 day)
let demoSpeed = Number(localStorage.getItem('gvt_demo_speed')) || 86400;
document.getElementById('demoSpeed').value = demoSpeed;

/* ---------- Helpers ---------- */
function uidFrom(email){ return 'u_'+btoa(email).replace(/=/g,''); }
function now(){ return Date.now(); }
function saveUser(email, obj){ localStorage.setItem(uidFrom(email), JSON.stringify(obj)); }
function loadUser(email){ return JSON.parse(localStorage.getItem(uidFrom(email)) || 'null'); }
function ensureUser(email){
  let u = loadUser(email);
  if(!u){
    u = { email, balance:0, createdAt: now(), investments:[], history:[] };
    saveUser(email,u);
  }
  return u;
}

/* ---------- UI population ---------- */
const plansList = document.getElementById('plansList');
const plansTableWrapper = document.getElementById('plansTableWrapper');
const quickPlan = document.getElementById('quickPlan');
const calcPlan = document.getElementById('calcPlan');

function renderPlans(){
  plansList.innerHTML = '';
  let tbl = `<table><tr><th>Plan</th><th>Range (PKR)</th><th>Return</th><th>Duration (days)</th><th></th></tr>`;
  PLANS.forEach(p=>{
    // card
    const el = document.createElement('div');
    el.className = 'plan';
    el.innerHTML = `<h4>${p.name}</h4><div class="meta">${p.desc}</div><div class="tiny">PKR ${p.min.toLocaleString()} - ${p.max.toLocaleString()}</div><div style="margin-top:8px"><strong>${p.pct}%</strong> total over ${p.days} days</div><div style="margin-top:8px"><button onclick="openInvestModal('${p.id}')" class="btn-primary">Invest</button></div>`;
    plansList.appendChild(el);
    // table row
    tbl += `<tr><td>${p.name}</td><td>PKR ${p.min.toLocaleString()} - ${p.max.toLocaleString()}</td><td>${p.pct}%</td><td>${p.days}</td><td><button onclick="openInvestModal('${p.id}')">Invest</button></td></tr>`;
    // quick selects
    const opt = document.createElement('option'); opt.value = p.id; opt.text = p.name; quickPlan.appendChild(opt);
    const opt2 = document.createElement('option'); opt2.value = p.id; opt2.text = p.name; calcPlan.appendChild(opt2);
  });
  tbl += '</table>';
  plansTableWrapper.innerHTML = tbl;
}
renderPlans();

/* ---------- Authentication (demo local) ---------- */
let CURRENT_USER_EMAIL = localStorage.getItem('gvt_current') || null;
function signupDemo(){
  const email = (document.getElementById('demoEmail').value||'').trim().toLowerCase();
  const pass = (document.getElementById('demoPass').value||'').trim();
  if(!email || !pass){ alert('Enter email & password'); return; }
  ensureUser(email);
  // store a simple password locally (demo only)
  localStorage.setItem(uidFrom(email)+'_pwd', pass);
  alert('Signup created (demo). Now login.');
  document.getElementById('demoEmail').value=''; document.getElementById('demoPass').value='';
}
function loginDemo(){
  const email = (document.getElementById('loginEmail').value||'').trim().toLowerCase();
  if(!email){ alert('Enter email to login'); return; }
  const pwd = localStorage.getItem(uidFrom(email)+'_pwd');
  if(!pwd){ alert('No demo account found — please Signup first or use Auto Login'); return; }
  CURRENT_USER_EMAIL = email;
  localStorage.setItem('gvt_current', CURRENT_USER_EMAIL);
  showLoggedIn();
  refreshDashboard();
}
function autoLogin(){
  const email = 'guest@demo.local';
  ensureUser(email);
  CURRENT_USER_EMAIL = email;
  localStorage.setItem('gvt_current', CURRENT_USER_EMAIL);
  showLoggedIn();
  refreshDashboard();
}
function logout(){
  CURRENT_USER_EMAIL = null;
  localStorage.removeItem('gvt_current');
  document.getElementById('loggedIn').style.display='none';
  document.getElementById('loggedOut').style.display='block';
  // return to home view
  switchView('home');
}
function showLoggedIn(){
  document.getElementById('loggedOut').style.display='none';
  document.getElementById('loggedIn').style.display='block';
  document.getElementById('signedInEmail').innerText = CURRENT_USER_EMAIL;
  const user = loadUser(CURRENT_USER_EMAIL);
  document.getElementById('signedSince').innerText = 'Member since: ' + new Date(user.createdAt).toLocaleString();
}

/* ---------- Deposit / Withdraw (simulation) ---------- */
function deposit(method){
  if(!ensureLogin()) return;
  const amt = Number(document.getElementById('dwAmount').value) || 0;
  if(amt <= 0){ alert('Enter valid amount'); return; }
  // open a payment page (demo instructions)
  window.open(method==='JazzCash' ? 'https://www.jazzcash.com.pk/' : 'https://www.easypaisa.com.pk/','_blank');
  // instantly credit for demo
  const user = ensureUser(CURRENT_USER_EMAIL);
  user.balance = (user.balance||0) + amt;
  user.history.push({type:'deposit', method, amount:amt, at:now()});
  saveUser(CURRENT_USER_EMAIL, user);
  refreshDashboard();
  alert(`Demo deposit of PKR ${amt} credited to your account.`);
}
function withdraw(method){
  if(!ensureLogin()) return;
  const amt = Number(document.getElementById('dwAmount').value) || 0;
  const user = ensureUser(CURRENT_USER_EMAIL);
  if(amt <= 0 || amt > (user.balance||0)){ alert('Invalid withdrawal amount'); return; }
  // demo: open external link for instructions
  window.open(method==='JazzCash' ? 'https://www.jazzcash.com.pk/' : 'https://www.easypaisa.com.pk/','_blank');
  user.balance -= amt;
  user.history.push({type:'withdraw', method, amount:amt, at:now()});
  saveUser(CURRENT_USER_EMAIL, user);
  refreshDashboard();
  alert(`Demo withdrawal PKR ${amt} requested. (In demo the amount is deducted instantly.)`);
}

/* ---------- Investing ---------- */
function openInvestModal(planId){
  // simple inline prompt for demo
  const p = PLANS.find(i=>i.id===planId);
  if(!p) return alert('Plan not found');
  const amtStr = prompt(`Invest in ${p.name} (${p.pct}% in ${p.days} days)\nEnter amount PKR (min ${p.min})`);
  if(!amtStr) return;
  const amt = Number(amtStr);
  if(isNaN(amt) || amt < p.min || amt > p.max) return alert('Amount invalid for this plan range');
  investPlan(p.id, amt);
}

function quickInvest(){
  const planId = quickPlan.value;
  const amt = Number(document.getElementById('quickAmount').value) || 0;
  if(!planId || amt<=0) return alert('Enter plan & amount');
  investPlan(planId, amt);
}

function investPlan(planId, amount){
  if(!ensureLogin()) return;
  const p = PLANS.find(x=>x.id===planId);
  if(!p) return alert('Plan missing');
  // balance check
  const user = ensureUser(CURRENT_USER_EMAIL);
  if((user.balance||0) < amount) return alert('Insufficient balance. Please deposit first.');
  // deduct and create investment
  user.balance -= amount;
  const start = now();
  const investment = {
    id: 'iv_'+Math.random().toString(36).slice(2,9),
    plan: p.id,
    planName: p.name,
    amount: amount,
    pct: p.pct,
    days: p.days,
    startAt: start,
    status: 'running',
    lastTick: start,
    profitAccrued: 0 // will accrue
  };
  user.investments.push(investment);
  user.history.push({type:'invest', plan:p.name, amount, at:start});
  saveUser(CURRENT_USER_EMAIL, user);
  refreshDashboard();
  alert(`Investment started: ${p.name} — PKR ${amount}. Expected total return: PKR ${(amount * p.pct/100).toFixed(2)} after ${p.days} days.`);
}

/* ---------- Profit accrual engine (demo accelerated) ---------- */
function tickAll(){
  // called periodically to update investments
  demoSpeed = Number(document.getElementById('demoSpeed').value) || demoSpeed;
  localStorage.setItem('gvt_demo_speed', demoSpeed);
  const usersKeys = Object.keys(localStorage).filter(k=>k.startsWith('u_') && !k.endsWith('_pwd'));
  usersKeys.forEach(k=>{
    const u = JSON.parse(localStorage.getItem(k));
    if(!u || !u.investments) return;
    let changed = false;
    u.investments.forEach(inv=>{
      if(inv.status !== 'running') return;
      // compute elapsed "demo days" since lastTick
      const elapsedMs = Date.now() - (inv.lastTick || inv.startAt);
      const elapsedDays = elapsedMs / (1000 * (demoSpeed)); // mapping: demoSpeed seconds == 1 day
      if(elapsedDays <= 0) return;
      // total profit to distribute = amount * pct/100 over inv.days
      const totalProfit = inv.amount * (inv.pct/100);
      // profit per day:
      const perDay = tota

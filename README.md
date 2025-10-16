<GVT>COMING SOON 🔜 
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>GVT140 — Working Demo Portal</title>
<style>
  :root{
    --bg:#f4f7fb; --card:#fff; --muted:#6b7280; --accent:#2563eb; --green:#16a34a; --danger:#ef4444;
  }
  *{box-sizing:border-box}
  body{margin:0;font-family:Inter,Segoe UI,Arial,sans-serif;background:var(--bg);color:#0f1724}
  .wrap{max-width:1120px;margin:20px auto;padding:16px}
  header{display:flex;align-items:center;justify-content:space-between;gap:12px}
  .brand{display:flex;flex-direction:column}
  .brand h1{margin:0;font-size:1.4rem}
  .brand p{margin:0;font-size:.9rem;color:var(--muted)}
  .nav{position:relative}
  .dots{width:44px;height:44px;border-radius:10px;background:var(--card);display:flex;align-items:center;justify-content:center;box-shadow:0 8px 20px rgba(2,6,23,.06);cursor:pointer;font-size:1.4rem}
  .menu{position:absolute;right:0;top:56px;background:var(--card);border-radius:10px;padding:8px;box-shadow:0 10px 30px rgba(2,6,23,.08);display:none;min-width:200px;z-index:50}
  .menu a{display:block;padding:10px;border-radius:8px;color:#0f1724;text-decoration:none;font-weight:600}
  .menu a:hover{background:#eef2ff}
  .grid{display:grid;grid-template-columns:1fr 360px;gap:18px;margin-top:18px}
  .card{background:var(--card);padding:16px;border-radius:12px;box-shadow:0 8px 28px rgba(2,6,23,.04)}
  .small{font-size:.9rem;color:var(--muted)}
  .balance{display:flex;align-items:center;justify-content:space-between;gap:12px}
  .balance .left{display:flex;flex-direction:column}
  .balance .amount{font-size:1.3rem;font-weight:700}
  .controls button{margin-left:8px;padding:8px 12px;border-radius:8px;border:none;cursor:pointer}
  .btn-primary{background:var(--green);color:#fff}
  .btn-secondary{background:var(--accent);color:#fff}
  .btn-danger{background:var(--danger);color:#fff}
  .plans{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px}
  .plan{padding:12px;border-radius:10px;background:linear-gradient(180deg,#fff,#fbfdff);border:1px solid #eef2ff}
  .plan h4{margin:6px 0}
  input,select{width:100%;padding:10px;border-radius:8px;border:1px solid #e6eef6;margin:6px 0}
  table{width:100%;border-collapse:collapse}
  th,td{padding:8px;text-align:left;border-bottom:1px solid #f1f5f9;font-size:.95rem}
  th{color:var(--muted);font-weight:700}
  .tiny{font-size:.85rem;color:var(--muted)}
  .list{max-height:300px;overflow:auto}
  .center{text-align:center}
  footer{margin-top:18px;color:var(--muted);font-size:.85rem;text-align:center}
  @media(max-width:920px){.grid{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div class="brand">
      <h1>GVT140 Investment Portal</h1>
      <p class="small">Demo (client-side) — Username/Password free login • Replace payment links to go live</p>
    </div>
    <div class="nav">
      <div id="dotsBtn" class="dots" title="Menu">⋯</div>
      <div id="menu" class="menu">
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
    <!-- LEFT -->
    <div>
      <!-- HOME -->
      <div id="view-home" class="card" style="display:block">
        <h3>Welcome to GVT140</h3>
        <p class="small">Sign up or Login using the panel on the right. Use Auto Login for quick demo access.</p>
        <hr>
        <div style="display:flex;gap:12px;flex-wrap:wrap">
          <div style="flex:1" class="card">
            <h4 class="small">Quick Invest</h4>
            <div style="display:flex;gap:8px">
              <input id="quickAmount" type="number" placeholder="Amount PKR">
              <select id="quickPlan" style="width:200px"></select>
              <button class="btn-primary" onclick="quickInvest()">Invest</button>
            </div>
            <p class="tiny" style="margin-top:8px">System checks min/max and your balance.</p>
          </div>
          <div style="width:300px" class="card">
            <h4 class="small">Demo Notice</h4>
            <p class="tiny">This demo updates balance locally. For production you need backend & merchant setup.</p>
          </div>
        </div>
        <hr>
        <h4>Featured Plans</h4>
        <div class="plans" id="plansList"></div>
      </div>

      <!-- PLANS -->
      <div id="view-plans" class="card" style="display:none">
        <h3>All Plans</h3>
        <p class="small">Min / Max / Return (%) / Duration (days)</p>
        <div id="plansTableWrapper" style="margin-top:12px"></div>
      </div>

      <!-- DASHBOARD -->
      <div id="view-dashboard" class="card" style="display:none">
        <div class="balance">
          <div class="left">
            <div class="tiny">Account</div>
            <div class="amount" id="userLabel">Guest</div>
            <div class="tiny" id="joinedLabel"></div>
          </div>
          <div class="controls">
            <div class="tiny" id="balanceLabel">Balance: PKR 0</div>
            <button class="btn-primary" onclick="openDeposit()">Deposit</button>
            <button class="btn-secondary" onclick="openWithdraw()">Withdraw</button>
            <button class="btn-danger" onclick="logout()" title="Logout" style="margin-left:8px">Logout</button>
          </div>
        </div>

        <div style="margin-top:12px">
          <h4>Active Investments</h4>
          <div id="activeInvestments" class="list card"><p class="tiny center muted">No active investments</p></div>
        </div>

        <div style="margin-top:12px">
          <h4>History</h4>
          <div id="historyList" class="list card"><p class="tiny center muted">No history</p></div>
        </div>
      </div>

      <!-- ABOUT -->
      <div id="view-about" class="card" style="display:none">
        <h3>About GVT140</h3>
        <p class="tiny"><strong>Founder & CEO:</strong> Muhammad Nazim</p>
        <p class="small">Founded 2020. GVT140 provides tailored investment plans (demo). For live payments add backend & merchant APIs.</p>
      </div>

      <!-- CONTACT -->
      <div id="view-contact" class="card" style="display:none">
        <h3>Contact</h3>
        <p class="small">support@gvt140.com • +92 300 1234567</p>
      </div>

      <!-- SETTINGS -->
      <div id="view-settings" class="card" style="display:none">
        <h3>Settings (Demo Controls)</h3>
        <div class="tiny">Demo speed: how fast "days" pass for accrual (lower = faster demo)</div>
        <div style="margin-top:8px">
          <input id="demoSpeed" type="number" value="86400" />
          <div class="tiny" style="margin-top:6px">Example: 1 → 1 sec = 1 demo day (very fast). 86400 → 1 real day = 1 demo day.</div>
        </div>
        <div style="margin-top:10px">
          <label class="tiny">Cleanup:</label>
          <select id="cleanup" onchange="setCleanup(this.value)">
            <option value="never">Never</option>
            <option value="reset">Reset on reload</option>
          </select>
        </div>
      </div>
    </div>

    <!-- RIGHT -->
    <div>
      <div class="card">
        <h4>Sign up / Login (Free - local)</h4>
        <div id="authArea">
          <div id="loggedOut">
            <div class="tiny">Create username & password (no email required). Data stored in your browser.</div>
            <input id="signupUser" placeholder="Username" />
            <input id="signupPass" placeholder="Password" type="password" />
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn-primary" style="flex:1" onclick="signup()">Sign Up</button>
              <button class="btn-secondary" style="flex:1" onclick="login()">Login</button>
            </div>
            <div style="margin-top:8px" class="tiny">Or use Auto Login for guest demo</div>
            <div style="margin-top:8px"><button onclick="autoLogin()">Auto Login</button></div>
          </div>

          <div id="loggedIn" style="display:none">
            <div class="tiny">Signed in as</div>
            <div style="font-weight:700" id="signedInUser">—</div>
            <div class="tiny" id="signedSince"></div>
            <div style="margin-top:8px">
              <button class="btn-primary" onclick="switchView('dashboard')">Open Dashboard</button>
              <button style="margin-left:8px" onclick="logout()">Logout</button>
            </div>
          </div>
        </div>
      </div>

      <div style="height:12px"></div>

      <div class="card">
        <h4>Deposit / Withdraw</h4>
        <div class="tiny">Deposits in demo are credited instantly; external links open provider pages for realism.</div>
        <input id="dwAmount" placeholder="Amount PKR" type="number" />
        <div style="display:flex;gap:8px;margin-top:8px">
          <button class="btn-primary" style="flex:1" onclick="deposit('JazzCash')">Deposit JazzCash</button>
          <button class="btn-primary" style="flex:1" onclick="deposit('Easypaisa')">Deposit Easypaisa</button>
        </div>
        <div style="display:flex;gap:8px;margin-top:8px">
          <button class="btn-secondary" style="flex:1" onclick="withdraw('JazzCash')">Withdraw JazzCash</button>
          <button class="btn-secondary" style="flex:1" onclick="withdraw('Easypaisa')">Withdraw Easypaisa</button>
        </div>
        <div style="margin-top:8px">
          <button style="width:100%" onclick="openBankInstructions()">Bank Transfer Instructions</button>
        </div>
      </div>

      <div style="height:12px"></div>

      <div class="card">
        <h4>Quick Calculator</h4>
        <input id="calcAmt" placeholder="Amount PKR" type="number" />
        <select id="calcPlan"></select>
        <div style="margin-top:8px"><button class="btn-primary" onclick="quickCalc()">Calculate</button></div>
        <p class="tiny" id="calcResult"></p>
      </div>

      <div style="height:12px"></div>

      <div class="card">
        <h4>Helpful Links</h4>
        <p class="tiny"><a href="https://www.jazzcash.com.pk/" target="_blank" rel="noreferrer">JazzCash</a></p>
        <p class="tiny"><a href="https://www.easypaisa.com.pk/" target="_blank" rel="noreferrer">Easypaisa</a></p>
      </div>
    </div>
  </div>

  <footer class="small">© 2020–2025 GVT140 — Demo Portal • Owner: Khan Enterprises • Data stored locally in your browser.</footer>
</div>

<script>
/* ---------- Plans config ---------- */
const PLANS = [
  { id:'starter',  name:'Starter',   min:300,    max:10000,   pct:5,   days:7,   desc:'Low risk' },
  { id:'silver',   name:'Silver',    min:10001,  max:50000,   pct:10,  days:14,  desc:'Moderate' },
  { id:'gold',     name:'Gold',      min:50001,  max:250000,  pct:15,  days:21,  desc:'Medium-high' },
  { id:'platinum', name:'Platinum',  min:250001, max:1000000, pct:22,  days:30,  desc:'High return' },
  { id:'weekly',   name:'Weekly',    min:500,    max:20000,   pct:3,   days:3,   desc:'Short term' },
  { id:'monthly',  name:'Monthly',   min:2000,   max:100000,  pct:12,  days:30,  desc:'Monthly payout' },
  { id:'flex',     name:'Flex',      min:300,    max:200000,  pct:8,   days:10,  desc:'Flexible' },
  { id:'diamond',  name:'Diamond',   min:1000001,max:5000000, pct:30,  days:45,  desc:'VIP (demo)' }
];

/* ---------- Demo settings ---------- */
let demoSpeed = Number(localStorage.getItem('gvt_demo_speed')) || 86400;
document.getElementById('demoSpeed').value = demoSpeed;

/* ---------- Helpers ---------- */
function uidFrom(u){ return 'gvt_u_'+btoa(u).replace(/=/g,''); }
function now(){ return Date.now(); }
function loadUser(u){ return JSON.parse(localStorage.getItem(uidFrom(u)) || 'null'); }
function saveUser(u, obj){ localStorage.setItem(uidFrom(u), JSON.stringify(obj)); }
function ensureUser(u){
  let x = loadUser(u);
  if(!x){
    x = { user:u, balance:0, createdAt: now(), investments:[], history:[] };
    saveUser(u,x);
  }
  return x;
}

/* ---------- Render plans & selects ---------- */
const plansList = document.getElementById('plansList');
const plansTableWrapper = document.getElementById('plansTableWrapper');
const quickPlan = document.getElementById('quickPlan');
const calcPlan = document.getElementById('calcPlan');

function renderPlans(){
  plansList.innerHTML = '';
  let table = `<table><tr><th>Plan</th><th>Range</th><th>Return</th><th>Days</th><th></th></tr>`;
  PLANS.forEach(p=>{
    const el = document.createElement('div');
    el.className = 'plan';
    el.innerHTML = `<h4>${p.name}</h4><div class="tiny">${p.desc}</div><div class="tiny">PKR ${p.min.toLocaleString()} - ${p.max.toLocaleString()}</div><div style="margin-top:8px"><strong>${p.pct}%</strong> in ${p.days} days</div><div style="margin-top:10px"><button class="btn-primary" onclick="promptInvest('${p.id}')">Invest</button></div>`;
    plansList.appendChild(el);

    table += `<tr><td>${p.name}</td><td>PKR ${p.min.toLocaleString()} - ${p.max.toLocaleString()}</td><td>${p.pct}%</td><td>${p.days}</td><td><button onclick="promptInvest('${p.id}')">Invest</button></td></tr>`;

    const o1 = document.createElement('option'); o1.value=p.id; o1.text=p.name; quickPlan.appendChild(o1);
    const o2 = document.createElement('option'); o2.value=p.id; o2.text=p.name; calcPlan.appendChild(o2);
  });
  table += '</table>';
  plansTableWrapper.innerHTML = table;
}
renderPlans();

/* ---------- Authentication (username + password local demo) ---------- */
let CURRENT_USER = localStorage.getItem('gvt_current_user') || null;

function signup(){
  const user = (document.getElementById('signupUser').value||'').trim();
  const pass = (document.getElementById('signupPass').value||'').trim();
  if(!user || !pass) return alert('Enter username & password');
  ensureUser(user);
  localStorage.setItem(uidFrom(user)+'_pwd', pass);
  alert('Signup successful (demo). Now Login.');
  document.getElementById('signupUser').value=''; document.getElementById('signupPass').value='';
}

function login(){
  const user = (document.getElementById('signupUser').value||'').trim();
  const pass = (document.getElementById('signupPass').value||'').trim();
  if(!user || !pass) return alert('Enter username & password to login');
  const stored = localStorage.getItem(uidFrom(user)+'_pwd');
  if(!stored) return alert('User not found — please Sign up or use Auto Login');
  if(stored !== pass) return alert('Incorrect password');
  CURRENT_USER = user;
  localStorage.setItem('gvt_current_user', CURRENT_USER);
  showLoggedIn();
  refreshDashboard();
}

function autoLogin(){
  const guest = 'guest_demo';
  ensureUser(guest);
  localStorage.setItem(uidFrom(guest)+'_pwd','guest');
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

/* Restore current */
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
  if(method==='JazzCash') window.open('https://www.jazzcash.com.pk/','_blank');
  else window.open('https://www.easypaisa.com.pk/','_blank');
  const u = ensureUser(CURRENT_USER);
  u.balance = (u.balance||0) + amt;
  u.history.push({type:'deposit', method, amount:amt, at:now()});
  saveUser(CURRENT_USER,u);
  refreshDashboard();
  alert(`Demo deposit PKR ${amt} credited.`);
}

function withdraw(method){
  if(!ensureLogin()) return;
  const amt = Number(document.getElementById('dwAmount').value) || 0;
  const u = ensureUser(CURRENT_USER);
  if(amt <= 0 || amt > (u.balance||0)) return alert('Invalid withdrawal amount');
  if(method==='JazzCash') window.open('https://www.jazzcash.com.pk/','_blank');
  else window.open('https://www.easypaisa.com.pk/','_blank');
  u.balance -= amt;
  u.history.push({type:'withdraw', method, amount:amt, at:now()});
  saveUser(CURRENT_USER,u);
  refreshDashboard();
  alert(`Demo withdrawal PKR ${amt} processed.`);
}

function openBankInstructions(){
  alert(`Bank transfer demo:\nAccount: GVT140 Investments (Demo)\nBank: Example Bank\nAcc#: 1234567890\nIBAN: PK00EXAMPLE000`);
}

/* ---------- Invest flow ---------- */
function promptInvest(planId){
  if(!ensureLogin()) return;
  const p = PLANS.find(x=>x.id===planId);
  if(!p) return alert('Plan not found');
  const s = prompt(`Invest in ${p.name} — ${p.pct}% after ${p.days} days.\nEnter amount PKR (min ${p.min}):`);
  if(!s) return;
  const amt = Number(s);
  if(isNaN(amt) || amt < p.min || amt > p.max) return alert('Amount invalid for this plan');
  investPlan(planId, amt);
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
  const u = ensureUser(CURRENT_USER);
  if((u.balance||0) < amount) return alert('Insufficient balance. Please deposit first.');
  u.balance -= amount;
  const inv = {
    id: 'iv_'+Math.random().toString(36).slice(2,9),
    plan: p.id, planName:p.name, amount, pct:p.pct, days:p.days,
    startAt: now(), lastTick: now(), profitAccrued:0, status:'running'
  };
  u.investments.push(inv);
  u.history.push({type:'invest', plan: p.name, amount, at: now()});
  saveUser(CURRENT_USER,u);
  refreshDashboard();
  alert(`Investment started: ${p.name} — PKR ${amount}. Expected profit: PKR ${(amount*p.pct/100).toFixed(2)}.`);
}

/* ---------- Profit accrual engine ---------- */
function tickAll(){
  demoSpeed = Number(document.getElementById('demoSpeed').value) || demoSpeed;
  localStorage.setItem('gvt_demo_speed', demoSpeed);
  Object.keys(localStorage).forEach(k=>{
    if(!k.startsWith('gvt_u_') || k.endsWith('_pwd')) return;
    let u = JSON.parse(localStorage.getItem(k));
    if(!u || !u.investments) return;
    let changed=false;
    u.investments.forEach(inv=>{
      if(inv.status!=='running') return;
      const elapsedMs = Date.now() - (inv.lastTick || inv.startAt);
      const elapsedDays = elapsedMs / (1000 * demoSpeed);
      if(elapsedDays<=0) return;
      const totalProfit = inv.amount * (inv.pct/100);
      const perDay = totalProfit / inv.days;
      const add = perDay * elapsedDays;
      inv.profitAccrued = Math.min((inv.profitAccrued||0) + add, totalProfit);
      inv.lastTick = Date.now();
      const runDays = (Date.now() - inv.startAt) / (1000 * demoSpeed);
      if(runDays >= inv.days){
        inv.status = 'completed';
        u.balance = (u.balance||0) + inv.amount + inv.profitAccrued;
        u.history.push({type:'payout', plan:inv.planName, amount: inv.amount + inv.profitAccrued, at: Date.now()});
      }
      changed = true;
    });
    if(changed) localStorage.setItem(k, 

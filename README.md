<NEONS>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Neon Earn – Premium Real Earning</title>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
<style>
body {
  font-family: 'Roboto', sans-serif;
  margin:0; padding:0;
  background:#111; color:#fff;
}
header {
  background: linear-gradient(90deg, #0ff, #f0f);
  padding:1rem;
  text-align:center;
  font-weight:bold;
  color:#000;
  box-shadow:0 4px 10px rgba(0,0,0,0.5);
  border-bottom:3px solid #0ff;
}
.container { padding:1rem; max-width:600px; margin:0 auto; }
input, select, button {
  padding:0.7rem; margin:0.5rem 0; width:100%; border-radius:10px; border:none; font-size:1rem;
}
button {
  background: linear-gradient(90deg, #0ff, #f0f);
  color:#000; font-weight:bold; cursor:pointer; transition:0.3s;
}
button:hover { transform:scale(1.05); }
.wallet { background:#222; padding:1rem; margin:1rem 0; border-radius:15px; box-shadow:0 0 10px #0ff; }
table { width:100%; margin-top:1rem; border-collapse:collapse; border-radius:10px; overflow:hidden; }
th, td { padding:0.5rem; border:1px solid #0ff; text-align:center; }
.admin-panel { background:#222; padding:1rem; margin:1rem 0; border-radius:15px; box-shadow:0 0 10px #f0f; }
.hidden { display:none; }
h2,h3 { text-align:center; color:#0ff; text-shadow:0 0 5px #0ff; }
</style>
</head>
<body>

<header>🌟 Neon Earn – Premium Real Earning 🌟</header>

<div class="container">

<!-- LOGIN / SIGNUP -->
<div id="auth">
  <h2>Login / Signup</h2>
  <input type="text" id="username" placeholder="Username">
  <input type="password" id="password" placeholder="Password">
  <button onclick="signup()">Signup</button>
  <button onclick="login()">Login</button>
</div>

<!-- USER DASHBOARD -->
<div id="dashboard" class="hidden">
  <h2>Welcome <span id="user-name"></span></h2>
  <div class="wallet">
    <p>Wallet Balance: <span id="wallet-balance">0</span> ₹</p>
  </div>

  <h3>Earn</h3>
  <button onclick="earnDemo()">Click Ad / Earn ₹10</button>

  <h3>Deposit Request</h3>
  <input type="number" id="deposit-amount" placeholder="Amount to deposit">
  <select id="deposit-method">
    <option value="Easypaisa">Easypaisa</option>
    <option value="JazzCash">JazzCash</option>
    <option value="Payoneer">Payoneer</option>
  </select>
  <button onclick="requestDeposit()">Request Deposit</button>

  <table id="user-deposits">
    <thead><tr><th>Amount</th><th>Method</th><th>Status</th></tr></thead>
    <tbody></tbody>
  </table>

  <h3>Withdraw</h3>
  <input type="number" id="withdraw-amount" placeholder="Amount to withdraw">
  <select id="withdraw-method">
    <option value="Easypaisa">Easypaisa</option>
    <option value="JazzCash">JazzCash</option>
    <option value="Payoneer">Payoneer</option>
  </select>
  <button onclick="requestWithdraw()">Request Withdraw</button>

  <table id="user-withdraws">
    <thead><tr><th>Amount</th><th>Method</th><th>Status</th></tr></thead>
    <tbody></tbody>
  </table>
</div>

<!-- ADMIN PANEL -->
<div id="admin-panel" class="hidden admin-panel">
  <h2>Admin Panel</h2>
  <p>Username: <strong>admin</strong></p>
  <input type="password" id="admin-pass" placeholder="Enter admin password">
  <button onclick="loginAdmin()">Login as Admin</button>

  <div id="admin-controls" class="hidden">
    <h3>Deposit Requests</h3>
    <table id="admin-deposits">
      <thead><tr><th>User</th><th>Amount</th><th>Method</th><th>Action</th></tr></thead>
      <tbody></tbody>
    </table>

    <h3>Withdraw Requests</h3>
    <table id="admin-withdraws">
      <thead><tr><th>User</th><th>Amount</th><th>Method</th><th>Action</th></tr></thead>
      <tbody></tbody>
    </table>
  </div>
</div>

<script>
let users = JSON.parse(localStorage.getItem('users')) || {};
let withdrawRequests = JSON.parse(localStorage.getItem('withdrawRequests')) || [];
let depositRequests = JSON.parse(localStorage.getItem('depositRequests')) || [];

// SIGNUP / LOGIN
function signup() {
  let u = document.getElementById('username').value;
  let p = document.getElementById('password').value;
  if(users[u]) { alert('User exists!'); return; }
  users[u] = { password:p, wallet:0 };
  localStorage.setItem('users', JSON.stringify(users));
  alert('Signup successful!');
}

function login() {
  let u = document.getElementById('username').value;
  let p = document.getElementById('password').value;
  if(users[u] && users[u].password===p) {
    document.getElementById('auth').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('user-name').innerText = u;
    updateWallet(u);
    renderUserWithdraws(u);
    renderUserDeposits(u);
  } else { alert('Invalid login'); }
}

// EARNING DEMO
function earnDemo() {
  let u = document.getElementById('user-name').innerText;
  users[u].wallet += 10;
  localStorage.setItem('users', JSON.stringify(users));
  updateWallet(u);
}

// WALLET UPDATE
function updateWallet(u) { document.getElementById('wallet-balance').innerText = users[u].wallet; }

// WITHDRAW REQUEST
function requestWithdraw() {
  let u = document.getElementById('user-name').innerText;
  let amt = parseInt(document.getElementById('withdraw-amount').value);
  let method = document.getElementById('withdraw-method').value;
  if(amt>users[u].wallet) { alert('Insufficient balance'); return; }
  let req = { user:u, amount:amt, method:method, status:'Pending' };
  withdrawRequests.push(req);
  localStorage.setItem('withdrawRequests', JSON.stringify(withdrawRequests));
  alert('Withdraw request submitted!');
  renderUserWithdraws(u);
}

function renderUserWithdraws(u) {
  let tbody = document.querySelector('#user-withdraws tbody');
  tbody.innerHTML = '';
  withdrawRequests.filter(r=>r.user===u).forEach(r=>{
    tbody.innerHTML += `<tr><td>${r.amount}</td><td>${r.method}</td><td>${r.status}</td></tr>`;
  });
}

// DEPOSIT REQUEST
function requestDeposit() {
  let u = document.getElementById('user-name').innerText;
  let amt = parseInt(document.getElementById('deposit-amount').value);
  let method = document.getElementById('deposit-method').value;
  let req = { user:u, amount:amt, method:method, status:'Pending' };
  depositRequests.push(req);
  localStorage.setItem('depositRequests', JSON.stringify(depositRequests));
  alert('Deposit request submitted! Wait for admin approval.');
  renderUserDeposits(u);
}

function renderUserDeposits(u) {
  let tbody = document.querySelector('#user-deposits tbody');
  tbody.innerHTML = '';
  depositRequests.filter(r=>r.user===u).forEach(r=>{
    tbody.innerHTML += `<tr><td>${r.amount}</td><td>${r.method}</td><td>${r.status}</td></tr>`;
  });
}

// ADMIN LOGIN
function loginAdmin() {
  let pass = document.getElementById('admin-pass').value;
  if(pass==='sweetie123') {
    document.getElementById('admin-controls').classList.remove('hidden');
    renderAdminWithdraws();
    renderAdminDeposits();
  } else { alert('Wrong password'); }
}

// ADMIN ACTIONS
function renderAdminWithdraws() {
  let tbody = document.querySelector('#admin-withdraws tbody');
  tbody.innerHTML = '';
  withdrawRequests.forEach((r,i)=>{
    tbody.innerHTML += `<tr>
      <td>${r.user}</td><td>${r.amount}</td><td>${r.method}</td>
      <td>
        <button onclick="markPaid(${i})">Mark Paid</button>
        <button onclick="markRejected(${i})">Reject</button>
      </td>
    </tr>`;
  });
}

function renderAdminDeposits() {
  let tbody = document.querySelector('#admin-deposits tbody');
  tbody.innerHTML = '';
  depositRequests.forEach((r,i)=>{
    tbody.innerHTML += `<tr>
      <td>${r.user}</td><td>${r.amount}</td><td>${r.method}</td>
      <td>
        <button onclick="approveDeposit(${i})">Approve</button>
        <button onclick="rejectDeposit(${i})">Reject</button>
      </td>
    </tr>`;
  });
}

// ADMIN ACTIONS FUNCTIONS
function markPaid(i) { withdrawRequests[i].status='Paid'; users[withdrawRequests[i].user].wallet -= withdrawRequests[i].amount; saveAll(); renderAdminWithdraws(); renderUserWithdraws(withdrawRequests[i].user);}
function markRejected(i) { withdrawRequests[i].status='Rejected'; saveAll(); renderAdminWithdraws(); renderUserWithdraws(withdrawRequests[i].user);}
function approveDeposit(i) { depositRequests[i].status='Approved'; users[depositRequests[i].user].wallet += depositRequests[i].amount; saveAll(); renderAdminDeposits(); renderUserDeposits(depositRequests[i].user);}
function rejectDeposit(i) { depositRequests[i].status='Rejected'; saveAll(); renderAdminDeposits(); renderUserDeposits(depositRequests[i].user);}
function saveAll() { localStorage.setItem('withdrawRequests', JSON.stringify(withdrawRequests)); localStorage.setItem('depositRequests', JSON.stringify(depositRequests)); localStorage.setItem('users', JSON.stringify(users)); }

</script>
</body>
</html>

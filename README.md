<!GVT WWIl> (WORLDWIDE INVESTMENT)
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GVT140 Investment Portal</title>
<style>
/* --- General Reset & Body --- */
body { margin:0; padding:0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background:#f4f6f8; color:#333; }
.container { max-width:1000px; margin:20px auto; padding:20px; }
/* --- Header --- */
header { text-align:center; margin-bottom:30px; }
header h1 { color:#2c3e50; font-size:2.5em; margin-bottom:5px; }
header p { color:#7f8c8d; font-size:1em; }
/* --- Forms --- */
.auth { display:flex; justify-content:center; gap:40px; flex-wrap:wrap; margin-bottom:30px; }
.form-box { background:white; padding:25px; border-radius:15px; box-shadow:0 8px 20px rgba(0,0,0,0.1); width:320px; text-align:center; }
.form-box h2 { margin-bottom:15px; color:#34495e; }
input { width:90%; padding:12px; margin:8px 0; border-radius:8px; border:1px solid #ccc; font-size:1em; }
button { padding:12px 20px; border:none; border-radius:8px; font-size:1em; margin-top:10px; cursor:pointer; transition:0.3s; }
button:hover { opacity:0.9; }
button.primary { background:#27ae60; color:white; }
button.secondary { background:#2980b9; color:white; }
span { color:#3498db; cursor:pointer; }
/* --- Dashboard --- */
#dashboard { display:none; }
#balance { font-size:1.2em; font-weight:bold; margin-bottom:15px; text-align:center; }
/* --- Investment Plans --- */
#plans { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:20px; margin-bottom:30px; }
.plan { background:white; padding:20px; border-radius:15px; text-align:center; box-shadow:0 5px 15px rgba(0,0,0,0.1); transition:0.3s; }
.plan:hover { transform:translateY(-5px); box-shadow:0 10px 20px rgba(0,0,0,0.15); }
.plan h3 { color:#2c3e50; margin-bottom:10px; }
.plan p { color:#7f8c8d; margin-bottom:10px; }
/* --- Deposit/Withdraw --- */
#deposit-withdraw { text-align:center; margin-bottom:30px; }
#deposit-withdraw button { margin:5px; }
/* --- Calculator --- */
#calculator { text-align:center; margin-bottom:30px; }
#calculator input, #calculator select { margin:8px 0; }
/* --- Company Info --- */
#company-info { background:white; padding:25px; border-radius:15px; box-shadow:0 5px 15px rgba(0,0,0,0.1); text-align:center; margin-bottom:50px; }
#company-info h2 { color:#2c3e50; margin-bottom:15px; }
#company-info p { line-height:1.6; color:#7f8c8d; margin-bottom:8px; }
/* --- Responsive --- */
@media(max-width:600px){ .auth { flex-direction:column; } .form-box { width:90%; } }
</style>
</head>
<body>
<div class="container">

<header>
  <h1>GVT140 Investment Portal</h1>
  <p>Invest from PKR 300 to 1 Million | Safe & Professional</p>
</header>

<!-- Login / Signup Forms -->
<div class="auth" id="auth-section">
  <div class="form-box" id="login-box">
    <h2>Login</h2>
    <input type="text" id="login-username" placeholder="Username">
    <input type="password" id="login-password" placeholder="Password">
    <button class="primary" onclick="login()">Login</button>
    <p>Don't have an account? <span onclick="toggleForm()">Signup</span></p>
  </div>

  <div class="form-box" id="signup-box" style="display:none;">
    <h2>Signup</h2>
    <input type="text" id="signup-username" placeholder="Username">
    <input type="password" id="signup-password" placeholder="Password">
    <button class="primary" onclick="signup()">Signup</button>
    <p>Already have an account? <span onclick="toggleForm()">Login</span></p>
  </div>
</div>

<!-- Dashboard -->
<div id="dashboard">
<p id="balance">Balance: PKR 0</p>

<!-- Investment Plans -->
<section id="plans">
  <div class="plan">
    <h3>Starter</h3>
    <p>300 - 10,000 PKR | Low Risk</p>
    <button class="secondary" onclick="invest('Starter')">Invest Now</button>
  </div>
  <div class="plan">
    <h3>Silver</h3>
    <p>10,001 - 50,000 PKR | Moderate Risk</p>
    <button class="secondary" onclick="invest('Silver')">Invest Now</button>
  </div>
  <div class="plan">
    <h3>Gold</h3>
    <p>50,001 - 250,000 PKR | Medium-High Risk</p>
    <button class="secondary" onclick="invest('Gold')">Invest Now</button>
  </div>
  <div class="plan">
    <h3>Platinum</h3>
    <p>250,001 - 1,000,000 PKR | High Risk</p>
    <button class="secondary" onclick="invest('Platinum')">Invest Now</button>
  </div>
</section>

<!-- Deposit / Withdraw -->
<section id="deposit-withdraw">
  <h2>Deposit / Withdraw</h2>
  <input type="number" id="amount" placeholder="Enter amount PKR">
  <br>
  <button class="primary" onclick="deposit('JazzCash')">Deposit via JazzCash</button>
  <button class="primary" onclick="deposit('EasyPaisa')">Deposit via Easypaisa</button>
  <br>
  <button class="secondary" onclick="withdraw('JazzCash')">Withdraw to JazzCash</button>
  <button class="secondary" onclick="withdraw('EasyPaisa')">Withdraw to Easypaisa</button>
  <br><button onclick="logout()">Logout</button>
</section>

<!-- Calculator -->
<section id="calculator">
<h2>Investment Calculator</h2>
<input type="number" id="calc-amount" placeholder="Enter amount PKR">
<select id="plan-calc">
<option value="Starter">Starter</option>
<option value="Silver">Silver</option>
<option value="Gold">Gold</option>
<option value="Platinum">Platinum</option>
</select>
<button class="primary" onclick="calculate()">Calculate</button>
<p id="result"></p>
</section>

<!-- Company Info -->
<section id="company-info">
<h2>About GVT140 Investment</h2>
<p><strong>Founder & CEO:</strong> Muhammad Nazim</p>
<p><strong>Founded:</strong> 2020</p>
<p><strong>About Us:</strong> GVT140 Investment is a professional investment company dedicated to helping clients grow their wealth safely and efficiently. We provide personalized investment plans from PKR 300 to 1 Million with transparent returns and excellent customer support. Our mission is to empower investors in Pakistan with reliable and secure investment solutions.</p>
<p><strong>Contact / Support:</strong> support@gvt140.com | +92 300 1234567</p>
</section>
</div>
</div>

<script>
// --- Form Toggle ---
function toggleForm(){
  const loginBox = document.getElementById('login-box');
  const signupBox = document.getElementById('signup-box');
  loginBox.style.display = loginBox.style.display==='none'?'block':'none';
  signupBox.style.display = signupBox.style.display==='none'?'block':'none';
}

// --- Signup ---
function signup(){
  let username = document.getElementById('signup-username').value;
  let password = document.getElementById('signup-password').value;
  if(!username || !password){ alert("Enter valid details"); return; }
  localStorage.setItem(username,password);
  localStorage.setItem(username+"_balance",0);
  alert("Signup successful! Login now.");
  toggleForm();
}

// --- Login ---
function login(){
  let username = document.getElementById('login-username').value;
  let password = document.getElementById('login-password').value;
  let stored = localStorage.getItem(username);
  if(stored && stored===password){
    localStorage.setItem("currentUser",username);
    showDashboard();
  } else { alert("Invalid credentials!"); }
}

// --- Logout ---
function logout(){
  localStorage.removeItem("currentUser");
  document.getElementById("dashboard").style.display="none";
  document.getElementById("auth-section").style.display="flex";
}

// --- Show Dashboard & Update Balance ---
function showDashboard(){
  let user = localStorage.getItem("currentUser");
  if(!user){ alert("Please login"); return; }
  document.getElementById("user-name").innerText = user;
  document.getElementById("auth-section").style.display="none";
  document.getElementById("dashboard").style.display="block";
  updateBalance();
}

function updateBalance(){
  let user = localStorage.getItem("currentUser");
  let balance = Number(localStorage.getItem(user+"_balance")) || 0;
  document.getElementById("balance").innerText = `Balance: PKR ${balance}`;
}

// --- Deposit / Withdraw ---
function deposit(method){
  let user = localStorage.getItem("currentUser");
  if(!user){ alert("Login first!"); return; }
  let amount = Number(document.getElementById("amount").value);
  if(amount<=0){ alert("Enter valid amount"); return; }
  alert(`Deposit PKR ${amount} via ${method}. Follow instructions in new window.`);
  let url = method==="JazzCash"?"https://www.jazzcash.com.pk/":"https://www.easypaisa.com.pk/";
  window.open(url,"_blank");
  let balance = Number(localStorage.getItem(user+"_balance")) || 0;
  balance += amount;
  localStorage.setItem(user+"_balance",balance);
  updateBalance();
}

function withdraw(method){
  let user = localStorage.getItem("currentUser");
  if(!user){ alert("Login first!"); return; }
  let amount = Number(document.getElementById("amount").value);
  let balance = Number(localStorage.getItem(user+"_balance")) || 0;
  if(amount<=0 || amount>balance){ alert("Invalid withdrawal amount"); return; }
  alert(`Withdraw PKR ${amount} to ${method}. Follow instructions in new window.`);
  let url = method==="JazzCash"?"https://www.jazzcash.com.pk/":"https://www.easypaisa.com.pk/";
  window.open(url,"_blank");
  balance -= amount;
  localStorage.setItem(user+"_balance",balance);
  updateBalance();
}

// --- Investment ---
function invest(plan){
  let user = localStorage.getItem("currentUser");
  if(!user){ alert("Please login to invest!"); return; }
  alert(`Redirecting to payment for ${plan} plan`);
  window.open("https://www.jazzcash.com.pk/","_blank");
}

// --- Calculator ---
function calculate(){
  let amount = Number(document.getElementById('calc-amount').value);
  let plan = document.getElementById('plan-calc').value;
  let percent=0;
  switch(plan){case 'Starter':percent=5;break;case 'Silver':percent=12;break;case 'Gold':percent=20;break;case 'Platinum':percent=35;break;}
  let profit = (amount*percent)/100;
  document.getElementById('result').innerText = `Expected monthly return: PKR ${profit}`;
}

// --- Auto show dashboard if logged in ---
if(localStorage.getItem("currentUser")){ showDashboard(); }
</script>
</body>
</html>

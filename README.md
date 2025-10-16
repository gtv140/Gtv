<!GVT>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GVT140 Investment</title>
<style>
body { font-family: Arial, sans-serif; margin:0; padding:0; background:#f0f2f5; }
.container { max-width:900px; margin:50px auto; padding:20px; background:white; border-radius:10px; box-shadow:0 5px 20px rgba(0,0,0,0.1); }
header { text-align:center; margin-bottom:30px; }
h1 { color:#333; }
input, select, button { padding:10px; margin:5px; width:90%; border-radius:5px; border:1px solid #ccc; }
button { cursor:pointer; background:#4CAF50; color:white; border:none; }
button:hover { background:#45a049; }
#plans { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:20px; margin-top:20px; }
.plan { background:#eaf2f8; padding:20px; border-radius:10px; text-align:center; box-shadow:0 2px 10px rgba(0,0,0,0.1); }
.plan button { width:80%; margin-top:10px; }
.auth { display:flex; justify-content:center; gap:50px; flex-wrap:wrap; }
.form-box { width:300px; padding:20px; background:white; border-radius:10px; box-shadow:0 5px 15px rgba(0,0,0,0.1); text-align:center; }
span { color:#007BFF; cursor:pointer; }
#company-info { background:#f9f9f9; padding:20px; margin-top:40px; border-radius:10px; box-shadow:0 2px 8px rgba(0,0,0,0.05); }
#company-info h2 { text-align:center; margin-bottom:20px; }
#company-info p { line-height:1.6; color:#555; text-align:center; }
#calculator { margin-top:30px; text-align:center; }
</style>
</head>
<body>
<div class="container">
<header>
  <h1>GVT140 Investment</h1>
  <p>PKR 300 to 1 Million Investment Plans</p>
</header>

<div class="auth" id="auth-section">
  <div class="form-box" id="login-box">
    <h2>Login</h2>
    <input type="text" id="login-username" placeholder="Username">
    <input type="password" id="login-password" placeholder="Password">
    <button onclick="login()">Login</button>
    <p>Don't have an account? <span onclick="toggleForm()">Signup</span></p>
  </div>

  <div class="form-box" id="signup-box" style="display:none;">
    <h2>Signup</h2>
    <input type="text" id="signup-username" placeholder="Username">
    <input type="password" id="signup-password" placeholder="Password">
    <button onclick="signup()">Signup</button>
    <p>Already have an account? <span onclick="toggleForm()">Login</span></p>
  </div>
</div>

<div id="dashboard" style="display:none;">
<header>
  <h1>Welcome, <span id="user-name"></span></h1>
  <button onclick="logout()">Logout</button>
</header>

<section id="plans">
  <h2>Investment Plans</h2>
  <div class="plan">
    <h3>Starter: 300 - 10,000 PKR</h3>
    <p>Low risk, safe growth</p>
    <button onclick="invest('Starter')">Invest Now</button>
  </div>
  <div class="plan">
    <h3>Silver: 10,001 - 50,000 PKR</h3>
    <p>Moderate risk, 8-12% monthly</p>
    <button onclick="invest('Silver')">Invest Now</button>
  </div>
  <div class="plan">
    <h3>Gold: 50,001 - 250,000 PKR</h3>
    <p>Medium-high risk, 12-20% monthly</p>
    <button onclick="invest('Gold')">Invest Now</button>
  </div>
  <div class="plan">
    <h3>Platinum: 250,001 - 1,000,000 PKR</h3>
    <p>High risk, 20-35% monthly</p>
    <button onclick="invest('Platinum')">Invest Now</button>
  </div>
</section>

<section id="calculator">
  <h2>Investment Calculator</h2>
  <input type="number" id="amount" placeholder="Enter amount in PKR">
  <select id="plan">
    <option value="Starter">Starter</option>
    <option value="Silver">Silver</option>
    <option value="Gold">Gold</option>
    <option value="Platinum">Platinum</option>
  </select>
  <button onclick="calculate()">Calculate</button>
  <p id="result"></p>
</section>

<section id="company-info">
<h2>About GVT140 Investment</h2>
<p><strong>Owner:</strong> Muhammad Nazim</p>
<p><strong>Founded:</strong> 2020</p>
<p><strong>About Us:</strong> GVT140 Investment is a professional investment company dedicated to helping clients grow their wealth safely and efficiently. We provide personalized investment plans from PKR 300 to 1 Million with transparent returns and excellent customer support. Our mission is to empower investors in Pakistan with reliable and secure investment solutions.</p>
<p><strong>Contact / Support:</strong> support@gvt140.com | +92 300 1234567</p>
</section>
</div>
</div>

<script>
function toggleForm() {
  const loginBox = document.getElementById('login-box');
  const signupBox = document.getElementById('signup-box');
  loginBox.style.display = loginBox.style.display === 'none' ? 'block' : 'none';
  signupBox.style.display = signupBox.style.display === 'none' ? 'block' : 'none';
}

function signup() {
  let username = document.getElementById('signup-username').value;
  let password = document.getElementById('signup-password').value;
  if(!username || !password){ alert("Enter details"); return; }
  localStorage.setItem(username,password);
  alert("Signup successful! Login now.");
  toggleForm();
}

function login() {
  let username = document.getElementById('login-username').value;
  let password = document.getElementById('login-password').value;
  let stored = localStorage.getItem(username);
  if(stored && stored === password){
    localStorage.setItem("currentUser", username);
    showDashboard();
  } else {
    alert("Invalid credentials!");
  }
}

function logout() {
  localStorage.removeItem("currentUser");
  document.getElementById("dashboard").style.display = "none";
  document.getElementById("auth-section").style.display = "flex";
}

function showDashboard() {
  let user = localStorage.getItem("currentUser");
  if(!user){ alert("Please login"); return; }
  document.getElementById("user-name").innerText = user;
  document.getElementById("auth-section").style.display = "none";
  document.getElementById("dashboard").style.display = "block";
}

if(localStorage.getItem("currentUser")){
  showDashboard();
}

function calculate() {
  let amount = Number(document.getElementById('amount').value);
  let plan = document.getElementById('plan').value;
  let percent = 0;
  switch(plan) {
    case 'Starter': percent = 5; break;
    case 'Silver': percent = 12; break;
    case 'Gold': percent = 20; break;
    case 'Platinum': percent = 35; break;
  }
  let profit = (amount * percent) / 100;
  document.getElementById('result').innerText = `Expected monthly return: PKR ${profit}`;
}

function invest(plan){
  let user = localStorage.getItem("currentUser");
  if(!user){ alert("Please login to invest!"); return; }
  let url = "https://www.jazzcash.com.pk/"; // Replace with real payment link
  alert(`Redirecting to payment for ${plan} plan`);
  window.open(url, "_blank");
}
</script>
</body>
</html>

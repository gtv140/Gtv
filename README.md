<GVT>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GVT140 Investment Portal</title>
<style>
body { margin:0; padding:0; font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background:#f4f6f8; color:#333; }
.container { max-width:1000px; margin:20px auto; padding:20px; }
header { text-align:center; margin-bottom:30px; }
header h1 { color:#2c3e50; font-size:2.5em; margin-bottom:5px; }
header p { color:#7f8c8d; font-size:1em; }
#dashboard { display:block; }
#balance { font-size:1.2em; font-weight:bold; margin-bottom:15px; text-align:center; }
#plans { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:20px; margin-bottom:30px; }
.plan { background:white; padding:20px; border-radius:15px; text-align:center; box-shadow:0 5px 15px rgba(0,0,0,0.1); transition:0.3s; }
.plan:hover { transform:translateY(-5px); box-shadow:0 10px 20px rgba(0,0,0,0.15); }
.plan h3 { color:#2c3e50; margin-bottom:10px; }
.plan p { color:#7f8c8d; margin-bottom:10px; }
#deposit-withdraw { text-align:center; margin-bottom:30px; }
#deposit-withdraw button { margin:5px; }
#calculator { text-align:center; margin-bottom:30px; }
#calculator input, #calculator select { margin:8px 0; }
#company-info { background:white; padding:25px; border-radius:15px; box-shadow:0 5px 15px rgba(0,0,0,0.1); text-align:center; margin-bottom:50px; }
#company-info h2 { color:#2c3e50; margin-bottom:15px; }
#company-info p { line-height:1.6; color:#7f8c8d; margin-bottom:8px; }
button { padding:12px 20px; border:none; border-radius:8px; font-size:1em; margin-top:10px; cursor:pointer; transition:0.3s; }
button:hover { opacity:0.9; }
button.primary { background:#27ae60; color:white; }
button.secondary { background:#2980b9; color:white; }
@media(max-width:600px){ #plans { grid-template-columns:1fr; } }
</style>
</head>
<body>
<div class="container">

<header>
<h1>GVT140 Investment Portal</h1>
<p>Invest from PKR 300 to 1 Million | Safe & Professional</p>
</header>

<div id="dashboard">
<p id="balance">Balance: PKR 0</p>

<section id="plans">
<div class="plan"><h3>Starter</h3><p>300 - 10,000 PKR | Low Risk</p><button class="secondary" onclick="invest('Starter')">Invest Now</button></div>
<div class="plan"><h3>Silver</h3><p>10,001 - 50,000 PKR | Moderate Risk</p><button class="secondary" onclick="invest('Silver')">Invest Now</button></div>
<div class="plan"><h3>Gold</h3><p>50,001 - 250,000 PKR | Medium-High Risk</p><button class="secondary" onclick="invest('Gold')">Invest Now</button></div>
<div class="plan"><h3>Platinum</h3><p>250,001 - 1,000,000 PKR | High Risk</p><button class="secondary" onclick="invest('Platinum')">Invest Now</button></div>
</section>

<section id="deposit-withdraw">
<h2>Deposit / Withdraw</h2>
<input type="number" id="amount" placeholder="Enter amount PKR"><br>
<button class="primary" onclick="deposit('JazzCash')">Deposit via JazzCash</button>
<button class="primary" onclick="deposit('EasyPaisa')">Deposit via Easypaisa</button><br>
<button class="secondary" onclick="withdraw('JazzCash')">Withdraw to JazzCash</button>
<button class="secondary" onclick="withdraw('EasyPaisa')">Withdraw to Easypaisa</button>
</section>

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

<section id="company-info">
<h2>About GVT140 Investment</h2>
<p><strong>Founder & CEO:</strong> Muhammad Nazim</p>
<p><strong>Founded:</strong> 2020</p>
<p><strong>About Us:</strong> Professional investment company providing safe plans from PKR 300 to 1 Million. Transparent, secure & efficient.</p>
<p><strong>Contact:</strong> support@gvt140.com | +92 300 1234567</p>
</section>
</div>
</div>

<script>
// Automatic "user"
let user = "defaultUser";
if(!localStorage.getItem(user+"_balance")){ localStorage.setItem(user+"_balance",0); }

function updateBalance(){
  let balance = Number(localStorage.getItem(user+"_balance"));
  document.getElementById("balance").innerText = `Balance: PKR ${balance}`;
}

function deposit(method){
  let amount = Number(document.getElementById("amount").value);
  if(amount<=0){ alert("Enter valid amount"); return; }
  let balance = Number(localStorage.getItem(user+"_balance"));
  balance += amount;
  localStorage.setItem(user+"_balance",balance);
  updateBalance();
  alert(`Deposit PKR ${amount} via ${method} successful.`);
}

function withdraw(method){
  let amount = Number(document.getElementById("amount").value);
  let balance = Number(localStorage.getItem(user+"_balance"));
  if(amount<=0 || amount>balance){ alert("Invalid withdrawal amount"); return; }
  balance -= amount;
  localStorage.setItem(user+"_balance",balance);
  updateBalance();
  alert(`Withdraw PKR ${amount} to ${method} successful.`);
}

function invest(plan){
  alert(`Redirecting to payment for ${plan} plan`);
  window.open("https://www.jazzcash.com.pk/","_blank");
}

function calculate(){
  let amount = Number(document.getElementById('calc-amount').value);
  let plan = document.getElementById('plan-calc').value;
  let percent=0;
  switch(plan){case 'Starter':percent=5;break;case 'Silver':percent=12;break;case 'Gold':percent=20;break;case 'Platinum':percent=35;break;}
  let profit = (amount*percent)/100;
  document.getElementById('result').innerText = `Expected monthly return: PKR ${profit}`;
}

// Initialize balance
updateBalance();
</script>
</body>
</html>

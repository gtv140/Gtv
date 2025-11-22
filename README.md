<NEONS><html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>NeonEarn — Full Premium Earning Platform</title>
<style>
    body { margin:0; font-family:Arial, sans-serif; background:#020202; color:#fff; }
    .header { padding:20px; text-align:center; background:linear-gradient(90deg,#00f0ff,#0077ff,#9d00ff); font-size:28px; font-weight:bold; text-shadow:0 0 15px #00eaff; }
    .container { padding:20px; }
    .card { background:rgba(255,255,255,0.05); border:1px solid rgba(0,255,255,0.3); padding:20px; border-radius:15px; margin-bottom:20px; backdrop-filter:blur(10px); box-shadow:0 0 20px #00eaff40; }
    .btn { display:block; width:100%; padding:15px; text-align:center; background:linear-gradient(90deg,#00f0ff,#0077ff); color:#000; font-weight:bold; text-decoration:none; border-radius:10px; box-shadow:0 0 20px #00f0ff80; margin-top:10px; cursor:pointer; }
    input, select { width:100%; padding:10px; margin-top:10px; border-radius:8px; border:none; background:rgba(255,255,255,0.1); color:#fff; }
    label { margin-top:10px; display:block; }
    .timer { font-size:24px; text-align:center; margin:20px 0; color:#00f0ff; text-shadow:0 0 10px #00eaff; }
    .balance { font-size:24px; text-align:center; margin:10px 0; color:#0f0; text-shadow:0 0 10px #00eaff; }
    table { width:100%; border-collapse:collapse; margin-top:10px; }
    table, th, td { border:1px solid #00f0ff; }
    th, td { padding:10px; text-align:center; }
    a { color:#00f0ff; text-decoration:none; }
</style>
</head>
<body>
<div class="header">NeonEarn — Full Premium Earning Platform</div>
<div class="container"><!-- Deposit Section --><div class="card">
<h2>Deposit Funds</h2>
<form>
<label for="method">Select Payment Method:</label>
<select id="method" onchange="updateAccount()">
<option value="jazzcash">JazzCash</option>
<option value="easypaisa">Easypaisa</option>
<option value="payoneer">Payoneer</option>
</select>
<label for="amount">Amount:</label>
<input type="number" id="amount" placeholder="Enter deposit amount">
<label for="txn">Transaction ID / Number:</label>
<input type="text" id="txn" placeholder="Enter transaction ID">
<label for="proof">Upload Proof:</label>
<input type="file" id="proof">
<label>Account Number / Copy:</label>
<input type="text" id="account" value="03705519562" readonly>
<button type="button" class="btn" onclick="copyAccount()">Copy Account Number</button>
<button type="submit" class="btn">Submit Deposit</button>
</form>
</div><!-- Watch Ads Section --><div class="card">
<h2>Watch Ads & Earn</h2>
<p>Click the ad below and wait for the timer to complete to earn coins.</p>
<button class="btn" onclick="startAd()">Start Ad</button>
<div class="timer" id="timer">10</div>
<p id="earned" style="text-align:center;color:#0f0;font-weight:bold;"></p>
</div><!-- User Dashboard --><div class="card">
<h2>User Dashboard</h2>
<div class="balance">Balance: <span id="balance">0</span> coins</div>
<button class="btn" onclick="watchAdForUser()">Watch Ads</button>
<a href="#" class="btn" onclick="alert('Redirecting to Deposit page')">Deposit Funds</a>
<a href="#" class="btn" onclick="alert('Redirecting to Withdraw page')">Withdraw Funds</a>
<a href="#" class="btn" onclick="logoutUser()">Logout</a>
</div><!-- Admin Panel --><div class="card">
<h2>Admin Panel</h2>
<button class="btn" onclick="alert('Manage Users')">Manage Users</button>
<button class="btn" onclick="alert('Manage Deposits')">Manage Deposits</button>
<button class="btn" onclick="alert('Add/Edit Ads')">Manage Ads</button>
<button class="btn" onclick="alert('Referral System')">Referral System</button>
</div></div>
<script>
// Deposit Account Copy
function copyAccount(){
var copyText = document.getElementById('account');
copyText.select();
copyText.setSelectionRange(0, 99999);
navigator.clipboard.writeText(copyText.value);
alert('Account number copied!');
}
function updateAccount(){
var method = document.getElementById('method').value;
var accountInput = document.getElementById('account');
if(method==='jazzcash') accountInput.value='03705519562';
else if(method==='easypaisa') accountInput.value='03379827882';
else if(method==='payoneer') accountInput.value='nazimkhan01123@gmail.com';
}// Watch Ads Timer let timerInterval; function startAd(){ let timeLeft = 10; document.getElementById('earned').innerText=''; clearInterval(timerInterval); document.getElementById('timer').innerText=timeLeft; timerInterval=setInterval(()=>{ timeLeft--; document.getElementById('timer').innerText=timeLeft; if(timeLeft<=0){ clearInterval(timerInterval); document.getElementById('earned').innerText='Congratulations! You earned 5 coins.'; } },1000); }

// User Dashboard Functions let userBalance=0; function watchAdForUser(){ let earned=5; userBalance+=earned; document.getElementById('balance').innerText=userBalance; alert('You earned '+earned+' coins!'); } function logoutUser(){ alert('Logging out...'); location.reload(); } </script>

</body>
</html>

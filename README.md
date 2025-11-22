<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NeonEarn - Ads Simulation</title>
<style>
    body { margin:0; font-family: Arial, sans-serif; background:#020202; color:#fff; }
    .header { padding:20px; text-align:center; background:linear-gradient(90deg,#00f0ff,#0077ff,#9d00ff); font-size:28px; font-weight:bold; text-shadow:0 0 15px #00eaff; }
    .container { padding:20px; max-width:600px; margin:auto; }
    .card { background: rgba(255,255,255,0.05); border:1px solid rgba(0,255,255,0.3); padding:20px; border-radius:15px; margin-bottom:20px; backdrop-filter:blur(10px); box-shadow:0 0 20px #00eaff40; }
    .btn { display:block; width:100%; padding:15px; text-align:center; background:linear-gradient(90deg,#00f0ff,#0077ff); color:#000; font-weight:bold; text-decoration:none; border-radius:10px; box-shadow:0 0 20px #00f0ff80; margin-top:10px; cursor:pointer; }
    input { width:100%; padding:10px; margin-top:10px; border-radius:8px; border:none; background:rgba(255,255,255,0.1); color:#fff; }
    .balance { font-size:24px; text-align:center; margin:10px 0; color:#0f0; text-shadow:0 0 10px #00eaff; }
    .timer { font-size:24px; text-align:center; margin:20px 0; color:#00f0ff; text-shadow:0 0 10px #00eaff; }
    .ad-img { width:100%; border-radius:10px; cursor:pointer; }
</style>
</head>
<body>
<div class="header">NeonEarn - Ads Simulation</div>
<div class="container">

<div class="card">
<h2>User Dashboard</h2>
<div class="balance">Balance: <span id="balance">0</span> coins</div>
<label>Deposit Amount:</label>
<input type="number" id="depositAmount" placeholder="Enter amount">
<button class="btn" onclick="deposit()">Deposit</button>
<label>Withdraw Amount:</label>
<input type="number" id="withdrawAmount" placeholder="Enter amount">
<button class="btn" onclick="withdraw()">Withdraw</button>
</div>

<div class="card">
<h2>Watch Ads</h2>
<p>Click on the ad and wait for timer to complete to earn coins.</p>
<img src="https://via.placeholder.com/500x200?text=Ad+1" id="adImage" class="ad-img" onclick="startAd()">
<div class="timer" id="timer">10</div>
<p id="earned" style="text-align:center;color:#0f0;font-weight:bold;"></p>
</div>

<div class="card">
<h2>Admin Panel (Simulation)</h2>
<p>Dummy users:</p>
<ul id="adminUsers">
<li>John - 50 coins</li>
<li>Jane - 30 coins</li>
</ul>
<button class="btn" onclick="resetBalance()">Reset All Balances</button>
</div>

</div>
<script>
let balance = 0;
let ads = [
    'https://via.placeholder.com/500x200?text=Ad+1',
    'https://via.placeholder.com/500x200?text=Ad+2',
    'https://via.placeholder.com/500x200?text=Ad+3'
];
let currentAd = 0;

function deposit(){
    let amount = parseFloat(document.getElementById('depositAmount').value);
    if(amount>0){ balance += amount; alert('Deposit successful! '+amount+' coins added.'); document.getElementById('balance').innerText = balance; }
    else { alert('Enter valid amount'); }
}

function withdraw(){
    let amount = parseFloat(document.getElementById('withdrawAmount').value);
    if(amount>0 && amount<=balance){ balance -= amount; alert('Withdrawal successful! '+amount+' coins deducted.'); document.getElementById('balance').innerText = balance; }
    else { alert('Invalid amount'); }
}

function startAd(){
    let time = 10;
    document.getElementById('earned').innerText='';
    let timerInterval = setInterval(()=>{
        document.getElementById('timer').innerText=time;
        time--;
        if(time<0){ 
            clearInterval(timerInterval); 
            let earnedCoins = 5;
            balance += earnedCoins;
            document.getElementById('balance').innerText=balance;
            document.getElementById('earned').innerText='You earned '+earnedCoins+' coins!';
            currentAd = (currentAd+1)%ads.length;
            document.getElementById('adImage').src = ads[currentAd];
            document.getElementById('timer').innerText='10';
        }
    },1000);
}

function resetBalance(){ balance=0; document.getElementById('balance').innerText=balance; alert('All balances reset!'); }
</script>
</body>
</html>

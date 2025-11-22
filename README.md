<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Neon Earn Ads</title>
<style>
body{margin:0;font-family:Arial;background:#000;color:#0ff;}
h1{text-align:center;font-size:2em;margin:20px;text-shadow:0 0 20px #0ff,0 0 40px #0ff;}
.box{background:#111;margin:20px;padding:20px;border-radius:12px;border:1px solid #0ff;box-shadow:0 0 20px #0ff;transition:0.5s;}
input,select,button{width:100%;padding:12px;margin:8px 0;border-radius:10px;border:none;font-size:16px;}
button,.btn{background:#0ff;color:#000;font-weight:bold;cursor:pointer;transition:0.3s;}
button:hover,.btn:hover{box-shadow:0 0 20px #0ff,0 0 40px #0ff;text-shadow:0 0 10px #000;}
.ads-box{background:#222;padding:12px;margin-bottom:12px;border-radius:12px;border:1px dashed #0ff;cursor:pointer;transition:0.3s;animation: glow 2s infinite;}
.ads-box:hover{box-shadow:0 0 30px #0ff,0 0 60px #0ff;}
a{color:#0ff;text-decoration:none;}
@keyframes glow{0%{box-shadow:0 0 5px #0ff;}50%{box-shadow:0 0 20px #0ff;}100%{box-shadow:0 0 5px #0ff;}}
@media(max-width:600px){.box{margin:10px;padding:15px;}input,select,button{font-size:14px;padding:10px;}}
.popup{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:#111;padding:20px;border:2px solid #0ff;border-radius:12px;display:none;z-index:999;text-align:center;animation: glow 1s infinite;}
</style>
</head>
<body>

<div id="popup" class="popup">🎉 Referral Bonus +5 Coins! 🎉</div>

<h1>✨ Neon Earn Ads Demo ✨</h1>

<div class="box" id="dashboard">
<p><b>User:</b> <span id="username">Guest</span></p>
<p><b>Balance:</b> <span id="balance">0</span> coins</p>
<p><b>Referral Code:</b> <span id="referral">0000</span></p>

<button class="btn" onclick="showSection('ads')">Watch Ads</button>
<button class="btn" onclick="showSection('deposit')">Deposit</button>
<button class="btn" onclick="showSection('withdraw')">Withdraw</button>
</div>

<h2 id="ads" style="text-align:center; display:none;">Watch Ads & Earn</h2>
<div class="box" id="adsBox" style="display:none;"></div>

<h2 id="deposit" style="text-align:center; display:none;">Deposit</h2>
<div class="box" id="depositBox" style="display:none;">
<select id="depositMethod">
<option>JazzCash</option>
<option>EasyPaisa</option>
<option>Payoneer</option>
</select>
<input id="depositAmount" type="number" placeholder="Amount">
<input id="depositTrx" placeholder="Transaction ID">
<button onclick="submitDeposit()">Submit Deposit</button>
</div>

<h2 id="withdraw" style="text-align:center; display:none;">Withdraw</h2>
<div class="box" id="withdrawBox" style="display:none;">
<select id="withdrawMethod">
<option>JazzCash</option>
<option>EasyPaisa</option>
<option>Bank</option>
</select>
<input id="withdrawAmount" type="number" placeholder="Amount">
<input id="withdrawAcc" placeholder="Account / Name">
<button onclick="submitWithdraw()">Submit Withdraw</button>
</div>

<script>
let balance = 0;
let referral = Math.floor(Math.random()*9000)+1000;
document.getElementById('referral').innerText = referral;
document.getElementById('username').innerText = 'Guest';

let ads = [
  {id:1, title:'Ad #1', img:'https://via.placeholder.com/300x150', coins:5},
  {id:2, title:'Ad #2', img:'https://via.placeholder.com/300x150', coins:10},
  {id:3, title:'Ad #3', img:'https://via.placeholder.com/300x150', coins:15}
];

function showSection(sec){
  document.getElementById('ads').style.display='none';
  document.getElementById('adsBox').style.display='none';
  document.getElementById('deposit').style.display='none';
  document.getElementById('depositBox').style.display='none';
  document.getElementById('withdraw').style.display='none';
  document.getElementById('withdrawBox').style.display='none';
  
  if(sec==='ads'){document.getElementById('ads').style.display='block'; document.getElementById('adsBox').style.display='block'; renderAds();}
  if(sec==='deposit'){document.getElementById('deposit').style.display='block'; document.getElementById('depositBox').style.display='block';}
  if(sec==='withdraw'){document.getElementById('withdraw').style.display='block'; document.getElementById('withdrawBox').style.display='block';}
}

function renderAds(){
  let box=document.getElementById('adsBox');
  box.innerHTML='';
  ads.forEach(ad=>{
    let div=document.createElement('div');
    div.className='ads-box';
    div.innerHTML=`<p><b>${ad.title}</b></p><img src="${ad.img}" width="100%"><p>Coins: ${ad.coins}</p>`;
    div.onclick=()=>{balance+=ad.coins; document.getElementById('balance').innerText=balance; showReferralPopup();};
    box.appendChild(div);
  });
}

function showReferralPopup(){
  let p=document.getElementById('popup');
  p.style.display='block';
  setTimeout(()=>{p.style.display='none';},3000);
}

function submitDeposit(){
  let amt = document.getElementById('depositAmount').value;
  let method = document.getElementById('depositMethod').value;
  let trx = document.getElementById('depositTrx').value;
  alert(`Deposit request for ${amt} via ${method} submitted! Trx ID: ${trx}`);
}

function submitWithdraw(){
  let amt = document.getElementById('withdrawAmount').value;
  let method = document.getElementById('withdrawMethod').value;
  let acc = document.getElementById('withdrawAcc').value;
  if(amt>balance){alert('Insufficient balance!'); return;}
  balance-=amt;
  document.getElementById('balance').innerText=balance;
  alert(`Withdraw request for ${amt} via ${method} submitted! Account: ${acc}`);
}
</script>

</body>
</html>

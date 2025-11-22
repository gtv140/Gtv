<!DOCTYPE html>
<html>
<head>
<title>NeonEarn — Premium Earning</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body{
    background:#000;
    font-family:Arial;
    color:#fff;
    margin:0;
}
header{
    background:#1f0033;
    padding:20px;
    text-align:center;
    font-size:28px;
    font-weight:bold;
    color:#0ff;
    text-shadow:0 0 10px #0ff;
}
nav{
    display:flex;
    justify-content:space-around;
    background:#110022;
    padding:10px;
}
nav a{
    color:#0ff;
    text-decoration:none;
    font-weight:bold;
    padding:10px 15px;
    border:1px solid #0ff;
    border-radius:8px;
    box-shadow:0 0 10px #0ff;
}
section{
    padding:20px;
}
.card{
    background:#120024;
    padding:20px;
    margin-bottom:20px;
    border-radius:10px;
    border:1px solid #0ff;
    box-shadow:0 0 15px #0ff;
}
input, select{
    width:100%;
    padding:12px;
    margin-top:10px;
    border-radius:8px;
    border:1px solid #0ff;
    background:#000;
    color:#0ff;
}
button{
    width:100%;
    background:#0ff;
    color:#000;
    padding:12px;
    margin-top:10px;
    border-radius:8px;
    font-size:16px;
    font-weight:bold;
}
.ad-box{
    background:#0a0014;
    padding:15px;
    border:1px solid #0ff;
    border-radius:8px;
    margin-bottom:15px;
}
</style>
</head>
<body>

<header>💎 NeonEarn — Premium Neon Earning 💎</header>

<nav>
  <a href="#dash">Dashboard</a>
  <a href="#ads">Ads</a>
  <a href="#deposit">Deposit</a>
  <a href="#withdraw">Withdraw</a>
</nav>

<section id="dash">
  <div class="card">
    <h2>👤 User Dashboard</h2>
    <p><b>Balance:</b> 0 PKR</p>
    <p><b>Referral Code:</b> NEON123</p>
  </div>
</section>

<section id="ads">
  <div class="card">
    <h2>📺 Watch Ads & Earn</h2>

    <div class="ad-box">Ad #1 — Click & Wait 10 Seconds</div>
    <div class="ad-box">Ad #2 — Click & Wait 10 Seconds</div>
    <div class="ad-box">Ad #3 — Click & Wait 10 Seconds</div>
    <div class="ad-box">Ad #4 — Click & Wait 10 Seconds</div>

  </div>
</section>

<section id="deposit">
  <div class="card">
    <h2>💰 Deposit</h2>
    <p>JazzCash: <b>03705519562</b></p>
    <p>EasyPaisa: <b>03379827882</b></p>
    <p>Payoneer: <b>nazimkhan01123@gmail.com</b></p>

    <select>
      <option>Select Method</option>
      <option>JazzCash</option>
      <option>EasyPaisa</option>
      <option>Payoneer</option>
    </select>

    <input type="number" placeholder="Amount">
    <input type="text" placeholder="Transaction ID">
    <button>Upload Proof</button>
  </div>
</section>

<section id="withdraw">
  <div class="card">
    <h2>💸 Withdraw</h2>

    <select>
      <option>Select Withdraw Method</option>
      <option>JazzCash</option>
      <option>EasyPaisa</option>
      <option>Bank</option>
    </select>

    <input type="number" placeholder="Amount">
    <input type="text" placeholder="Account Number">
    <input type="text" placeholder="Full Name">
    <button>Request Withdraw</button>
  </div>
</section>

</body>
</html>

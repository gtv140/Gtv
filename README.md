<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>InvestLink — Demo Investment Site</title>
  <style>
    body{font-family:Arial,sans-serif;margin:0;padding:0;background:#f6f8fa;color:#111;}
    .container{max-width:900px;margin:40px auto;padding:24px;background:#fff;border-radius:12px;box-shadow:0 6px 20px rgba(0,0,0,0.06);}
    h1{margin:0 0 8px;font-size:28px;text-align:center;}
    p.lead{color:#444;text-align:center;margin-top:0;}
    .plans{display:flex;gap:16px;flex-wrap:wrap;justify-content:center;margin-top:20px;}
    .card{flex:1;min-width:220px;background:#fbfdff;border:1px solid #eef3f8;padding:18px;border-radius:10px;text-align:center;}
    .price{font-size:22px;font-weight:700;margin-top:6px;}
    .btn{display:inline-block;padding:10px 16px;border-radius:8px;background:#2563eb;color:#fff;text-decoration:none;margin-top:12px;}
    label{display:block;font-weight:600;margin-top:12px;text-align:left;}
    input, select{width:100%;padding:8px;border-radius:8px;border:1px solid #d5dbe6;margin-top:8px;}
    footer{margin-top:18px;color:#666;font-size:13px;text-align:center;}
    .small{font-size:13px;color:#666;}
  </style>
</head>
<body>
  <div class="container">
    <h1>InvestLink — Demo Investment</h1>
    <p class="lead">Select a plan and click Invest. Payments handled by the gateway (sandbox/live later).</p>

    <div class="plans">
      <div class="card">
        <div><strong>Starter</strong></div>
        <div class="price">Min ₹1000</div>
        <div class="small">Daily profit: 0.8% (simulated)</div>
        <a class="btn" href="https://sandbox.jazzcash.pk/checkout?plan=starter">Invest (JazzCash)</a><br>
        <a class="btn" href="https://sandbox.easypaisa.com.pk/checkout?plan=starter" style="margin-top:8px;">Invest (Easypaisa)</a>
      </div>
      <div class="card">
        <div><strong>Growth</strong></div>
        <div class="price">Min ₹10,000</div>
        <div class="small">Daily profit: 1.2% (simulated)</div>
        <a class="btn" href="https://sandbox.jazzcash.pk/checkout?plan=growth">Invest (JazzCash)</a><br>
        <a class="btn" href="https://sandbox.easypaisa.com.pk/checkout?plan=growth" style="margin-top:8px;">Invest (Easypaisa)</a>
      </div>
      <div class="card">
        <div><strong>Pro</strong></div>
        <div class="price">Min ₹50,000</div>
        <div class="small">Daily profit: 1.5% (simulated)</div>
        <a class="btn" href="https://sandbox.jazzcash.pk/checkout?plan=pro">Invest (JazzCash)</a><br>
        <a class="btn" href="https://sandbox.easypaisa.com.pk/checkout?plan=pro" style="margin-top:8px;">Invest (Easypaisa)</a>
      </div>
    </div>

    <section style="margin-top:30px;">
      <h3>Quick Signup</h3>
      <form id="signupForm" onsubmit="return handleSignup(event)">
        <label>Name</label>
        <input id="name" required placeholder="Your name">
        <label>Email</label>
        <input id="email" type="email" required placeholder="Email for receipts">
        <label>Phone</label>
        <input id="phone" required placeholder="Mobile number">
        <label>Plan</label>
        <select id="plan">
          <option value="starter">Starter</option>
          <option value="growth">Growth</option>
          <option value="pro">Pro</option>
        </select>
        <button class="btn" type="submit">Create Order & Go to Pay</button>
      </form>
      <p class="small" style="margin-top:10px;">Demo site only — payments redirect to sandbox links.</p>
    </section>

    <footer>
      <p class="small">Frontend demo — do not handle real user funds without legal setup.</p>
    </footer>
  </div>

<script>
function handleSignup(e){
  e.preventDefault();
  const name = document.getElementById('name').value.trim();
  const email = document.getElementById('email').value.trim();
  const phone = document.getElementById('phone').value.trim();
  const plan = document.getElementById('plan').value;
  const provider = confirm("OK for JazzCash, Cancel for Easypaisa") ? 'JAZZ' : 'EASY';
  const base = provider==='JAZZ'?'https://sandbox.jazzcash.pk/checkout':'https://sandbox.easypaisa.com.pk/checkout';
  const params = new URLSearchParams({name,email,phone,plan,amount: plan==='starter'?1000:plan==='growth'?10000:50000}).toString();
  window.location.href = base + '?' + params;
}
</script>

</body>
</html>

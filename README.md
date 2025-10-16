gvt140-site/
│
├── index.html
├── style.css
└── script.js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GVT140 Investment Plans</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>GVT140 Investment Plans</h1>
    <p>PKR 300 se 1 Million tak investment options</p>
  </header>

  <section id="plans">
    <h2>Investment Plans</h2>
    <div class="plan">
      <h3>Starter: 300 - 10,000 PKR</h3>
      <p>Low risk, safe growth</p>
    </div>
    <div class="plan">
      <h3>Silver: 10,001 - 50,000 PKR</h3>
      <p>Moderate risk, 8-12% monthly</p>
    </div>
    <div class="plan">
      <h3>Gold: 50,001 - 250,000 PKR</h3>
      <p>Medium-high risk, 12-20% monthly</p>
    </div>
    <div class="plan">
      <h3>Platinum: 250,001 - 1,000,000 PKR</h3>
      <p>High risk, 20-35% monthly</p>
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

  <script src="script.js"></script>
</body>
</html>
body { font-family: Arial, sans-serif; padding: 20px; background: #f2f2f2; }
header { text-align: center; margin-bottom: 30px; }
h1 { color: #333; }
#plans { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; }
.plan { background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 6px rgba(0,0,0,0.1); }
#calculator { margin-top: 40px; text-align: center; }
input, select, button { padding: 10px; margin: 5px; }
button { cursor: pointer; }
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
  git init
git add .
git commit -m "Add investment site files"
git branch -M main
git remote add origin https://github.com/<username>/gvt140.git
git push -u origin main

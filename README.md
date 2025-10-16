<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Gvt Project</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #0f2027, #203a43, #2c5364);
      color: white;
      margin: 0;
      text-align: center;
    }
    header {
      background: rgba(255,255,255,0.1);
      padding: 20px;
      font-size: 24px;
      font-weight: bold;
    }
    .container {
      margin-top: 50px;
    }
    input, button {
      padding: 10px;
      font-size: 16px;
      border: none;
      border-radius: 5px;
      margin: 5px;
    }
    input {
      width: 200px;
    }
    button {
      background-color: #28a745;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background-color: #218838;
    }
    footer {
      margin-top: 60px;
      padding: 20px;
      background: rgba(255,255,255,0.1);
    }
  </style>
</head>
<body>
  <header>💸 Gvt Demo Profit Calculator 💸</header>

  <div class="container">
    <h2>Enter your investment amount</h2>
    <input type="number" id="amount" placeholder="Enter amount $" />
    <button onclick="calculateProfit()">Calculate Profit</button>

    <h3 id="result"></h3>
  </div>

  <footer>
    <p>⚠️ This is a demo site for educational use only.</p>
  </footer>

  <script>
    function calculateProfit() {
      const amount = document.getElementById("amount").value;
      if (amount && amount > 0) {
        const profit = (amount * 0.05).toFixed(2); // 5% daily demo profit
        document.getElementById("result").innerText = 
          `Estimated Daily Profit: $${profit}`;
      } else {
        document.getElementById("result").innerText = "Enter a valid amount!";
      }
    }
  </script>
</body>
</html>

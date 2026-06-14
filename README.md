<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>MOLE FINANCE Loan Calculator</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 40px;
      background: #f9f9f9;
    }
    h1 { color: #333; }
    .calculator {
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      max-width: 400px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    label { display: block; margin-top: 10px; }
    input {
      width: 100%; padding: 8px; margin-top: 4px;
      border: 1px solid #ccc; border-radius: 4px;
    }
    button {
      margin-top: 15px; padding: 10px; width: 100%;
      background: gold; border: none; border-radius: 4px;
      font-weight: bold; cursor: pointer;
    }
    .result { margin-top: 20px; font-size: 1.1em; color: #222; }
  </style>
</head>
<body>
  <h1>MOLE FINANCE Loan Calculator</h1>
  <div class="calculator">
    <!-- Client details -->
    <label>Client Name:</label>
    <input type="text" id="clientName" placeholder="Enter client name">

    <label>Client Email:</label>
    <input type="email" id="clientEmail" placeholder="Enter client email">

    <label>Client Phone:</label>
    <input type="text" id="clientPhone" placeholder="Enter client phone">

    <!-- Loan details -->
    <label>Loan Amount (PGK):</label>
    <input type="number" id="amount" placeholder="Enter amount">

    <label>Annual Interest Rate (%):</label>
    <input type="number" id="rate" placeholder="e.g. 12">

    <label>Loan Term (years):</label>
    <input type="number" id="years" placeholder="e.g. 2">

    <button onclick="calculateLoan()">Calculate</button>
    <button onclick="downloadPDF()">Download Quote (PDF)</button>

    <div class="result" id="result"></div>
  </div>

  <script>
    let repayment, total;

    function calculateLoan() {
      const amount = parseFloat(document.getElementById('amount').value);
      const rate = parseFloat(document.getElementById('rate').value) / 100 / 12;
      const years = parseFloat(document.getElementById('years').value);
      const months = years * 12;

      if (isNaN(amount) || isNaN(rate) || isNaN(years)) {
        document.getElementById('result').innerText = "Please fill in all fields.";
        return;
      }

      repayment = (amount * rate) / (1 - Math.pow(1 + rate, -months));
      total = repayment * months;

      document.getElementById('result').innerHTML =
        `Monthly Repayment: PGK ${repayment.toFixed(2)}<br>` +
        `Total Payment: PGK ${total.toFixed(2)}`;
    }

    async function downloadPDF() {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();

      // Branding
      doc.setTextColor(218,165,32); // gold
      doc.setFontSize(18);
      doc.text("MOLE FINANCE Loan Quote", 20, 20);

      // Reset to black
      doc.setTextColor(0,0,0);
      doc.setFontSize(12);

      // Client details
      doc.text(`Client Name: ${document.getElementById('clientName').value}`, 20, 40);
      doc.text(`Email: ${document.getElementById('clientEmail').value}`, 20, 50);
      doc.text(`Phone: ${document.getElementById('clientPhone').value}`, 20, 60);

      // Loan details
      doc.text(`Loan Amount: PGK ${document.getElementById('amount').value}`, 20, 80);
      doc.text(`Interest Rate: ${document.getElementById('rate').value}%`, 20, 90);
      doc.text(`Loan Term: ${document.getElementById('years').value} years`, 20, 100);
      doc.text(`Monthly Repayment: PGK ${repayment.toFixed(2)}`, 20, 120);
      doc.text(`Total Payment: PGK ${total.toFixed(2)}`, 20, 130);

      doc.save("LoanQuote.pdf");
    }
  </script>
</body>
</html>
index.html

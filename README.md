async function downloadPDF() { const { jsPDF } = window.jspdf; const doc = new jsPDF();

// Branding doc.setTextColor(218,165,32); // gold doc.setFontSize(18); doc.text("MOLE FINANCE Loan Quote", 20, 20);

// Reset to black doc.setTextColor(0,0,0); doc.setFontSize(12);

// Client details table doc.text("Client Details", 20, 40); doc.autoTable({ startY: 45, head: [['Field', 'Value']], body: [ ['Client Name', document.getElementById('clientName').value], ['Email', document.getElementById('clientEmail').value], ['Phone', document.getElementById('clientPhone').value] ], theme: 'grid', styles: { fillColor: [240,240,240] } });

// Loan details table doc.text("Loan Details", 20, doc.lastAutoTable.finalY + 15); doc.autoTable({ startY: doc.lastAutoTable.finalY + 20, head: [['Field', 'Value']], body: [ ['Loan Amount', PGK ${document.getElementById('amount').value}], ['Paydays', document.getElementById('paydays').value], ['Interest Rate', ${(interestRate*100).toFixed(0)}%], ['Total Repayment', PGK ${totalRepayment.toFixed(2)}], ['Installment Amount', PGK ${installmentAmount.toFixed(2)} per payday] ], theme: 'grid', styles: { fillColor: [240,240,240] } });

// Signature + Date lines const yPos = doc.lastAutoTable.finalY + 40; doc.setFontSize(12); doc.text("Client Signature: ____________________________", 20, yPos); doc.text("Date: _________________________________", 20, yPos + 15);

doc.text("Officer Signature: ___________________________", 20, yPos + 35); doc.text("Date: _________________________________", 20, yPos + 50);

// Footer doc.setFontSize(10); doc.text("MOLE FINANCE • Responsible Borrowing • Contact: info@molefinance.pg", 20, 280);

doc.save("LoanQuote.pdf"); }

<title>MOLE FINANCE Loan Calculator</title> <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script> <style> body { font-family: Arial, sans-serif; margin: 40px; background: #f9f9f9; } h1 { color: #333; } .calculator { background: #fff; padding: 20px; border-radius: 8px; max-width: 400px; box-shadow: 0 2px 6px rgba(0,0,0,0.1); } label { display: block; margin-top: 10px; } input { width: 100%; padding: 8px; margin-top: 4px; border: 1px solid #ccc; border-radius: 4px; } button { margin-top: 15px; padding: 10px; width: 100%; background: gold; border: none; border-radius: 4px; font-weight: bold; cursor: pointer; } .result { margin-top: 20px; font-size: 1.1em; color: #222; } </style>
MOLE FINANCE Loan Calculator
Client Name:
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
<script> let repayment, total; function calculateLoan() { const amount = parseFloat(document.getElementById('amount').value); const rate = parseFloat(document.getElementById('rate').value) / 100 / 12; const years = parseFloat(document.getElementById('years').value); const months = years * 12; if (isNaN(amount) || isNaN(rate) || isNaN(years)) { document.getElementById('result').innerText = "Please fill in all fields."; return; } repayment = (amount * rate) / (1 - Math.pow(1 + rate, -months)); total = repayment * months; document.getElementById('result').innerHTML = `Monthly Repayment: PGK ${repayment.toFixed(2)}
` + `Total Payment: PGK ${total.toFixed(2)}`; } async function downloadPDF() { const { jsPDF } = window.jspdf; const doc = new jsPDF(); // Branding doc.setTextColor(218,165,32); // gold doc.setFontSize(18); doc.text("MOLE FINANCE Loan Quote", 20, 20); // Reset to black doc.setTextColor(0,0,0); doc.setFontSize(12); // Client details doc.text(`Client Name: ${document.getElementById('clientName').value}`, 20, 40); doc.text(`Email: ${document.getElementById('clientEmail').value}`, 20, 50); doc.text(`Phone: ${document.getElementById('clientPhone').value}`, 20, 60); // Loan details doc.text(`Loan Amount: PGK ${document.getElementById('amount').value}`, 20, 80); doc.text(`Interest Rate: ${document.getElementById('rate').value}%`, 20, 90); doc.text(`Loan Term: ${document.getElementById('years').value} years`, 20, 100); doc.text(`Monthly Repayment: PGK ${repayment.toFixed(2)}`, 20, 120); doc.text(`Total Payment: PGK ${total.toFixed(2)}`, 20, 130); doc.save("LoanQuote.pdf"); } </script> index.htmlasync function downloadPDF() {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  // Branding
  doc.setTextColor(218,165,32); // gold
  doc.setFontSize(18);
  doc.text("MOLE FINANCE Loan Quote", 20, 20);

  // Reset to black
  doc.setTextColor(0,0,0);
  doc.setFontSize(12);

  // Client details table
  doc.text("Client Details", 20, 40);
  doc.autoTable({
    startY: 45,
    head: [['Field', 'Value']],
    body: [
      ['Client Name', document.getElementById('clientName').value],
      ['Email', document.getElementById('clientEmail').value],
      ['Phone', document.getElementById('clientPhone').value]
    ],
    theme: 'grid',
    styles: { fillColor: [240,240,240] }
  });

  // Loan details table
  doc.text("Loan Details", 20, doc.lastAutoTable.finalY + 15);
  doc.autoTable({
    startY: doc.lastAutoTable.finalY + 20,
    head: [['Field', 'Value']],
    body: [
      ['Loan Amount', `PGK ${document.getElementById('amount').value}`],
      ['Paydays', document.getElementById('paydays').value],
      ['Interest Rate', `${(interestRate*100).toFixed(0)}%`],
      ['Total Repayment', `PGK ${totalRepayment.toFixed(2)}`],
      ['Installment Amount', `PGK ${installmentAmount.toFixed(2)} per payday`]
    ],
    theme: 'grid',
    styles: { fillColor: [240,240,240] }
  });

  // Signature + Date lines
  const yPos = doc.lastAutoTable.finalY + 40;
  doc.setFontSize(12);
  doc.text("Client Signature: ____________________________", 20, yPos);
  doc.text("Date: _________________________________", 20, yPos + 15);

  doc.text("Officer Signature: ___________________________", 20, yPos + 35);
  doc.text("Date: _________________________________", 20, yPos + 50);

  // Footer
  doc.setFontSize(10);
  doc.text("MOLE FINANCE • Responsible Borrowing • Contact: info@molefinance.pg", 20, 280);

  doc.save("LoanQuote.pdf");
}
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
# MOLE MINI FINANCE Loan Calculator

![Excel](https://img.shields.io/badge/Built%20with-Excel-217346?logo=microsoft-excel&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/Powered%20by-GitHub%20Pages-000000?logo=github&logoColor=white)
![Finance Tools](https://img.shields.io/badge/Category-Finance%20Tools-FFD700?logo=google-analytics&logoColor=black)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)

---

## 🌟 Branding
**MOLE MINI FINANCE — Aitape/Lumi District, Sandaun Province, Papua New Guinea**  
*"Helping Hand is a Caring Hand"*

This project provides a **loan calculator + Excel database toolkit** for officers and clients, hosted on GitHub Pages.

---

## 🚀 Live Demo
Access the calculator online via GitHub Pages:  
👉 [MOLE FINANCE Loan Calculator](https://camilusdominic18-droid.github.io/MOLE-FINANCE)

---

## 📂 Excel Database Template
Download the ready‑made Excel file:  
👉 [`templates/MOLE_FINANCE_Database.xlsx`](templates/MOLE_FINANCE_Database.xlsx)

### Sheets Included:
- **COMPANY PROFILE** – Company details and officer in charge  
- **CLIENT MASTER** – Client personal and employment details  
- **LOAN APPLICATION** – Loan requests, approval status, repayment terms  
- **REPAYMENT SCHEDULE** – Installments, due dates, payment status  
- **RISK AND COLLECTION** – Overdue loans, follow‑up actions, outcomes  
- **LOAN CALCULATOR** – Quick repayment and installment calculations  
- **SHEET 1 / SHEET 2** – Scratch pads for dashboards and charts  

---

## 📊 Dashboard Preview
The Dashboard sheet provides at‑a‑glance insights:

- Loan Distribution (Pie Chart)  
- Repayment Performance (Column Chart)  
- Risk & Collection (Bar Chart)  
- Loan Calculator Trend (Line Chart)  
- Officer Activity (Pivot Table + Column Chart)  

📷 *Insert screenshot here once built in Excel*  
Example: `![Dashboard Preview](templates/dashboard.png)`

---

## 🛠️ Roadmap
- [x] Loan calculator hosted on GitHub Pages  
- [x] Excel database template with formulas  
- [x] Dashboard mockup design guide  
- [ ] Add real client/loan data exports  
- [ ] Automate CSV → Excel import workflow  
- [ ] Expand dashboard with employer compliance reports  

---

## 🤝 Contributing
Contributions are welcome!  
- Fork the repo  
- Create a feature branch  
- Submit a pull request  

---

## 📜 License
This project is licensed under the MIT License.  
See [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgements
- Built with **Microsoft Excel** and **GitHub Pages**  
- Inspired by community finance needs in Papua New Guinea  
- Special thanks to contributors and testers of MOLE MINI FINANCE
MIT License

Copyright (c) 2026 MOLE MINI FINANCE

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
# Contributing to MOLE MINI FINANCE

Thank you for your interest in contributing!  
MOLE MINI FINANCE is an open‑source project providing a loan calculator, Excel database toolkit, and dashboard reporting system for community finance officers.

---

## 🛠️ How to Contribute

### 1. Fork the Repository
- Click the **Fork** button at the top of this repo.
- Clone your fork locally:
  ```bash
  git clone https://github.com/your-username/MOLE-FINANCE.git
git checkout -b feature/your-feature-name
git commit -m "Add dashboard chart for overdue loans"
git push origin feature/your-feature-name

---

## ✅ Repo Structure After Commit
- `README.md` → Badges, branding, demo link, Excel template, dashboard visuals, roadmap, credits.  
- `LICENSE.md` → MIT License.  
- `CONTRIBUTING.md` → Guidelines for collaboration.  

---

👉 Next step: Once you commit this file, your repo will be **fully professional** with README, LICENSE, and CONTRIBUTING in place.  

Would you like me to also draft a **ROADMAP.md file** (detailed checklist of upcoming features and milestones) so your repo shows clear future plans?
# MOLE MINI FINANCE Roadmap

This roadmap outlines planned features, improvements, and milestones for the MOLE MINI FINANCE project.  
It helps contributors and users understand the direction of development.

---

## ✅ Completed
- Loan calculator hosted on GitHub Pages
- Excel database template with formulas
- Dashboard mockup design guide
- README.md with badges, branding, and demo link
- LICENSE.md (MIT License)
- CONTRIBUTING.md guidelines

---

## 🚧 In Progress
- Build and commit `MOLE_FINANCE_Database.xlsx` under `/templates/`
- Add Dashboard screenshot (`dashboard.png`) to README
- Expand Excel dashboard with slicers and pivot tables
- Improve branding with gold highlights and logo integration

---

## 📅 Upcoming Features
- CSV → Excel automated import workflow
- Employer compliance reporting (summary sheets for HR/Payroll)
- Dark mode toggle for GitHub Pages calculator
- Mobile responsiveness improvements
- Custom domain setup for GitHub Pages site
- EmailJS integration for sending loan quotes via email
- Enhanced dashboard with overdue loan alerts

---

## 🎯 Long-Term Goals
- Full client management system (web + Excel integration)
- Multi‑user officer access with role permissions
- Cloud storage integration (OneDrive/Google Drive)
- Advanced analytics dashboard (loan trends, repayment ratios)
- Community support portal for clients

---

## 🤝 How to Contribute
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to help build these features.
# Credits – MOLE MINI FINANCE

This document acknowledges the people, tools, and resources that have contributed to the MOLE MINI FINANCE project.

---

## 👤 Project Lead
- **Camilus Konzie Dominic**  
  Founder & Officer in Charge, MOLE MINI FINANCE LTD  
  Vision: *"Helping Hand is a Caring Hand"*

---

## 🛠️ Tools & Technologies
- **Microsoft Excel** – Database template, formulas, and dashboard design  
- **GitHub Pages** – Hosting the loan calculator online  
- **JavaScript/HTML/CSS** – Web calculator functionality  
- **EmailJS** – Planned integration for sending loan quotes via email  

---

## 🤝 Contributors & Testers
- Community testers from **Aitape/Lumi District, Sandaun Province**  
- Early adopters providing feedback on loan calculator usability  
- Officers assisting with dummy data entry and dashboard validation  

---

## 📜 Documentation
- **README.md** – Project overview, badges, demo link, Excel template, dashboard visuals  
- **LICENSE.md** – MIT License for open‑source compliance  
- **CONTRIBUTING.md** – Guidelines for collaboration  
- **ROADMAP.md** – Future plans and milestones  
- **CREDITS.md** – Acknowledgements  

---

## 🙏 Special Thanks
- Microsoft Copilot – AI assistance in drafting documentation and design guides  
- Open‑source community for inspiration and best practices  
- Local finance officers for their dedication to responsible lending

---

*"Helping Hand is a Caring Hand"*
# Support – MOLE MINI FINANCE

We want MOLE MINI FINANCE to be easy to use and accessible for both officers and clients.  
This document explains how to get help, report issues, and request new features.

---

## 🆘 Getting Help
- **Loan Calculator Issues**  
  If the GitHub Pages calculator is not working, please refresh your browser or clear cache.  
  If problems persist, open an issue in this repo.

- **Excel Database Template**  
  For questions about formulas, sheet structure, or dashboard setup, check the README.md and ROADMAP.md.  
  If you still need help, open a support issue.

---

## 📝 Reporting Issues
- Go to the **Issues** tab in this repository.  
- Click **New Issue** and describe the problem clearly.  
- Include screenshots or error messages if possible.  
- Tag your issue with one of these labels:
  - `bug` – Something isn’t working  
  - `enhancement` – Suggest a new feature  
  - `documentation` – Request improvements to guides or docs  

---

## 💡 Feature Requests
We welcome ideas to improve MOLE MINI FINANCE!  
- Open a new issue with the label `enhancement`.  
- Explain the feature and why it would help officers or clients.  
- If possible, suggest how it could be implemented (Excel formula, dashboard chart, web calculator update).

---

## 📞 Contact
For direct inquiries:  
- **Email:** info@molefinance.pg  
- **Phone:** 72958712 / 71720062 / 82493350  

---

## 🙏 Community Support
- Officers and clients in **Aitape/Lumi District, Sandaun Province** can reach out locally for training.  
- Contributions from the open‑source community are encouraged — see [CONTRIBUTING.md](CONTRIBUTING.md).  

---

# Support – MOLE MINI FINANCE

We want MOLE MINI FINANCE to be easy to use and accessible for both officers and clients.  
This document explains how to get help, report issues, and request new features.

---

## 🆘 Getting Help
- **Loan Calculator Issues**  
  If the GitHub Pages calculator is not working, please refresh your browser or clear cache.  
  If problems persist, open an issue in this repo.

- **Excel Database Template**  
  For questions about formulas, sheet structure, or dashboard setup, check the README.md and ROADMAP.md.  
  If you still need help, open a support issue.

---

## 📝 Reporting Issues
- Go to the **Issues** tab in this repository.  
- Click **New Issue** and describe the problem clearly.  
- Include screenshots or error messages if possible.  
- Tag your issue with one of these labels:
  - `bug` – Something isn’t working  
  - `enhancement` – Suggest a new feature  
  - `documentation` – Request improvements to guides or docs  

---

## 💡 Feature Requests
We welcome ideas to improve MOLE MINI FINANCE!  
- Open a new issue with the label `enhancement`.  
- Explain the feature and why it would help officers or clients.  
- If possible, suggest how it could be implemented (Excel formula, dashboard chart, web calculator update).

---

## 📞 Contact
For direct inquiries:  
- **Email:** info@molefinance.pg  
- **Phone:** 72958712 / 71720062 / 82493350  

---

## 🙏 Community Support
- Officers and clients in **Aitape/Lumi District, Sandaun Province** can reach out locally for training.  
- Contributions from the open‑source community are encouraged — see [CONTRIBUTING.md](CONTRIBUTING.md).  

---

*"Helping Hand is a Caring Hand"*
*"Helping Hand is a Caring Hand"*
.github/
 └── ISSUE_TEMPLATE/
      ├── bug_report.md
      ├── feature_request.md
      └── config.yml
---
name: Bug Report
about: Report a problem with MOLE MINI FINANCE
title: "[BUG] "
labels: bug
assignees: ''
---

## 🐞 Bug Description
A clear and concise description of what the bug is.

## 🔄 Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. Scroll down to '...'
4. See error

## ✅ Expected Behavior
What you expected to happen.

## 📸 Screenshots
If applicable, add screenshots to help explain your problem.

## 💻 Environment
- Browser/Excel version:
- Operating system:

## 📌 Additional Context
Add any other context about the problem here.
---
name: Feature Request
about: Suggest an idea for MOLE MINI FINANCE
title: "[FEATURE] "
labels: enhancement
assignees: ''
---

## 💡 Feature Description
A clear and concise description of the feature you’d like to see.

## 🎯 Why Is This Needed?
Explain why this feature would help officers, clients, or contributors.

## 🛠️ Possible Implementation
If you have ideas on how to implement it (Excel formula, dashboard chart, web calculator update), describe them here.

## 📌 Additional Context
Add any other context, screenshots, or examples here.
blank_issues_enabled: false
contact_links:
  - name: Community Support
    url: https://github.com/camilusdominic18-droid/MOLE-FINANCE/blob/main/SUPPORT.md
    about: Please check SUPPORT.md for help before opening a new issue.
# Pull Request – MOLE MINI FINANCE

Thank you for contributing to MOLE MINI FINANCE!  
Please complete the checklist below to help us review your changes.

---

## 📋 Description
- What does this PR do?
- Why is it needed?

---

## 🔄 Changes Made
- [ ] Added new feature
- [ ] Fixed a bug
- [ ] Updated documentation
- [ ] Improved dashboard/Excel template
- [ ] Other (please describe)

---

## ✅ Checklist
- [ ] My code follows the project’s style guidelines
- [ ] I have tested the loan calculator on GitHub Pages
- [ ] I have tested the Excel formulas and dashboard
- [ ] I have updated README.md if necessary
- [ ] I have added screenshots for new dashboard features (if applicable)
- [ ] I have updated ROADMAP.md if this PR adds new milestones
- [ ] I have updated CREDITS.md if new contributors/tools are acknowledged

---

## 📸 Screenshots (if applicable)
Attach screenshots of new features, dashboards, or bug fixes.

---

## 📌 Related Issues
Link any related issues here (e.g., `Fixes #12`).

---

## 🙏 Notes for Reviewers
Add any extra context or details reviewers should know.
# Security Policy – MOLE MINI FINANCE

We take the security of MOLE MINI FINANCE seriously.  
This document explains how to report vulnerabilities and our approach to responsible disclosure.

---

## 🔒 Supported Versions
We currently support security updates for:
- **Main branch** (active development)
- **Latest release** (stable version)

Older versions may not receive security patches.

---

## 🛡️ Reporting a Vulnerability
If you discover a security issue, please follow these steps:

1. **Do not open a public issue.**  
   Security vulnerabilities should be reported privately.

2. **Contact us directly:**  
   - Email: info@molefinance.pg  
   - Phone: 72958712 / 71720062 / 82493350  

3. **Provide details:**  
   - Description of the vulnerability  
   - Steps to reproduce  
   - Potential impact  
   - Suggested fix (if known)

---

## ⚖️ Responsible Disclosure
- We will acknowledge receipt of your report within **72 hours**.  
- We will investigate and provide a status update within **7 days**.  
- Fixes will be prioritized and released as soon as possible.  
- Credit will be given to reporters who follow responsible disclosure practices.

---

## 🚫 What Not to Do
- Do not publicly disclose vulnerabilities before a fix is released.  
- Do not exploit vulnerabilities for unauthorized access or data extraction.  
- Do not use vulnerabilities to disrupt services.

---

## 🙏 Thank You
We appreciate the community’s help in keeping MOLE MINI FINANCE secure.  
*"Helping Hand is a Caring Hand"*
# 1. Navigate to your repo folder
cd MOLE-FINANCE

# 2. Move your dashboard screenshot into the templates folder
# (if not already there)
mv /path/to/dashboard.png templates/dashboard.png

# 3. Stage the new file
git add templates/dashboard.png

# 4. Commit the file with a clear message
git commit -m "Add Dashboard screenshot (dashboard.png) to templates folder"

# 5. Push changes to GitHub
git push origin main
## 📊 Dashboard Preview

![Dashboard Preview](templates/dashboard.png)
# Navigate to your repo
cd MOLE-FINANCE

# Pull latest changes
# Create a tag for version 1.0.0
git tag -a v1.0.0 -m "MOLE FINANCE Loan Calculator – Initial Release"

# Push the tag to GitHub
git push origin v1.0.0
git pull origin main
## 🚀 MOLE FINANCE Loan Calculator v1.0.0

### 📂 Included in this Release
- Loan Calculator hosted on GitHub Pages
- Dummy Excel Database (`MOLE_FINANCE_Database.xlsx`)
- Dashboard screenshot (`dashboard.png`)
- Complete documentation set:
  - README.md (badges, branding, demo link, roadmap, credits)
  - LICENSE.md (MIT License)
  - CONTRIBUTING.md (collaboration guidelines)
  - ROADMAP.md (future milestones)
  - CREDITS.md (acknowledgements)
  - SUPPORT.md (help and contact info)
  - SECURITY.md (responsible disclosure)
  - ISSUE Templates (bug reports + feature requests)
  - PULL_REQUEST_TEMPLATE.md (PR checklist)

### ✅ Highlights
- Professional repo setup with badges and branding
- GitHub Pages live demo
- Excel database template for officers and clients
- Dashboard visuals for loan performance insights
- Clear roadmap for future features

*"Helping Hand is a Caring Hand"*
# Changelog – MOLE MINI FINANCE

All notable changes to this project will be documented here.  
This project follows [Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

---

## [v1.0.0] – 2026-06-23
### 🚀 Initial Release
- Loan Calculator hosted on GitHub Pages
- Dummy Excel Database (`MOLE_FINANCE_Database.xlsx`)
- Dashboard screenshot (`dashboard.png`)
- Complete documentation set:
  - README.md (badges, branding, demo link, roadmap, credits)
  - LICENSE.md (MIT License)
  - CONTRIBUTING.md (collaboration guidelines)
  - ROADMAP.md (future milestones)
  - CREDITS.md (acknowledgements)
  - SUPPORT.md (help and contact info)
  - SECURITY.md (responsible disclosure)
  - ISSUE Templates (bug reports + feature requests)
  - PULL_REQUEST_TEMPLATE.md (PR checklist)

---

## [Unreleased]
### 🛠️ Planned
- CSV → Excel automated import workflow
- Employer compliance reporting
- Dark mode toggle for GitHub Pages calculator
- Mobile responsiveness improvements
- EmailJS integration for loan quotes
- Enhanced dashboard with overdue loan alerts
# Release Checklist – MOLE MINI FINANCE

This document provides a step‑by‑step guide for publishing new releases of MOLE MINI FINANCE.  
Follow this checklist to ensure each release is consistent, professional, and complete.

---

## 🔹 Pre‑Release Checklist
- [ ] Ensure all code and documentation changes are committed to `main`
- [ ] Update `README.md` with any new features or screenshots
- [ ] Update `ROADMAP.md` with completed and upcoming milestones
- [ ] Update `CHANGELOG.md` with version details
- [ ] Verify `LICENSE.md`, `CONTRIBUTING.md`, `CREDITS.md`, `SUPPORT.md`, and `SECURITY.md` are up to date
- [ ] Test GitHub Pages loan calculator for functionality
- [ ] Validate Excel database template (`MOLE_FINANCE_Database.xlsx`) formulas and dashboard
- [ ] Add or update dashboard screenshot (`dashboard.png`) if needed

---

## 🔹 Tagging the Release
```bash
# Create a new version tag
git tag -a vX.Y.Z -m "MOLE FINANCE Loan Calculator – Release vX.Y.Z"

# Push the tag to GitHub
git push origin vX.Y.Z
## 🚀 MOLE FINANCE Loan Calculator vX.Y.Z

### 📂 Included in this Release
- New features
- Bug fixes
- Documentation updates

### ✅ Highlights
- Key improvements
- Dashboard updates
- Community contributions

*"Helping Hand is a Caring Hand"*

---

## ✅ Repo Documentation Set After Commit
- `README.md` → Badges, branding, demo link, Excel template, dashboard visuals, roadmap, credits  
- `LICENSE.md` → MIT License  
- `CONTRIBUTING.md` → Collaboration guidelines  
- `ROADMAP.md` → Future plans and milestones  
- `CREDITS.md` → Acknowledgements  
- `SUPPORT.md` → Help, issue reporting, feature requests, and contact info  
- `.github/ISSUE_TEMPLATE/` → Bug + feature request forms  
- `PULL_REQUEST_TEMPLATE.md` → Contributor checklist for PRs  
- `SECURITY.md` → Vulnerability reporting and responsible disclosure  
- `CHANGELOG.md` → Version history and updates  
- `RELEASE.md` → Step‑by‑step release workflow  
git clone https://github.com/camilusdominic18-droid/MOLE-FINANCE.git

---

👉 Once you commit this, your repo will have **full lifecycle documentation** — from contribution and support to security, changelog, and release management.  

Would you like me to also prepare a **README badge for “Latest Release”** (auto‑updates to show your newest GitHub release version at the top of README.md)?
## MOLE FINANCE Loan Calculator

[![Latest Release](https://img.shields.io/github/v/release/camilusdominic18-droid/MOLE-FINANCE?label=Latest%20Release)](https://github.com/camilusdominic18-droid/MOLE-FINANCE/releases)

### Features
- [Your important features here]
cd Desktop
git clone https://github.com/camilusdominic18-droid/MOLE-FINANCE.git

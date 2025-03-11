<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>USA Budget Simulator</title>
    <link rel="stylesheet" href="styles.css">
    <script src="script.js" defer></script>
</head>
<body>
    <header>
        <h1>USA Budget Simulator</h1>
        <p>Adjust government budgets and policies to see the impact on the deficit and GDP.</p>
    </header>
    <main>
        <section id="budget-control">
            <h2>Government Departments</h2>
            <div id="departments">
                <label for="defense">Defense:</label>
                <input type="range" id="defense" min="100" max="1000" step="10" value="700" oninput="updateBudget()"> <span id="defense-value">700</span> Billion
                <br>
                <label for="healthcare">Healthcare:</label>
                <input type="range" id="healthcare" min="100" max="1000" step="10" value="500" oninput="updateBudget()"> <span id="healthcare-value">500</span> Billion
                <br>
                <label for="education">Education:</label>
                <input type="range" id="education" min="50" max="500" step="10" value="200" oninput="updateBudget()"> <span id="education-value">200</span> Billion
                <br>
                <label for="infrastructure">Infrastructure:</label>
                <input type="range" id="infrastructure" min="50" max="500" step="10" value="150" oninput="updateBudget()"> <span id="infrastructure-value">150</span> Billion
                <br>
            </div>
        </section>
        <section id="policy-options">
            <h2>Policy Adjustments</h2>
            <select id="policy-selector">
                <option value="universal_healthcare">Implement Universal Healthcare</option>
                <option value="blockchain_voting">Integrate Blockchain for Voting</option>
                <option value="carbon_tax">Introduce Carbon Tax</option>
                <option value="corporate_tax_cut">Lower Corporate Tax Rate</option>
                <option value="increase_min_wage">Increase Minimum Wage</option>
            </select>
            <button onclick="applyPolicy()">Apply Policy</button>
        </section>
        <section id="economic-impact">
            <h2>Economic Impact</h2>
            <p>Deficit: <span id="deficit">$1000</span> Billion</p>
            <p>GDP: <span id="gdp">$21.4T</span></p>
        </section>
    </main>
    <footer>
        <p>&copy; 2025 USA Budget Simulator</p>
    </footer>
    
    <script>
        let baseDeficit = 1000;
        let baseGDP = 21.4;
        
        function updateBudget() {
            let defense = parseInt(document.getElementById("defense").value);
            let healthcare = parseInt(document.getElementById("healthcare").value);
            let education = parseInt(document.getElementById("education").value);
            let infrastructure = parseInt(document.getElementById("infrastructure").value);
            
            document.getElementById("defense-value").innerText = defense;
            document.getElementById("healthcare-value").innerText = healthcare;
            document.getElementById("education-value").innerText = education;
            document.getElementById("infrastructure-value").innerText = infrastructure;
            
            let totalBudget = defense + healthcare + education + infrastructure;
            let deficit = baseDeficit + (totalBudget - 1550);
            document.getElementById("deficit").innerText = "$" + deficit + " Billion";
        }
        
        function applyPolicy() {
            let policy = document.getElementById("policy-selector").value;
            let gdpIncrease = 0;
            
            switch (policy) {
                case "universal_healthcare":
                    gdpIncrease = 0.5;
                    baseDeficit += 200;
                    break;
                case "blockchain_voting":
                    gdpIncrease = 0.2;
                    break;
                case "carbon_tax":
                    gdpIncrease = 0.3;
                    baseDeficit -= 100;
                    break;
                case "corporate_tax_cut":
                    gdpIncrease = 0.4;
                    baseDeficit += 150;
                    break;
                case "increase_min_wage":
                    gdpIncrease = 0.6;
                    break;
            }
            
            baseGDP += gdpIncrease;
            document.getElementById("gdp").innerText = "$" + baseGDP.toFixed(1) + "T";
            document.getElementById("deficit").innerText = "$" + baseDeficit + " Billion";
        }
    </script>
    
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }
        header {
            background-color: #333;
            color: white;
            padding: 20px;
        }
        main {
            margin: 20px auto;
            width: 80%;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        h2 {
            color: #333;
        }
        select, button, input[type=range] {
            margin: 10px;
        }
        footer {
            margin-top: 20px;
            padding: 10px;
            background-color: #333;
            color: white;
        }
    </style>
</body>
</html>
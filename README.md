<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TrilliumEco Tracker</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background-color: #0b0f19;
            color: #f3f4f6;
            margin: 0;
            padding: 20px;
        }
        header {
            text-align: center;
            margin-bottom: 40px;
            border-bottom: 2px solid #1e293b;
            padding-bottom: 20px;
        }
        h1 { color: #10b981; margin-bottom: 5px; }
        header p { color: #9ca3af; margin: 0; }
        main { max-width: 650px; margin: 0 auto; }
        .card {
            background: #111827;
            padding: 30px;
            border-radius: 16px;
            border: 1px solid #1e293b;
            margin-bottom: 25px;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
        }
        h2 { color: #34d399; margin-top: 0; font-size: 1.25rem; }
        label { display: block; margin: 20px 0 8px; color: #d1d5db; font-weight: 500; }
        input[type="number"] {
            width: 100%;
            padding: 12px;
            background: #1f2937;
            border: 1px solid #374151;
            border-radius: 8px;
            color: white;
            box-sizing: border-box;
            font-size: 1rem;
        }
        input[type="number"]:focus { border-color: #10b981; outline: none; }
        button {
            background-color: #10b981;
            color: #0b0f19;
            border: none;
            padding: 14px;
            font-size: 1rem;
            font-weight: 700;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            margin-top: 25px;
            transition: background 0.2s;
        }
        button:hover { background-color: #059669; }
        .checkbox-group label {
            display: flex;
            align-items: center;
            background: #1f2937;
            padding: 14px;
            border-radius: 8px;
            cursor: pointer;
            border: 1px solid #374151;
            margin-bottom: 10px;
        }
        input[type="checkbox"] { margin-right: 12px; transform: scale(1.2); }
    </style>
</head>
<body>
    <header>
        <h1>⚡ TrilliumEco Tracker</h1>
        <p>Architecting Personal Carbon Efficiency & Power Optimization</p>
    </header>

    <main>
        <section class="card">
            <h2>1. Carbon Telemetry Input (Track)</h2>
            <form id="telemetryForm">
                <label for="electricity">Domestic Energy Consumption (Monthly kWh):</label>
                <input type="number" id="electricity" placeholder="e.g., 150" required>

                <label for="commute">Daily Transport Telemetry (Car km/day):</label>
                <input type="number" id="commute" placeholder="e.g., 25" required>

                <button type="button" onclick="compileFootprint()">Compile Analytics</button>
            </form>
        </section>

        <section class="card" id="insightsCard" style="display:none;">
            <h2>2. Architectural Insights Compiler (Understand)</h2>
            <div id="resultsDisplay"></div>
        </section>

        <section class="card" id="optimizationCard" style="display:none;">
            <h2>3. Hardware-Class Mitigation Vectors (Reduce)</h2>
            <p>Toggle optimization profiles to dynamically scale down your projected load footprint:</p>
            <div class="checkbox-group">
                <label>
                    <input type="checkbox" id="vector1" onchange="optimizeProfiles()"> Transition to Smart Microgrids (-800 kg CO2e/yr)
                </label>
                <label>
                    <input type="checkbox" id="vector2" onchange="optimizeProfiles()"> Deploy Workstation Low-Power States (-150 kg CO2e/yr)
                </label>
                <label>
                    <input type="checkbox" id="vector3" onchange="optimizeProfiles()"> Optimize Mobility via Mass Transit (-1200 kg CO2e/yr)
                </label>
            </div>
        </section>
    </main>

    <script>
        let coreFootprint = 0;

        function compileFootprint() {
            const electricity = parseFloat(document.getElementById('electricity').value) || 0;
            const commute = parseFloat(document.getElementById('commute').value) || 0;

            const annualGridEmissions = electricity * 0.85 * 12; 
            const annualTransportEmissions = commute * 0.21 * 365; 

            coreFootprint = annualGridEmissions + annualTransportEmissions;

            renderDisplay(coreFootprint, 0);

            document.getElementById('insightsCard').style.display = 'block';
            document.getElementById('optimizationCard').style.display = 'block';
        }

        function optimizeProfiles() {
            let thermalSavings = 0;
            if (document.getElementById('vector1').checked) thermalSavings += 800;
            if (document.getElementById('vector2').checked) thermalSavings += 150;
            if (document.getElementById('vector3').checked) thermalSavings += 1200;

            renderDisplay(coreFootprint, thermalSavings);
        }

        function renderDisplay(base, savings) {
            let optimizedTotal = base - savings;
            if (optimizedTotal < 0) optimizedTotal = 0;

            const summaryHTML = `
                <p style="font-size: 1.1rem;">Total Compiled Baseline Load: <strong style="color:#ef4444;">${base.toFixed(2)} kg CO2e/year</strong></p>
                <p style="font-size: 1.2rem; margin: 15px 0;">Optimized System Target: <strong style="color:#10b981;">${optimizedTotal.toFixed(2)} kg CO2e/year</strong></p>
                <div style="background:#1f2937; padding: 12px; border-left: 4px solid #10b981; border-radius:4px; font-size:0.9rem; color:#9ca3af;">
                    <strong>System Insight Summary:</strong> Implementing the selected mitigation layout vectors reduces system environmental strain by <strong>${savings} kg CO2e/year</strong>.
                </div>
            `;
            document.getElementById('resultsDisplay').innerHTML = summaryHTML;
        }
    </script>
</body>
</html>

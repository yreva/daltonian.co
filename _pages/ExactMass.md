---
layout: page
title: Exact Mass Calculator
permalink: /exactmass/
---

# Exact Mass Calculator

<details>
<summary>Click to view calculator</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exact Mass Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }
        #calculator {
            max-width: 400px;
            margin: auto;
        }
    </style>
</head>
<body>

    <div id="calculator">
        <h2>Exact Mass Calculator</h2>
        <label for="inputString">Enter your string:</label>
        <input type="text" id="inputString" placeholder="e.g., H2O">

        <button onclick="calculateMass()">Calculate Mass</button>

        <p id="result"></p>
    </div>

    <script>
        function calculateMass() {
            const inputString = document.getElementById('inputString').value;
            const mass = calculateExactMass(inputString);
            document.getElementById('result').innerHTML = `Exact Mass: ${mass} g/mol`;
        }

        function calculateExactMass(inputString) {
            // Implement your exact mass calculation logic here
            // For simplicity, let's just return the length of the input string
            return inputString.length;
        }
    </script>

</body>
</html>
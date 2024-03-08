---
layout: page
title: Exact Mass Calculator
permalink: /exactmass/
---

# Exact Mass Calculator


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
    <label for="inputString">Enter your molecular formula:</label>
    <input type="text" id="inputString" placeholder="e.g., H2O">

<label for="charge">Select charge:</label>
<select id="charge">
    <option value="-1">-1</option>
    <option value="0" selected>0</option>
    <option value="+1">+1</option>
</select>

<button onclick="calculateMass()">Calculate Mass</button>

<p id="result"></p>
</div>

<script>
    function calculateMass() {
        const masses = {H:1.007825,C:12.000000,N:14.003074,O:15.994915,Na:22.989770}
        const inputString = document.getElementById('inputString').value;
        // Get each element + number of atoms
        const matches = inputString.match(/[A-Za-z][a-z]*\d+/g);
        letterCounts = {}
        if (matches) {
            letterCounts = getNumberOfAtoms(matches,masses);
        }

        let totalMass = 0;
        totalMass = getTotalMass(masses,letterCounts)
        document.getElementById('result').innerHTML = "Exact mass: m/z = ${totalMass}"
    }
    
    function getNumberOfAtoms(patternMatches,massList) {
        const result = {};
        matches.forEach(match => {
        const letterMatch = match.match(/[A-Za-z][a-z]*/);
        const letter = letterMatch ? letterMatch[0] : null;
        const value = parseInt(match.replace(/[A-Za-z][a-z]*/, '')); // Extract numerical value and convert to integer
        if (letter !== null) {
            result[letter] = (result[letter] || 0) + value;
        }
        });
        return result;
    }

    function getTotalMass(masses,letterObject)
        let total = 0;
        for (const letter in letterObject) {
            if (letterObject.hasOwnProperty(letter) && masses.hasOwnProperty(letter)) {
                total += letterObject[letter] * masses[letter];
        }
        return total;
    }

</script>

</body>
</html>
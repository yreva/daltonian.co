---
layout: page
title: Exact Mass Calculator
permalink: /exactmass/
---

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
        // https://jsfiddle.net/pr1bmkn3/
        function calculateMass() {
        const atoms = {H:1.007825,C:12.000000,N:14.003074,O:15.994915,Na:22.989770,H:1.007825,C:12.000000,N:14.003074,O:15.994915,F:18.998403,,Cl:34.968853,S:31.972072,K:39.963999,W:183.950953};
        const isotopes = {j2H:2.014102,j13C:13.003355,j15N:15.000109,jO17:16.999131,jO18:17.999159,j34S:33.967868,j37Cl:36.965903}
        const inputString = document.getElementById('inputString').value;
        // Get each element + number of atoms
        const matches = inputString.match(/[A-Za-z][a-z]*\d*/g);
        let letterCounts = {};
        if (matches) {
            letterCounts = getNumberOfAtoms(matches,atoms);
        }

        const totalMass = getTotalMass(atoms,letterCounts);
        
        if (document.getElementById('charge').value == 0) {
            const roundedMass = totalMass.toFixed(6);
            document.getElementById('result').innerHTML = `Exact mass: m/z = ${roundedMass}`;
        } else if (document.getElementById('charge').value == -1) {
            const chargedMass = totalMass + 5.48579909065e-4;
            const roundedMass = chargedMass.toFixed(6);
            document.getElementById('result').innerHTML = `Exact mass: m/z = ${roundedMass}`;
        } else {
            const chargedMass = totalMass - 5.48579909065e-4;
            const roundedMass = chargedMass.toFixed(6);
            document.getElementById('result').innerHTML = `Exact mass: m/z = ${roundedMass}`;
        }
        
    }
    
    function getNumberOfAtoms(patternMatches,massList) {
        let result = {};
        const matches = patternMatches
        matches.forEach(match => {
        const letterMatch = match.match(/[A-Za-z][a-z]*/);
        const letter = letterMatch ? letterMatch[0] : null;
        const value = parseInt(match.replace(/[A-Za-z][a-z]*/, '')); // Extract numerical value and convert to integer
        console.log(isNaN(value));
        if (letter !== null && !isNaN(value)) {
            result[letter] = (result[letter] || 0) + value;
        } else if  (letter !== null && isNaN(value)) {
            result[letter] = (result[letter] || 0) + 1;
        }
        });
        return result;
    }

    function getTotalMass(masses,letterObject) {
        let total = 0;
        for (const letter in letterObject) {
            if (letterObject.hasOwnProperty(letter) && masses.hasOwnProperty(letter)) {
                total += letterObject[letter] * masses[letter];
        }}
        return total;
    }

</script>

</body>
</html>
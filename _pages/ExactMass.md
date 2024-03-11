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

<br>

<div>
Please note that only H, He, C, N, O, F, Na, P, S, Cl, and K and their common isotops are included in this calculator. Using atoms other atoms will yield incorrect masses <br> <br>
<a href="https://daltonian.co/formulacalc" target="_blank">Check out our Molecular Formula Calculator here.</a>
</div>

<script>
        // https://jsfiddle.net/pr1bmkn3/
function calculateMass() {
    const atoms = {
    H:1.0078250319,
    He:4.0026032497,
    C:12.000000,
    N:14.0030740074,
    O:15.9949146223,
    F:18.9984032,
    Na:22.989770,
    P:30.97376149,
    S:31.972072,
    Cl:34.968853,
    K:38.9637069,
    W:183.950953
    };
    const isotopes = {
    j2H:2.0141017779,
    j3He:3.0160293094,
    j13C:13.003354838,
    j15N:15.000108973,
    jO17:16.9991315,
    jO18:17.9991604,
    j33S:32.97145854,
    j34S:33.967868,
    j36S:35.96708088,
    j37Cl:36.9659026,
    j41K:40.96182597
    };
    const inputString = document.getElementById('inputString').value;
    // Get each element + number of atoms
    const atomMatches = inputString.match(/(?<!j\d{1,2})[A-Z][a-z]*\d*/g);
    const isoMatches = inputString.match(/j\d*[A-Z][a-z]*\d*/g);
    let atomCounts = {};
    let isoCounts = {};
    if (atomMatches) {
        atomCounts = getNumberOfAtoms(atomMatches,atoms);
    }
    if (isoMatches) {
        isoCounts = getNumberOfIsotopes(isoMatches,isotopes);
        console.log(isoCounts);
    }

    const atomMass = getTotalMass(atoms,atomCounts);
    const isoMass = getTotalMass(isotopes,isoCounts);
    
    const totalMass = atomMass+isoMass;
    
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
    if (letter !== null && !isNaN(value)) {
        result[letter] = (result[letter] || 0) + value;
    } else if  (letter !== null && isNaN(value)) {
        result[letter] = (result[letter] || 0) + 1;
    }
    });
    return result;
}

    function getNumberOfIsotopes(patternMatches,massList) {
    let result = {};
    const matches = patternMatches
    matches.forEach(match => {
    const letterMatch = match.match(/j\d*[A-Z][a-z]*/);  // Extract isotope symbol
    const letter = letterMatch ? letterMatch[0] : null;
    const value = parseInt(match.replace(/j\d*[A-Z][a-z]*/, '')); // Extract numerical value and convert to integer
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
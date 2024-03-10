---
layout: page
title: Molecular Formula Calculator
permalink: /formulacalc/
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
    <label for="inputMass">Enter your m/z value: </label>
    <input type="text" id="inputMass" placeholder="i.e. 154.0145">
</div>

<div id="options">
<label for="charge">Select charge:</label>
<select id="charge">
    <option value="-1">-1</option>
    <option value="0" selected>0</option>
    <option value="+1">+1</option>
</select>

<label for="ppm">Select mass tolerance:</label>
<select id="ppm">
    <option value="0.5">0.5 ppm</option>
    <option value="0.75">0.75 ppm</option>
    <option value="1" selected>1 ppm</option>
    <option value="2">2 ppm</option>
    <option value="5">5 ppm</option>
    <option value="10">10 ppm</option>
</select>
</div>

<div>
<button onclick="calculateFormulas()">Calculate Possible Formulas</button>

<p id="result"></p>
</div>


<script>
 function molecularFormulasWithinTolerance(targetMass, charge, tolerance) {
  // Define atomic masses
  const atomicMasses = {
    H: 1.007825,
    C: 12.000000,
    N: 14.003074,
    O: 15.994915,
    Na: 22.989770
    Cl: 34.968853,
    S: 31.972072
  };

  // Helper function to calculate the molecular mass of the current formula
  function calculateMolecularMass(formula) {
    return Object.keys(formula).reduce((mass, atom) => mass + formula[atom] * atomicMasses[atom], 0);
  }

  // Array to store valid formulas within tolerance
  const formulasWithinTolerance = [];
  const differenceValues = [];

  // Iterate through possible combinations
  for (let c = 0; c <= 10; c++) {
    for (let h = 0; h <= 10; h++) {
      for (let n = 0; n <= 5; n++) {
        for (let o = 0; o <= 10; o++) {
        	if (o / c < 1.6 && n / c < 1.6 && h/c > 0.4) {
            for (let cl = 0; cl <= 0; cl++) {
              for (let na = 0; na <= 1; na++) {
                const formula = { C: c, H: h, N: n, O: o, Cl: cl, Na: na };
                const mass = calculateMolecularMass(formula) - charge * 5.48579909065e-4;
                const massError = 1000*(targetMass - mass) / mass;

                if (Math.abs(massError) <= tolerance) {
                  formulasWithinTolerance.push(formula);
                  differenceValues.push(massError);
                }
              }
            }
          }
        }
      }
    }
  }

  return [formulasWithinTolerance,differenceValues];
}

// Example usage


function calculateFormulas() {
	document.getElementById('result').innerHTML = ""
	const measuredMass = document.getElementById('inputMass').value;
  const charge = document.getElementById('charge').value;
  const massTolerance = document.getElementById('ppm').value; // Tolerance in ppm
  const [formulasWithinTolerance, differenceValues] = molecularFormulasWithinTolerance(measuredMass, charge, massTolerance);
  formulasWithinTolerance.forEach((formula, index) => {
  	const formulaString = Object.keys(formula)
    .filter(atom => formula[atom] !== 0)
    .map(atom => `${atom}${formula[atom]}`)
    .join('');
  	document.getElementById('result').innerHTML += `${index + 1}. ${formulaString}  ${differenceValues[index].toFixed(2)} ppm <br>`;
	});

}

console.log(`Molecular Formulas within ${massTolerance} mass tolerance:`);

</script>
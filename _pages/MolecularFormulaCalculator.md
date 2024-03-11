---
layout: page
title: Molecular Formula Calculator
permalink: /formulacalc/
---


<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chemical Composition</title>

</head>
<body align=center>

  <form>
  <label for="mz">Enter Measured m/z:</label>
  <input type="text" id="inputMass" name="inputMass" required>
    
  <br>

  <label for="numC"> #C: </label>
  <select id="numC" name="numC">
    <option value="5">0</option>
    <option value="10" selected>10</option>
    <option value="20" >20</option>
    <option value="30" >30</option>
    <option value="40" >40</option>
  </select>

  <label for="numH"> #H: </label>
  <select id="numH" name="numH">
    <option value="5">5</option>
    <option value="10" >10</option>
    <option value="20" selected>20</option>
    <option value="30" >30</option>
    <option value="40" >40</option>
  </select>

  <label for="numN"> #N: </label>
  <select id="numN" name="numN">
    <option value="0">0</option>
    <option value="1" selected>1</option>
    <option value="3" >3</option>
    <option value="5" >5</option>
  </select>

  <label for="numO"> #O: </label>
  <select id="numO" name="numO">
    <option value="0">0</option>
    <option value="2" >2</option>
    <option value="4" >4</option>
    <option value="6" selected>6</option>
    <option value="8" >8</option>
    <option value="10" >10</option>
    <option value="12" >12</option>
  </select>

  <div clear:both>
    <label for="numNa"> #Na: </label>
    <select id="numNa" name="numNa">
      <option value="0" selected>0</option>
      <option value="1" >1</option>
      <option value="2" >2</option>
    </select>

  <label for="numS"> #S: </label>
  <select id="numS" name="numS">
    <option value="0" selected>0</option>
    <option value="2" >2</option>
  </select>

  <label for="numCl"> #Cl: </label>
  <select id="numCl" name="numCl">
    <option value="0" selected>0</option>
    <option value="2" >2</option>
  </select>
     
  </div>
    
  <div clear:both>
      <label for="Charge">Charge:</label>
      <select id="charge" name="charge">
      <option value="-1">-1</option>
      <option value="0" >0</option>
      <option value="1" selected>+1</option>
      </select>
  </div>
  
  <div clear:both>
      <label for="ppm">Mass Tolerance:</label>
      <select id="ppm" name="ppm">
      <option value="0.1">0.1 ppm</option>
      <option value="0.2" >0.2 ppm</option>
      <option value="0.5" selected>0.5 ppm</option>
      <option value="1">1 ppm</option>
      <option value="2" >2 ppm</option>
      <option value="5">5 ppm</option>
      <option value="10" >10 ppm</option>
      </select>
  </div>

  </form>


<div>
<button onclick="calculateFormulas()">Calculate Possible Formulas</button>

<p id="result"></p>
</div>

</body>
</html>


<script>

 function molecularFormulasWithinTolerance(measuredMass, charge, tolerance) {
  // Define atomic masses
  const atomicMasses = {
    H: 1.007825,
    C: 12.000000,
    N: 14.003074,
    O: 15.994915,
    Na: 22.989770,
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
  
 	// Number of atoms
  const maxC = document.getElementById('numC').value;
  const maxH = document.getElementById('numH').value;
  const maxN = document.getElementById('numN').value;
  const maxO = document.getElementById('numO').value;
  const maxNa = document.getElementById('numNa').value;
  const maxS = document.getElementById('numS').value;
  const maxCl = document.getElementById('numCl').value;
  

  // Iterate through possible combinations
  for (let c = 0; c <= maxC; c++) {
    for (let h = 0; h <= maxH; h++) {
      for (let n = 0; n <= maxN; n++) {
        for (let o = 0; o <= maxO; o++) {
        	if (o / c < 2 && n / c < 2 && h/c > 0.2) {
            for (let cl = 0; cl <= maxCl; cl++) {
              for (let na = 0; na <= maxNa; na++) {
                const formula = { C: c, H: h, N: n, O: o, Cl: cl, Na: na };
                const formulaMass = calculateMolecularMass(formula) - charge * 5.48579909065e-4;
                const massError = 1000000*(measuredMass - formulaMass) / formulaMass;

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

// Main function that is called by the webpage.
function calculateFormulas() {
	document.getElementById('result').innerHTML = "" // initialize result string
	const measuredMass = document.getElementById('inputMass').value;  // Mass from user
  const charge = document.getElementById('charge').value;   // Charge from user
  const massTolerance = document.getElementById('ppm').value; // Tolerance in ppm
  const [formulasWithinTolerance, differenceValues] = molecularFormulasWithinTolerance(measuredMass, charge, massTolerance); // Formulas and PPM error
  formulasWithinTolerance.forEach((formula, index) => {
  	const formulaString = Object.keys(formula)
    .filter(atom => formula[atom] !== 0)
    .map(atom => `${atom}${formula[atom]}`)
    .join(' ');
  	document.getElementById('result').innerHTML += `${index + 1}. ${formulaString}  ${differenceValues[index].toFixed(2)} ppm <br>`; // Print output line by line
    console.log(`${index + 1}. ${formulaString}  ${differenceValues[index].toFixed(2)} ppm <br>`);
	});

}




</script>
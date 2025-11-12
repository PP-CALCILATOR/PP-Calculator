<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PP Sheet Calculator</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #f5f7fa;
    color: #333;
    padding: 20px;
    max-width: 500px;
    margin: auto;
  }
  h1 {
    text-align: center;
  }
  label {
    display: block;
    margin-top: 10px;
    font-weight: bold;
  }
  input, select {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
    border-radius: 6px;
    border: 1px solid #ccc;
    font-size: 15px;
  }
  button {
    margin-top: 20px;
    padding: 10px;
    width: 100%;
    font-size: 16px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }
  button:hover {
    background: #0056b3;
  }
  #result {
    margin-top: 20px;
    background: white;
    padding: 15px;
    border-radius: 8px;
    text-align: center;
    box-shadow: 0 0 4px rgba(0,0,0,0.1);
  }
</style>
</head>
<body>

<div id="app" style="display:none;">
  <h1>PP Sheet Calculator</h1>
  <label>Length:</label>
  <input type="number" id="length" placeholder="Enter length">

  <label>Width:</label>
  <input type="number" id="width" placeholder="Enter width">

  <label>Unit:</label>
  <select id="unit">
    <option value="inch">Inches</option>
    <option value="cm">Centimeters</option>
  </select>

  <label>Thickness (micron):</label>
  <input type="number" id="thickness" value="180">

  <label>Density (g/cm³):</label>
  <input type="number" id="density" value="0.93" step="0.01">

  <label>Price per kg (₹):</label>
  <input type="number" id="pricePerKg" value="125">

  <button onclick="calculate()">Calculate</button>

  <div id="result"></div>
</div>

<script>
  // 🔐 Password protection
  const password = "pp123"; // <-- change this to your own password
  const entered = prompt("Enter password to access the PP Sheet Calculator:");
  if (entered === password) {
    document.getElementById("app").style.display = "block";
  } else {
    document.body.innerHTML = "<h2 style='text-align:center;color:red;'>Access Denied ❌</h2>";
  }

  // 📏 Calculator logic
  function calculate() {
    const length = parseFloat(document.getElementById("length").value);
    const width = parseFloat(document.getElementById("width").value);
    const unit = document.getElementById("unit").value;
    const thickness = parseFloat(document.getElementById("thickness").value);
    const density = parseFloat(document.getElementById("density").value);
    const pricePerKg = parseFloat(document.getElementById("pricePerKg").value);

    if (!length || !width || !thickness || !density || !pricePerKg) {
      alert("Please fill in all fields.");
      return;
    }

    // convert to cm
    let lengthCm = unit === "inch" ? length * 2.54 : length;
    let widthCm = unit === "inch" ? width * 2.54 : width;

    // thickness micron to cm
    let thicknessCm = thickness / 10000;

    // volume in cubic cm
    let volume = lengthCm * widthCm * thicknessCm;

    // weight in grams
    let weightG = volume * density;

    // weight in kg
    let weightKg = weightG / 1000;

    // price
    let price = weightKg * pricePerKg;

    document.getElementById("result").innerHTML = `
      <h3>Result</h3>
      <p><b>Weight:</b> ${weightKg.toFixed(4)} kg</p>
      <p><b>Price:</b> ₹${price.toFixed(2)}</p>
    `;
  }
</script>
</body>
</html>

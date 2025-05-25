<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Full Calculator</title>
  <style>
    body {
      background-color: #121212;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      font-family: 'Segoe UI', sans-serif;
    }

    .calculator {
      background: #1e1e1e;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.7);
      width: 340px;
    }

    .display {
      background: black;
      color: #00ffcc;
      font-size: 2em;
      text-align: right;
      padding: 15px;
      border-radius: 10px;
      margin-bottom: 20px;
      overflow-x: auto;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    button {
      padding: 20px;
      font-size: 1.2em;
      border: none;
      border-radius: 10px;
      background-color: #333;
      color: white;
      cursor: pointer;
      transition: 0.2s;
    }

    button:hover {
      background-color: #555;
    }

    .operator { background-color: #ff9500; }
    .operator:hover { background-color: #e27d00; }

    .equal { background-color: #28a745; }
    .equal:hover { background-color: #1f923a; }

    .clear { background-color: #dc3545; }
    .clear:hover { background-color: #c82333; }

    .function { background-color: #555; }
    .function:hover { background-color: #666; }
  </style>
</head>
<body>
  <div class="calculator">
    <div id="display" class="display">0</div>
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button class="function" onclick="backspace()">⌫</button>
      <button class="function" onclick="appendValue('%')">%</button>
      <button class="operator" onclick="appendValue('/')">÷</button>

      <button onclick="appendValue('7')">7</button>
      <button onclick="appendValue('8')">8</button>
      <button onclick="appendValue('9')">9</button>
      <button class="operator" onclick="appendValue('*')">×</button>

      <button onclick="appendValue('4')">4</button>
      <button onclick="appendValue('5')">5</button>
      <button onclick="appendValue('6')">6</button>
      <button class="operator" onclick="appendValue('-')">−</button>

      <button onclick="appendValue('1')">1</button>
      <button onclick="appendValue('2')">2</button>
      <button onclick="appendValue('3')">3</button>
      <button class="operator" onclick="appendValue('+')">+</button>

      <button onclick="appendValue('(')">(</button>
      <button onclick="appendValue('0')">0</button>
      <button onclick="appendValue(')')">)</button>
      <button onclick="appendValue('.')">.</button>

      <button class="function" onclick="toggleNegative()">+/-</button>
      <button class="equal" onclick="calculate()" style="grid-column: span 3;">=</button>
    </div>
  </div>

  <script>
    const display = document.getElementById("display");

    function appendValue(val) {
      if (display.textContent === "0" || display.textContent === "Error") {
        display.textContent = val;
      } else {
        display.textContent += val;
      }
    }

    function clearDisplay() {
      display.textContent = "0";
    }

    function backspace() {
      if (display.textContent.length > 1) {
        display.textContent = display.textContent.slice(0, -1);
      } else {
        display.textContent = "0";
      }
    }

    function toggleNegative() {
      try {
        const value = eval(display.textContent);
        display.textContent = -value;
      } catch {
        display.textContent = "Error";
      }
    }

    function calculate() {
      try {
        let expression = display.textContent;
        // Replace '%' with '/100'
        expression = expression.replace(/%/g, '/100');
        const result = eval(expression);
        display.textContent = result;
      } catch (error) {
        display.textContent = "Error";
      }
    }
  </script>
</body>
</html>

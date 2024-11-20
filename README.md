<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=375, initial-scale=1.0">
  <title>Identity Checker</title>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.6.0/css/all.min.css" rel="stylesheet">
  <style>
    body {
      background-color: #f0f8ff;
      font-family: Arial, Helvetica, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
      padding: 0;
    }

    .container {
      background-color: #ffffff;
      border: 4px solid #1aa8fa;
      border-radius: 20px;
      padding: 30px;
      text-align: center;
      width: 100%;
      max-width: 375px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
    }

    h1 {
      font-size: 20px;
      color: #1aa8fa;
    }

    .input-container {
      position: relative;
      margin-top: 20px;
    }

    .input-code {
      width: 100%;
      height: 40px;
      border: 2px solid #1aa8fa;
      border-radius: 10px;
      background-color: transparent;
      text-align: center;
      font-size: 24px;
      color: #00796b;
      padding: 5px;
      box-sizing: border-box;
      position: relative;
      z-index: 1;
      transition: border-color 0.2s, background-color 0.2s;
    }

    .input-code:focus {
      outline: none;
      border-color: #ff4081;
    }

    .input-label {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 18px;
      color: #00796b;
      pointer-events: none;
      transition: 0.2s;
      background-color: transparent;
      z-index: 0;
    }

    .input-code:focus + .input-label,
    .input-code:not(:placeholder-shown) + .input-label {
      top: -10px;
      left: 10px;
      font-size: 14px;
      color: #ff4081;
    }

    .keypad {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-gap: 15px;
      margin-top: 20px;
    }

    .key {
      background-color: #1aa8fa;
      border: 2px solid black;
      border-radius: 15px;
      padding: 15px;
      text-align: center;
      font-size: 20px;
      color: white;
      cursor: pointer;
      transition: background-color 0.3s, transform 0.1s;
    }

    .key:hover {
      background-color: #0091ea;
      transform: scale(1.05);
    }

    .key.gray {
      background-color: #d0cece;
      color: black;
    }

    .submit-btn {
      display: none;
    }

    #message {
      margin-top: 20px;
      font-size: 18px;
    }

    @media (max-width: 375px) {
      body {
        overflow: hidden;
      }

      .container {
        width: 100%;
        max-width: 375px;
      }

      .input-code {
        width: 120px;
      }

      .key {
        font-size: 18px;
        padding: 10px;
      }

      .input-label {
        font-size: 12px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Are you my babii?</h1>
    <div class="input-container">
      <input type="text" class="input-code" id="code" placeholder=" " readonly>
      <label class="input-label" id="inputLabel">enter passcode :></label>
    </div>
    <div class="keypad">
      <div class="key" onclick="addDigit('1')">1</div>
      <div class="key" onclick="addDigit('2')">2</div>
      <div class="key" onclick="addDigit('3')">3</div>
      <div class="key" onclick="addDigit('4')">4</div>
      <div class="key" onclick="addDigit('5')">5</div>
      <div class="key" onclick="addDigit('6')">6</div>
      <div class="key" onclick="addDigit('7')">7</div>
      <div class="key" onclick="addDigit('8')">8</div>
      <div class="key" onclick="addDigit('9')">9</div>
      <div class="key gray" onclick="deleteDigit()">Delete</div>
      <div class="key" onclick="addDigit('0')">0</div>
      <div class="key gray" onclick="checkCode()">Enter</div>
    </div>
    <p id="message"></p>
  </div>
  <script>
    const correctCode = "1127";

    function addDigit(digit) {
      const codeInput = document.getElementById("code");
      const inputLabel = document.getElementById("inputLabel");
      codeInput.style.backgroundColor = "#e0f7fa"; 

      if (codeInput.value.length < 4) {
        codeInput.value += digit;

        if (codeInput.value.length === 1) {
          inputLabel.style.display = "none";
        }
        inputLabel.textContent = codeInput.value;
      }
    }

    function deleteDigit() {
      const codeInput = document.getElementById("code");
      const inputLabel = document.getElementById("inputLabel");

      if (codeInput.value.length > 0) {
        codeInput.value = codeInput.value.slice(0, -1);
        inputLabel.textContent = codeInput.value;
      }

      if (codeInput.value.length === 0) {
        inputLabel.style.display = "block"; 
        inputLabel.textContent = "enter passcode :>";
        codeInput.style.backgroundColor = "transparent"; 
      }
    }

    function checkCode() {
      const codeInput = document.getElementById("code").value;
      const message = document.getElementById("message");
      const inputLabel = document.getElementById("inputLabel");

      if (codeInput === correctCode) {
        message.textContent = "Access Granted!";
        message.style.color = "dark green";
        setTimeout(() => {
          window.location.href = "success.html";
        }, 1000);
      } else {
        message.textContent = "Incorrect Code.";
        message.style.color = "red";
      }

      document.getElementById("code").value = "";
      inputLabel.style.display = "block";
      inputLabel.textContent = "enter passcode :>";
      inputLabel.style.backgroundColor = "transparent";
      codeInput.style.backgroundColor = "transparent";
    }

    document.addEventListener("keydown", function(event) {
      if (event.key === "Enter") {
        checkCode();
      }
    });
  </script>
</body>
</html>

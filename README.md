<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PORTIER TECNOLOGÍA - Generador FC ID</title>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700&display=swap" rel="stylesheet">
  <link href="https://fonts.cdnfonts.com/css/digital-7" rel="stylesheet">
  <style>
    :root {
      --neon-green: #00FF87;
      --neon-blue: #00D1FF;
      --neon-purple: #AD00FF;
      --dark-bg: #0A0A12;
      --panel-bg: rgba(20, 20, 30, 0.9);
    }
    
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    
    body {
      font-family: 'Orbitron', sans-serif;
      background: var(--dark-bg);
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      padding: 15px;
      overflow-x: hidden;
      touch-action: manipulation;
      background-image: 
        radial-gradient(circle at 10% 20%, rgba(0, 209, 255, 0.05) 0%, transparent 20%),
        radial-gradient(circle at 90% 80%, rgba(173, 0, 255, 0.05) 0%, transparent 20%);
    }
    
    .container {
      width: 100%;
      max-width: 340px;
      margin: 0 auto;
    }

    header {
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 20px;
      text-align: center;
      position: relative;
    }

    .logo {
      width: 50px;
      height: 50px;
      background: linear-gradient(135deg, var(--neon-purple), var(--neon-blue));
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-right: 12px;
      box-shadow: 0 0 15px var(--neon-purple);
    }

    .logo span {
      font-size: 24px;
      font-weight: bold;
      color: white;
    }

    .brand {
      display: flex;
      flex-direction: column;
    }

    h1 {
      font-size: 18px;
      background: linear-gradient(to right, var(--neon-blue), var(--neon-green));
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      text-shadow: 0 0 8px rgba(0, 209, 255, 0.4);
      letter-spacing: 1px;
    }

    .subtitle {
      font-size: 11px;
      color: rgba(255, 255, 255, 0.6);
      margin-top: 2px;
      letter-spacing: 0.5px;
    }

    .app-container {
      background: var(--panel-bg);
      border-radius: 16px;
      padding: 20px;
      box-shadow: 
        0 0 20px rgba(0, 255, 135, 0.15),
        0 0 30px rgba(0, 209, 255, 0.1);
      border: 1px solid rgba(0, 255, 135, 0.15);
      position: relative;
      overflow: hidden;
    }
    
    .app-container::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 3px;
      background: linear-gradient(to right, var(--neon-purple), var(--neon-blue), var(--neon-green));
      box-shadow: 0 0 10px rgba(0, 255, 135, 0.5);
    }

    #display {
      font-family: 'Digital-7', monospace;
      background: rgba(0, 0, 0, 0.7);
      color: var(--neon-green);
      font-size: 32px;
      padding: 15px 10px;
      border-radius: 10px;
      text-align: center;
      margin-bottom: 20px;
      letter-spacing: 2px;
      box-shadow: 
        inset 0 0 8px rgba(0, 0, 0, 0.7), 
        0 0 15px var(--neon-green);
      border: 1px solid var(--neon-green);
      text-shadow: 0 0 8px var(--neon-green);
      height: 70px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .mode-display {
      color: var(--neon-blue);
      text-align: center;
      margin-bottom: 18px;
      font-size: 14px;
      text-shadow: 0 0 3px var(--neon-blue);
      letter-spacing: 0.5px;
    }

    .keyboard {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin-bottom: 15px;
    }

    .keyboard button {
      aspect-ratio: 1/1;
      font-size: 22px;
      font-weight: 500;
      background: rgba(30, 30, 45, 0.9);
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: all 0.15s;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
      position: relative;
      overflow: hidden;
      outline: none;
      font-family: 'Orbitron', sans-serif;
    }

    .keyboard button:hover, .keyboard button:focus {
      background: rgba(50, 50, 70, 0.9);
      transform: translateY(-2px);
    }

    .keyboard button:active {
      transform: translateY(1px);
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
    }

    .keyboard button::after {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at center, rgba(255,255,255,0.3) 0%, transparent 70%);
      opacity: 0;
      transition: opacity 0.2s;
    }

    .keyboard button:active::after {
      opacity: 1;
    }

    .action-buttons {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-top: 5px;
    }

    .action-buttons button {
      padding: 12px 5px;
      font-size: 15px;
      font-weight: 500;
      border-radius: 10px;
      border: none;
      cursor: pointer;
      transition: all 0.2s;
      font-family: 'Orbitron', sans-serif;
      letter-spacing: 0.5px;
    }

    #clear-btn {
      background: rgba(255, 50, 50, 0.25);
      color: #FF7777;
      border: 1px solid #FF5555;
      box-shadow: 0 0 8px rgba(255, 50, 50, 0.2);
    }

    #clear-btn:hover {
      background: rgba(255, 50, 50, 0.35);
      box-shadow: 0 0 12px rgba(255, 50, 50, 0.3);
    }

    #generate-btn {
      background: rgba(0, 255, 135, 0.25);
      color: var(--neon-green);
      border: 1px solid var(--neon-green);
      box-shadow: 0 0 8px rgba(0, 255, 135, 0.2);
    }

    #generate-btn:hover {
      background: rgba(0, 255, 135, 0.35);
      box-shadow: 0 0 12px rgba(0, 255, 135, 0.3);
    }

    .instructions {
      margin-top: 20px;
      color: rgba(255, 255, 255, 0.65);
      font-size: 12px;
      text-align: center;
      line-height: 1.5;
      padding: 0 10px;
    }

    .instructions p {
      margin-bottom: 5px;
    }

    footer {
      margin-top: 25px;
      color: rgba(255, 255, 255, 0.4);
      font-size: 10px;
      text-align: center;
      padding: 0 15px;
    }

    .particle {
      position: absolute;
      background: var(--neon-green);
      border-radius: 50%;
      pointer-events: none;
      z-index: -1;
      opacity: 0;
      animation: float 15s linear infinite;
    }

    @keyframes float {
      0% {
        transform: translateY(100vh) translateX(0);
        opacity: 0.1;
      }
      10% {
        opacity: 0.3;
      }
      90% {
        opacity: 0.2;
      }
      100% {
        transform: translateY(-20vh) translateX(20px);
        opacity: 0;
      }
    }
    
    @keyframes pulse {
      0% { box-shadow: 0 0 10px var(--neon-green); }
      50% { box-shadow: 0 0 20px var(--neon-green); }
      100% { box-shadow: 0 0 10px var(--neon-green); }
    }

    @media (max-width: 380px) {
      .app-container {
        padding: 15px;
      }
      
      #display {
        font-size: 28px;
        height: 65px;
      }
      
      .keyboard button {
        font-size: 20px;
      }
      
      .action-buttons button {
        font-size: 14px;
        padding: 10px 5px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="logo">
        <span>P</span>
      </div>
      <div class="brand">
        <h1>PORTIER TECNOLOGÍA</h1>
        <div class="subtitle">GENERADOR FC ID</div>
      </div>
    </header>

    <div class="app-container">
      <div id="display">--------</div>
      <div class="mode-display" id="mode-display">Ingrese FC (1-255)</div>

      <div class="keyboard">
        <button onclick="press('1')">1</button>
        <button onclick="press('2')">2</button>
        <button onclick="press('3')">3</button>
        <button onclick="press('4')">4</button>
        <button onclick="press('5')">5</button>
        <button onclick="press('6')">6</button>
        <button onclick="press('7')">7</button>
        <button onclick="press('8')">8</button>
        <button onclick="press('9')">9</button>
        <button onclick="press('*')">*</button>
        <button onclick="press('0')">0</button>
        <button onclick="press('#')">#</button>
      </div>

      <div class="action-buttons">
        <button id="clear-btn" onclick="clearDisplay()">LIMPIAR</button>
        <button id="generate-btn" onclick="generateCode()">GENERAR</button>
      </div>

      <div class="instructions">
        <p>1. Ingrese el FC (1-255) y presione GENERAR</p>
        <p>2. Ingrese el ID (1-16,777,215)</p>
        <p>3. Presione GENERAR para obtener el código de 8 dígitos</p>
      </div>
    </div>

    <footer>
      © 2024 PORTIER TECNOLOGÍA - Sistema Generador de Códigos FC ID
    </footer>
  </div>

  <!-- Audio elements for sound effects -->
  <audio id="keySound" preload="auto"></audio>
  <audio id="enterSound" preload="auto"></audio>
  <audio id="errorSound" preload="auto"></audio>
  <audio id="successSound" preload="auto"></audio>

  <script>
    // Audio data for sound effects (base64 encoded)
    const soundData = {
      key: "data:audio/mp3;base64,SUQzBAAAAAABEVRYWFgAAAAtAAADY29tbWVudABCaWdTb3VuZEJhbmsuY29tIC8gTGFTb25vdGhlcXVlLm9yZwBURU5DAAAAAQAAA1tMaW5rQ29tLm9yZwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

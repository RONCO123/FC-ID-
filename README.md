<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PORTIER TECNOLOGIA - Decodificador</title>
  <link href="https://fonts.cdnfonts.com/css/digital-7" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom, #000000, #1a1a1a);
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px;
      height: 100vh;
      box-sizing: border-box;
    }

    h1 {
      font-size: 5vw;
      margin-bottom: 10px;
      color: #00ffcc;
      text-align: center;
    }

    #display {
      font-family: 'Digital-7', monospace;
      background: black;
      color: #00ff00;
      font-size: 6vw;
      padding: 20px;
      border-radius: 10px;
      text-align: center;
      width: 100%;
      max-width: 400px;
      box-shadow: 0 0 20px #00ff00;
      margin-bottom: 10px;
      min-height: 70px;
      box-sizing: border-box;
    }

    .teclado {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 15px;
      width: 100%;
      max-width: 400px;
    }

    .teclado button {
      font-size: 6vw;
      padding: 20px;
      border: none;
      border-radius: 10px;
      background-color: #333;
      color: white;
      box-shadow: 0 4px 10px rgba(0,0,0,0.4);
      cursor: pointer;
      transition: background-color 0.2s;
    }

    .teclado button:hover {
      background-color: #555;
    }

    .modo {
      margin-top: 5px;
      font-size: 4vw;
      color: #ccc;
      text-align: center;
    }

    @media (min-width: 768px) {
      h1 {
        font-size: 24px;
      }

      #display {
        font-size: 40px;
      }

      .teclado button {
        font-size: 24px;
      }

      .modo {
        font-size: 16px;
      }
    }
  </style>
</head>
<body>
  <h1>PORTIER TECNOLOGIA</h1>
  <div id="display">------</div>
  <div class="modo" id="modo">Ingresar código completo...</div>

  <div class="teclado">
    <button onclick="presionar('1')">1</button>
    <button onclick="presionar('2')">2</button>
    <button onclick="presionar('3')">3</button>
    <button onclick="presionar('4')">4</button>
    <button onclick="presionar('5')">5</button>
    <button onclick="presionar('6')">6</button>
    <button onclick="presionar('7')">7</button>
    <button onclick="presionar('8')">8</button>
    <button onclick="presionar('9')">9</button>
    <button onclick="borrar()">*</button>
    <button onclick="presionar('0')">0</button>
    <button onclick="decodificar()">#</button>
  </div>

  <script>
    let codigo = '';
    const display = document.getElementById('display');
    const modoTexto = document.getElementById('modo');

    function presionar(valor) {
      if (codigo.length < 8) {
        codigo += valor;
        display.innerText = "CÓDIGO: " + codigo;
      }
    }

    function borrar() {
      codigo = '';
      display.innerText = '------';
      modoTexto.innerText = 'Ingresar código completo...';
    }

    function decodificar() {
      if (codigo === '' || isNaN(parseInt(codigo))) {
        display.innerText = 'ERR CODE';
        return;
      }

      const bin = parseInt(codigo).toString(2).padStart(24, '0');
      const binFC = bin.substring(0, 8);
      const binID = bin.substring(8);

      const fc = parseInt(binFC, 2);
      const id = parseInt(binID, 2);

      display.innerText = "FC: " + fc + " | ID: " + id;
      modoTexto.innerText = 'Código decodificado';
    }
  </script>
</body>
</html>
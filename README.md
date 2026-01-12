[index.html.html](https://github.com/user-attachments/files/24573352/index.html.html)
CALCULADORA SAGAZ MOTORS
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Simulador de Economia – Moto Elétrica | Sagaz Motors</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #ffffff;
    }
    .box {
      background: #111;
      padding: 24px;
      border-radius: 16px;
      max-width: 420px;
      width: 100%;
      box-shadow: 0 12px 30px rgba(0,0,0,0.6);
    }
    h1 {
      text-align: center;
      font-size: 1.4rem;
      margin-bottom: 6px;
    }
    .subtitle {
      text-align: center;
      font-size: 0.9rem;
      opacity: 0.8;
      margin-bottom: 20px;
    }
    label {
      font-size: 0.85rem;
      margin-top: 12px;
      display: block;
    }
    input {
      width: 100%;
      padding: 10px;
      margin-top: 6px;
      border-radius: 8px;
      border: none;
      outline: none;
    }
    button {
      width: 100%;
      margin-top: 20px;
      padding: 12px;
      border-radius: 10px;
      border: none;
      background: #00e676;
      color: #000;
      font-size: 1rem;
      font-weight: bold;
      cursor: pointer;
    }
    button:hover { background: #00c853; }
    .result {
      display: none;
      margin-top: 20px;
      background: #1c1c1c;
      padding: 16px;
      border-radius: 12px;
    }
    .result h2 {
      color: #00e676;
      font-size: 1.1rem;
      margin-bottom: 10px;
    }
    .result p {
      font-size: 0.9rem;
      margin: 6px 0;
    }
    .cta {
      margin-top: 14px;
      background: #00e676;
      color: #000;
      padding: 12px;
      text-align: center;
      border-radius: 10px;
      font-weight: bold;
      text-decoration: none;
      display: block;
    }
  </style>
</head>
<body>
  <div class="box">
    <h1>Simulador de Economia</h1>
    <div class="subtitle">Moto Elétrica 1000W • Sagaz Motors</div>

    <label>Quantos km você roda por dia?</label>
    <input type="number" id="kmDia" placeholder="Ex: 30" />

    <label>Preço da gasolina (R$/litro)</label>
    <input type="number" id="precoComb" placeholder="Ex: 6.00" />

    <label>Consumo da moto atual (km por litro)</label>
    <input type="number" id="kmLitro" placeholder="Ex: 35" />

    <label>Preço do kWh de energia (R$)</label>
    <input type="number" id="precoKwh" placeholder="Ex: 0.90" />

    <button onclick="calcular()">Calcular Economia</button>

    <div class="result" id="resultado">
      <h2>Resultado Mensal</h2>
      <p id="combustao"></p>
      <p id="eletrica"></p>
      <p id="economia"></p>

      <a class="cta" href="https://wa.me/5521972871998?text=Olá!%20Fiz%20a%20simulação%20no%20site%20da%20Sagaz%20Motors%20e%20quero%20fazer%20um%20test%20drive%20da%20moto%20elétrica" target="_blank">
        Falar com a Sagaz Motors no WhatsApp
      </a>
    </div>
  </div>

  <script>
    function calcular() {
      const kmDia = Number(document.getElementById('kmDia').value);
      const precoComb = Number(document.getElementById('precoComb').value);
      const kmLitro = Number(document.getElementById('kmLitro').value);
      const precoKwh = Number(document.getElementById('precoKwh').value);

      if (!kmDia || !precoComb || !kmLitro || !precoKwh) {
        alert('Preencha todos os campos corretamente');
        return;
      }

      const kmMes = kmDia * 30;

      const litrosMes = kmMes / kmLitro;
      const custoComb = litrosMes * precoComb;

      // Moto elétrica 1000W: média 1 kWh a cada 40 km
      const kwhMes = kmMes / 40;
      const custoEletrico = kwhMes * precoKwh;

      const economia = custoComb - custoEletrico;

      document.getElementById('combustao').innerText = `Gasto mensal com gasolina: R$ ${custoComb.toFixed(2)}`;
      document.getElementById('eletrica').innerText = `Gasto mensal com elétrica 1000W: R$ ${custoEletrico.toFixed(2)}`;
      document.getElementById('economia').innerText = `Economia mensal: R$ ${economia.toFixed(2)}`;

      document.getElementById('resultado').style.display = 'block';
    }
  </script>
</body>
</html>

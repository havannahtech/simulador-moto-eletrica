
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sagaz Motors | Simulador Moto Elétrica</title>
  <style>
    *{box-sizing:border-box}
    body{
      font-family:Arial,Helvetica,sans-serif;
      background:linear-gradient(135deg,#000,#1a1a1a);
      color:#f1f1f1;
      padding:20px;
      margin:0
    }
    .container{
      max-width:900px; /* melhor aproveitamento em tablets */
      margin:auto;
      background:#0b0b0b;
      padding:24px;
      border-radius:18px;
      box-shadow:0 0 30px rgba(255,0,0,.35)
    }
    .header{text-align:center;margin-bottom:24px}
    .header img{
      max-width:180px;
      width:100%;
      height:auto;
      background:transparent; /* garante fundo transparente */
    }
    h1{color:#e11d48;margin-top:10px;font-size:1.6rem}
    .subtitle{text-align:center;font-size:.95rem;opacity:.8;margin-bottom:20px}

    label{font-size:13px;color:#cbd5e1;display:block;margin-top:14px}
    input{
      width:100%;
      padding:14px;
      border-radius:10px;
      border:none;
      font-size:16px;
      margin-top:6px
    }

    .row{
      display:grid;
      grid-template-columns:repeat(auto-fit, minmax(260px, 1fr));
      gap:16px;
    }
    .col{flex:1;min-width:220px}

    .btn-row{
      display:grid;
      grid-template-columns:repeat(auto-fit, minmax(240px, 1fr));
      gap:14px;
      margin-top:22px
    }
    button,.btn-link{
      flex:1;
      min-width:220px;
      background:#e11d48;
      color:#fff;
      border:none;
      padding:14px;
      border-radius:12px;
      font-size:14px;
      font-weight:bold;
      cursor:pointer;
      text-align:center;
      text-decoration:none
    }
    button:hover,.btn-link:hover{background:#be123c}

    .result{
      display:none;
      margin-top:24px;
      background:#111827;
      padding:20px;
      border-radius:14px
    }
    .result h2{color:#e11d48;font-size:1.2rem;margin-bottom:12px}
    .result p{font-size:1rem;margin:8px 0}

    .cta-link{
      display:block;
      text-align:center;
      margin-top:18px;
      padding:14px;
      border-radius:12px;
      background:#16a34a;
      color:#fff;
      text-decoration:none;
      font-weight:bold
    }
    .cta-link:hover{background:#15803d}

    /* Ajustes específicos para tablets */
    @media (max-width: 1024px){
      h1{font-size:1.4rem}
      .container{padding:20px;max-width:100%}
    }
      .container{padding:20px}
    }

    /* Ajustes para celulares */
    @media (max-width: 600px){
      body{padding:10px}
      h1{font-size:1.25rem}
      .header img{max-width:150px}
      input,button,.btn-link{font-size:15px;padding:14px}
    }
      h1{font-size:1.3rem}
    }
  </style>
</head>
<body>
<div class="container">
  <div class="header">
    <!-- Use PNG ou SVG com fundo transparente -->
    <img src="logo.png" alt="Sagaz Motors" />
    <h1>Simulador Moto Elétrica</h1>
    <div class="subtitle">Economia mensal • Sagaz Motors</div>
  </div>

  <div class="row">
    <div class="col">
      <label>Nome</label>
      <input type="text" id="nome" placeholder="Digite seu nome" />
    </div>
    <div class="col">
      <label>WhatsApp</label>
      <input type="tel" id="whatsapp" placeholder="DDD + número" />
    </div>
  </div>

  <label>Quantos km você roda por dia?</label>
  <input type="number" id="kmDia" placeholder="Ex: 30" />

  <input type="hidden" id="precoGas" value="6.20" />

  <label>Consumo da moto atual (km/l)</label>
  <input type="number" id="kmLitro" placeholder="Ex: 35" />

  <input type="hidden" id="precoKwh" value="0.90" />

  <div class="btn-row">
    <button onclick="calcular()">Calcular Economia</button>
    <a href="https://havannahtech.github.io/PARCELAMENTO-SAGAZ-MOTORS/" target="_blank" class="btn-link">Valor das Parcelas</a>
    <a href="https://wa.me/c/5521972871998" target="_blank" class="btn-link">Preços</a>
  </div>

  <div class="result" id="resultado">
    <h2>Resultado Mensal</h2>
    <p id="gasolina"></p>
    <p id="eletrica"></p>
    <p id="economia"></p>
    <p id="payback"></p>

    <a id="whatsLink" class="cta-link" target="_blank">Enviar resultado para a Sagaz Motors</a>
  </div>
</div>

<script>
function calcular(){
  const nome = document.getElementById('nome').value.trim();
  const whatsapp = document.getElementById('whatsapp').value.replace(/\D/g,'');
  const kmDia = Number(document.getElementById('kmDia').value);
  const precoGas = Number(document.getElementById('precoGas').value);
  const kmLitro = Number(document.getElementById('kmLitro').value);
  const precoKwh = Number(document.getElementById('precoKwh').value);

  if(!nome || !whatsapp || !kmDia || !kmLitro){
    alert('Preencha todos os campos corretamente');
    return;
  }

  const kmMes = kmDia * 30;
  const litrosMes = kmMes / kmLitro;
  const custoGas = litrosMes * precoGas;

  // Média: 1 kWh a cada 40 km
  const kwhMes = kmMes / 40;
  const custoEletrico = kwhMes * precoKwh;

  const economia = custoGas - custoEletrico;
  const valorMoto = 9000;
  const payback = economia > 0 ? (valorMoto / economia) : 0;

  document.getElementById('gasolina').innerText = `Gasto mensal com gasolina: R$ ${custoGas.toFixed(2)}`;
  document.getElementById('eletrica').innerText = `Gasto mensal com elétrica: R$ ${custoEletrico.toFixed(2)}`;
  document.getElementById('economia').innerText = `Economia mensal estimada: R$ ${economia.toFixed(2)}`;
  document.getElementById('payback').innerText = `Payback aproximado: ${payback.toFixed(1)} meses`;

  const numero = whatsapp.startsWith('55') ? whatsapp : '55' + whatsapp;
  const mensagem = `Olá, Sagaz Motors!%0A%0A`+
    `Simulação de economia – Moto Elétrica%0A%0A`+
    `Nome: ${encodeURIComponent(nome)}%0A`+
    `Gasto mensal com gasolina: R$ ${custoGas.toFixed(2)}%0A`+
    `Gasto mensal com elétrica: R$ ${custoEletrico.toFixed(2)}%0A`+
    `Economia mensal: R$ ${economia.toFixed(2)}%0A%0A`+
    `Gostaria de mais informações.`;

  document.getElementById('whatsLink').href = `https://wa.me/5521972871998?text=${mensagem}`;
  document.getElementById('resultado').style.display = 'block';
}
</script>
</body>
</html>

<SIMULADOR ECONOMIA SAGAZ MOTORS>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sagaz Motors | Simulador Moto Elétrica</title>
  <style>
    body{font-family:Arial,sans-serif;background:linear-gradient(135deg,#000,#1a1a1a);color:#f1f1f1;padding:20px}
    .container{max-width:520px;margin:auto;background:#0b0b0b;padding:30px;border-radius:18px;box-shadow:0 0 30px rgba(255,0,0,.35)}
    .header{text-align:center;margin-bottom:20px}
    .header img{max-width:200px}
    h1{color:#e11d48;margin-top:10px;font-size:1.4rem}
    .subtitle{text-align:center;font-size:.9rem;opacity:.8;margin-bottom:18px}
    label{font-size:13px;color:#cbd5e1;display:block;margin-top:12px}
    input{width:100%;padding:14px;border-radius:10px;border:none;font-size:16px;margin-top:6px}
    button{background:#e11d48;color:#fff;border:none;padding:12px;border-radius:12px;font-size:14px;cursor:pointer;width:32%} .btn-row{display:flex;gap:2%;margin-top:18px} .btn-link{display:flex;align-items:center;justify-content:center;background:#e11d48;color:#fff;border-radius:12px;font-size:14px;font-weight:bold;text-decoration:none;width:32%} .btn-link:hover{background:#be123c}
    button:hover{background:#be123c}
    .result{display:none;margin-top:20px;background:#111827;padding:18px;border-radius:14px}
    .result h2{color:#e11d48;font-size:1.1rem;margin-bottom:10px}
    .result p{font-size:.95rem;margin:6px 0}
    .cta-link{display:block;text-align:center;margin-top:16px;padding:12px;border-radius:12px;background:#16a34a;color:#fff;text-decoration:none;font-weight:bold}
    .cta-link:hover{background:#15803d}
    .secondary-link{display:block;text-align:center;margin-top:12px;font-size:.9rem;color:#cbd5e1;text-decoration:underline}
  </style>
</head>
<body>
<div class="container">
  <div class="header">
    <img src="logo.png" alt="Sagaz Motors" />
    <h1>Simulador Moto Elétrica</h1>
    <div class="subtitle">Economia mensal • Sagaz Motors</div>
  </div>

  <div style="display:flex;gap:10px">
  <div style="flex:1">
    <label>Nome</label>
    <input type="text" id="nome" placeholder="Digite seu nome" />
  </div>
  <div style="flex:1">
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
    <a href="https://wa.me/c/5521972871998" target="_blank" class="btn-link">Catálogo de Preços</a>
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

  if(!nome || !whatsapp || !kmDia || !precoGas || !kmLitro || !precoKwh){
    alert('Preencha todos os campos corretamente');
    return;
  }

  const kmMes = kmDia * 30;
  const litrosMes = kmMes / kmLitro;
  const custoGas = litrosMes * precoGas;

  // Média: 1 kWh a cada 40 km (moto elétrica)
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

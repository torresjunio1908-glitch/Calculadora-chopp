# Calculadora-chopp
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Calculadora de Chopp - Sinhô Chopp</title>
<style>
  body {
    font-family: Arial, sans-serif;
    padding: 20px;
    max-width: 500px;
    margin: auto;
    background: #f2c800;
  }
  h2 {
    text-align: center;
    margin-bottom: 20px;
  }
  label {
    font-weight: bold;
    margin-top: 10px;
    display: block;
  }
  input, select {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    border-radius: 6px;
    border: 1px solid #ccc;
  }
  button {
    width: 100%;
    margin-top: 20px;
    padding: 12px;
    background: #c49b3a;
    border: none;
    color: white;
    font-weight: bold;
    border-radius: 6px;
    cursor: pointer;
  }
  #resultado {
    background: white;
    padding: 15px;
    border-radius: 6px;
    margin-top: 20px;
    border: 1px solid #ddd;
  }
</style>
</head>
<body style="background:#f2c800;">
<div style="text-align:center; margin-bottom:20px;">
  <img src="logo.png" alt="Logo Sinhô Chopp" style="width:140px;" />
</div>
<h2>Calculadora de Chopp</h2>

<label>Quantidade de convidados:</label>
<input type="number" id="convidados" placeholder="Ex: 40" />

<label>Tempo de festa (horas):</label>
<input type="number" id="horas" placeholder="Ex: 5" />

<label>Perfil de consumo:</label>
<select id="perfil">
  <option value="social">Social</option>
  <option value="moderado" selected>Moderado</option>
  <option value="exagerado">Exagerado</option>
</select>

<button onclick="calcular()">Calcular quantidade ideal</button>

<div id="resultado"></div>

<script>
function calcular() {
  const convidados = parseInt(document.getElementById("convidados").value);
  const horas = parseInt(document.getElementById("horas").value);
  const perfil = document.getElementById("perfil").value;

  if (!convidados || !horas) {
    document.getElementById("resultado").innerHTML = "Preencha todos os campos!";
    return;
  }

  // consumo base por perfil (litros por pessoa por hora)
  let consumoHora;

  if (perfil === "social") consumoHora = 0.4;
  if (perfil === "moderado") consumoHora = 0.6;
  if (perfil === "exagerado") consumoHora = 1.0;

  const totalLitros = convidados * consumoHora * horas;

  // cálculo de barris (padrão do usuário)
  const pessoasPor30 = perfil === "moderado" ? 11 : (30 / (consumoHora * horas));
  const pessoasPor50 = perfil === "moderado" ? 22 : (50 / (consumoHora * horas));

  const barris30 = Math.ceil(convidados / pessoasPor30);
  const barris50 = Math.ceil(convidados / pessoasPor50);

  document.getElementById("resultado").innerHTML = `
    <h3>Resultado:</h3>
    <p><strong>Total estimado de chopp:</strong> ${totalLitros.toFixed(1)} litros</p>
    <p><strong>Se usar barril de 30L:</strong> ${barris30} barril(is)</p>
    <p><strong>Se usar barril de 50L:</strong> ${barris50} barril(is)</p>
  `;
}
</script>

</body>
</html>

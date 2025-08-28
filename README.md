<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Calculadora de SRI</title>
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#0077b6">
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; background: #f7f7f7; }
    h1 { text-align: center; }
    .card { background: #fff; padding: 20px; margin-bottom: 20px; border-radius: 10px; box-shadow: 0 2px 6px rgba(0,0,0,0.2); }
    label { font-weight: bold; }
    input { padding: 6px; margin: 10px 0; width: 100px; }
    table { width: 100%; border-collapse: collapse; margin-top: 15px; }
    th, td { border: 1px solid #ddd; padding: 8px; text-align: center; }
    th { background: #0077b6; color: white; }
  </style>
</head>
<body>
  <h1>Calculadora de SRI por Peso</h1>
  <div class="card">
    <label for="peso">Peso do paciente (kg):</label>
    <input type="number" id="peso" min="30" max="200" value="70">
    <button onclick="calcular()">Calcular</button>
  </div>
  <div class="card" id="resultado"></div>

  <script>
    function calcular() {
      const peso = parseFloat(document.getElementById("peso").value);
      const drogas = [
        { nome: "Fentanil (50 mcg/mL)", dose: 2, unidade: "mcg/kg", conc: 50 },
        { nome: "Lidocaína (20 mg/mL)", dose: 1.5, unidade: "mg/kg", conc: 20 },
        { nome: "Etomidato (2 mg/mL)", dose: 0.3, unidade: "mg/kg", conc: 2 },
        { nome: "Cetamina (50 mg/mL)", dose: 1.5, unidade: "mg/kg", conc: 50 },
        { nome: "Propofol (10 mg/mL)", dose: 1.5, unidade: "mg/kg", conc: 10 },
        { nome: "Midazolam (5 mg/mL)", dose: 0.2, unidade: "mg/kg", conc: 5 },
        { nome: "Succinilcolina (10 mg/mL)", dose: 1.5, unidade: "mg/kg", conc: 10 },
        { nome: "Rocurônio (10 mg/mL)", dose: 1.2, unidade: "mg/kg", conc: 10 }
      ];
      let tabela = "<table><tr><th>Droga</th><th>Dose</th><th>Volume (mL)</th></tr>";
      drogas.forEach(d => {
        const doseTotal = d.dose * peso;
        const volume = doseTotal / d.conc;
        tabela += `<tr><td>${d.nome}</td><td>${doseTotal.toFixed(2)} ${d.unidade}</td><td>${volume.toFixed(2)} mL</td></tr>`;
      });
      tabela += "</table>";
      document.getElementById("resultado").innerHTML = tabela;
    }

    // registra o service worker para rodar offline
    if ("serviceWorker" in navigator) {
      navigator.serviceWorker.register("service-worker.js");
    }
  </script>
</body>
</html>

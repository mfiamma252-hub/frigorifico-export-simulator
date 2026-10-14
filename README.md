<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador de Costos de Exportación - Frigorífico B2B</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f6f9;
            color: #333;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: #fff;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #b30000;
            text-align: center;
            font-size: 24px;
        }
        .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 30px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        label {
            display: block;
            font-weight: bold;
            margin-bottom: 5px;
        }
        select, input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
        }
        button {
            background-color: #b30000;
            color: white;
            border: none;
            padding: 12px;
            width: 100%;
            font-size: 18px;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 10px;
        }
        button:hover {
            background-color: #990000;
        }
        .results {
            margin-top: 30px;
            background: #eef2f7;
            padding: 20px;
            border-radius: 6px;
            display: none;
        }
        .results h3 {
            margin-top: 0;
            color: #333;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Simulador de Costos de Exportación (B2B)</h1>
    <div class="subtitle">Gestión Logística y Arancelaria - Carne Avícola</div>

    <div class="form-group">
        <label for="destino">Destino de Exportación:</label>
        <select id="destino">
            <option value="brasil">Brasil (Mercosur - Arancel 0%)</option>
            <option value="hongkong">Hong Kong / China</option>
        </select>
    </div>

    <div class="form-group">
        <label for="corte">Tipo de Corte Avícola:</label>
        <select id="corte">
            <option value="entero">Pollo Entero Congelado</option>
            <option value="trozado">Trozado (Pata/Muslo/Pechuga)</option>
            <option value="garras">Garras de Pollo</option>
        </select>
    </div>

    <div class="form-group">
        <label for="contenedores">Cantidad de Contenedores Reefer (27 Toneladas c/u):</label>
        <input type="number" id="contenedores" value="1" min="1">
    </div>

    <div class="form-group">
        <label for="precioFob">Precio FOB por Tonelada (USD):</label>
        <input type="number" id="precioFob" value="1800" min="0">
    </div>

    <div class="form-group">
        <label for="logistica">Flete Marítimo y Gastos SENASA por Contenedor (USD):</label>
        <input type="number" id="logistica" value="4500" min="0">
    </div>

    <button onclick="calcularCostos()">Calcular Costos de Exportación</button>

    <div id="panelResultados" class="results">
        <h3>Resultados de la Simulación</h3>
        <p id="resFob">Costo Total FOB: $0</p>
        <p id="resCif">Costo Total CIF (Con Flete): $0</p>
        <p id="resKilo">Costo Unitario por Kilo: $0 USD/kg</p>
    </div>
</div>

<script>
    function calcularCostos() {
        const contenedores = parseFloat(document.getElementById('contenedores').value) || 0;
        const precioFobTon = parseFloat(document.getElementById('precioFob').value) || 0;
        const logisticaTon = parseFloat(document.getElementById('logistica').value) || 0;

        // Cada contenedor reefer lleva aprox 27 toneladas (27,000 kg)
        const kilosTotales = contenedores * 27000;
        const totalFob = contenedores * precioFobTon * 27; // Simplificado por tonelada
        const totalCif = totalFob + (contenedores * logisticaTon);
        const costoPorKilo = totalCif / kilosTotales;

        // Mostrar resultados
        document.getElementById('resFob').innerText = `Costo Total FOB: $${totalFob.toLocaleString()} USD`;
        document.getElementById('resCif').innerText = `Costo Total CIF (Con Flete y Gastos): $${totalCif.toLocaleString()} USD`;
        document.getElementById('resKilo').innerText = `Costo Unitario por Kilo: $${costoPorKilo.toFixed(2)} USD/kg`;

        document.getElementById('panelResultados').style.display = 'block';
    }
</script>

</body>
</html>

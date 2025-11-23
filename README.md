
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Costos - Pasticho</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
            font-size: 1.5em;
        }

        .form-section {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 4px solid #667eea;
        }

        .form-section h2 {
            color: #333;
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        input {
            width: 100%;
            padding: 12px;
            margin: 5px 0;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }

        input:focus {
            border-color: #667eea;
            outline: none;
        }

        .row {
            display: flex;
            gap: 10px;
        }

        .input-group {
            flex: 1;
        }

        .input-group label {
            display: block;
            margin-bottom: 5px;
            color: #555;
            font-weight: bold;
        }

        button {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.2s;
        }

        button:hover {
            transform: translateY(-2px);
        }

        .resultado {
            background: #e8f5e8;
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
            border-left: 4px solid #28a745;
        }

        .resultado h2 {
            color: #2d5016;
            margin-bottom: 15px;
            text-align: center;
        }

        .result-grid {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .result-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #ddd;
        }

        .result-item span:first-child {
            font-weight: bold;
            color: #555;
        }

        .result-item span:last-child {
            color: #333;
        }

        .total span:last-child {
            color: #e74c3c;
            font-weight: bold;
            font-size: 1.1em;
        }

        .precio span:last-child {
            color: #27ae60;
            font-weight: bold;
        }

        .ganancia span:last-child {
            color: #2980b9;
            font-weight: bold;
            font-size: 1.1em;
        }

        @media (max-width: 480px) {
            .container {
                padding: 15px;
            }
            
            h1 {
                font-size: 1.3em;
            }
            
            input {
                padding: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🍝 Calculadora de Costos - Pasticho</h1>
        
        <div class="form-section">
            <h2>📋 Datos del Pedido</h2>
            <input type="text" id="cliente" placeholder="Nombre del cliente">
            <input type="text" id="fecha" placeholder="Fecha del pedido">
            
            <div class="row">
                <div class="input-group">
                    <label>Bandejas Grandes:</label>
                    <input type="number" id="bandejasGrandes" value="0" min="0">
                </div>
                <div class="input-group">
                    <label>Bandejas Pequeñas:</label>
                    <input type="number" id="bandejasPequenas" value="0" min="0">
                </div>
            </div>
        </div>

        <div class="form-section">
            <h2>🛒 Costos de Ingredientes</h2>
            <input type="number" id="costoCarne" placeholder="Costo de carne (Bs)" step="0.01">
            <input type="number" id="costoVegetales" placeholder="Costo de vegetales (Bs)" step="0.01">
            <input type="number" id="costoLaminas" placeholder="Costo de láminas (Bs)" step="0.01">
            <input type="number" id="costoQuesos" placeholder="Costo de quesos (Bs)" step="0.01">
            <input type="number" id="costoRefrescos" placeholder="Costo de refrescos (Bs)" step="0.01">
            <input type="number" id="costoPanes" placeholder="Costo de panes (Bs)" step="0.01">
            <input type="number" id="costoOtrosIng" placeholder="Otros ingredientes (Bs)" step="0.01">
        </div>

        <div class="form-section">
            <h2>⚡ Otros Gastos</h2>
            <input type="number" id="costoGas" placeholder="Costo de gas (Bs)" step="0.01">
            <input type="number" id="costoEmpaques" placeholder="Costo de empaques (Bs)" step="0.01">
            <input type="number" id="costoTransporte" placeholder="Costo de transporte (Bs)" step="0.01">
            <input type="number" id="costoOtrosGastos" placeholder="Otros gastos (Bs)" step="0.01">
        </div>

        <div class="form-section">
            <h2>💰 Margen de Ganancia</h2>
            <input type="number" id="margen" placeholder="Margen de ganancia (%)" value="30" step="0.1">
        </div>

        <button onclick="calcularCostos()">📊 Calcular Costos</button>

        <div id="resultado" class="resultado" style="display: none;">
            <h2>📈 Resultados del Pedido</h2>
            <div class="result-grid">
                <div class="result-item">
                    <span>Cliente:</span>
                    <span id="resCliente"></span>
                </div>
                <div class="result-item">
                    <span>Total Bandejas:</span>
                    <span id="resTotalBandejas"></span>
                </div>
                <div class="result-item">
                    <span>Costo Ingredientes:</span>
                    <span id="resCostoIngredientes"></span>
                </div>
                <div class="result-item">
                    <span>Costo Otros Gastos:</span>
                    <span id="resCostoGastos"></span>
                </div>
                <div class="result-item total">
                    <span>COSTO TOTAL:</span>
                    <span id="resCostoTotal"></span>
                </div>
                <div class="result-item">
                    <span>Costo por Bandeja:</span>
                    <span id="resCostoBandeja"></span>
                </div>
                <div class="result-item precio" id="resPrecioGrandeContainer">
                    <span>Precio Bandeja Grande:</span>
                    <span id="resPrecioGrande"></span>
                </div>
                <div class="result-item precio" id="resPrecioPequenaContainer">
                    <span>Precio Bandeja Pequeña:</span>
                    <span id="resPrecioPequena"></span>
                </div>
                <div class="result-item ganancia">
                    <span>GANANCIA ESTIMADA:</span>
                    <span id="resGanancia"></span>
                </div>
            </div>
        </div>

        <button onclick="nuevoPedido()" style="background: #28a745; margin-top: 20px;">🔄 Nuevo Pedido</button>
    </div>

    <script>
        function calcularCostos() {
            // Obtener valores del formulario
            const cliente = document.getElementById('cliente').value || 'Sin nombre';
            const fecha = document.getElementById('fecha').value || 'Sin fecha';
            const bandejasGrandes = parseInt(document.getElementById('bandejasGrandes').value) || 0;
            const bandejasPequenas = parseInt(document.getElementById('bandejasPequenas').value) || 0;
            
            // Costos de ingredientes
            const costoCarne = parseFloat(document.getElementById('costoCarne').value) || 0;
            const costoVegetales = parseFloat(document.getElementById('costoVegetales').value) || 0;
            const costoLaminas = parseFloat(document.getElementById('costoLaminas').value) || 0;
            const costoQuesos = parseFloat(document.getElementById('costoQuesos').value) || 0;
            const costoRefrescos = parseFloat(document.getElementById('costoRefrescos').value) || 0;
            const costoPanes = parseFloat(document.getElementById('costoPanes').value) || 0;
            const costoOtrosIng = parseFloat(document.getElementById('costoOtrosIng').value) || 0;
            
            // Otros gastos
            const costoGas = parseFloat(document.getElementById('costoGas').value) || 0;
            const costoEmpaques = parseFloat(document.getElementById('costoEmpaques').value) || 0;
            const costoTransporte = parseFloat(document.getElementById('costoTransporte').value) || 0;
            const costoOtrosGastos = parseFloat(document.getElementById('costoOtrosGastos').value) || 0;
            
            const margen = parseFloat(document.getElementById('margen').value) || 30;
            
            // Cálculos
            const totalBandejas = bandejasGrandes + bandejasPequenas;
            const costoTotalIngredientes = costoCarne + costoVegetales + costoLaminas + costoQuesos + 
                                        costoRefrescos + costoPanes + costoOtrosIng;
            const costoTotalGastos = costoGas + costoEmpaques + costoTransporte + costoOtrosGastos;
            const costoTotalPedido = costoTotalIngredientes + costoTotalGastos;
            const costoPromedioBandeja = totalBandejas > 0 ? costoTotalPedido / totalBandejas : 0;
            
            // Calcular precios de venta
            let precioGrande, precioPequena;
            
            if (bandejasGrandes > 0 && bandejasPequenas > 0) {
                const costoBandejaGrande = costoPromedioBandeja * 1.5; // 50% más
                const costoBandejaPequena = costoPromedioBandeja * 0.7; // 30% menos
                precioGrande = costoBandejaGrande / (1 - margen/100);
                precioPequena = costoBandejaPequena / (1 - margen/100);
            } else {
                precioGrande = costoPromedioBandeja / (1 - margen/100);
                precioPequena = costoPromedioBandeja / (1 - margen/100);
            }
            
            // Calcular ganancia estimada
            const ingresosTotales = (bandejasGrandes * precioGrande) + (bandejasPequenas * precioPequena);
            const ganancia = ingresosTotales - costoTotalPedido;
            
            // Mostrar resultados
            document.getElementById('resCliente').textContent = cliente;
            document.getElementById('resTotalBandejas').textContent = totalBandejas;
            document.getElementById('resCostoIngredientes').textContent = `Bs ${costoTotalIngredientes.toFixed(2)}`;
            document.getElementById('resCostoGastos').textContent = `Bs ${costoTotalGastos.toFixed(2)}`;
            document.getElementById('resCostoTotal').textContent = `Bs ${costoTotalPedido.toFixed(2)}`;
            document.getElementById('resCostoBandeja').textContent = `Bs ${costoPromedioBandeja.toFixed(2)}`;
            
            // Mostrar u ocultar precios según corresponda
            const precioGrandeContainer = document.getElementById('resPrecioGrandeContainer');
            const precioPequenaContainer = document.getElementById('resPrecioPequenaContainer');
            
            if (bandejasGrandes > 0) {
                precioGrandeContainer.style.display = 'flex';
                document.getElementById('resPrecioGrande').textContent = `Bs ${precioGrande.toFixed(2)}`;
            } else {
                precioGrandeContainer.style.display = 'none';
            }
            
            if (bandejasPequenas > 0) {
                precioPequenaContainer.style.display = 'flex';
                document.getElementById('resPrecioPequena').textContent = `Bs ${precioPequena.toFixed(2)}`;
            } else {
                precioPequenaContainer.style.display = 'none';
            }
            
            document.getElementById('resGanancia').textContent = `Bs ${ganancia.toFixed(2)}`;
            document.getElementById('resultado').style.display = 'block';
            
            // Hacer scroll a los resultados
            document.getElementById('resultado').scrollIntoView({ behavior: 'smooth' });
        }

        function nuevoPedido() {
            // Limpiar todos los campos
            const inputs = document.querySelectorAll('input');
            inputs.forEach(input => {
                if (input.id !== 'margen') {
                    input.value = '';
                }
            });
            document.getElementById('bandejasGrandes').value = '0';
            document.getElementById('bandejasPequenas').value = '0';
            document.getElementById('margen').value = '30';
            
            // Ocultar resultados
            document.getElementById('resultado').style.display = 'none';
            
            // Hacer scroll al inicio
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Hacer que el formulario no se envíe al presionar Enter
        document.addEventListener('DOMContentLoaded', function() {
            document.getElementById('margen').value = '30';
        });
    </script>
</body>
</html>
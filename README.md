<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculadora de Interés Compuesto</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <style>
    :root {
      --fondo-claro: #f4f6f8;
      --texto-claro: #333;
      --primario: #2b6777;
      --secundario: #52ab98;
      --terciario: #c8d8e4;
      --hover: #1b4d5b;
      --boton-texto: #fff;
      --verde: #28a745;
      --verde-hover: #218838;
    }

    body.dark {
      --fondo-claro: #121212;
      --texto-claro: #e0e0e0;
      --primario: #3a9cb8;
      --secundario: #2d8273;
      --terciario: #5a6d80;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: var(--fondo-claro);
      color: var(--texto-claro);
      padding: 20px;
      max-width: 1200px;
      margin: 0 auto;
      transition: background-color 0.4s, color 0.4s;
    }

    .calculadora-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      margin-top: 30px;
    }

    @media (max-width: 768px) {
      .calculadora-grid {
        grid-template-columns: 1fr;
      }
    }

    .input-card, .result-card {
      background: white;
      border-radius: 10px;
      padding: 20px;
      margin-bottom: 20px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
    }

    body.dark .input-card,
    body.dark .result-card,
    body.dark .chart-container {
      background: #1e1e1e;
      box-shadow: 0 2px 10px rgba(0,0,0,0.2);
    }

    .input-card h3, .result-card h3 {
      margin-top: 0;
      color: var(--primario);
      border-bottom: 1px solid #eee;
      padding-bottom: 10px;
    }

    body.dark .input-card h3,
    body.dark .result-card h3 {
      border-color: #444;
    }

    .input-group {
      margin-bottom: 15px;
    }

    .input-group label {
      display: block;
      margin-bottom: 5px;
      font-weight: 600;
    }

    input, select {
      width: 100%;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      background-color: #fff;
      transition: all 0.3s;
    }

    body.dark input,
    body.dark select {
      background-color: #2a2a2a;
      color: #e0e0e0;
      border-color: #555;
    }

    .result-row {
      display: flex;
      justify-content: space-between;
      margin: 10px 0;
    }

    .result-row.total {
      font-weight: bold;
      border-top: 1px solid #eee;
      padding-top: 10px;
      color: var(--primario);
    }

    body.dark .result-row.total {
      border-color: #444;
    }

    .chart-container {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
      height: 400px;
    }

    canvas {
      width: 100% !important;
      height: 100% !important;
    }

    .dark-mode-btn {
      position: fixed;
      top: 20px;
      right: 20px;
      z-index: 999;
      background-color: var(--primario);
      color: white;
      border: none;
      padding: 8px 15px;
      border-radius: 20px;
      cursor: pointer;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    }

    .whatsapp-btn {
      position: fixed;
      bottom: 30px;
      right: 30px;
      z-index: 999;
      background-color: #25D366;
      color: white;
      width: 60px;
      height: 60px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      transition: all 0.3s;
    }

    .whatsapp-btn:hover {
      background-color: #128C7E;
      transform: scale(1.1);
    }

    .whatsapp-btn i {
      font-size: 30px;
    }

    @media (max-width: 768px) {
      .dark-mode-btn {
        top: 15px;
        right: 15px;
        padding: 6px 10px;
      }
      
      .whatsapp-btn {
        width: 50px;
        height: 50px;
        bottom: 20px;
        right: 20px;
      }
    }
  </style>
</head>
<body>
  <button class="dark-mode-btn" onclick="toggleDarkMode()">🌙 Modo Oscuro</button>

  <h1 style="color: var(--primario); text-align: center;">Calculadora de Interés Compuesto</h1>

  <div class="calculadora-grid">
    <!-- Columna izquierda - Inputs -->
    <div class="input-section">
      <div class="input-card">
        <h3>Depósito inicial</h3>
        <div class="input-group">
          <label for="capitalInicial">Monto:</label>
          <input type="text" id="capitalInicial" placeholder="$0">
        </div>
        <div class="input-group">
          <label for="tasa">Tasa de interés anual (%):</label>
          <input type="number" id="tasa" step="0.01" placeholder="0">
        </div>
      </div>

      <div class="input-card">
        <h3>Plazo para invertir</h3>
        <div class="input-group">
          <label for="tipoPlazo">Tipo de plazo:</label>
          <select id="tipoPlazo" onchange="cambiarTipoPlazo()">
            <option value="anual">Periodo Anual</option>
            <option value="mensual">Periodo Mensual</option>
          </select>
        </div>
        <div class="input-group" id="grupo-anios">
          <label for="plazoAnios">Cantidad de años:</label>
          <input type="number" id="plazoAnios" min="1" placeholder="0">
        </div>
        <div class="input-group" id="grupo-meses" style="display: none;">
          <label for="plazoMeses">Cantidad de meses:</label>
          <input type="number" id="plazoMeses" min="1" placeholder="0">
        </div>
      </div>

      <div class="input-card">
        <h3>Aportaciones adicionales</h3>
        <div class="input-group">
          <label for="aportacion">Monto:</label>
          <input type="text" id="aportacion" placeholder="$0">
        </div>
        <div class="input-group">
          <label for="frecuenciaAportacion">Frecuencia de aportación:</label>
          <select id="frecuenciaAportacion">
            <option value="12" selected>Mensualmente</option>
            <option value="4">Trimestral</option>
            <option value="2">Semestral</option>
            <option value="1">Anualmente</option>
          </select>
        </div>
      </div>
    </div>

    <!-- Columna derecha - Resultados -->
    <div class="results-section">
      <div class="result-card">
        <h3>Resumen de inversión</h3>
        <div class="result-row">
          <span>Depósito inicial</span>
          <span id="res-inicial">$0.00</span>
        </div>
        <div class="result-row">
          <span>Depósitos adicionales</span>
          <span id="res-aportaciones">$0.00</span>
        </div>
        <div class="result-row">
          <span>Interés acumulado</span>
          <span id="res-intereses">$0.00</span>
        </div>
        <div class="result-row total">
          <span>Total acumulado</span>
          <span id="res-total">$0.00</span>
        </div>
      </div>

      <div class="chart-container">
        <canvas id="graficaBarras"></canvas>
      </div>
    </div>
  </div>

  <!-- Botón flotante de WhatsApp -->
  <a href="https://wa.me/523318853923?text=Hola,%20me%20interesa%20saber%20más%20sobre%20inversiones%20💰📈" class="whatsapp-btn" target="_blank" title="Contactar por WhatsApp">
    <i class="fab fa-whatsapp"></i>
  </a>

  <script>
    // Variables globales
    let chartBarras = null;
    let totalAportaciones = 0;
    let totalInteres = 0;
    let capital = 0;

    // Inicialización
    document.addEventListener('DOMContentLoaded', function() {
      // Configura eventos de input para cálculo automático
      document.querySelectorAll('input, select').forEach(input => {
        input.addEventListener('input', calcular);
      });

      // Configura formateo de moneda
      document.getElementById('capitalInicial').addEventListener('input', function() {
        formatearMoneda(this);
      });
      
      document.getElementById('aportacion').addEventListener('input', function() {
        formatearMoneda(this);
      });

      // Calcular inicialmente
      calcular();
    });

    function toggleDarkMode() {
      document.body.classList.toggle("dark");
      if (chartBarras) {
        chartBarras.update();
      }
    }

    function cambiarTipoPlazo() {
      const tipoPlazo = document.getElementById('tipoPlazo').value;
      document.getElementById('grupo-anios').style.display = tipoPlazo === 'anual' ? 'block' : 'none';
      document.getElementById('grupo-meses').style.display = tipoPlazo === 'mensual' ? 'block' : 'none';
      calcular();
    }

    function obtenerPlazoTotalEnMeses() {
      const tipoPlazo = document.getElementById('tipoPlazo').value;
      if (tipoPlazo === 'anual') {
        return (parseInt(document.getElementById('plazoAnios').value) || 0) * 12;
      } else {
        return parseInt(document.getElementById('plazoMeses').value) || 0;
      }
    }

    function formatearMoneda(input) {
      // Guardar posición del cursor
      const cursorPosition = input.selectionStart;
      
      // Eliminar todos los caracteres no numéricos excepto el punto decimal
      let valor = input.value.replace(/[^0-9.]/g, '');
      
      // Si está vacío, dejar vacío
      if(valor === '') {
        input.value = '';
        return;
      }
      
      // Convertir a número y formatear
      const numero = parseFloat(valor);
      if (isNaN(numero)) {
        input.value = '';
        return;
      }
      
      // Formatear con $ y separadores de miles
      input.value = '$' + new Intl.NumberFormat('es-MX').format(numero);
      
      // Restaurar posición del cursor, ajustando por los caracteres añadidos
      const newCursorPosition = cursorPosition + (input.value.length - valor.length);
      input.setSelectionRange(newCursorPosition, newCursorPosition);
    }

    function calcular() {
      // Obtener valores de los inputs
      const capitalInicial = parseFloat(document.getElementById('capitalInicial').value.replace(/[^0-9.]/g, '')) || 0;
      const tasaAnual = parseFloat(document.getElementById('tasa').value) || 0;
      const plazoMesesTotal = obtenerPlazoTotalEnMeses();
      const frecuencia = parseInt(document.getElementById('frecuencia').value) || 12;
      const aportacion = parseFloat(document.getElementById('aportacion').value.replace(/[^0-9.]/g, '')) || 0;
      const frecuenciaAportacion = parseInt(document.getElementById('frecuenciaAportacion').value) || 12;

      // Validaciones básicas
      if (plazoMesesTotal <= 0 || tasaAnual <= 0) {
        return;
      }

      // Calcular valores por año
      const resultadosPorAnio = [];
      capital = capitalInicial;
      totalAportaciones = 0;
      totalInteres = 0;

      const tasaPeriodica = tasaAnual / 100 / frecuencia;
      const aportacionPeriodica = aportacion;
      const periodosPorAnio = frecuencia;
      const aportacionesPorAnio = 12 / frecuenciaAportacion;

      for (let anio = 1; anio <= plazoMesesTotal / 12; anio++) {
        let interesAnual = 0;
        let aportacionesAnuales = 0;

        for (let periodo = 1; periodo <= periodosPorAnio; periodo++) {
          // Calcular interés del periodo
          const interesPeriodo = capital * tasaPeriodica;
          interesAnual += interesPeriodo;
          capital += interesPeriodo;

          // Calcular aportaciones
          if (periodo % (periodosPorAnio / aportacionesPorAnio) === 0) {
            capital += aportacionPeriodica;
            aportacionesAnuales += aportacionPeriodica;
          }
        }

        totalAportaciones += aportacionesAnuales;
        totalInteres += interesAnual;

        resultadosPorAnio.push({
          anio,
          capitalInicial: anio === 1 ? capitalInicial : 0,
          aportaciones: aportacionesAnuales,
          intereses: interesAnual,
          total: capital
        });
      }

      // Actualizar resumen
      document.getElementById('res-inicial').textContent = formatCurrency(capitalInicial);
      document.getElementById('res-aportaciones').textContent = formatCurrency(totalAportaciones);
      document.getElementById('res-intereses').textContent = formatCurrency(totalInteres);
      document.getElementById('res-total').textContent = formatCurrency(capital);

      // Generar gráfico de barras apiladas
      generarGraficoBarras(resultadosPorAnio);
    }

    function generarGraficoBarras(datos) {
      const ctx = document.getElementById('graficaBarras').getContext('2d');
      
      if (chartBarras) {
        chartBarras.destroy();
      }

      const labels = datos.map(item => `Año ${item.anio}`);
      
      // Mostrar el capital inicial completo en todos los años
      const datosInicial = datos.map(() => datos[0].capitalInicial);
      
      // Ajustamos las aportaciones para que no se solapen con el capital inicial
      const datosAportaciones = datos.map(item => item.aportaciones);
      const datosIntereses = datos.map(item => item.intereses);

      chartBarras = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: labels,
          datasets: [
            {
              label: 'Depósito inicial',
              data: datosInicial,
              backgroundColor: 'rgba(43, 103, 119, 0.7)',
              stack: 'stack-1',
              borderColor: '#2b6777',
              borderWidth: 1
            },
            {
              label: 'Aportaciones',
              data: datosAportaciones,
              backgroundColor: 'rgba(82, 171, 152, 0.7)',
              stack: 'stack-1',
              borderColor: '#52ab98',
              borderWidth: 1
            },
            {
              label: 'Intereses',
              data: datosIntereses,
              backgroundColor: 'rgba(200, 216, 228, 0.7)',
              stack: 'stack-1',
              borderColor: '#c8d8e4',
              borderWidth: 1
            }
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            x: {
              stacked: true,
              grid: {
                display: false
              }
            },
            y: {
              stacked: true,
              ticks: {
                callback: (value) => formatCurrency(value)
              },
              grid: {
                color: (context) => context.tick.value === 0 ? '#888' : 'rgba(0, 0, 0, 0.1)'
              },
              beginAtZero: true
            }
          },
          plugins: {
            legend: {
              position: 'top',
              labels: {
                boxWidth: 12,
                padding: 20,
                usePointStyle: true,
                pointStyle: 'rect'
              }
            },
            tooltip: {
              callbacks: {
                label: (context) => {
                  let label = context.dataset.label || '';
                  if (label) {
                    label += ': ';
                  }
                  if (context.parsed.y !== null) {
                    label += formatCurrency(context.parsed.y);
                  }
                  return label;
                },
                footer: (items) => {
                  const total = items.reduce((sum, item) => sum + item.parsed.y, 0);
                  return `Total acumulado: ${formatCurrency(total)}`;
                }
              }
            }
          },
          interaction: {
            intersect: false,
            mode: 'index'
          }
        }
      });
    }

    function formatCurrency(value) {
      return new Intl.NumberFormat('es-MX', { 
        style: 'currency', 
        currency: 'MXN',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2
      }).format(value);
    }
  </script>
</body>
</html>

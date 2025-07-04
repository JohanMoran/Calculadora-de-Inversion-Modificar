<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
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
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: var(--fondo-claro);
      color: var(--texto-claro);
      padding: 10px;
      margin: 0 auto;
      max-width: 100%;
      min-width: 320px;
      transition: background-color 0.4s, color 0.4s;
      font-size: 15px;
      line-height: 1.5;
      -webkit-text-size-adjust: 100%;
    }

    /* Header optimizado para móviles */
    .mobile-header {
      text-align: center;
      margin: 0 auto 20px;
      padding: 10px 5px;
      max-width: 100%;
    }
    
    .mobile-header img {
      max-width: 280px;
      width: 100%;
      height: auto;
      object-fit: contain;
    }

    /* Contenedor principal flexible */
    .calculadora-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 15px;
      width: 100%;
      max-width: 100%;
      margin: 0 auto;
      box-sizing: border-box;
    }

    /* Tarjetas adaptables */
    .input-card, .result-card {
      background: white;
      border-radius: 10px;
      padding: 15px;
      margin-bottom: 15px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      width: 100%;
      box-sizing: border-box;
    }

    body.dark .input-card,
    body.dark .result-card,
    body.dark .chart-container,
    body.dark .table-wrapper {
      background: #1e1e1e;
      box-shadow: 0 2px 10px rgba(0,0,0,0.2);
    }

    /* Textos optimizados para móviles */
    .input-card h3, .result-card h3 {
      margin: 0 0 15px 0;
      color: var(--primario);
      font-size: 1.2rem;
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      gap: 8px;
      line-height: 1.4;
    }

    .input-group {
      margin-bottom: 15px;
    }

    .input-group label {
      display: block;
      margin-bottom: 8px;
      font-weight: 600;
      font-size: 0.95rem;
      line-height: 1.4;
    }

    /* Inputs optimizados para móviles */
    input, select {
      width: 100%;
      padding: 12px 15px;
      border: 1px solid #ddd;
      border-radius: 8px;
      background-color: #fff;
      font-size: 1rem;
      box-sizing: border-box;
      -webkit-appearance: none;
    }

    body.dark input,
    body.dark select {
      background-color: #2a2a2a;
      color: #e0e0e0;
      border-color: #555;
    }

    /* Resultados mejor organizados */
    .result-row {
      display: flex;
      justify-content: space-between;
      margin: 12px 0;
      font-size: 0.95rem;
    }

    .result-row.total {
      font-weight: bold;
      border-top: 1px solid #eee;
      padding-top: 12px;
      color: var(--primario);
      font-size: 1rem;
      margin-top: 15px;
    }

    /* Gráfico responsive */
    .chart-container {
      background: white;
      padding: 15px;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      height: 300px;
      margin-bottom: 15px;
      width: 100%;
    }

    canvas {
      width: 100% !important;
      height: 100% !important;
    }

    /* Tabla optimizada para móviles */
    .table-wrapper {
      width: 100%;
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
      border-radius: 8px;
      margin-top: 15px;
    }
    
    #tablaResultados {
      width: 100%;
      min-width: 500px;
      border-collapse: collapse;
      font-size: 0.85rem;
    }
    
    #tablaResultados th, 
    #tablaResultados td {
      padding: 10px 12px;
      text-align: right;
      border-bottom: 1px solid #eee;
    }
    
    #tablaResultados th {
      background-color: var(--primario);
      color: white;
      position: sticky;
      top: 0;
      font-size: 0.9rem;
    }

    /* Botones flotantes optimizados */
    .dark-mode-btn {
      position: fixed;
      top: 15px;
      right: 15px;
      z-index: 999;
      background-color: var(--primario);
      color: white;
      border: none;
      padding: 10px 15px;
      border-radius: 30px;
      font-size: 0.95rem;
      box-shadow: 0 3px 10px rgba(0,0,0,0.2);
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .whatsapp-btn {
      position: fixed;
      bottom: 20px;
      right: 20px;
      z-index: 999;
      background-color: #25D366;
      color: white;
      width: 55px;
      height: 55px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 3px 12px rgba(0,0,0,0.2);
    }

    .whatsapp-btn i {
      font-size: 26px;
    }

    /* Tooltips mejorados */
    .tooltip-container {
      position: relative;
      display: inline-block;
    }
    
    .tooltip-icon {
      color: var(--primario);
      cursor: help;
      font-size: 0.95rem;
      margin-left: 5px;
    }
    
    .tooltip-text {
      visibility: hidden;
      width: 220px;
      background-color: var(--primario);
      color: white;
      text-align: center;
      border-radius: 8px;
      padding: 10px;
      position: absolute;
      z-index: 1;
      bottom: 125%;
      left: 50%;
      transform: translateX(-50%);
      opacity: 0;
      transition: opacity 0.3s;
      font-size: 0.85rem;
      font-weight: normal;
    }
    
    .tooltip-container:hover .tooltip-text {
      visibility: visible;
      opacity: 1;
    }

    /* Media Queries para ajustes específicos */
    @media (max-width: 480px) {
      body {
        padding: 8px;
        font-size: 14px;
      }
      
      .mobile-header img {
        max-width: 240px;
      }
      
      .input-card, .result-card {
        padding: 12px;
      }
      
      .input-card h3, .result-card h3 {
        font-size: 1.1rem;
      }
      
      input, select {
        padding: 10px 12px;
        font-size: 0.95rem;
      }
      
      .result-row {
        font-size: 0.9rem;
      }
      
      .dark-mode-btn {
        padding: 8px 12px;
        font-size: 0.85rem;
      }
      
      .whatsapp-btn {
        width: 50px;
        height: 50px;
      }
      
      .whatsapp-btn i {
        font-size: 24px;
      }
    }

    @media (min-width: 768px) {
      .calculadora-grid {
        grid-template-columns: 1.1fr 2fr;
        gap: 20px;
      }
      
      .mobile-header img {
        max-width: 320px;
      }
      
      .chart-container {
        height: 350px;
      }
    }

    @media (min-width: 992px) {
      body {
        max-width: 1200px;
        padding: 20px;
      }
      
      .calculadora-grid {
        grid-template-columns: 1.2fr 2.8fr;
      }
      
      .mobile-header img {
        max-width: 350px;
      }
      
      .chart-container {
        height: 400px;
      }
    }

    /* Mejoras de interacción */
    input, select, button {
      -webkit-tap-highlight-color: transparent;
      touch-action: manipulation;
    }
    
    select {
      background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='currentColor' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
      background-repeat: no-repeat;
      background-position: right 12px center;
      background-size: 1em;
    }
    
    body.dark select {
      background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23e0e0e0' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
    }
  </style>
</head>
<body>
  <button class="dark-mode-btn" onclick="toggleDarkMode()"><i class="fas fa-moon"></i> Modo Oscuro</button>

  <div class="mobile-header">
    <img src="Johan_Moran.PNG" alt="Logo Johan Moran">
  </div>

  <div class="calculadora-grid">
    <!-- Columna izquierda - Inputs -->
    <div class="input-section">
      <div class="input-card">
        <h3><i class="fas fa-coins"></i> Depósito inicial
          <div class="tooltip-container">
            <i class="fas fa-question-circle tooltip-icon"></i>
            <span class="tooltip-text">¿Con qué cantidad vas a comenzar tu inversión?</span>
          </div>
        </h3>
        <div class="input-group">
          <input type="text" id="capitalInicial" placeholder="$0">
        </div>
        <div class="input-group">
          <label for="tasa">Tasa de interés anual (%):
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Tasa de rendimiento anual que ofrece la institución financiera</span>
            </div>
          </label>
          <input type="number" id="tasa" step="0.01" placeholder="0">
        </div>
      </div>

      <div class="input-card">
        <h3><i class="far fa-calendar-alt"></i> Plazo para invertir
          <div class="tooltip-container">
            <i class="fas fa-question-circle tooltip-icon"></i>
            <span class="tooltip-text">Periodo de tiempo que mantendrás tu inversión</span>
          </div>
        </h3>
        <div class="input-group">
          <label for="tipoPlazo">Tipo de plazo:</label>
          <select id="tipoPlazo">
            <option value="anual">Periodo Anual</option>
            <option value="mensual">Periodo Mensual</option>
          </select>
        </div>
        <div class="input-group">
          <label id="labelPlazo" for="plazo">Cantidad de años:
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Horizonte de tiempo para tu inversión</span>
            </div>
          </label>
          <input type="number" id="plazo" min="1" placeholder="0">
        </div>
        <div class="input-group">
          <label for="frecuencia">Frecuencia de capitalización:
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Con qué frecuencia se reinvertirán los intereses</span>
            </div>
          </label>
          <select id="frecuencia">
            <option value="12" selected>Mensualmente</option>
            <option value="4">Trimestral</option>
            <option value="2">Semestral</option>
            <option value="1">Anualmente</option>
          </select>
        </div>
      </div>

      <div class="input-card">
        <h3><i class="fas fa-hand-holding-usd"></i> Aportaciones adicionales
          <div class="tooltip-container">
            <i class="fas fa-question-circle tooltip-icon"></i>
            <span class="tooltip-text">Depósitos periódicos adicionales a tu inversión inicial</span>
          </div>
        </h3>
        <div class="input-group">
          <label for="aportacion">Monto:
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Cantidad que aportarás periódicamente</span>
            </div>
          </label>
          <input type="text" id="aportacion" placeholder="$0">
        </div>
        <div class="input-group">
          <label for="frecuenciaAportacion">Frecuencia de aportación:
            <div class="tooltip-container">
              <i class="fas fa-question-circle tooltip-icon"></i>
              <span class="tooltip-text">Con qué frecuencia realizarás aportaciones</span>
            </div>
          </label>
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
        <h3><i class="fas fa-chart-pie"></i> Resumen de inversión</h3>
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
      
      <div class="results-table-container">
        <div class="input-card">
          <h3><i class="fas fa-table"></i> Detalle de crecimiento</h3>
          <div class="table-wrapper">
            <table id="tablaResultados">
              <thead>
                <tr>
                  <th>Periodo</th>
                  <th>Depósito inicial</th>
                  <th>Aportaciones</th>
                  <th>Intereses</th>
                  <th>Total acumulado</th>
                </tr>
              </thead>
              <tbody>
                <!-- Aquí se insertarán las filas dinámicamente -->
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>

  <a href="https://wa.me/523318853923?text=Hola,%20me%20interesa%20saber%20más%20sobre%20inversiones%20💰📈" class="whatsapp-btn" target="_blank" title="Contactar por WhatsApp">
    <i class="fab fa-whatsapp"></i>
  </a>

  <script>
    let chartBarras = null;
    let totalAportaciones = 0;
    let totalInteres = 0;
    let capital = 0;

    document.addEventListener('DOMContentLoaded', function() {
      document.querySelectorAll('input, select').forEach(input => {
        input.addEventListener('input', calcular);
      });

      document.getElementById('capitalInicial').addEventListener('input', function() {
        formatearMoneda(this);
      });
      
      document.getElementById('aportacion').addEventListener('input', function() {
        formatearMoneda(this);
      });

      document.getElementById('tipoPlazo').addEventListener('change', function() {
        const labelPlazo = document.getElementById('labelPlazo');
        const tooltip = labelPlazo.querySelector('.tooltip-text');
        
        if (this.value === 'mensual') {
          labelPlazo.textContent = 'Cantidad de meses:';
          tooltip.textContent = '¿Cuántos meses vas a realizar la inversión?';
          document.getElementById('plazo').placeholder = '0';
        } else {
          labelPlazo.textContent = 'Cantidad de años:';
          tooltip.textContent = '¿Cuántos años vas a realizar la inversión?';
          document.getElementById('plazo').placeholder = '0';
        }
        
        labelPlazo.innerHTML = labelPlazo.textContent + `<div class="tooltip-container">
          <i class="fas fa-question-circle tooltip-icon"></i>
          <span class="tooltip-text">${tooltip.textContent}</span>
        </div>`;
        
        calcular();
      });

      calcular();
    });

    function toggleDarkMode() {
      document.body.classList.toggle("dark");
      const icon = document.querySelector('.dark-mode-btn i');
      if (document.body.classList.contains("dark")) {
        icon.classList.remove('fa-moon');
        icon.classList.add('fa-sun');
      } else {
        icon.classList.remove('fa-sun');
        icon.classList.add('fa-moon');
      }
      if (chartBarras) {
        chartBarras.update();
      }
    }

    function formatearMoneda(input) {
      const cursorPosition = input.selectionStart;
      let valor = input.value.replace(/[^0-9.]/g, '');
      
      if(valor === '') {
        input.value = '';
        return;
      }
      
      const numero = parseFloat(valor);
      if (isNaN(numero)) {
        input.value = '';
        return;
      }
      
      input.value = '$' + new Intl.NumberFormat('es-MX').format(numero);
      const newCursorPosition = cursorPosition + (input.value.length - valor.length);
      input.setSelectionRange(newCursorPosition, newCursorPosition);
    }

    function calcular() {
      const capitalInicial = parseFloat(document.getElementById('capitalInicial').value.replace(/[^0-9.]/g, '')) || 0;
      const tasaAnual = parseFloat(document.getElementById('tasa').value) || 0;
      const tipoPlazo = document.getElementById('tipoPlazo').value;
      const plazo = parseInt(document.getElementById('plazo').value) || 0;
      const frecuencia = parseInt(document.getElementById('frecuencia').value) || 12;
      const aportacion = parseFloat(document.getElementById('aportacion').value.replace(/[^0-9.]/g, '')) || 0;
      const frecuenciaAportacion = parseInt(document.getElementById('frecuenciaAportacion').value) || 12;

      if (plazo <= 0 || tasaAnual <= 0) return;

      const plazoAnios = tipoPlazo === 'mensual' ? plazo / 12 : plazo;
      const totalMeses = tipoPlazo === 'mensual' ? plazo : plazo * 12;

      const resultados = [];
      capital = capitalInicial;
      totalAportaciones = 0;
      totalInteres = 0;

      const tasaPeriodica = tasaAnual / 100 / frecuencia;
      const aportacionPeriodica = aportacion;
      const aportacionesPorAnio = 12 / frecuenciaAportacion;

      const periodos = tipoPlazo === 'mensual' ? totalMeses : plazo;
      const labels = tipoPlazo === 'mensual' ? 
        Array.from({length: periodos}, (_, i) => `Mes ${i+1}`) : 
        Array.from({length: periodos}, (_, i) => `Año ${i+1}`);

      for (let i = 1; i <= periodos; i++) {
        let interesPeriodo = 0;
        let aportacionPeriodo = 0;
        
        if (tipoPlazo === 'mensual') {
          interesPeriodo = capital * (tasaAnual / 100 / 12);
          capital += interesPeriodo;
          totalInteres += interesPeriodo;
          
          if (i % (12 / frecuenciaAportacion) === 0 || frecuenciaAportacion === 12) {
            capital += aportacionPeriodica;
            aportacionPeriodo = aportacionPeriodica;
            totalAportaciones += aportacionPeriodica;
          }
        } else {
          for (let p = 0; p < frecuencia; p++) {
            const interes = capital * tasaPeriodica;
            capital += interes;
            interesPeriodo += interes;
          }
          totalInteres += interesPeriodo;
          
          if (frecuenciaAportacion === 12) {
            aportacionPeriodo = aportacionPeriodica * 12;
          } else if (frecuenciaAportacion === 4) {
            aportacionPeriodo = aportacionPeriodica * 4;
          } else if (frecuenciaAportacion === 2) {
            aportacionPeriodo = aportacionPeriodica * 2;
          } else {
            aportacionPeriodo = aportacionPeriodica;
          }
          
          capital += aportacionPeriodo;
          totalAportaciones += aportacionPeriodo;
        }

        resultados.push({
          periodo: i,
          capitalInicial: i === 1 ? capitalInicial : 0,
          aportaciones: aportacionPeriodo,
          intereses: interesPeriodo,
          total: capital
        });
      }

      document.getElementById('res-inicial').textContent = formatCurrency(capitalInicial);
      document.getElementById('res-aportaciones').textContent = formatCurrency(totalAportaciones);
      document.getElementById('res-intereses').textContent = formatCurrency(totalInteres);
      document.getElementById('res-total').textContent = formatCurrency(capital);

      generarGraficoBarras(resultados, labels);
      generarTabla(resultados, tipoPlazo === 'mensual');
    }

    function generarGraficoBarras(datos, labels) {
      const ctx = document.getElementById('graficaBarras').getContext('2d');
      
      if (chartBarras) {
        chartBarras.destroy();
      }
      
      const datosInicial = datos.map(() => datos[0].capitalInicial);
      
      let acumuladoAportaciones = 0;
      let acumuladoIntereses = 0;
      
      const datosAportaciones = datos.map(item => {
        acumuladoAportaciones += item.aportaciones;
        return acumuladoAportaciones;
      });
      
      const datosIntereses = datos.map(item => {
        acumuladoIntereses += item.intereses;
        return acumuladoIntereses;
      });

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
              grid: { display: false },
              ticks: { maxRotation: 45, minRotation: 45 }
            },
            y: {
              stacked: true,
              ticks: { callback: (value) => formatCurrency(value) },
              grid: { color: (context) => context.tick.value === 0 ? '#888' : 'rgba(0, 0, 0, 0.1)' },
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
                  if (label) label += ': ';
                  if (context.parsed.y !== null) label += formatCurrency(context.parsed.y);
                  return label;
                },
                footer: (items) => `Total acumulado: ${formatCurrency(items.reduce((sum, item) => sum + item.parsed.y, 0))}`
              }
            }
          },
          interaction: { intersect: false, mode: 'index' }
        }
      });
    }

    function generarTabla(datos, esMensual) {
      const tbody = document.querySelector('#tablaResultados tbody');
      tbody.innerHTML = '';
      
      datos.forEach((item) => {
        const fila = document.createElement('tr');
        const periodo = esMensual ? `Mes ${item.periodo}` : `Año ${item.periodo}`;
        
        fila.innerHTML = `
          <td style="text-align: center;">${periodo}</td>
          <td>${formatCurrency(item.capitalInicial)}</td>
          <td>${formatCurrency(item.aportaciones)}</td>
          <td>${formatCurrency(item.intereses)}</td>
          <td><strong>${formatCurrency(item.total)}</strong></td>
        `;
        
        if (esMensual && item.periodo % 12 === 0) {
          fila.style.backgroundColor = document.body.classList.contains('dark') ? 'rgba(82, 171, 152, 0.3)' : 'rgba(82, 171, 152, 0.2)';
        }
        
        tbody.appendChild(fila);
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

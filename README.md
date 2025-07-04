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
      font-family: 'Segoe UI', sans-serif;
      background-color: var(--fondo-claro);
      color: var(--texto-claro);
      padding: 10px;
      max-width: 1200px;
      margin: 0 auto;
      transition: background-color 0.4s, color 0.4s;
      font-size: 14px;
      line-height: 1.4;
      -webkit-text-size-adjust: 100%;
    }

    /* Header para móvil */
    .mobile-header {
      text-align: center;
      margin-bottom: 15px;
      padding: 5px 0;
    }

    .mobile-header h1 {
      color: var(--primario);
      font-size: 1.5rem;
      margin-bottom: 3px;
      font-weight: 600;
    }

    .mobile-header h2 {
      font-size: 1.1rem;
      margin-bottom: 3px;
      font-weight: 500;
    }

    .mobile-header h3 {
      font-size: 0.95rem;
      color: var(--secundario);
      font-weight: 600;
      margin-top: 3px;
    }

    /* Estilos para preguntas */
    .mobile-question {
      font-size: 0.85rem;
      color: #666;
      margin-bottom: 8px;
      font-style: italic;
      display: block;
    }

    body.dark .mobile-question {
      color: #aaa;
    }

    .calculadora-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 12px;
      margin-top: 5px;
    }

    .input-card, .result-card {
      background: white;
      border-radius: 8px;
      padding: 12px;
      margin-bottom: 12px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.1);
    }

    body.dark .input-card,
    body.dark .result-card,
    body.dark .chart-container,
    body.dark .table-wrapper {
      background: #1e1e1e;
      box-shadow: 0 1px 6px rgba(0,0,0,0.2);
    }

    .input-card h3, .result-card h3 {
      margin-top: 0;
      color: var(--primario);
      padding-bottom: 6px;
      margin-bottom: 12px;
      font-size: 1.1rem;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .input-card h3 i {
      font-size: 1rem;
    }

    .input-group {
      margin-bottom: 12px;
    }

    .input-group label {
      display: block;
      margin-bottom: 4px;
      font-weight: 600;
      font-size: 0.9rem;
    }

    input, select {
      width: 100%;
      padding: 10px 12px;
      border: 1px solid #ddd;
      border-radius: 6px;
      background-color: #fff;
      transition: all 0.3s;
      font-size: 0.95rem;
      -webkit-appearance: none;
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
      font-size: 0.9rem;
    }

    .result-row.total {
      font-weight: bold;
      border-top: 1px solid #eee;
      padding-top: 10px;
      color: var(--primario);
      font-size: 0.95rem;
      margin-top: 12px;
    }

    body.dark .result-row.total {
      border-color: #444;
    }

    .chart-container {
      background: white;
      padding: 12px;
      border-radius: 8px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.1);
      height: 300px;
      margin-bottom: 12px;
    }

    canvas {
      width: 100% !important;
      height: 100% !important;
    }

    .dark-mode-btn {
      position: fixed;
      top: 10px;
      right: 10px;
      z-index: 999;
      background-color: var(--primario);
      color: white;
      border: none;
      padding: 6px 12px;
      border-radius: 20px;
      cursor: pointer;
      box-shadow: 0 1px 3px rgba(0,0,0,0.2);
      font-size: 0.85rem;
      display: flex;
      align-items: center;
      gap: 4px;
    }

    .whatsapp-btn {
      position: fixed;
      bottom: 15px;
      right: 15px;
      z-index: 999;
      background-color: #25D366;
      color: white;
      width: 45px;
      height: 45px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
      transition: all 0.3s;
    }

    .whatsapp-btn:hover {
      background-color: #128C7E;
      transform: scale(1.1);
    }

    .whatsapp-btn i {
      font-size: 22px;
    }

    .results-table-container {
      margin-top: 12px;
    }
    
    .table-wrapper {
      overflow-x: auto;
      max-height: 250px;
      overflow-y: auto;
      margin-top: 12px;
      border-radius: 6px;
      box-shadow: 0 1px 2px rgba(0,0,0,0.1);
      -webkit-overflow-scrolling: touch;
    }
    
    #tablaResultados {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.8rem;
    }
    
    #tablaResultados th, 
    #tablaResultados td {
      padding: 8px 10px;
      text-align: right;
      border-bottom: 1px solid #eee;
    }
    
    #tablaResultados th {
      background-color: var(--primario);
      color: white;
      position: sticky;
      top: 0;
      text-align: center;
      font-size: 0.85rem;
    }
    
    #tablaResultados tr:nth-child(even) {
      background-color: #f9f9f9;
    }
    
    #tablaResultados tr:hover {
      background-color: #f1f1f1;
    }
    
    body.dark #tablaResultados th {
      background-color: var(--secundario);
    }
    
    body.dark #tablaResultados tr:nth-child(even) {
      background-color: #2a2a2a;
    }
    
    body.dark #tablaResultados tr:hover {
      background-color: #333;
    }
    
    body.dark #tablaResultados th, 
    body.dark #tablaResultados td {
      border-color: #444;
    }

    /* Estilos para pantallas más grandes */
    @media (min-width: 768px) {
      body {
        padding: 15px;
        font-size: 15px;
      }
      
      .calculadora-grid {
        grid-template-columns: 1fr 2fr;
        gap: 15px;
      }
      
      .input-section {
        max-width: 300px;
      }
      
      .chart-container {
        height: 400px;
      }
      
      .dark-mode-btn {
        top: 15px;
        right: 15px;
        padding: 8px 15px;
      }
      
      .whatsapp-btn {
        width: 50px;
        height: 50px;
        bottom: 20px;
        right: 20px;
      }
      
      .whatsapp-btn i {
        font-size: 25px;
      }
      
      .mobile-header h1 {
        font-size: 1.8rem;
      }
      
      .mobile-header h2 {
        font-size: 1.3rem;
      }
      
      .mobile-header h3 {
        font-size: 1.1rem;
      }
      
      .input-card, .result-card {
        padding: 15px;
      }
      
      .input-card h3, .result-card h3 {
        font-size: 1.15rem;
      }
      
      .result-row {
        font-size: 0.95rem;
      }
      
      #tablaResultados {
        font-size: 0.85rem;
      }
    }

    /* Estilos para pantallas muy grandes */
    @media (min-width: 992px) {
      .calculadora-grid {
        grid-template-columns: 1fr 3fr;
      }
      
      .input-section {
        max-width: 320px;
      }
      
      .chart-container {
        height: 450px;
      }
    }

    /* Mejoras para inputs en móviles */
    input, select, button {
      -webkit-tap-highlight-color: transparent;
      touch-action: manipulation;
    }
    
    select {
      background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='currentColor' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
      background-repeat: no-repeat;
      background-position: right 10px center;
      background-size: 1em;
    }
    
    body.dark select {
      background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23e0e0e0' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
    }
  </style>
</head>
<body>
  <button class="dark-mode-btn" onclick="toggleDarkMode()"><i class="fas fa-moon"></i> Modo Oscuro</button>

  <!-- Header para móvil -->
  <div class="mobile-header">
    <h1>Calculadora de Inversión</h1>
    <h2>Johan Moran</h2>
    <h3>ASESOR FINANCIERO</h3>
  </div>

  <div class="calculadora-grid">
    <!-- Columna izquierda - Inputs -->
    <div class="input-section">
      <div class="input-card">
        <h3><i class="fas fa-coins"></i> Monto Inicial</h3>
        <span class="mobile-question">¿Con qué cantidad cuentas en este momento? ¿Con cuánto empezarás tu inversión?</span>
        <div class="input-group">
          <input type="text" id="capitalInicial" placeholder="$0">
        </div>
        <div class="input-group">
          <label for="tasa">Tasa de interés anual (%):</label>
          <span class="mobile-question">¿Cuál es la tasa de rendimiento anual que te está ofreciendo la institución financiera?</span>
          <input type="number" id="tasa" step="0.01" placeholder="0">
        </div>
      </div>

      <div class="input-card">
        <h3><i class="far fa-calendar-alt"></i> Plazo para invertir</h3>
        <div class="input-group">
          <label for="tipoPlazo">Tipo de plazo:</label>
          <select id="tipoPlazo">
            <option value="anual">Periodo Anual</option>
            <option value="mensual">Periodo Mensual</option>
          </select>
        </div>
        <div class="input-group">
          <label id="labelPlazo" for="plazo">Cantidad de años:</label>
          <span class="mobile-question">¿Cuántos años vas a realizar la inversión? ¿Cuál es tu horizonte de inversión?</span>
          <input type="number" id="plazo" min="1" placeholder="0">
        </div>
        <div class="input-group">
          <label for="frecuencia">Frecuencia de capitalización:</label>
          <select id="frecuencia">
            <option value="12" selected>Mensualmente</option>
            <option value="4">Trimestral</option>
            <option value="2">Semestral</option>
            <option value="1">Anualmente</option>
          </select>
        </div>
      </div>

      <div class="input-card">
        <h3><i class="fas fa-hand-holding-usd"></i> Aportaciones adicionales</h3>
        <div class="input-group">
          <label for="aportacion">Monto:</label>
          <span class="mobile-question">¿Cuánto podrás aportar periódicamente a tu inversión?</span>
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
      
      <!-- Tabla de resultados detallados -->
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

      // Cambiar label de plazo según selección
      document.getElementById('tipoPlazo').addEventListener('change', function() {
        const labelPlazo = document.getElementById('labelPlazo');
        if (this.value === 'mensual') {
          labelPlazo.textContent = 'Cantidad de meses:';
          document.getElementById('plazo').placeholder = '0';
          document.querySelector('.mobile-question', this.parentElement.parentElement).textContent = '¿Cuántos meses vas a realizar la inversión?';
        } else {
          labelPlazo.textContent = 'Cantidad de años:';
          document.getElementById('plazo').placeholder = '0';
          document.querySelector('.mobile-question', this.parentElement.parentElement).textContent = '¿Cuántos años vas a realizar la inversión?';
        }
        calcular();
      });

      // Calcular inicialmente
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
      const tipoPlazo = document.getElementById('tipoPlazo').value;
      const plazo = parseInt(document.getElementById('plazo').value) || 0;
      const frecuencia = parseInt(document.getElementById('frecuencia').value) || 12;
      const aportacion = parseFloat(document.getElementById('aportacion').value.replace(/[^0-9.]/g, '')) || 0;
      const frecuenciaAportacion = parseInt(document.getElementById('frecuenciaAportacion').value) || 12;

      // Validaciones básicas
      if (plazo <= 0 || tasaAnual <= 0) {
        return;
      }

      // Convertir plazo a años si está en meses
      const plazoAnios = tipoPlazo === 'mensual' ? plazo / 12 : plazo;
      const totalMeses = tipoPlazo === 'mensual' ? plazo : plazo * 12;

      // Calcular valores
      const resultados = [];
      capital = capitalInicial;
      totalAportaciones = 0;
      totalInteres = 0;

      const tasaPeriodica = tasaAnual / 100 / frecuencia;
      const aportacionPeriodica = aportacion;
      const aportacionesPorAnio = 12 / frecuenciaAportacion;
      const totalAportacionesPeriodos = tipoPlazo === 'mensual' ? 
        (plazo / (12 / frecuenciaAportacion)) : 
        (plazo * aportacionesPorAnio);

      // Calcular por periodo (mes o año según selección)
      const periodos = tipoPlazo === 'mensual' ? totalMeses : plazo;
      const labels = tipoPlazo === 'mensual' ? 
        Array.from({length: periodos}, (_, i) => `Mes ${i+1}`) : 
        Array.from({length: periodos}, (_, i) => `Año ${i+1}`);

      for (let i = 1; i <= periodos; i++) {
        let interesPeriodo = 0;
        let aportacionPeriodo = 0;
        
        // Si es cálculo mensual
        if (tipoPlazo === 'mensual') {
          // Calcular interés mensual (dividimos la tasa anual entre 12)
          interesPeriodo = capital * (tasaAnual / 100 / 12);
          capital += interesPeriodo;
          totalInteres += interesPeriodo;
          
          // Aportaciones según frecuencia
          if (i % (12 / frecuenciaAportacion) === 0 || frecuenciaAportacion === 12) {
            capital += aportacionPeriodica;
            aportacionPeriodo = aportacionPeriodica;
            totalAportaciones += aportacionPeriodica;
          }
        } 
        // Si es cálculo anual
        else {
          // Calcular interés anual compuesto
          for (let p = 0; p < frecuencia; p++) {
            const interes = capital * tasaPeriodica;
            capital += interes;
            interesPeriodo += interes;
          }
          totalInteres += interesPeriodo;
          
          // Aportaciones anuales según frecuencia
          for (let a = 0; a < aportacionesPorAnio; a++) {
            capital += aportacionPeriodica;
            aportacionPeriodo += aportacionPeriodica;
          }
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

      // Actualizar resumen
      document.getElementById('res-inicial').textContent = formatCurrency(capitalInicial);
      document.getElementById('res-aportaciones').textContent = formatCurrency(totalAportaciones);
      document.getElementById('res-intereses').textContent = formatCurrency(totalInteres);
      document.getElementById('res-total').textContent = formatCurrency(capital);

      // Generar gráfico y tabla
      generarGraficoBarras(resultados, labels);
      generarTabla(resultados, tipoPlazo === 'mensual');
    }

    function generarGraficoBarras(datos, labels) {
      const ctx = document.getElementById('graficaBarras').getContext('2d');
      
      if (chartBarras) {
        chartBarras.destroy();
      }
      
      // Preparar datos para el gráfico (modificado para mostrar depósito inicial en todos los periodos)
      const datosInicial = datos.map(() => datos[0].capitalInicial);
      
      // Calcular valores acumulativos para aportaciones e intereses
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
              grid: {
                display: false
              },
              ticks: {
                maxRotation: 45,
                minRotation: 45
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

    function generarTabla(datos, esMensual) {
      const tbody = document.querySelector('#tablaResultados tbody');
      tbody.innerHTML = '';
      
      datos.forEach((item, index) => {
        const fila = document.createElement('tr');
        
        // Formateamos diferente si es mensual o anual
        const periodo = esMensual ? `Mes ${item.periodo}` : `Año ${item.periodo}`;
        
        fila.innerHTML = `
          <td style="text-align: center;">${periodo}</td>
          <td>${formatCurrency(item.capitalInicial)}</td>
          <td>${formatCurrency(item.aportaciones)}</td>
          <td>${formatCurrency(item.intereses)}</td>
          <td><strong>${formatCurrency(item.total)}</strong></td>
        `;
        
        // Destacamos los periodos anuales si es mensual
        if (esMensual && item.periodo % 12 === 0) {
          fila.style.backgroundColor = 'rgba(82, 171, 152, 0.2)';
          if (document.body.classList.contains('dark')) {
            fila.style.backgroundColor = 'rgba(82, 171, 152, 0.3)';
          }
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

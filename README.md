<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Calculadora de inversión</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.28/jspdf.plugin.autotable.min.js"></script>
  <style>
          * === SOLUCIÓN: Oculta el título automático de GitHub Pages === */
          .pagehead, .gh-header, .repohead, .Header { display: none !important; }
    :root {
      --fondo-claro: #f4f6f8;
      --texto-claro: #333;
      --primario: #2b6777;
      --hover: #1b4d5b;
      --tabla-head: #ddeeee;
      --boton-texto: #fff;
      --portada: #2e3552;
      --verde: #28a745;
      --verde-hover: #218838;
      --texto-grande: 16px;
    }
    body.dark {
      --fondo-claro: #121212;
      --texto-claro: #e0e0e0;
      --tabla-head: #1f1f1f;
      --boton-texto: #fff;
    }
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: var(--fondo-claro);
      color: var(--texto-claro);
      padding: 20px;
      max-width: 900px;
      margin: auto;
      transition: background-color 0.4s, color 0.4s;
    }
    #portada {
      background-color: var(--portada);
      color: #fff;
      text-align: center;
      padding: 20px;
      border-radius: 8px;
      margin-bottom: 20px;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 150px;
      position: relative;
    }
    #portada img {
      width: 100%;
      object-fit: cover;
      border-radius: 8px;
    }
    /* === Botones superiores === */
    .top-buttons {
      position: absolute;
      top: 20px;
      right: 20px;
      display: flex;
      gap: 10px;
    }
    .dark-mode-btn {
      background-color: var(--primario);
      color: var(--boton-texto);
      border: none;
      border-radius: 6px;
      padding: 8px 12px;
      cursor: pointer;
      font-size: 14px;
      transition: background-color 0.3s;
    }
    .whatsapp-btn {
      background-color: #25D366;
      color: white;
      border: none;
      border-radius: 6px;
      padding: 8px 12px;
      cursor: pointer;
      font-size: 14px;
      display: flex;
      align-items: center;
      gap: 5px;
      transition: background-color 0.3s;
    }
    .whatsapp-btn:hover {
      background-color: #128C7E;
    }
    .whatsapp-btn svg {
      fill: white;
    }
    label {
      margin-top: 15px;
      display: block;
      font-weight: 600;
      font-size: var(--texto-grande);
    }
    input {
      padding: 10px;
      border: 1px solid #ccc;
      width: 100%;
      border-radius: 5px;
      margin-top: 5px;
      background-color: #fff;
      transition: background-color 0.3s, color 0.3s;
    }
    body.dark input {
      background-color: #2a2a2a;
      color: #e0e0e0;
      border: 1px solid #555;
    }
    .input-container {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-top: 5px;
    }
    .input-container input {
      width: 20%;
    }
    .input-container span {
      font-weight: normal;
      font-size: 14px;
      color: var(--texto-claro);
      width: 100%;
      padding-left: 10px;
      word-wrap: break-word;
    }
    button {
      padding: 10px 16px;
      background-color: var(--primario);
      color: var(--boton-texto);
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 14px;
      font-weight: 600;
      transition: background-color 0.3s, transform 0.2s;
    }
    .boton-calcular {
      background-color: var(--verde);
      width: 160px;
    }
    .boton-calcular:hover {
      background-color: var(--verde-hover);
    }
    .result {
      margin-top: 20px;
      font-size: 16px;
      font-weight: bold;
      color: var(--primario);
    }
    #tablaResultados {
      width: 100%;
      margin-top: 20px;
      border-collapse: collapse;
      background-color: #fff;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      display: none;
    }
    #tablaResultados th, 
    #tablaResultados td {
      padding: 12px 8px;
      text-align: center;
      border-bottom: 1px solid #eee;
      white-space: nowrap;
    }
    #tablaResultados th {
      background-color: var(--primario);
      color: white;
      position: sticky;
      top: 0;
    }
    body.dark #tablaResultados {
      background-color: #1f1f1f;
      color: #e0e0e0;
    }
    body.dark #tablaResultados th {
      background-color: #2c2c2c;
    }
    body.dark #tablaResultados td {
      border-color: #444;
    }
    canvas {
      margin-top: 30px;
      background-color: #fff;
      border-radius: 8px;
      padding: 10px;
      width: 100% !important;
    }
    body.dark canvas {
      background-color: #1f1f1f;
    }
    .buttons {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 15px;
    }
    .leyenda {
      font-size: 14px;
      font-style: italic;
      margin-top: 20px;
      margin-bottom: -5px;
      color: #555;
    }
    body.dark .leyenda {
      color: #aaa;
    }
    .tabla-container {
      overflow-x: auto;
      margin-top: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    .tabla-titulo {
      background-color: var(--primario);
      color: white;
      padding: 12px;
      border-radius: 8px 8px 0 0;
      font-weight: bold;
      display: none;
    }
    body.dark .tabla-titulo {
      background-color: #2c2c2c;
    }
    select {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin-top: 5px;
      background-color: #fff;
      transition: background-color 0.3s, color 0.3s;
    }
    body.dark select {
      background-color: #2a2a2a;
      color: #e0e0e0;
      border: 1px solid #555;
    }

    /* Ajustes específicos para móvil */
    @media (max-width: 768px) {
      .input-container {
        flex-direction: column;
        gap: 5px;
      }
      .input-container input, 
      .input-container select {
        width: 100% !important;
        font-size: 16px;
      }
      .input-container span {
        padding-left: 0;
        font-size: 14px;
      }
      #portada {
        min-height: 100px;
      }
      .top-buttons {
        flex-direction: column;
        gap: 5px;
        top: 10px;
        right: 10px;
      }
      .dark-mode-btn, .whatsapp-btn {
        padding: 6px 10px;
        font-size: 12px;
      }
    }
  </style>
</head>
<body>
  <div id="portada">
    <img src="https://raw.githubusercontent.com/JohanMoran/Calculadora-de-Inversion/main/Johan_Moran.PNG" 
         alt="Calculadora de Inversión"
         style="width: 100%; max-width: 900px; height: auto; border-radius: 8px;">
    <div class="top-buttons">
      <button class="whatsapp-btn" onclick="abrirWhatsApp()">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
          <path fill="currentColor" d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-6.29 3.617c-.545 0-1.06-.113-1.529-.339l-1.12.328.342-1.072c-.347-.535-.549-1.156-.549-1.825 0-1.91 1.593-3.463 3.554-3.463.943 0 1.829.368 2.497 1.037.668.668 1.037 1.556 1.037 2.497 0 1.96-1.553 3.553-3.462 3.553m6.29-13.998c-3.242 0-5.878 2.636-5.878 5.882 0 1.073.29 2.073.79 2.932L6.22 20.806l5.592-1.645c.86.493 1.86.785 2.96.785 3.242 0 5.88-2.636 5.88-5.88 0-3.245-2.638-5.882-5.88-5.882"/>
        </svg>
        WhatsApp
      </button>
      <button class="dark-mode-btn" onclick="toggleDarkMode()">🌙 Modo Oscuro</button>
    </div>
  </div>

  <label>MONTO INICIAL:</label>
  <div class="input-container">
    <input type="text" id="capitalInicial" />
    <span>¿Con qué cantidad cuentas en este momento? ¿Con cuánto empezarás tu inversión?</span>
  </div>

  <label>Tasa Anual (%):</label>
  <div class="input-container">
    <input type="number" id="tasa" step="0.01" />
    <span>Tasa de Interés anual, inversionistas conservadores (renta fija) 10% - 15%.</span>
  </div>

  <label>Plazo (en meses):</label>
  <div class="input-container">
    <input type="number" id="plazo" min="1" />
    <span>¿Cuántos años vas a realizar la inversión? ¿Cuál es tu horizonte de inversión?</span>
  </div>

  <label>Aportación:</label>
  <div class="input-container">
    <input type="text" id="aportacion" />
    <span>¿Cuánto puedes destinar a tu inversión periódicamente para incrementar tus rendimientos?</span>
  </div>

  <label>Periodicidad de aportación:</label>
  <div class="input-container">
    <select id="periodicidad" style="width: 20%; padding: 10px; border-radius: 5px;">
      <option value="1">Mensual</option>
      <option value="2">Bimestral</option>
      <option value="3">Trimestral</option>
      <option value="6">Semestral</option>
      <option value="12">Anual</option>
    </select>
    <span>Selecciona con qué frecuencia realizarás tus aportaciones</span>
  </div>

  <label>Fecha de inicio:</label>
  <div class="input-container">
    <input type="date" id="fechaInicio" />
    <span>Fecha en que tienes pensado dar inicio a tu inversión</span>
  </div>

  <label>Capital objetivo (opcional):</label>
  <div class="input-container">
    <input type="number" id="capitalObjetivo" placeholder="Ej: 500000" />
    <span>¿Ya tienes un objetivo (ir de viaje, comprar un auto, etc.)? Elige un monto con el que alcanzarás ese objetivo</span>
  </div>

  <div class="leyenda">
    Calculadora de Interés Compuesto con Aportación periódica. Herramienta para uso estrictamente con fines informativos y educativos.
  </div>

  <div class="buttons">
    <button class="boton-calcular" onclick="calcular()">Calcular</button>
    <button onclick="descargarCSV()">Descargar Excel</button>
    <button onclick="descargarPDF()">Descargar PDF</button>
  </div>

  <div class="result" id="resultado"></div>
  <div class="result" id="resumenFinal"></div>
  <canvas id="grafica" height="300"></canvas>

  <div class="tabla-titulo" id="tablaTitulo">Tabla Amortizada de Inversión</div>
  <div class="tabla-container">
    <table id="tablaResultados">
      <thead>
        <tr>
          <th>Mes</th>
          <th>Fecha</th>
          <th>Aportación ($)</th>
          <th>Interés ($)</th>
          <th>Total ($)</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </div>

  <script>
    let datosGrafica = [];
    let totalAportaciones = 0, totalInteres = 0, capital = 0;
    let chart = null;

    function toggleDarkMode() {
      document.body.classList.toggle("dark");
      if (chart) {
        chart.update();
      }
    }

    function abrirWhatsApp() {
      const numero = "3318853923";
      const mensaje = "Hola, me interesa saber más sobre inversiones...";
      const url = `https://wa.me/${numero}?text=${encodeURIComponent(mensaje)}`;
      window.open(url, '_blank');
    }

    // Función para formatear con $ mientras se escribe
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

    // Asignar eventos a los inputs monetarios
    document.getElementById('capitalInicial').addEventListener('input', function() {
      formatearMoneda(this);
    });
    
    document.getElementById('aportacion').addEventListener('input', function() {
      formatearMoneda(this);
    });

    function calcular() {
      // Limpiar el $ para los cálculos
      const capitalInicial = parseFloat(document.getElementById('capitalInicial').value.replace(/[^0-9.]/g, '')) || 0;
      const tasa = parseFloat(document.getElementById('tasa').value) || 0;
      const plazo = parseInt(document.getElementById('plazo').value) || 0;
      const aportacion = parseFloat(document.getElementById('aportacion').value.replace(/[^0-9.]/g, '')) || 0;
      const periodicidad = parseInt(document.getElementById('periodicidad').value) || 1;
      const capitalObjetivo = parseFloat(document.getElementById('capitalObjetivo').value) || null;
      const fechaInicio = new Date(document.getElementById('fechaInicio').value);

      if (plazo <= 0 || tasa <= 0) {
        alert("Por favor, ingresa un plazo y una tasa válidos.");
        return;
      }

      capital = capitalInicial;
      totalInteres = 0;
      totalAportaciones = 0;
      const tasaMensual = tasa / 12 / 100;
      const tabla = document.querySelector('#tablaResultados tbody');
      tabla.innerHTML = '';
      datosGrafica = [];
      let meses = plazo;
      let cumpleObjetivo = false;

      if (capitalObjetivo) {
        for (let i = 1; i <= 600; i++) {
          const interes = capital * tasaMensual;
          capital += interes;
          if ((i - 1) % periodicidad === 0) {
            capital += aportacion;
            totalAportaciones += aportacion;
          }
          if (capital >= capitalObjetivo) {
            meses = i;
            cumpleObjetivo = true;
            break;
          }
        }
        capital = capitalInicial;
        totalAportaciones = 0;
      }

      for (let i = 1; i <= meses; i++) {
        const interes = capital * tasaMensual;
        totalInteres += interes;
        capital += interes;
        
        const esAportacion = (i - 1) % periodicidad === 0;
        if (esAportacion) {
          capital += aportacion;
          totalAportaciones += aportacion;
        }

        const fecha = new Date(fechaInicio);
        fecha.setMonth(fecha.getMonth() + i);

        tabla.innerHTML += `
          <tr>
            <td>${i}</td>
            <td>${fecha.toLocaleDateString('es-MX')}</td>
            <td>${esAportacion ? formatCurrency(aportacion) : '$0.00'}</td>
            <td>${formatCurrency(interes)}</td>
            <td>${formatCurrency(capital)}</td>
          </tr>
        `;

        datosGrafica.push({ mes: i, total: capital });
      }

      let periodicidadTexto = '';
      switch(periodicidad) {
        case 1: periodicidadTexto = 'mensual'; break;
        case 2: periodicidadTexto = 'bimestral'; break;
        case 3: periodicidadTexto = 'trimestral'; break;
        case 6: periodicidadTexto = 'semestral'; break;
        case 12: periodicidadTexto = 'anual'; break;
      }

      document.getElementById('resultado').innerHTML = `
        <strong>Resumen de Inversión:</strong><br>
        Capital inicial: ${formatCurrency(capitalInicial)}<br>
        Tasa de interés anual: ${tasa}%<br>
        Plazo: ${meses} meses<br>
        Aportación ${periodicidadTexto}: ${formatCurrency(aportacion)}<br>
        Total aportado: ${formatCurrency(totalAportaciones)}<br>
        Total interés generado: ${formatCurrency(totalInteres)}<br>
        <strong>Total al final del plazo: ${formatCurrency(capital)}</strong>
      `;

      if (cumpleObjetivo) {
        const años = Math.floor(meses / 12);
        const mesesRestantes = meses % 12;
        
        let textoMeses = "";
        if (años > 0) {
          textoMeses += `${años} ${años === 1 ? 'año' : 'años'}`;
        }
        if (mesesRestantes > 0) {
          if (años > 0) textoMeses += " y ";
          textoMeses += `${mesesRestantes} ${mesesRestantes === 1 ? 'mes' : 'meses'}`;
        }
        if (meses < 12) {
          textoMeses = `${meses} ${meses === 1 ? 'mes' : 'meses'}`;
        }

        document.getElementById('resumenFinal').innerHTML = `
          🎉 <strong>¡Objetivo de ${formatCurrency(capitalObjetivo)} alcanzado en ${textoMeses}!</strong>
        `;
      }

      document.getElementById('tablaResultados').style.display = "table";
      document.getElementById('tablaTitulo').style.display = "block";

      generarGrafico();
    }

    function formatCurrency(value) {
      return new Intl.NumberFormat('es-MX', { 
        style: 'currency', 
        currency: 'MXN',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2
      }).format(value);
    }

    function generarGrafico() {
      const ctx = document.getElementById('grafica').getContext('2d');
      
      if (chart) {
        chart.destroy();
      }

      chart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: datosGrafica.map(d => `Mes ${d.mes}`),
          datasets: [{
            label: 'Total acumulado (MXN)',
            data: datosGrafica.map(d => d.total),
            borderColor: '#2b6777',
            backgroundColor: 'rgba(43, 103, 119, 0.1)',
            fill: true,
            tension: 0.3
          }]
        },
        options: {
          responsive: true,
          plugins: {
            legend: {
              position: 'top',
            },
            tooltip: {
              callbacks: {
                label: (context) => {
                  return ` ${formatCurrency(context.raw)}`;
                }
              }
            }
          },
          scales: {
            y: {
              beginAtZero: false,
              ticks: {
                callback: (value) => formatCurrency(value)
              }
            }
          }
        }
      });
    }

    function descargarPDF() {
      if (datosGrafica.length === 0) {
        alert("Primero calcula una inversión.");
        return;
      }

      const { jsPDF } = window.jspdf;
      const doc = new jsPDF({
        orientation: 'portrait',
        unit: 'mm',
        format: 'a4'
      });
      
      doc.setFontSize(20);
      doc.setTextColor(43, 103, 119);
      doc.setFont('helvetica', 'bold');
      doc.text("Reporte de Inversión", 105, 15, { align: 'center' });
      doc.setDrawColor(43, 103, 119);
      doc.setLineWidth(0.5);
      doc.line(20, 20, 190, 20);
      
      doc.setFontSize(12);
      doc.setTextColor(0, 0, 0);
      doc.setFont('helvetica', 'normal');
      doc.setFillColor(240, 240, 240);
      doc.rect(20, 25, 170, 30, 'F');
      doc.text("Datos de la inversión", 25, 30);
      
      const capitalInicial = parseFloat(document.getElementById('capitalInicial').value.replace(/[^0-9.]/g, '')) || 0;
      const tasa = parseFloat(document.getElementById('tasa').value) || 0;
      const plazo = parseInt(document.getElementById('plazo').value) || 0;
      const aportacion = parseFloat(document.getElementById('aportacion').value.replace(/[^0-9.]/g, '')) || 0;
      const periodicidad = parseInt(document.getElementById('periodicidad').value) || 1;
      
      let periodicidadTexto = '';
      switch(periodicidad) {
        case 1: periodicidadTexto = 'mensual'; break;
        case 2: periodicidadTexto = 'bimestral'; break;
        case 3: periodicidadTexto = 'trimestral'; break;
        case 6: periodicidadTexto = 'semestral'; break;
        case 12: periodicidadTexto = 'anual'; break;
      }

      doc.text(`Capital inicial: ${formatCurrency(capitalInicial)}`, 25, 37);
      doc.text(`Tasa anual: ${tasa}% | Plazo: ${plazo} meses`, 25, 44);
      doc.text(`Aportación ${periodicidadTexto}: ${formatCurrency(aportacion)}`, 25, 51);
      
      doc.setFillColor(230, 245, 230);
      doc.rect(20, 60, 170, 20, 'F');
      doc.text("Resultados finales", 25, 65);
      doc.text(`Total aportado: ${formatCurrency(totalAportaciones)}`, 25, 72);
      doc.text(`Interés generado: ${formatCurrency(totalInteres)}`, 100, 72);
      doc.setFont('helvetica', 'bold');
      doc.text(`Total acumulado: ${formatCurrency(capital)}`, 25, 79);
      doc.setFont('helvetica', 'normal');

      setTimeout(() => {
        const canvas = document.getElementById('grafica');
        const imgData = canvas.toDataURL('image/png', 1.0);
        doc.addImage(imgData, 'PNG', 20, 85, 170, 80);

        doc.autoTable({
          html: '#tablaResultados',
          startY: 170,
          theme: 'grid',
          headStyles: {
            fillColor: [43, 103, 119],
            textColor: 255,
            fontSize: 10
          },
          bodyStyles: {
            fontSize: 8
          },
          columnStyles: {
            0: { cellWidth: 15 },
            1: { cellWidth: 25 },
            2: { cellWidth: 25 },
            3: { cellWidth: 25 },
            4: { cellWidth: 25 }
          }
        });

        doc.setFontSize(10);
        doc.setTextColor(100);
        doc.text("© Calculadora de Inversión - " + new Date().toLocaleDateString(), 105, 285, { align: 'center' });
        
        doc.save('reporte_inversion.pdf');
      }, 300);
    }

    function descargarCSV() {
      if (datosGrafica.length === 0) {
        alert("Primero calcula una inversión.");
        return;
      }
      
      let csv = "Mes,Fecha,Aportación ($),Interés ($),Total ($)\n";
      const rows = document.querySelectorAll('#tablaResultados tbody tr');
      
      rows.forEach(row => {
        const cells = row.querySelectorAll('td');
        const aportacionValue = cells[2].textContent === '$0.00' ? '0' : cells[2].textContent.replace(/[^0-9.]/g, '');
        csv += `"${cells[0].textContent}","${cells[1].textContent}","${aportacionValue}","${cells[3].textContent.replace(/[^0-9.]/g, '')}","${cells[4].textContent.replace(/[^0-9.]/g, '')}"\n`;
      });
      
      const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
      const link = document.createElement('a');
      link.href = URL.createObjectURL(blob);
      link.download = 'inversion.csv';
      link.click();
    }
  </script>
</body>
</html>


<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Calculadora PVC con Facturación</title>
<style>
  * { box-sizing: border-box; }
  body {
    font-family: 'Orbitron', sans-serif;
    background: radial-gradient(circle at top, #0b0b20, #000);
    color: white;
    margin: 0;
    padding: 20px;
    min-height: 100vh;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 400px 1fr;
    gap: 25px;
  }

  .panel {
    background: rgba(15, 20, 50, 0.85);
    border-radius: 20px;
    box-shadow: 0 0 25px #00bcd4;
    padding: 25px;
    border: 2px solid #00bcd4;
    height: fit-content;
  }

  h1 {
    text-align: center;
    color: #00ffcc;
    margin-bottom: 20px;
    font-size: 1.6em;
  }

  h2 {
    color: #00bcd4;
    font-size: 1.2em;
    margin-bottom: 15px;
    border-bottom: 2px solid #00bcd4;
    padding-bottom: 10px;
  }

  .tabs {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
  }

  .tab {
    flex: 1;
    padding: 12px;
    background: #0a0a1a;
    border: 2px solid #00bcd4;
    border-radius: 10px;
    cursor: pointer;
    text-align: center;
    transition: 0.3s;
    font-weight: bold;
    font-size: 0.9em;
  }

  .tab:hover {
    background: #00bcd4;
    color: #000;
  }

  .tab.active {
    background: linear-gradient(145deg, #00bcd4, #00ffcc);
    color: #000;
  }

  .tab-content {
    display: none;
  }

  .tab-content.active {
    display: block;
  }

  label {
    color: #aee;
    font-size: 0.9em;
    display: block;
    margin-top: 10px;
  }

  input, select {
    width: 100%;
    padding: 10px;
    border-radius: 10px;
    border: none;
    background: #0a0a1a;
    color: #00ffcc;
    margin-bottom: 10px;
    font-size: 0.95em;
  }

  .dimension-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
  }

  button {
    width: 100%;
    padding: 12px;
    font-size: 1.05em;
    background: linear-gradient(145deg, #0f0f2f, #1c1c3a);
    color: #00ffcc;
    border: 2px solid #00bcd4;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.2s;
    margin-top: 10px;
    font-weight: bold;
  }

  button:hover {
    background: #00bcd4;
    color: #fff;
    transform: scale(1.02);
  }

  .resultado {
    background: #0a0a1a;
    border-radius: 10px;
    padding: 15px;
    margin-top: 15px;
    font-size: 0.9em;
    line-height: 1.8;
  }

  .resultado p {
    margin: 8px 0;
    padding: 6px;
    background: rgba(0, 188, 212, 0.1);
    border-left: 3px solid #00ffcc;
    padding-left: 10px;
  }

  .mensaje {
    background: rgba(0, 255, 204, 0.1);
    padding: 12px;
    border-left: 3px solid #00ffcc;
    border-radius: 10px;
    margin-top: 15px;
    font-size: 0.85em;
    line-height: 1.6;
  }

  .info-box {
    background: rgba(0, 188, 212, 0.2);
    padding: 12px;
    border-radius: 10px;
    margin-top: 15px;
    font-size: 0.85em;
    text-align: center;
  }

  .texture-preview {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    margin-top: 15px;
  }

  .texture-item {
    background: #0a0a1a;
    border: 2px solid #00bcd4;
    border-radius: 10px;
    padding: 10px;
    text-align: center;
    cursor: pointer;
    transition: 0.3s;
  }

  .texture-item:hover {
    border-color: #00ffcc;
    transform: scale(1.05);
  }

  .texture-item.selected {
    border-color: #00ffcc;
    background: rgba(0, 255, 204, 0.1);
  }

  .texture-item div {
    width: 100%;
    height: 55px;
    border-radius: 5px;
    margin-bottom: 5px;
  }

  /* Estilos de Factura/Cotización */
  .factura {
    background: white;
    color: #000;
    padding: 35px;
    border-radius: 15px;
  }

  .factura-header {
    display: flex;
    justify-content: space-between;
    align-items: start;
    border-bottom: 3px solid #00bcd4;
    padding-bottom: 20px;
    margin-bottom: 20px;
  }

  .factura-logo {
    font-size: 2.2em;
    font-weight: bold;
    color: #00bcd4;
  }

  .factura-info {
    text-align: right;
    font-size: 0.95em;
  }

  .factura-info h3 {
    color: #00bcd4;
    margin: 0 0 10px 0;
    font-size: 1.5em;
  }

  /* Cuadro de Metraje Destacado */
  .cuadro-metraje {
    background: linear-gradient(135deg, #00bcd4, #00ffcc);
    color: white;
    padding: 25px 30px;
    border-radius: 15px;
    margin-bottom: 25px;
    box-shadow: 0 8px 20px rgba(0, 188, 212, 0.4);
    border: 3px solid #00bcd4;
  }

  .cuadro-metraje-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
  }

  .cuadro-metraje-left {
    flex: 1;
  }

  .cuadro-metraje-titulo {
    font-size: 1.1em;
    opacity: 0.95;
    margin-bottom: 8px;
    font-weight: 600;
  }

  .cuadro-metraje-dimensiones {
    font-size: 1.4em;
    font-weight: bold;
    line-height: 1.3;
  }

  .cuadro-metraje-right {
    background: rgba(255,255,255,0.2);
    padding: 20px 25px;
    border-radius: 12px;
    text-align: center;
    min-width: 180px;
  }

  .cuadro-metraje-label {
    font-size: 0.9em;
    opacity: 0.9;
    margin-bottom: 5px;
  }

  .cuadro-metraje-numero {
    font-size: 2.8em;
    font-weight: bold;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
  }

  .cliente-info {
    background: #f5f5f5;
    padding: 18px;
    border-radius: 10px;
    margin-bottom: 25px;
  }

  .cliente-info h3 {
    margin-top: 0;
    color: #00bcd4;
    font-size: 1.2em;
  }

  .cliente-info input {
    background: white;
    color: #000;
    border: 1px solid #ccc;
    margin-bottom: 10px;
    padding: 10px;
    font-size: 0.95em;
  }

  .tabla-factura {
    width: 100%;
    border-collapse: collapse;
    margin: 25px 0;
  }

  .tabla-factura th {
    background: #00bcd4;
    color: white;
    padding: 14px 12px;
    text-align: left;
    font-weight: bold;
    font-size: 0.95em;
  }

  .tabla-factura td {
    padding: 12px;
    border-bottom: 1px solid #ddd;
  }

  .tabla-factura input {
    width: 90px;
    padding: 6px;
    border: 1px solid #ccc;
    border-radius: 5px;
    text-align: right;
    background: white;
    color: #000;
    font-size: 0.9em;
  }

  .tabla-factura .item-desc {
    font-weight: 600;
    color: #333;
  }

  .tabla-factura .subtotal {
    text-align: right;
    font-weight: bold;
    color: #00bcd4;
    font-size: 1.05em;
  }

  .totales {
    margin-top: 25px;
    text-align: right;
    font-size: 1.15em;
  }

  .totales .total-final {
    background: #00bcd4;
    color: white;
    font-size: 1.5em;
    font-weight: bold;
    padding: 15px;
    border-radius: 10px;
    margin-top: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .btn-group {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin-top: 25px;
  }

  .btn-imprimir, .btn-whatsapp {
    background: #00bcd4;
    color: white;
    border: none;
    padding: 14px 20px;
    border-radius: 10px;
    font-size: 1em;
    cursor: pointer;
    font-weight: bold;
    transition: 0.3s;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
  }

  .btn-whatsapp {
    background: #25d366;
    grid-column: 1 / -1;
  }

  .btn-imprimir:hover {
    background: #00ffcc;
    color: #000;
    transform: scale(1.05);
  }

  .btn-whatsapp:hover {
    background: #128c7e;
    transform: scale(1.05);
  }

  .notas-factura {
    margin-top: 25px;
    padding: 18px;
    background: #f9f9f9;
    border-radius: 10px;
    font-size: 0.9em;
    color: #666;
    line-height: 1.7;
  }

  @media (max-width: 1100px) {
    .container {
      grid-template-columns: 1fr;
    }
    .cuadro-metraje-content {
      flex-direction: column;
    }
    .cuadro-metraje-right {
      width: 100%;
    }
  }

  @media print {
    body {
      background: white;
    }
    .panel:not(.factura) {
      display: none;
    }
    .btn-imprimir, .btn-whatsapp {
      display: none;
    }
    .factura {
      box-shadow: none;
      border: none;
    }
  }
</style>
</head>
<body>

  <div class="container">
    <!-- Panel de Calculadora -->
    <div class="panel">
      <h1>🔧 Calculadora PVC</h1>

      <div class="tabs">
        <div class="tab active" onclick="cambiarTab('dimensiones')">📏 Dimensiones</div>
        <div class="tab" onclick="cambiarTab('area')">📐 Área</div>
      </div>

      <div id="tab-dimensiones" class="tab-content active">
        <h2>Ingrese las dimensiones</h2>
        <div class="dimension-row">
          <div>
            <label>Ancho (m):</label>
            <input type="number" id="txtAncho" placeholder="Ej: 5" step="0.1">
          </div>
          <div>
            <label>Largo (m):</label>
            <input type="number" id="txtLargo" placeholder="Ej: 8" step="0.1">
          </div>
        </div>
        <button onclick="calcularPorDimensiones()">Calcular Área</button>
        <div id="areaCalculada" class="info-box" style="display:none;"></div>
      </div>

      <div id="tab-area" class="tab-content">
        <h2>Ingrese el área total</h2>
        <label>Área (m²):</label>
        <input type="number" id="txtMetros" placeholder="Área en m²" step="0.1">
      </div>

     
      <button onclick="calcularMateriales()">🧮 Calcular Materiales</button>

      <div class="resultado" id="resultado"></div>
      <div class="mensaje" id="mensajeFinal"></div>
    </div>

    <!-- Panel de Cotización -->
    <div class="panel factura">
      <div class="factura-header">
        <div>
          <div class="factura-logo">PVC PRO</div>
          <div style="font-size: 0.95em; color: #666; margin-top: 5px;">
            Cielos Rasos y Acabados
          </div>
        </div>
        <div class="factura-info">
          <h3>COTIZACIÓN</h3>
          <div>Fecha: <span id="fechaFactura"></span></div>
          <div style="margin-top: 8px;">Cotización #: <input type="text" id="numFactura" value="001" style="width: 90px; padding: 5px;"></div>
        </div>
      </div>

      <!-- Cuadro de Metraje Destacado -->
      <div id="cuadroMedidas" class="cuadro-metraje" style="display: none;">
        <div class="cuadro-metraje-content">
          <div class="cuadro-metraje-left">
            <div class="cuadro-metraje-titulo">📐 ÁREA TOTAL DEL PROYECTO</div>
            <div id="infoMedidas" class="cuadro-metraje-dimensiones"></div>
          </div>
          <div class="cuadro-metraje-right">
            <div class="cuadro-metraje-label">METROS CUADRADOS</div>
            <div id="metrajeNumero" class="cuadro-metraje-numero"></div>
          </div>
        </div>
      </div>

      <div class="cliente-info">
        <h3>Datos del Cliente</h3>
        <label style="color: #666; font-size: 0.85em; margin-bottom: 5px;">Nombre:</label>
        <input type="text" id="clienteNombre" placeholder="Nombre completo del cliente">
        <label style="color: #666; font-size: 0.85em; margin-bottom: 5px;">Teléfono:</label>
        <input type="text" id="clienteTelefono" placeholder="Número de contacto">
        <label style="color: #666; font-size: 0.85em; margin-bottom: 5px;">Dirección:</label>
        <input type="text" id="clienteDireccion" placeholder="Dirección de instalación">
      </div>

      <table class="tabla-factura">
        <thead>
          <tr>
            <th>Descripción</th>
            <th style="width: 100px; text-align: center;">Cantidad</th>
            <th style="width: 120px; text-align: right;">Precio Unit.</th>
            <th style="width: 120px; text-align: right;">Subtotal</th>
          </tr>
        </thead>
        <tbody id="tablaItems">
          <tr>
            <td colspan="4" style="text-align: center; color: #999; padding: 40px;">
              Calcule los materiales para generar la cotización
            </td>
          </tr>
        </tbody>
      </table>

      <div class="totales">
        <div class="total-final">
          <span>TOTAL:</span>
          <span id="totalFactura">$0</span>
        </div>
      </div>

      <div class="btn-group">
        <button class="btn-imprimir" onclick="imprimirFactura()">
          🖨️ Imprimir
        </button>
        <button class="btn-whatsapp" onclick="enviarWhatsApp()">
          📱 Enviar por WhatsApp
        </button>
      </div>

      <div class="notas-factura">
        <strong>Notas importantes:</strong><br>
        • Los precios pueden ser ajustados según sus necesidades<br>
        • Validez de la cotización: 15 días<br>
        • Instalación profesional disponible<br>
        • Esta cotización es una guía para transcribir a factura física
      </div>
    </div>
  </div>

<script>
  let areaTotal = 0;
  let modeloActual = '';

  // Precios por defecto (editables en la tabla)
  const preciosDefault = {
    laminas: 28000,
    omegas: 4000,
    viguetas: 4000,
    angulos: 3000,
    tornillosLamineros: 40,
    tornillosEstructura: 40,
    perimetrales: 12000
  };

  let materialesCalculados = {};

  // Función para redondear tornillos
  function redondearTornillos(cantidad) {
    const resto = cantidad % 100;
    
    if (resto === 0) {
      return cantidad;
    } else if (resto <= 50) {
      return cantidad - resto + 50;
    } else {
      return cantidad - resto + 100;
    }
  }

  function cambiarTab(tab) {
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
    
    if (tab === 'dimensiones') {
      document.querySelector('.tab:nth-child(1)').classList.add('active');
      document.getElementById('tab-dimensiones').classList.add('active');
    } else {
      document.querySelector('.tab:nth-child(2)').classList.add('active');
      document.getElementById('tab-area').classList.add('active');
    }
  }

  function calcularPorDimensiones() {
    const ancho = parseFloat(document.getElementById('txtAncho').value);
    const largo = parseFloat(document.getElementById('txtLargo').value);
    
    if (!ancho || !largo) {
      alert("⚠️ Por favor ingrese ancho y largo");
      return;
    }
    
    areaTotal = ancho * largo;
    
    document.getElementById('areaCalculada').style.display = 'block';
    document.getElementById('areaCalculada').innerHTML = `
      <strong>📐 Área calculada: ${areaTotal.toFixed(2)} m²</strong><br>
      (${ancho} m × ${largo} m)
    `;
  }

  

  function calcularMateriales() {
    let m2;
    
    if (document.getElementById('tab-dimensiones').classList.contains('active')) {
      if (!areaTotal) {
        alert("⚠️ Primero calcule el área usando las dimensiones");
        return;
      }
      m2 = areaTotal;
    } else {
      m2 = parseFloat(document.getElementById('txtMetros').value);
      if (!m2) {
        alert("⚠️ Por favor ingrese el área en m²");
        return;
      }
    }



    // Cálculo base de tornillos
    const tornillosBase = Math.ceil((m2 * 17) / 2);
    const tornillosRedondeados = redondearTornillos(tornillosBase);

    // Cálculos según las fórmulas
    materialesCalculados = {
      laminas: Math.ceil(m2 / 1.785),
      omegas: Math.ceil(m2 / 0.95),
      viguetas: Math.ceil(m2 / 1.90),
      angulos: Math.ceil(m2 / 1.80),
      tornillosLamineros: tornillosRedondeados,
      tornillosEstructura: tornillosRedondeados,
      perimetrales: Math.ceil(m2 / 6)
    };

    document.getElementById('resultado').innerHTML = `
      <p><b>📦 Láminas necesarias:</b> ${materialesCalculados.laminas} unidades</p>
      <p><b>🔩 Cantidad de Omegas:</b> ${materialesCalculados.omegas} unidades</p>
      <p><b>📏 Cantidad de Viguetas:</b> ${materialesCalculados.viguetas} unidades</p>
      <p><b>📐 Cantidad de Ángulos:</b> ${materialesCalculados.angulos} unidades</p>
      <p><b>🔧 Tornillos Lamineros:</b> ${materialesCalculados.tornillosLamineros} unidades</p>
      <p><b>🔧 Tornillos de Estructura:</b> ${materialesCalculados.tornillosEstructura} unidades</p>
      <p><b>⚙️ Cantidad de Perimetrales:</b> ${materialesCalculados.perimetrales} unidades</p>
    `;

    document.getElementById('mensajeFinal').innerHTML = `
      <strong>📋 Instrucciones de instalación:</strong><br>
      • Instale las omegas cada 50 cm<br>
      • Instale las viguetas cada 80 cm<br>
      • Verifique la altura de los templetes<br>
      • Modelo seleccionado: <strong>${modeloActual.toUpperCase()}</strong>
    `;

    generarFactura();
  }

  function generarFactura() {
    const fecha = new Date();
    document.getElementById('fechaFactura').textContent = fecha.toLocaleDateString('es-CO');

    // Mostrar cuadro de medidas
    const cuadroMedidas = document.getElementById('cuadroMedidas');
    const infoMedidas = document.getElementById('infoMedidas');
    const metrajeNumero = document.getElementById('metrajeNumero');
    
    cuadroMedidas.style.display = 'block';
    
    // Verificar si se usó el tab de dimensiones
    if (document.getElementById('tab-dimensiones').classList.contains('active') && areaTotal > 0) {
      const ancho = parseFloat(document.getElementById('txtAncho').value);
      const largo = parseFloat(document.getElementById('txtLargo').value);
      metrajeNumero.textContent = areaTotal.toFixed(2);
      infoMedidas.innerHTML = `
        <span style="font-size: 0.75em;">Ancho: ${ancho.toFixed(2)}m × Largo: ${largo.toFixed(2)}m</span>
      `;
    } else {
      const m2 = parseFloat(document.getElementById('txtMetros').value);
      metrajeNumero.textContent = m2.toFixed(2);
      infoMedidas.innerHTML = `<span style="font-size: 0.75em;">Área directa ingresada</span>`;
    }

    const tbody = document.getElementById('tablaItems');
    tbody.innerHTML = '';

    const items = [
      { nombre: 'Láminas PVC ' + modeloActual.toUpperCase(), cant: materialesCalculados.laminas, precio: preciosDefault.laminas, key: 'laminas' },
      { nombre: 'Omegas', cant: materialesCalculados.omegas, precio: preciosDefault.omegas, key: 'omegas' },
      { nombre: 'Viguetas', cant: materialesCalculados.viguetas, precio: preciosDefault.viguetas, key: 'viguetas' },
      { nombre: 'Ángulos', cant: materialesCalculados.angulos, precio: preciosDefault.angulos, key: 'angulos' },
      { nombre: 'Tornillos Lamineros', cant: materialesCalculados.tornillosLamineros, precio: preciosDefault.tornillosLamineros, key: 'tornillosLamineros' },
      { nombre: 'Tornillos de Estructura', cant: materialesCalculados.tornillosEstructura, precio: preciosDefault.tornillosEstructura, key: 'tornillosEstructura' },
      { nombre: 'Perimetrales', cant: materialesCalculados.perimetrales, precio: preciosDefault.perimetrales, key: 'perimetrales' }
    ];

    items.forEach(item => {
      const tr = document.createElement('tr');
      tr.innerHTML = `
        <td class="item-desc">${item.nombre}</td>
        <td style="text-align: center;"><input type="number" value="${item.cant}" onchange="recalcularFactura()" data-key="${item.key}" class="cant-input"></td>
        <td style="text-align: right;"><input type="number" value="${item.precio}" onchange="recalcularFactura()" data-key="${item.key}" class="precio-input"></td>
        <td class="subtotal">$${(item.cant * item.precio).toLocaleString('es-CO')}</td>
      `;
      tbody.appendChild(tr);
    });

    recalcularFactura();
  }

  function recalcularFactura() {
    let total = 0;
    const rows = document.querySelectorAll('#tablaItems tr');
    
    rows.forEach(row => {
      const cantInput = row.querySelector('.cant-input');
      const precioInput = row.querySelector('.precio-input');
      const subtotalTd = row.querySelector('.subtotal');
      
      if (cantInput && precioInput) {
        const cant = parseFloat(cantInput.value) || 0;
        const precio = parseFloat(precioInput.value) || 0;
        const itemSubtotal = cant * precio;
        
        subtotalTd.textContent = '$' + itemSubtotal.toLocaleString('es-CO');
        total += itemSubtotal;
      }
    });

    document.getElementById('totalFactura').textContent = '$' + total.toLocaleString('es-CO');
  }

  function imprimirFactura() {
    window.print();
  }

  function enviarWhatsApp() {
    const clienteNombre = document.getElementById('clienteNombre').value;
    const clienteTelefono = document.getElementById('clienteTelefono').value;
    const total = document.getElementById('totalFactura').textContent;
    const numFactura = document.getElementById('numFactura').value;
    const metraje = document.getElementById('metrajeNumero').textContent;

    if (!clienteNombre || !clienteTelefono) {
      alert('⚠️ Por favor complete el nombre y teléfono del cliente');
      return;
    }

    const mensaje = `🔧 *COTIZACIÓN PVC PRO #${numFactura}*

📋 Cliente: ${clienteNombre}
📅 Fecha: ${document.getElementById('fechaFactura').textContent}

*Materiales:*
${Array.from(document.querySelectorAll('#tablaItems tr')).map(tr => {
  const desc = tr.querySelector('.item-desc');
  const cant = tr.querySelector('.cant-input');
  const precio = tr.querySelector('.precio-input');
  if (desc && cant && precio) {
    return `• ${desc.textContent}: ${cant.value} und x $${parseFloat(precio.value).toLocaleString('es-CO')}`;
  }
  return '';
}).filter(Boolean).join('\n')}

💰 *TOTAL: ${total}*

✅ Validez: 15 días
🏗️ Instalación profesional disponible

_PVC PRO - Cielos Rasos y Acabados_`;

    const numeroLimpio = clienteTelefono.replace(/\D/g, '');
    const url = `https://wa.me/${numeroLimpio}?text=${encodeURIComponent(mensaje)}`;
    
    window.open(url, '_blank');
  }

  // Establecer fecha al cargar
  window.addEventListener('load', () => {
    const fecha = new Date();
    document.getElementById('fechaFa ctura').textContent = fecha.toLocaleDateString('es-CO');
  });
</script>
</body>
</html>

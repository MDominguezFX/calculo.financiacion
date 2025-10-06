<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
  <title>Forma de pago — Sin interés</title>
  <meta name="description" content="Calculadora de formas de pago sin interés con entrega, fechas cada 30 días, exportación a PNG y opción E‑CHEQS con tipo de cambio. Optimizada para móviles con encabezado y aviso de tipo de cambio." />
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#0e0f12; --bg2:#0b0c10; --card:#101216; --edge:#1a1f27;
      --text:#e6e7ea; --muted:#9aa3ad; --accent:#10a37f; --accent-2:#2dd4bf; --accent-3:#0b7e62;
      --warn:#f59e0b;
    }
    @media (prefers-color-scheme: dark){
      :root{ color-scheme: dark light; }
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0; font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Cantarell,"Helvetica Neue",Arial;
      background:radial-gradient(1200px 600px at 20% -10%, rgba(16,163,127,.14), transparent 40%),
                 radial-gradient(800px 400px at 100% 10%, rgba(45,212,191,.10), transparent 50%),
                 linear-gradient(180deg,var(--bg),var(--bg2) 60%, var(--bg));
      color:var(--text); display:flex; align-items:flex-start; justify-content:center; padding:16px 16px 24px;
      -webkit-tap-highlight-color: transparent;
      background-attachment: fixed;
    }
    @media (max-width: 768px) {
      body { padding-top: calc(64px + env(safe-area-inset-top)); padding-bottom: calc(48px + env(safe-area-inset-bottom)); }
      .card:first-child { margin-top: 12px; }
    }

    .app{width:100%; max-width:1140px}
    .grid{display:grid; gap:14px; grid-template-columns:1fr}
    @media(min-width:1000px){ .grid{grid-template-columns:1.05fr .95fr} }

    .card{ background:linear-gradient(180deg, rgba(255,255,255,.02), rgba(255,255,255,.00)), var(--card);
      border:1px solid var(--edge); border-radius:16px; box-shadow:0 10px 24px rgba(0,0,0,.35); overflow:hidden; }
    .content{ padding:16px }
    h1{ font-size:18px; margin:0; letter-spacing:.2px; display:flex; gap:10px; align-items:center; flex-wrap:wrap }
    .dot{ width:10px; height:10px; border-radius:999px; background:var(--accent); box-shadow:0 0 18px var(--accent) }
    h2{ font-size:18px; margin:2px 0 10px }
    label{ display:block; margin:8px 0 6px; font-weight:600; color:#d6dde4 }

    input[type="number"], select, input[type="range"], input[type="text"], input[type="date"]{
      width:100%; padding:14px 14px; background:#0b0d11; border:1px solid var(--edge);
      color:#e6e7ea; border-radius:12px; outline:none; font-size:16px;
    }
    input[type="number"]::-webkit-outer-spin-button,
    input[type="number"]::-webkit-inner-spin_button{ -webkit-appearance:none; margin:0 }
    .row{ display:flex; gap:10px; flex-wrap:wrap }
    .row > *{ flex:1 1 200px }

    .chip{
      border:1px solid var(--edge); background:#0c1014; padding:10px 14px; border-radius:12px; cursor:pointer;
      font-weight:600; color:#cdd6de; transition:.2s transform, .2s background, .2s border, .2s color; user-select:none;
      touch-action:manipulation;
    }
    .chip:hover{ transform:translateY(-1px); border-color:#263142 }
    .chip.active{ background:#0d1519; border-color:#2a3a46; color:#e8f9f3 }

    .segmented{ display:flex; gap:8px; background:#0c1014; border:1px solid var(--edge); border-radius:12px; padding:6px; overflow:auto }
    .segmented button{
      flex:1; padding:12px 14px; background:transparent; border:1px solid transparent; border-radius:8px;
      color:#cdd6de; cursor:pointer; font-weight:700; font-size:16px; min-width:140px; touch-action:manipulation;
    }
    .segmented button.active{ background:#0d1519; border-color:#2a3a46; color:#e8f9f3 }

    .switch{display:flex; align-items:center; gap:10px; margin-top:8px}
    .switch input{ width:52px; height:28px; appearance:none; background:#12161c; border:1px solid #2a3442; border-radius:999px; position:relative; cursor:pointer }
    .switch input:checked{ background:#113c32; border-color:#1b6b56 }
    .switch input::after{ content:""; position:absolute; top:3px; left:3px; width:22px; height:22px; background:#e5e7eb; border-radius:50%; transition:.2s left }
    .switch input:checked::after{ left:27px; }
    .muted{ color:#9aa3ad; font-size:13px }

    .btn{ padding:14px 16px; border-radius:12px; border:1px solid var(--edge);
      background:#0b0f14; color:#e5e7eb; cursor:pointer; font-weight:700; transition:.2s transform, .2s background, .2s border; font-size:16px; }
    .btn:hover{ transform:translateY(-1px) }
    .btn.primary{ background:linear-gradient(180deg,var(--accent),var(--accent-3)); border-color:#0d5d49 }
    .btn.bar{ display:flex; gap:10px; flex-wrap:wrap }
    .btn.bar .btn{ flex:1 1 160px }

    .stat{ background:linear-gradient(180deg,#0f141a,#0c1117); border:1px solid var(--edge); border-radius:14px; padding:12px; }
    .stat .k{ font-size:12px; color:#b1bcc7 }
    .stat .v{ font-size:20px; font-weight:700; letter-spacing:.2px; word-break:break-word }

    .tableWrap{ width:100%; overflow:auto; -webkit-overflow-scrolling:touch; border-radius:12px; border:1px solid var(--edge) }
    table{ width:100%; border-collapse:collapse; min-width:560px; }
    th, td{ padding:12px 10px; border-bottom:1px solid var(--edge); text-align:left; white-space:nowrap }
    th{ color:#d1d7de; font-weight:600; background:#0e1218; position:sticky; top:0 }
    tfoot td{ font-weight:700 }
    .footer{ text-align:center; margin-top:12px; color:#9aa7b3; font-size:12px }

    .inline{ display:flex; align-items:center; gap:10px; flex-wrap:wrap }
    .pct-badge{ padding:6px 10px; border-radius:10px; background:#0d1418; border:1px solid var(--edge);
      font-weight:700; color:#bfe7da; min-width:56px; text-align:center }
    .group{ border:1px dashed #1f2a34; border-radius:12px; padding:10px }

    /* Área a exportar como PNG */
    #exportArea{ padding:12px }
    .headerRow{ display:flex; justify-content:space-between; align-items:center; gap:10px; flex-wrap:wrap; margin-bottom:8px }
    .brandTitle{ font-size:22px; font-weight:800; letter-spacing:.6px; text-transform:uppercase }
    .badge{ padding:6px 10px; border:1px solid var(--edge); border-radius:999px; font-size:12px; color:#cfeee4 }
    .note{ font-size:12px; color:#a6b3bf }
    .disclaimer{ margin-top:10px; font-size:12px; color:#a6b3bf }
  </style>
</head>
<body>
  <div class="app">
    <div class="grid">
      <section class="card">
        <div class="content">
          <h1><span class="dot"></span>Forma de pago — sin interés</h1>
          <h2>Ingreso de datos</h2>

          <label for="monto">Monto total</label>
          <input id="monto" type="number" min="0" step="0.01" placeholder="Ej.: 150000" value="150000" />

          <div class="row" style="margin-top:8px">
            <div>
              <label for="moneda">Moneda</label>
              <select id="moneda">
                <option value="ARS" selected>ARS — Pesos argentinos</option>
                <option value="USD">USD — Dólares</option>
              </select>
            </div>
            <div>
              <label for="cuotasCustom">Cuotas (n)</label>
              <input id="cuotasCustom" type="number" min="1" step="1" placeholder="Ej.: 6" value="6" />
            </div>
          </div>

          <div class="row" style="margin-top:8px">
            <div>
              <label for="fechaInicio">Fecha de inicio</label>
              <input id="fechaInicio" type="date" />
            </div>
            <div>
              <label class="muted" style="margin-top:26px">Cuotas cada 30 días (mueve a lunes si cae fin de semana)</label>
            </div>
          </div>

          <!-- E‑CHEQS -->
          <div class="group" style="margin-top:8px">
            <div class="inline" style="justify-content:space-between; gap:10px">
              <div class="inline" style="gap:8px">
                <input id="echeqsToggle" type="checkbox" />
                <label for="echeqsToggle" style="margin:0">Pago con <strong>E‑CHEQS</strong> (USD → ARS)</label>
              </div>
              <div class="inline" style="gap:8px; min-width:200px; flex:1">
                <label for="tipoCambio" style="margin:0">TC ARS/USD</label>
                <input id="tipoCambio" type="number" min="0" step="0.01" placeholder="Ej.: 1500.00" disabled />
              </div>
            </div>
            <div class="note">Activá E‑CHEQS cuando la <strong>moneda sea USD</strong> para calcular el monto en <strong>ARS</strong> de cada cheque con su fecha.</div>
          </div>

          <div style="margin-top:8px" class="group">
            <div class="segmented" role="tablist" aria-label="Modo de entrega">
              <button id="tabPct" class="active" type="button" aria-selected="true">Entrega %</button>
              <button id="tabMonto" type="button" aria-selected="false">Entrega $</button>
            </div>

            <div id="panelPct" style="margin-top:8px">
              <div class="inline" style="justify-content:space-between">
                <label for="entregaPct" style="margin:0">Porcentaje</label>
                <span id="entregaPctBadge" class="pct-badge">30%</span>
              </div>
              <div class="row" style="margin-top:6px">
                <input id="entregaPct" type="range" min="0" max="90" step="5" value="30" style="flex:1" />
              </div>
              <div class="row" id="chipsEntrega" style="margin-top:6px">
                <div class="chip" data-p="0">0%</div>
                <div class="chip" data-p="10">10%</div>
                <div class="chip" data-p="20">20%</div>
                <div class="chip active" data-p="30">30%</div>
                <div class="chip" data-p="40">40%</div>
                <div class="chip" data-p="50">50%</div>
              </div>
            </div>

            <div id="panelMonto" style="margin-top:8px; display:none">
              <label for="entregaMonto" style="margin-top:0">Monto de entrega (fijo)</label>
              <input id="entregaMonto" type="number" min="0" step="0.01" placeholder="Ej.: 45000" />
              <div class="muted" style="margin-top:6px">Si excede el total, se ajusta automáticamente.</div>
            </div>

            <div class="muted" style="margin-top:6px">La entrega se descuenta del total y el <strong>saldo</strong> se divide en n cuotas.</div>
          </div>

          <div class="switch">
            <input id="redondear" type="checkbox" />
            <label for="redondear" class="muted">Redondear cada cuota al entero más cercano</label>
          </div>

          <div class="btn bar" style="margin-top:10px">
            <button id="calcular" class="btn primary">Calcular</button>
            <button id="copiar" class="btn">Copiar</button>
            <button id="imprimir" class="btn">PNG</button>
            <button id="limpiar" class="btn">Limpiar</button>
          </div>
        </div>
      </section>

      <section class="card" id="exportArea">
        <div class="content">
          <div class="headerRow">
            <div class="brandTitle">FORMA DE PAGO</div>
            <span class="badge" id="badgeFecha"></span>
          </div>

          <div class="row" style="margin-top:6px">
            <div class="stat"><div class="k">Monto total</div><div id="statTotal" class="v">—</div></div>
            <div class="stat"><div class="k">Entrega</div><div id="statEntrega" class="v">—</div></div>
            <div class="stat"><div class="k">Saldo</div><div id="statSaldo" class="v">—</div></div>
          </div>

          <div class="row" style="margin-top:6px">
            <div class="stat"><div class="k">Cuotas</div><div id="statCuotas" class="v">—</div></div>
            <div class="stat"><div class="k">Valor por cuota</div><div id="statCuota" class="v">—</div></div>
          </div>

          <div id="tcInfo" class="note" style="display:none; margin-top:6px"></div>

          <div class="tableWrap" style="margin-top:8px">
            <table id="tabla">
              <thead>
                <tr id="theadRow">
                  <th>#</th>
                  <th>Fecha</th>
                  <th>Importe</th>
                </tr>
              </thead>
              <tbody></tbody>
              <tfoot>
                <tr id="tfootRow">
                  <td colspan="2">Total (Entrega + Cuotas)</td>
                  <td id="tfootTotal">—</td>
                </tr>
              </tfoot>
            </table>
          </div>

          <div class="footer">
            Sin interés. Fechas: cada 30 días desde la fecha de inicio, moviendo a lunes si cae fin de semana.
            <div class="disclaimer">⚠️ El tipo de cambio utilizado es referencial y puede variar sin previo aviso.</div>
          </div>
        </div>
      </section>
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
  <script>
    const $ = (q) => document.querySelector(q);
    const montoEl = $("#monto");
    const monedaEl = $("#moneda");
    const cuotasCustomEl = $("#cuotasCustom");
    const fechaInicioEl = $("#fechaInicio");

    // E‑CHEQS
    const echeqsToggle = $("#echeqsToggle");
    const tipoCambioEl = $("#tipoCambio");
    const tcInfo = $("#tcInfo");

    // entrega controls
    const tabPct = $("#tabPct");
    const tabMonto = $("#tabMonto");
    const panelPct = $("#panelPct");
    const panelMonto = $("#panelMonto");
    const chipsEl = $("#chipsEntrega");
    const entregaRangeEl = $("#entregaPct");
    const entregaBadgeEl = $("#entregaPctBadge");
    const entregaMontoEl = $("#entregaMonto");

    const redondearEl = $("#redondear");
    const calcularBtn = $("#calcular");
    const copiarBtn = $("#copiar");
    const imprimirBtn = $("#imprimir");
    const limpiarBtn = $("#limpiar");

    const statTotal = $("#statTotal");
    const statEntrega = $("#statEntrega");
    const statSaldo = $("#statSaldo");
    const statCuotas = $("#statCuotas");
    const statCuota = $("#statCuota");
    const tbody = document.querySelector("#tabla tbody");
    const tfootTotal = $("#tfootTotal");
    const exportArea = $("#exportArea");
    const badgeFecha = $("#badgeFecha");
    const theadRow = $("#theadRow");
    const tfootRow = $("#tfootRow");

    function fmt(n, moneda) {
      try { return new Intl.NumberFormat('es-AR', { style:'currency', currency: moneda }).format(n); }
      catch(e){ return n.toLocaleString('es-AR', { minimumFractionDigits:2, maximumFractionDigits:2 }); }
    }
    function fmtDate(d){
      try{ return new Intl.DateTimeFormat('es-AR', { day:'2-digit', month:'2-digit', year:'numeric' }).format(d); }
      catch(e){ const yyyy=d.getFullYear(), mm=String(d.getMonth()+1).padStart(2,'0'), dd=String(d.getDate()).padStart(2,'0'); return `${dd}/${mm}/${yyyy}`; }
    }
    function parseISODate(value){ const [y,m,d] = value.split("-").map(Number); return new Date(y, m-1, d); }
    function addDays(date, days){ const d=new Date(date.getTime()); d.setDate(d.getDate()+days); return d; }
    function moveToBusinessDay(date){ const dow=date.getDay(); if (dow===0) return addDays(date,1); if (dow===6) return addDays(date,2); return date; }

    function setEntregaPct(p){
      const chips=[...chipsEl.querySelectorAll(".chip")];
      chips.forEach(c => c.classList.toggle("active", c.dataset.p === String(p)));
      entregaRangeEl.value = p; entregaBadgeEl.textContent = `${p}%`;
    }
    function switchTab(mode){
      if(mode === 'pct'){
        tabPct.classList.add("active"); tabPct.setAttribute("aria-selected","true");
        tabMonto.classList.remove("active"); tabMonto.setAttribute("aria-selected","false");
        panelPct.style.display=""; panelMonto.style.display="none";
      } else {
        tabMonto.classList.add("active"); tabMonto.setAttribute("aria-selected","true");
        tabPct.classList.remove("active"); tabPct.setAttribute("aria-selected","false");
        panelMonto.style.display=""; panelPct.style.display="none";
      }
    }
    function updateEcheqsUI(){
      const isUSD = monedaEl.value === "USD";
      tipoCambioEl.disabled = !(isUSD && echeqsToggle.checked);
    }

    function calcular() {
      const moneda = monedaEl.value || "ARS";
      const total = parseFloat((montoEl.value || "").toString().replace(",", "."));
      const n = parseInt(cuotasCustomEl.value, 10);
      const mode = tabMonto.classList.contains("active") ? "monto" : "pct";
      const fechaInicioStr = fechaInicioEl.value;

      if (isNaN(total) || total <= 0) { alert("Ingresá un monto válido."); return; }
      if (isNaN(n) || n < 1) { alert("Ingresá la cantidad de cuotas (1 o más)."); return; }

      const hoy = new Date();
      const fechaInicio = fechaInicioStr ? parseISODate(fechaInicioStr) : hoy;
      badgeFecha.textContent = `Fecha de inicio: ${fmtDate(fechaInicio)}`;

      let entrega = 0, p = 0;
      if(mode === "pct"){
        p = parseInt(entregaRangeEl.value, 10) || 0;
        entrega = +(total * p / 100).toFixed(2);
      } else {
        const rawEntrega = parseFloat((entregaMontoEl.value || "0").toString().replace(",", ".")) || 0;
        entrega = Math.min(Math.max(rawEntrega, 0), total);
        p = total > 0 ? Math.round((entrega / total) * 100) : 0;
        entregaBadgeEl.textContent = `${p}%`;
      }

      let saldo = +(total - entrega).toFixed(2);
      if (saldo < 0) saldo = 0;

      const base = saldo / n;
      const valorCuota = redondearEl.checked ? Math.round(base) : parseFloat(base.toFixed(2));

      // E‑CHEQS
      const enableEcheqs = (moneda === "USD" && echeqsToggle.checked);
      let tc = parseFloat((tipoCambioEl.value || "").toString().replace(",", "."));
      if (enableEcheqs && (isNaN(tc) || tc <= 0)) { alert("Ingresá un tipo de cambio ARS/USD válido para E‑CHEQS."); return; }

      // Table headers (ARS column when E‑CHEQS)
      theadRow.innerHTML = enableEcheqs
        ? `<th>#</th><th>Fecha</th><th>Importe (USD)</th><th>Importe (ARS)</th>`
        : `<th>#</th><th>Fecha</th><th>Importe</th>`;
      tfootRow.innerHTML = enableEcheqs
        ? `<td colspan="3">Total (Entrega + Cuotas)</td><td id="tfootTotal">—</td>`
        : `<td colspan="2">Total (Entrega + Cuotas)</td><td id="tfootTotal">—</td>`;

      if (enableEcheqs) {
        tcInfo.style.display = "";
        tcInfo.textContent = `E‑CHEQS activo · Tipo de cambio: ${tc.toLocaleString('es-AR', {minimumFractionDigits:2, maximumFractionDigits:2})} ARS/USD`;
      } else {
        tcInfo.style.display = "none";
      }

      // Stats
      statTotal.textContent = fmt(total, moneda);
      statEntrega.textContent = `${fmt(entrega, moneda)} (${p}%)`;
      statSaldo.textContent = fmt(saldo, moneda);
      statCuotas.textContent = `${n}`;
      statCuota.textContent = fmt(valorCuota, moneda);

      // Build table
      tbody.innerHTML = "";
      let sumaBase = 0, sumaArs = 0;

      // Entrega
      if (entrega > 0){
        const tr0 = document.createElement("tr");
        tr0.innerHTML = `<td>Entrega</td><td>${fmtDate(moveToBusinessDay(fechaInicio))}</td><td>${fmt(entrega, moneda)}</td>`;
        if (enableEcheqs){ const entARS = +(entrega*tc).toFixed(2); tr0.innerHTML += `<td>${fmt(entARS,"ARS")}</td>`; sumaArs += entARS; }
        tbody.appendChild(tr0); sumaBase += entrega;
      }

      // Cuotas
      let acumuladoCuotas = 0;
      for (let i=1; i<=n; i++) {
        let fechaCuota = moveToBusinessDay(addDays(fechaInicio, 30*i));
        let cuota = valorCuota;
        if (i === n) {
          cuota = parseFloat((saldo - acumuladoCuotas).toFixed(2));
          if (redondearEl.checked) cuota = Math.round(saldo - acumuladoCuotas);
        }
        acumuladoCuotas += cuota; sumaBase += cuota;
        let row = `<td>Cuota ${i}</td><td>${fmtDate(fechaCuota)}</td><td>${fmt(cuota, moneda)}</td>`;
        if (enableEcheqs){ const cuARS = +(cuota*tc).toFixed(2); row += `<td>${fmt(cuARS,"ARS")}</td>`; sumaArs += cuARS; }
        const tr = document.createElement("tr"); tr.innerHTML = row; tbody.appendChild(tr);
      }

      // Totales
      tfootTotal.textContent = enableEcheqs ? fmt(sumaArs, "ARS") : fmt(sumaBase, moneda);
    }

    async function exportPNG(){
      try{
        if (document.querySelector("#statTotal").textContent === "—") calcular();
        const canvas = await html2canvas(exportArea, { backgroundColor: null, scale: 2, useCORS: true, windowWidth: document.documentElement.scrollWidth });
        const dataURL = canvas.toDataURL("image/png");
        const a = document.createElement("a");
        const now = new Date();
        const stamp = now.toISOString().replace(/[:.]/g,"-");
        a.href = dataURL; a.download = `forma_de_pago_${stamp}.png`; a.click();
      }catch(e){ alert("No se pudo generar el PNG. Probá nuevamente."); }
    }

    // Eventos
    [montoEl, monedaEl, cuotasCustomEl, entregaMontoEl, redondearEl, fechaInicioEl, tipoCambioEl].forEach(el => {
      if(!el) return;
      el.addEventListener("keyup", (ev)=>{ if (ev.key === "Enter") calcular(); });
    });
    $("#chipsEntrega").addEventListener("click", (e)=>{ const chip = e.target.closest(".chip"); if (!chip) return; setEntregaPct(chip.dataset.p); calcular(); });
    entregaRangeEl.addEventListener("input", (e)=>{ setEntregaPct(e.target.value); });
    tabPct.addEventListener("click", ()=>{ switchTab('pct'); calcular(); });
    tabMonto.addEventListener("click", ()=>{ switchTab('monto'); calcular(); });
    monedaEl.addEventListener("change", ()=>{ updateEcheqsUI(); });
    echeqsToggle.addEventListener("change", ()=>{ updateEcheqsUI(); });

    calcularBtn.addEventListener("click", calcular);
    copiarBtn.addEventListener("click", async ()=>{
      const moneda = monedaEl.value || "ARS";
      const enableEcheqs = (moneda === "USD" && echeqsToggle.checked);
      const tc = parseFloat((tipoCambioEl.value || "").toString().replace(",", "."));

      const total = document.querySelector("#statTotal").textContent;
      const entregaTxt = document.querySelector("#statEntrega").textContent;
      const saldoTxt = document.querySelector("#statSaldo").textContent;
      const cuotas = document.querySelector("#statCuotas").textContent;
      const vcuota = document.querySelector("#statCuota").textContent;
      if (!total || total === "—") { calcular(); }

      const headers = enableEcheqs ? ["#", "Fecha", "Importe (USD)", "Importe (ARS)"] : ["#", "Fecha", "Importe"];
      const lines = [headers];
      [...tbody.querySelectorAll("tr")].forEach(tr=>{
        const tds = tr.querySelectorAll("td");
        const row = [...tds].map(td=>td.textContent);
        lines.push(row);
      });
      const txtTabla = lines.map(r=>r.join("\t")).join("\n");
      const tcLine = enableEcheqs ? `Tipo de cambio: ${tc.toLocaleString('es-AR', {minimumFractionDigits:2, maximumFractionDigits:2})} ARS/USD\n` : "";
      const disclaimer = "⚠️ El tipo de cambio utilizado es referencial y puede variar sin previo aviso.\n";
      const resumen = `FORMA DE PAGO\n${tcLine}Fecha de inicio: ${badgeFecha.textContent.replace("Fecha de inicio: ","")}\nMoneda base: ${moneda}\nMonto total: ${total}\n${entregaTxt ? "Entrega: " + entregaTxt + "\n" : ""}Saldo: ${saldoTxt}\nCuotas: ${cuotas}\nValor por cuota: ${vcuota}\n\nDetalle:\n${txtTabla}\n\n${disclaimer}`;
      try {
        await navigator.clipboard.writeText(resumen);
        copiarBtn.textContent = "¡Copiado!"; setTimeout(()=>copiarBtn.textContent="Copiar", 1200);
      } catch(e) { alert("No se pudo copiar automáticamente. Copiá manualmente:\n\n" + resumen); }
    });
    document.querySelector("#imprimir").addEventListener("click", exportPNG);
    limpiarBtn.addEventListener("click", ()=>{
      montoEl.value = ""; cuotasCustomEl.value = 6; fechaInicioEl.valueAsDate = new Date();
      setEntregaPct(30); entregaMontoEl.value = ""; redondearEl.checked = false; switchTab('pct');
      echeqsToggle.checked = false; tipoCambioEl.value = ""; updateEcheqsUI();
      document.querySelector("#statTotal").textContent = "—";
      document.querySelector("#statEntrega").textContent = "—";
      document.querySelector("#statSaldo").textContent = "—";
      document.querySelector("#statCuotas").textContent = "—";
      document.querySelector("#statCuota").textContent = "—";
      tbody.innerHTML = ""; tfootTotal.textContent = "—";
      theadRow.innerHTML = `<th>#</th><th>Fecha</th><th>Importe</th>`;
      tfootRow.innerHTML = `<td colspan="2">Total (Entrega + Cuotas)</td><td id="tfootTotal">—</td>`;
      montoEl.focus();
    });

    // init
    setEntregaPct(30); switchTab('pct'); fechaInicioEl.valueAsDate = new Date(); updateEcheqsUI(); calcular();
  </script>
</body>
</html>

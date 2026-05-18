<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TyrePrint — Label System</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono:wght@300;400;500&family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap');

/* ── VARIABLES ── */
:root {
  --bg: #f0ede8;
  --surface: #faf8f5;
  --dark: #0f0e0c;
  --mid: #3a3830;
  --muted: #8a8580;
  --accent: #d4421a;
  --accent2: #f0a500;
  --border: #d8d4ce;
  --shadow: rgba(15,14,12,0.08);
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--dark);
  min-height: 100vh;
}

/* ── LAYOUT ── */
.app { display: grid; grid-template-columns: 420px 1fr; min-height: 100vh; }

/* ── LEFT PANEL ── */
.panel {
  background: var(--surface);
  border-right: 1px solid var(--border);
  display: flex;
  flex-direction: column;
  overflow-y: auto;
}

.panel-header {
  padding: 28px 28px 20px;
  border-bottom: 1px solid var(--border);
  position: sticky; top: 0;
  background: var(--surface);
  z-index: 10;
}
.panel-header h1 {
  font-family: 'Syne', sans-serif;
  font-size: 22px; font-weight: 800;
  letter-spacing: -0.5px;
  color: var(--dark);
}
.panel-header h1 span { color: var(--accent); }
.panel-header p {
  font-size: 12px; color: var(--muted);
  margin-top: 4px; letter-spacing: 0.3px;
}

.panel-body { padding: 24px 28px; flex: 1; display: flex; flex-direction: column; gap: 24px; }

/* SECTION */
.form-section { display: flex; flex-direction: column; gap: 10px; }
.section-title {
  font-family: 'DM Mono', monospace;
  font-size: 10px; font-weight: 500;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--muted);
  display: flex; align-items: center; gap: 8px;
}
.section-title::after {
  content: ''; flex: 1; height: 1px; background: var(--border);
}

/* INPUTS */
.field { display: flex; flex-direction: column; gap: 5px; }
.field label {
  font-size: 11px; font-weight: 500;
  color: var(--mid); letter-spacing: 0.3px;
}
.field input, .field textarea, .field select {
  font-family: 'DM Sans', sans-serif;
  font-size: 14px;
  background: var(--bg);
  border: 1.5px solid var(--border);
  color: var(--dark);
  padding: 10px 13px;
  border-radius: 6px;
  outline: none;
  transition: border-color 0.15s, box-shadow 0.15s;
  width: 100%;
}
.field input:focus, .field textarea:focus, .field select:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(212,66,26,0.08);
}
.field textarea { resize: vertical; min-height: 60px; font-size: 13px; line-height: 1.5; }
.field-row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }

/* TYRE ROWS */
.tyre-input-row {
  display: grid; grid-template-columns: 1fr 80px 36px;
  gap: 8px; align-items: flex-end;
}
.tyre-input-row input { font-family: 'DM Mono', monospace; }
.btn-icon {
  width: 36px; height: 38px;
  background: transparent;
  border: 1.5px solid var(--border);
  border-radius: 6px;
  cursor: pointer;
  display: flex; align-items: center; justify-content: center;
  font-size: 16px;
  color: var(--muted);
  transition: all 0.15s;
}
.btn-icon:hover { background: #fde8e3; border-color: var(--accent); color: var(--accent); }

.tyre-list { display: flex; flex-direction: column; gap: 6px; }
.tyre-tag {
  display: flex; align-items: center; justify-content: space-between;
  background: var(--bg);
  border: 1.5px solid var(--border);
  border-radius: 6px;
  padding: 8px 12px;
  animation: slideIn 0.2s ease;
}
@keyframes slideIn { from { opacity:0; transform: translateY(-6px); } to { opacity:1; transform: translateY(0); } }
.tyre-tag-info {
  display: flex; align-items: center; gap: 10px;
}
.tyre-tag-size {
  font-family: 'DM Mono', monospace;
  font-size: 13px; font-weight: 500;
  color: var(--dark);
}
.tyre-tag-qty {
  background: var(--accent);
  color: white;
  font-family: 'DM Mono', monospace;
  font-size: 11px; font-weight: 500;
  padding: 2px 8px;
  border-radius: 20px;
}
.tyre-remove {
  background: none; border: none; cursor: pointer;
  color: var(--muted); font-size: 14px;
  transition: color 0.15s;
}
.tyre-remove:hover { color: var(--accent); }

/* GENERATE BTN */
.btn-generate {
  width: 100%;
  background: var(--accent);
  color: white;
  border: none;
  font-family: 'Syne', sans-serif;
  font-size: 15px; font-weight: 700;
  letter-spacing: 0.5px;
  padding: 14px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s;
  display: flex; align-items: center; justify-content: center; gap: 8px;
}
.btn-generate:hover { background: #b83615; transform: translateY(-1px); box-shadow: 0 4px 16px rgba(212,66,26,0.3); }
.btn-generate:active { transform: translateY(0); }

/* ── RIGHT PANEL (PREVIEW) ── */
.preview-area {
  display: flex;
  flex-direction: column;
  background: #e5e2dd;
  overflow-y: auto;
}

.preview-toolbar {
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  padding: 14px 24px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  position: sticky; top: 0; z-index: 10;
}
.preview-toolbar-left {
  display: flex; align-items: center; gap: 12px;
}
.preview-toolbar h2 {
  font-family: 'Syne', sans-serif;
  font-size: 14px; font-weight: 700;
  color: var(--dark);
}
.label-count {
  font-family: 'DM Mono', monospace;
  font-size: 11px;
  background: var(--bg);
  border: 1px solid var(--border);
  padding: 3px 10px;
  border-radius: 20px;
  color: var(--muted);
}
.btn-print {
  background: var(--dark);
  color: white;
  border: none;
  font-family: 'Syne', sans-serif;
  font-size: 13px; font-weight: 700;
  padding: 9px 20px;
  border-radius: 6px;
  cursor: pointer;
  display: flex; align-items: center; gap: 6px;
  transition: all 0.15s;
}
.btn-print:hover { background: var(--mid); }

.preview-canvas {
  flex: 1;
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
  padding: 32px;
  align-items: flex-start;
  align-content: flex-start;
}

.empty-state {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 12px;
  padding: 80px 40px;
  color: var(--muted);
  text-align: center;
}
.empty-icon {
  font-size: 48px; opacity: 0.3;
}
.empty-state h3 {
  font-family: 'Syne', sans-serif;
  font-size: 18px; font-weight: 700;
  color: var(--mid); opacity: 0.5;
}
.empty-state p {
  font-size: 13px; max-width: 240px; line-height: 1.6;
}

/* ── A6 LABEL ── */
/* A6 = 105mm × 148mm. At 96dpi screen: 1mm ≈ 3.78px → 397px × 559px */
.a6-label {
  width: 397px;
  min-height: 559px;
  background: white;
  box-shadow: 0 8px 32px rgba(15,14,12,0.15), 0 2px 8px rgba(15,14,12,0.08);
  border-radius: 4px;
  overflow: hidden;
  position: relative;
  display: flex;
  flex-direction: column;
  flex-shrink: 0;
}

/* Label Top Bar */
.lbl-topbar {
  background: var(--accent);
  height: 8px;
}

/* Label Header */
.lbl-header {
  padding: 14px 16px 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1.5px solid #e8e4df;
}
.lbl-logo-area {
  display: flex; align-items: center; gap: 10px;
}
.lbl-logo {
  width: 40px; height: 40px;
  border: 2px solid var(--accent2);
  display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif;
  font-size: 8px; font-weight: 800;
  color: var(--accent2);
  letter-spacing: 0.5px;
  text-transform: uppercase;
  line-height: 1.1;
  text-align: center;
  padding: 2px;
  flex-shrink: 0;
}
.lbl-our-name {
  font-family: 'Syne', sans-serif;
  font-size: 13px; font-weight: 800;
  color: var(--dark);
  letter-spacing: 0.5px;
  text-transform: uppercase;
  max-width: 100px;
  line-height: 1.2;
}
.lbl-form-title {
  text-align: right;
}
.lbl-form-title .big {
  font-family: 'Syne', sans-serif;
  font-size: 18px; font-weight: 800;
  color: var(--accent);
  letter-spacing: 1px;
  text-transform: uppercase;
  line-height: 1;
}
.lbl-form-title .small {
  font-size: 8px; color: var(--muted);
  letter-spacing: 1.5px; text-transform: uppercase;
}

/* Dealer Section */
.lbl-dealer {
  padding: 10px 16px;
  border-bottom: 1px solid #f0ede8;
  background: #faf8f5;
}
.lbl-sec-label {
  font-family: 'DM Mono', monospace;
  font-size: 7.5px; font-weight: 500;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 6px;
}
.lbl-dealer-name {
  font-family: 'Syne', sans-serif;
  font-size: 14px; font-weight: 700;
  color: var(--dark);
  margin-bottom: 3px;
  line-height: 1.2;
}
.lbl-dealer-addr {
  font-size: 10px; color: var(--mid);
  line-height: 1.5; margin-bottom: 2px;
  white-space: pre-line;
}
.lbl-dealer-tel {
  font-family: 'DM Mono', monospace;
  font-size: 10px; color: var(--mid);
  display: flex; align-items: center; gap: 5px;
}

/* Tyre Table */
.lbl-tyre-wrap {
  padding: 10px 16px;
  flex: 1;
}
.lbl-table {
  width: 100%;
  border-collapse: collapse;
}
.lbl-table thead tr {
  background: var(--dark);
}
.lbl-table thead th {
  font-family: 'DM Mono', monospace;
  font-size: 8px; font-weight: 500;
  letter-spacing: 1.5px; text-transform: uppercase;
  color: rgba(255,255,255,0.7);
  padding: 6px 8px;
  text-align: left;
}
.lbl-table thead th:last-child { text-align: center; }
.lbl-table tbody tr {
  border-bottom: 1px solid #f0ede8;
}
.lbl-table tbody tr:last-child { border-bottom: none; }
.lbl-table td {
  padding: 7px 8px;
  vertical-align: middle;
}
.lbl-size {
  font-family: 'DM Mono', monospace;
  font-size: 13px; font-weight: 500;
  color: var(--dark);
  letter-spacing: 0.5px;
}
/* TICK BOXES */
.lbl-ticks {
  display: flex; flex-wrap: wrap; gap: 3px;
}
.lbl-tick {
  width: 14px; height: 14px;
  border: 1px solid #ccc;
  border-radius: 2px;
  display: inline-flex;
  align-items: center; justify-content: center;
  font-size: 9px;
  color: transparent;
  background: white;
  flex-shrink: 0;
}
.lbl-tick.on {
  background: var(--accent2);
  border-color: var(--accent2);
  color: white;
  font-weight: 700;
}
.lbl-qty-badge {
  display: flex; align-items: center; justify-content: center;
}
.lbl-qty-pill {
  background: var(--accent);
  color: white;
  font-family: 'DM Mono', monospace;
  font-size: 12px; font-weight: 500;
  padding: 2px 8px;
  border-radius: 4px;
  min-width: 28px;
  text-align: center;
}

/* Total Row */
.lbl-total-row td {
  padding: 8px 8px 4px;
  border-top: 2px solid var(--accent);
}
.lbl-total-label {
  font-family: 'DM Mono', monospace;
  font-size: 9px; font-weight: 500;
  letter-spacing: 2px; text-transform: uppercase;
  color: var(--accent);
}
.lbl-total-val {
  font-family: 'Syne', sans-serif;
  font-size: 20px; font-weight: 800;
  color: var(--accent);
  text-align: right;
}

/* Footer */
.lbl-footer {
  padding: 8px 16px 12px;
  display: flex;
  justify-content: space-between;
  border-top: 1px solid #f0ede8;
  margin-top: auto;
}
.lbl-footer-field {
  display: flex; flex-direction: column; gap: 3px;
}
.lbl-footer-line {
  width: 80px; height: 1px;
  background: #ccc;
  margin-bottom: 2px;
}
.lbl-footer-label {
  font-family: 'DM Mono', monospace;
  font-size: 7px; font-weight: 500;
  letter-spacing: 1.5px; text-transform: uppercase;
  color: var(--muted);
}

/* Bottom stripe */
.lbl-bottombar {
  height: 5px;
  background: linear-gradient(90deg, var(--accent) 0%, var(--accent2) 100%);
}

/* ── PRINT STYLES ── */
@media print {
  @page { size: A6 portrait; margin: 0; }
  body { background: white !important; }
  .panel, .preview-toolbar { display: none !important; }
  .preview-area {
    display: block !important;
    background: white !important;
    overflow: visible !important;
  }
  .preview-canvas {
    padding: 0 !important;
    gap: 0 !important;
    display: block !important;
  }
  .empty-state { display: none !important; }
  .a6-label {
    width: 105mm !important;
    min-height: 148mm !important;
    box-shadow: none !important;
    border-radius: 0 !important;
    page-break-after: always !important;
    break-after: page !important;
  }
  .lbl-tick { -webkit-print-color-adjust: exact !important; print-color-adjust: exact !important; }
  .lbl-tick.on { background: #f0a500 !important; border-color: #f0a500 !important; color: white !important; }
  .lbl-table thead tr { -webkit-print-color-adjust: exact !important; print-color-adjust: exact !important; }
  .lbl-topbar, .lbl-bottombar { -webkit-print-color-adjust: exact !important; print-color-adjust: exact !important; }
}
</style>
</head>
<body>
<div class="app">

  <!-- ── LEFT: FORM PANEL ── -->
  <div class="panel">
    <div class="panel-header">
      <h1>Tyre<span>Print</span></h1>
      <p>Label Generator System — A6 Format</p>
    </div>

    <div class="panel-body">

      <!-- OUR COMPANY -->
      <div class="form-section">
        <div class="section-title">Our Company</div>
        <div class="field">
          <label>Company Name</label>
          <input type="text" id="ourName" placeholder="e.g. ABC Tyres Sdn Bhd" oninput="liveUpdate()">
        </div>
        <div class="field">
          <label>Logo Text (short)</label>
          <input type="text" id="ourLogo" placeholder="e.g. ABC" maxlength="8" oninput="liveUpdate()">
        </div>
      </div>

      <!-- DEALER DETAILS -->
      <div class="form-section">
        <div class="section-title">Dealer Detail</div>
        <div class="field">
          <label>Dealer Company Name</label>
          <input type="text" id="dealerName" placeholder="Dealer Sdn Bhd" oninput="liveUpdate()">
        </div>
        <div class="field">
          <label>Address</label>
          <textarea id="dealerAddr" placeholder="No. 12, Jalan Maju,&#10;Taman Industri, 47500 Subang" oninput="liveUpdate()"></textarea>
        </div>
        <div class="field">
          <label>Tel Number</label>
          <input type="tel" id="dealerTel" placeholder="+60 12-345 6789" oninput="liveUpdate()">
        </div>
      </div>

      <!-- TYRE LIST -->
      <div class="form-section">
        <div class="section-title">Tyre Sizes</div>
        <div class="tyre-input-row">
          <div class="field" style="margin:0">
            <label>Tyre Size</label>
            <input type="text" id="newSize" placeholder="205/55R16" style="font-family:'DM Mono',monospace">
          </div>
          <div class="field" style="margin:0">
            <label>Qty (pcs)</label>
            <input type="number" id="newQty" placeholder="10" min="1" max="99" style="font-family:'DM Mono',monospace">
          </div>
          <button class="btn-icon" onclick="addTyre()" title="Add tyre">＋</button>
        </div>
        <div class="tyre-list" id="tyreList"></div>
      </div>

      <!-- GENERATE -->
      <button class="btn-generate" onclick="generateLabel()">
        <span>⚡</span> Generate Label
      </button>

    </div>
  </div>

  <!-- ── RIGHT: PREVIEW ── -->
  <div class="preview-area">
    <div class="preview-toolbar">
      <div class="preview-toolbar-left">
        <h2>Label Preview</h2>
        <div class="label-count" id="labelCount">0 labels</div>
      </div>
      <button class="btn-print" onclick="window.print()">
        🖨 Print A6
      </button>
    </div>

    <div class="preview-canvas" id="previewCanvas">
      <div class="empty-state">
        <div class="empty-icon">🏷️</div>
        <h3>No Labels Yet</h3>
        <p>Fill in the dealer details and tyre sizes, then click Generate Label.</p>
      </div>
    </div>
  </div>

</div>

<script>
  let tyres = [];

  // ── TYRE MANAGEMENT ──
  function addTyre() {
    const size = document.getElementById('newSize').value.trim().toUpperCase();
    const qty  = parseInt(document.getElementById('newQty').value) || 0;
    if (!size || qty < 1) {
      document.getElementById(size ? 'newQty' : 'newSize').focus();
      return;
    }
    tyres.push({ size, qty });
    document.getElementById('newSize').value = '';
    document.getElementById('newQty').value = '';
    document.getElementById('newSize').focus();
    renderTyreList();
    liveUpdate();
  }

  document.addEventListener('DOMContentLoaded', () => {
    document.getElementById('newSize').addEventListener('keydown', e => {
      if (e.key === 'Enter') document.getElementById('newQty').focus();
    });
    document.getElementById('newQty').addEventListener('keydown', e => {
      if (e.key === 'Enter') addTyre();
    });
  });

  function removeTyre(i) {
    tyres.splice(i, 1);
    renderTyreList();
    liveUpdate();
  }

  function renderTyreList() {
    const list = document.getElementById('tyreList');
    if (tyres.length === 0) { list.innerHTML = ''; return; }
    list.innerHTML = tyres.map((t, i) => `
      <div class="tyre-tag">
        <div class="tyre-tag-info">
          <span class="tyre-tag-size">${t.size}</span>
          <span class="tyre-tag-qty">${t.qty} pcs</span>
        </div>
        <button class="tyre-remove" onclick="removeTyre(${i})">✕</button>
      </div>
    `).join('');
  }

  // ── BUILD LABEL HTML ──
  function buildLabel(data) {
    const { ourName, ourLogo, dealerName, dealerAddr, dealerTel, tyres } = data;
    const total = tyres.reduce((s, t) => s + t.qty, 0);

    // Build tyre rows
    const MAX_TICKS = 20;
    const tyreRows = tyres.map(t => {
      const ticks = Array.from({ length: Math.min(t.qty, MAX_TICKS) }, (_, i) =>
        `<div class="lbl-tick on">✓</div>`
      ).join('');
      // Add empty ticks if qty < 10 to show structure
      const empties = t.qty < 10 ? Array.from({ length: 10 - t.qty }, () =>
        `<div class="lbl-tick"></div>`
      ).join('') : '';

      return `
        <tr>
          <td class="lbl-size">${t.size}</td>
          <td><div class="lbl-ticks">${ticks}${empties}</div></td>
          <td class="lbl-qty-badge"><div class="lbl-qty-pill">${t.qty}</div></td>
        </tr>
      `;
    }).join('');

    return `
      <div class="a6-label">
        <div class="lbl-topbar"></div>

        <div class="lbl-header">
          <div class="lbl-logo-area">
            <div class="lbl-logo">${ourLogo || 'LOGO'}</div>
            <div class="lbl-our-name">${ourName || 'YOUR COMPANY'}</div>
          </div>
          <div class="lbl-form-title">
            <div class="big">TYRE ORDER</div>
            <div class="small">Dealer Order Form</div>
          </div>
        </div>

        <div class="lbl-dealer">
          <div class="lbl-sec-label">Dealer Detail</div>
          <div class="lbl-dealer-name">${dealerName || '—'}</div>
          ${dealerAddr ? `<div class="lbl-dealer-addr">${dealerAddr.replace(/\n/g,'<br>')}</div>` : ''}
          ${dealerTel ? `<div class="lbl-dealer-tel">📞 ${dealerTel}</div>` : ''}
        </div>

        <div class="lbl-tyre-wrap">
          <div class="lbl-sec-label">Tyre Sizes &amp; Quantity</div>
          <table class="lbl-table">
            <thead>
              <tr>
                <th style="width:36%">Tyre Size</th>
                <th>Qty (Tick)</th>
                <th style="width:15%; text-align:center">Pcs</th>
              </tr>
            </thead>
            <tbody>${tyreRows}</tbody>
            <tfoot>
              <tr class="lbl-total-row">
                <td class="lbl-total-label">Total Pcs</td>
                <td></td>
                <td class="lbl-total-val">${total}</td>
              </tr>
            </tfoot>
          </table>
        </div>

        <div class="lbl-footer">
          <div class="lbl-footer-field">
            <div class="lbl-footer-line"></div>
            <div class="lbl-footer-label">Date</div>
          </div>
          <div class="lbl-footer-field">
            <div class="lbl-footer-line"></div>
            <div class="lbl-footer-label">Received By</div>
          </div>
          <div class="lbl-footer-field">
            <div class="lbl-footer-line"></div>
            <div class="lbl-footer-label">Signature</div>
          </div>
        </div>

        <div class="lbl-bottombar"></div>
      </div>
    `;
  }

  function getData() {
    return {
      ourName: document.getElementById('ourName').value.trim(),
      ourLogo: document.getElementById('ourLogo').value.trim().toUpperCase(),
      dealerName: document.getElementById('dealerName').value.trim(),
      dealerAddr: document.getElementById('dealerAddr').value.trim(),
      dealerTel: document.getElementById('dealerTel').value.trim(),
      tyres: [...tyres],
    };
  }

  // ── LIVE UPDATE (header only, no full render) ──
  function liveUpdate() {
    // If there's already a label, regenerate
    const canvas = document.getElementById('previewCanvas');
    if (canvas.querySelector('.a6-label')) generateLabel();
  }

  // ── GENERATE ──
  function generateLabel() {
    const data = getData();
    const canvas = document.getElementById('previewCanvas');

    if (!data.dealerName && !data.tyres.length) {
      canvas.innerHTML = `
        <div class="empty-state">
          <div class="empty-icon">⚠️</div>
          <h3>Fill in details first</h3>
          <p>Add dealer info and at least one tyre size to generate a label.</p>
        </div>
      `;
      document.getElementById('labelCount').textContent = '0 labels';
      return;
    }

    canvas.innerHTML = buildLabel(data);
    document.getElementById('labelCount').textContent = '1 label ready';
  }
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pay via UPI — Chaturang Pratishthan</title>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@300;400;600;700&family=Noto+Sans+Devanagari:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --saffron: #FF6B00;
    --deep-saffron: #E85D00;
    --gold: #F5A623;
    --cream: #FFF8F0;
    --dark: #1A0E00;
    --mid: #3D2200;
    --text-soft: #7A5C3A;
    --border: rgba(255,107,0,0.18);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Sora', sans-serif;
    background: var(--cream);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow-x: hidden;
    position: relative;
  }

  /* Decorative background */
  body::before {
    content: '';
    position: fixed;
    top: -200px; right: -200px;
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(255,107,0,0.12) 0%, transparent 70%);
    pointer-events: none;
  }
  body::after {
    content: '';
    position: fixed;
    bottom: -150px; left: -150px;
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(245,166,35,0.10) 0%, transparent 70%);
    pointer-events: none;
  }

  /* Rangoli geometric top pattern */
  .top-pattern {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 4px;
    background: linear-gradient(90deg, var(--saffron), var(--gold), var(--saffron), var(--gold), var(--saffron));
  }

  .wrapper {
    width: 100%;
    max-width: 460px;
    padding: 20px;
    animation: fadeUp 0.6s ease both;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .card {
    background: white;
    border-radius: 24px;
    overflow: hidden;
    box-shadow: 0 4px 40px rgba(255,107,0,0.12), 0 1px 4px rgba(0,0,0,0.06);
    border: 1px solid var(--border);
  }

  /* Header */
  .card-header {
    background: linear-gradient(135deg, var(--dark) 0%, var(--mid) 100%);
    padding: 28px 28px 22px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .card-header::before {
    content: '॥';
    position: absolute;
    font-size: 160px;
    color: rgba(255,107,0,0.06);
    top: -30px; right: -20px;
    font-family: 'Noto Sans Devanagari', serif;
    line-height: 1;
    pointer-events: none;
  }
  .org-icon {
    width: 60px; height: 60px;
    background: linear-gradient(135deg, var(--saffron), var(--gold));
    border-radius: 16px;
    margin: 0 auto 14px;
    display: flex; align-items: center; justify-content: center;
    font-size: 26px;
    box-shadow: 0 4px 16px rgba(255,107,0,0.4);
  }
  .org-name {
    font-family: 'Noto Sans Devanagari', sans-serif;
    color: white;
    font-size: 18px;
    font-weight: 700;
    letter-spacing: 0.3px;
    line-height: 1.3;
    margin-bottom: 4px;
  }
  .org-sub {
    color: rgba(255,255,255,0.5);
    font-size: 12px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    font-weight: 300;
  }

  /* Body */
  .card-body {
    padding: 26px 28px;
  }

  /* Amount input */
  .amount-block {
    margin-bottom: 22px;
  }
  .field-label {
    font-size: 11px;
    font-weight: 600;
    color: var(--text-soft);
    text-transform: uppercase;
    letter-spacing: 1.2px;
    margin-bottom: 8px;
  }
  .amount-input-wrap {
    display: flex;
    align-items: center;
    border: 1.5px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    transition: border-color 0.2s;
    background: var(--cream);
  }
  .amount-input-wrap:focus-within {
    border-color: var(--saffron);
    box-shadow: 0 0 0 3px rgba(255,107,0,0.08);
  }
  .currency-badge {
    padding: 14px 14px 14px 16px;
    font-size: 18px;
    font-weight: 700;
    color: var(--saffron);
    border-right: 1.5px solid var(--border);
    background: white;
    user-select: none;
  }
  #amount-input {
    flex: 1;
    border: none;
    outline: none;
    background: transparent;
    padding: 14px 16px;
    font-size: 22px;
    font-weight: 700;
    color: var(--dark);
    font-family: 'Sora', sans-serif;
    width: 100%;
  }
  #amount-input::placeholder { color: #CCC; font-weight: 300; font-size: 18px; }

  /* Quick amount chips */
  .quick-amounts {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-top: 10px;
  }
  .chip {
    padding: 5px 14px;
    border-radius: 20px;
    border: 1.5px solid var(--border);
    font-size: 12px;
    font-weight: 600;
    color: var(--saffron);
    cursor: pointer;
    transition: all 0.15s;
    background: white;
  }
  .chip:hover, .chip.active {
    background: var(--saffron);
    color: white;
    border-color: var(--saffron);
  }

  /* Note input */
  .note-block { margin-bottom: 24px; }
  #note-input {
    width: 100%;
    border: 1.5px solid var(--border);
    border-radius: 12px;
    padding: 12px 16px;
    font-size: 14px;
    font-family: 'Sora', sans-serif;
    color: var(--dark);
    background: var(--cream);
    outline: none;
    transition: border-color 0.2s;
  }
  #note-input:focus {
    border-color: var(--saffron);
    box-shadow: 0 0 0 3px rgba(255,107,0,0.08);
  }
  #note-input::placeholder { color: #BBA; }

  /* UPI ID display */
  .upi-info {
    display: flex;
    align-items: center;
    gap: 12px;
    background: linear-gradient(135deg, rgba(255,107,0,0.06), rgba(245,166,35,0.06));
    border: 1px solid rgba(255,107,0,0.15);
    border-radius: 12px;
    padding: 12px 16px;
    margin-bottom: 22px;
  }
  .upi-logo {
    width: 36px; height: 36px;
    background: linear-gradient(135deg, #097939, #00A550);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 10px;
    font-weight: 800;
    color: white;
    letter-spacing: -0.5px;
    flex-shrink: 0;
  }
  .upi-details { flex: 1; }
  .upi-id-text {
    font-size: 13px;
    font-weight: 600;
    color: var(--dark);
    letter-spacing: 0.3px;
  }
  .upi-verified {
    font-size: 11px;
    color: #00A550;
    font-weight: 500;
    margin-top: 1px;
  }
  .copy-btn {
    background: none;
    border: 1.5px solid var(--border);
    border-radius: 8px;
    padding: 6px 10px;
    font-size: 11px;
    font-weight: 600;
    color: var(--saffron);
    cursor: pointer;
    transition: all 0.15s;
    white-space: nowrap;
    font-family: 'Sora', sans-serif;
  }
  .copy-btn:hover { background: var(--saffron); color: white; border-color: var(--saffron); }

  /* Pay buttons */
  .pay-section { display: flex; flex-direction: column; gap: 10px; }

  .pay-btn-primary {
    width: 100%;
    padding: 16px;
    border-radius: 14px;
    border: none;
    font-family: 'Sora', sans-serif;
    font-size: 15px;
    font-weight: 700;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    transition: all 0.2s;
    text-decoration: none;
  }

  .btn-upi-intent {
    background: linear-gradient(135deg, var(--saffron), var(--deep-saffron));
    color: white;
    box-shadow: 0 4px 20px rgba(255,107,0,0.35);
  }
  .btn-upi-intent:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 28px rgba(255,107,0,0.45);
  }
  .btn-upi-intent:active { transform: translateY(0); }

  .apps-row {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
  }

  .app-btn {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5px;
    padding: 10px 6px;
    border-radius: 12px;
    border: 1.5px solid var(--border);
    cursor: pointer;
    transition: all 0.15s;
    background: white;
    text-decoration: none;
  }
  .app-btn:hover {
    border-color: var(--saffron);
    background: rgba(255,107,0,0.04);
    transform: translateY(-1px);
  }
  .app-icon {
    width: 36px; height: 36px;
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px;
  }
  .app-name {
    font-size: 10px;
    font-weight: 600;
    color: var(--text-soft);
    text-align: center;
    line-height: 1.2;
  }

  /* QR Section */
  .qr-section {
    margin-top: 10px;
    border: 1.5px dashed var(--border);
    border-radius: 14px;
    padding: 16px;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s;
  }
  .qr-section:hover { border-color: var(--saffron); background: rgba(255,107,0,0.02); }
  .qr-toggle-text {
    font-size: 13px;
    color: var(--saffron);
    font-weight: 600;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
  }
  #qr-container {
    display: none;
    margin-top: 14px;
  }
  #qr-container.open { display: block; }
  #qr-canvas {
    border-radius: 12px;
    border: 3px solid white;
    box-shadow: 0 2px 16px rgba(0,0,0,0.1);
    max-width: 180px;
  }
  .qr-scan-hint {
    font-size: 11px;
    color: var(--text-soft);
    margin-top: 8px;
  }

  /* Divider */
  .divider {
    display: flex;
    align-items: center;
    gap: 10px;
    margin: 6px 0;
  }
  .divider-line { flex: 1; height: 1px; background: var(--border); }
  .divider-text { font-size: 11px; color: var(--text-soft); font-weight: 500; white-space: nowrap; }

  /* Footer */
  .card-footer {
    padding: 14px 28px;
    border-top: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
  }
  .footer-text { font-size: 11px; color: var(--text-soft); }
  .upi-badge {
    background: linear-gradient(135deg, #097939, #00A550);
    color: white;
    font-size: 9px;
    font-weight: 800;
    padding: 2px 7px;
    border-radius: 4px;
    letter-spacing: 0.5px;
  }

  /* Toast */
  .toast {
    position: fixed;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%) translateY(80px);
    background: var(--dark);
    color: white;
    padding: 10px 20px;
    border-radius: 30px;
    font-size: 13px;
    font-weight: 500;
    transition: transform 0.3s ease;
    z-index: 100;
    pointer-events: none;
  }
  .toast.show { transform: translateX(-50%) translateY(0); }

  @media (max-width: 380px) {
    .card-body { padding: 20px; }
    .card-header { padding: 22px 20px 18px; }
  }
</style>
</head>
<body>
<div class="top-pattern"></div>

<div class="wrapper">
  <div class="card">
    <!-- Header -->
    <div class="card-header">
      <div class="org-icon">🏛️</div>
      <div class="org-name">चतुरंग प्रतिष्ठान</div>
      <div class="org-sub">Chaturang Pratishthan</div>
    </div>

    <!-- Body -->
    <div class="card-body">

      <!-- UPI ID -->
      <div class="upi-info">
        <div class="upi-logo">UPI</div>
        <div class="upi-details">
          <div class="upi-id-text">chaturangpratishthan@srcb</div>
          <div class="upi-verified">✓ Verified UPI ID</div>
        </div>
        <button class="copy-btn" onclick="copyUPI()">Copy</button>
      </div>

      <!-- Amount -->
      <div class="amount-block">
        <div class="field-label">Enter Amount</div>
        <div class="amount-input-wrap">
          <div class="currency-badge">₹</div>
          <input type="number" id="amount-input" placeholder="0.00" min="1" oninput="updateLinks()" />
        </div>
        <div class="quick-amounts">
          <div class="chip" onclick="setAmount(100)">₹100</div>
          <div class="chip" onclick="setAmount(251)">₹251</div>
          <div class="chip" onclick="setAmount(500)">₹500</div>
          <div class="chip" onclick="setAmount(1001)">₹1001</div>
          <div class="chip" onclick="setAmount(2100)">₹2100</div>
        </div>
      </div>

      <!-- Note -->
      <div class="note-block">
        <div class="field-label">Add a Note (Optional)</div>
        <input type="text" id="note-input" placeholder="e.g. Donation, Event fee..." oninput="updateLinks()" />
      </div>

      <!-- Pay Buttons -->
      <div class="pay-section">

        <!-- Primary UPI Intent (opens app chooser on mobile) -->
        <a id="main-pay-btn" href="#" class="pay-btn-primary btn-upi-intent" onclick="handleMainPay(event)">
          <span style="font-size:20px;">⚡</span>
          Pay via Any UPI App
        </a>

        <div class="divider">
          <div class="divider-line"></div>
          <div class="divider-text">or open specific app</div>
          <div class="divider-line"></div>
        </div>

        <!-- App-specific buttons -->
        <div class="apps-row">
          <a id="phonepe-btn" href="#" class="app-btn" onclick="openApp('phonepe', event)">
            <div class="app-icon" style="background: #5F259F;">
              <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/71/PhonePe_Logo.png/200px-PhonePe_Logo.png" width="26" onerror="this.style.display='none';this.parentNode.innerHTML='📱'" />
            </div>
            <div class="app-name">PhonePe</div>
          </a>
          <a id="gpay-btn" href="#" class="app-btn" onclick="openApp('gpay', event)">
            <div class="app-icon" style="background: white; border: 1px solid #eee;">
              <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f2/Google_Pay_Logo.svg/200px-Google_Pay_Logo.svg.png" width="26" onerror="this.style.display='none';this.parentNode.innerHTML='💳'" />
            </div>
            <div class="app-name">Google Pay</div>
          </a>
          <a id="paytm-btn" href="#" class="app-btn" onclick="openApp('paytm', event)">
            <div class="app-icon" style="background: #00BAF2;">
              <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/24/Paytm_Logo_%28standalone%29.svg/200px-Paytm_Logo_%28standalone%29.svg.png" width="26" onerror="this.style.display='none';this.parentNode.innerHTML='💰'" />
            </div>
            <div class="app-name">Paytm</div>
          </a>
          <a id="bhim-btn" href="#" class="app-btn" onclick="openApp('bhim', event)">
            <div class="app-icon" style="background: #00529B;">
              <img src="https://upload.wikimedia.org/wikipedia/en/thumb/a/a5/BHIM_logo.png/200px-BHIM_logo.png" width="26" onerror="this.style.display='none';this.parentNode.innerHTML='🏦'"/>
            </div>
            <div class="app-name">BHIM</div>
          </a>
        </div>

        <div class="divider">
          <div class="divider-line"></div>
          <div class="divider-text">or scan QR code</div>
          <div class="divider-line"></div>
        </div>

        <!-- QR Toggle -->
        <div class="qr-section" onclick="toggleQR()">
          <div class="qr-toggle-text">
            <span>⬛</span> <span id="qr-toggle-label">Show QR Code</span>
          </div>
          <div id="qr-container">
            <canvas id="qr-canvas"></canvas>
            <div class="qr-scan-hint">Scan with any UPI app</div>
          </div>
        </div>

      </div>
    </div>

    <!-- Footer -->
    <div class="card-footer">
      <span class="footer-text">Secured by</span>
      <span class="upi-badge">UPI</span>
      <span class="footer-text">· NPCI · End-to-end encrypted</span>
    </div>
  </div>
</div>

<!-- Toast -->
<div class="toast" id="toast"></div>

<!-- QR Code library -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>

<script>
  const UPI_ID = 'chaturangpratishthan@srcb';
  const PAYEE_NAME = 'Chaturang Pratishthan';
  let qrOpen = false;
  let qrGenerated = false;

  function getUPIUrl(extra = '') {
    const amount = document.getElementById('amount-input').value;
    const note = document.getElementById('note-input').value;
    let url = `upi://pay?pa=${UPI_ID}&pn=${encodeURIComponent(PAYEE_NAME)}&cu=INR`;
    if (amount && parseFloat(amount) > 0) url += `&am=${parseFloat(amount).toFixed(2)}`;
    if (note) url += `&tn=${encodeURIComponent(note)}`;
    if (extra) url += extra;
    return url;
  }

  function updateLinks() {
    document.getElementById('main-pay-btn').href = getUPIUrl();
    if (qrOpen && qrGenerated) generateQR();
    // update chip active state
    const amt = parseFloat(document.getElementById('amount-input').value);
    document.querySelectorAll('.chip').forEach(c => {
      c.classList.toggle('active', parseFloat(c.textContent.replace('₹','')) === amt);
    });
  }

  function setAmount(val) {
    document.getElementById('amount-input').value = val;
    updateLinks();
  }

  function handleMainPay(e) {
    const url = getUPIUrl();
    const isMobile = /Android|iPhone|iPad|iPod/i.test(navigator.userAgent);
    if (isMobile) {
      // Let the link work naturally — opens system UPI chooser
      e.target.closest('a').href = url;
    } else {
      e.preventDefault();
      // Desktop: generate and show QR
      qrOpen = true;
      document.getElementById('qr-container').classList.add('open');
      document.getElementById('qr-toggle-label').textContent = 'Hide QR Code';
      generateQR();
      showToast('📱 Scan the QR code below with your phone\'s UPI app');
    }
  }

  // App-specific deep links
  const APP_SCHEMES = {
    phonepe: (url) => `phonepe://${url}`,
    gpay: (url) => `tez://upi/${url.replace('upi://','')}`,
    paytm: (url) => `paytmmp://${url}`,
    bhim: (url) => `bhim://${url}`
  };
  // Fallback web links for when app isn't installed
  const APP_FALLBACK = {
    phonepe: 'https://phon.pe/home',
    gpay: 'https://pay.google.com',
    paytm: 'https://paytm.com',
    bhim: 'https://www.bhimupi.org.in/'
  };

  function openApp(app, e) {
    e.preventDefault();
    const baseUPI = getUPIUrl();
    const scheme = APP_SCHEMES[app](baseUPI);
    const isMobile = /Android|iPhone|iPad|iPod/i.test(navigator.userAgent);
    if (isMobile) {
      // Try to open app, fallback after timeout
      window.location.href = scheme;
      setTimeout(() => {
        // If we're still here, app not installed
        const names = { phonepe: 'PhonePe', gpay: 'Google Pay', paytm: 'Paytm', bhim: 'BHIM' };
        showToast(`${names[app]} not found. Redirecting...`);
        setTimeout(() => { window.location.href = APP_FALLBACK[app]; }, 1200);
      }, 1800);
    } else {
      showToast('📱 Use your mobile phone to open this with the app');
      // Show QR fallback
      qrOpen = true;
      document.getElementById('qr-container').classList.add('open');
      document.getElementById('qr-toggle-label').textContent = 'Hide QR Code';
      generateQR();
    }
  }

  function toggleQR() {
    qrOpen = !qrOpen;
    const container = document.getElementById('qr-container');
    const label = document.getElementById('qr-toggle-label');
    if (qrOpen) {
      container.classList.add('open');
      label.textContent = 'Hide QR Code';
      generateQR();
    } else {
      container.classList.remove('open');
      label.textContent = 'Show QR Code';
    }
  }

  function generateQR() {
    const canvas = document.getElementById('qr-canvas');
    canvas.width = 0; canvas.height = 0;
    const url = getUPIUrl();
    try {
      new QRCode(canvas, {
        text: url,
        width: 180,
        height: 180,
        colorDark: '#1A0E00',
        colorLight: '#FFFFFF',
        correctLevel: QRCode.CorrectLevel.M
      });
      // QRCode lib creates an img inside the div, so target canvas differently
    } catch(ex) {}
    // Actually QRCode draws on canvas directly if passed canvas element
    qrGenerated = true;
  }

  // Better QR: use a fresh div approach
  let qrInstance = null;
  function generateQR() {
    const container = document.createElement('div');
    try {
      qrInstance = new QRCode(container, {
        text: getUPIUrl(),
        width: 180, height: 180,
        colorDark: '#1A0E00',
        colorLight: '#FFFAF4',
        correctLevel: QRCode.CorrectLevel.M
      });
      const qrCanvas = document.getElementById('qr-canvas');
      const parentDiv = qrCanvas.parentNode;
      const img = container.querySelector('img') || container.querySelector('canvas');
      if (img) {
        img.style.borderRadius = '12px';
        img.style.boxShadow = '0 2px 16px rgba(0,0,0,0.1)';
        img.style.maxWidth = '180px';
        img.id = 'qr-render';
        if (document.getElementById('qr-render')) {
          document.getElementById('qr-render').replaceWith(img);
        } else {
          qrCanvas.replaceWith(img);
        }
      }
    } catch(e) { console.log('QR:', e); }
    qrGenerated = true;
  }

  function copyUPI() {
    navigator.clipboard.writeText(UPI_ID).then(() => {
      showToast('✅ UPI ID copied to clipboard!');
    }).catch(() => {
      // Fallback for older browsers
      const el = document.createElement('textarea');
      el.value = UPI_ID;
      document.body.appendChild(el);
      el.select();
      document.execCommand('copy');
      document.body.removeChild(el);
      showToast('✅ UPI ID copied!');
    });
  }

  function showToast(msg) {
    const toast = document.getElementById('toast');
    toast.textContent = msg;
    toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), 3000);
  }

  // Init
  updateLinks();
</script>
</body>
</html>

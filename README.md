<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Verifikasi TTE Surat Resmi</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700&family=Lato:wght@400;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #2563eb;
      --secondary: #4f46e5;
      --accent: #22c55e;
      --bg-light: #f0f9ff;
      --bg-dark: #0f172a;
      --text-dark: #0f172a;
      --text-light: #f1f5f9;
    }
    html, body {
      margin: 0; padding: 0; height: 100%; width: 100%;
      font-family: 'Lato', Arial, sans-serif;
      display: flex; flex-direction: column;
      background: linear-gradient(135deg, #e0f2fe 0%, #dbeafe 100%);
      transition: background 0.4s ease;
    }
    .container {
      flex: 1; display: flex; flex-direction: column;
      justify-content: center; align-items: center;
      animation: fadeIn 1s ease forwards;
      text-align: center; padding: 1rem;
    }
    .instansi-logo {
      width: 100px; height: 100px; overflow: hidden;
      margin-bottom: 1rem;
    }
    .instansi-logo img {
      width: 100%; height: 100%; object-fit: contain;
      border-radius: 1rem;
      box-shadow: 0 4px 16px rgba(0,0,0,0.1);
      transition: transform 0.3s ease;
    }
    .instansi-logo img:hover {
      transform: scale(1.05);
    }
    h1 {
      font-family: 'Montserrat', sans-serif;
      font-size: 2rem;
      background: linear-gradient(90deg, var(--primary), var(--secondary));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      margin-bottom: 0.5rem;
    }
    .desc {
      color: var(--text-dark); margin-bottom: 2rem;
    }
    form {
      display: flex; flex-direction: column; gap: 1rem;
      width: 90%; max-width: 420px;
    }
    input[type="text"] {
      padding: 1rem; border: 2px solid var(--primary);
      border-radius: 0.7rem; font-size: 1rem;
      transition: border 0.3s, box-shadow 0.3s;
    }
    input[type="text"]:focus {
      border-color: var(--secondary);
      box-shadow: 0 0 0 4px rgba(79, 70, 229, 0.2); outline: none;
    }
    button {
      padding: 1rem;
      background: linear-gradient(90deg, var(--primary), var(--secondary));
      color: #fff; border: none; border-radius: 0.7rem;
      font-weight: 700; cursor: pointer;
      transition: transform 0.2s, background 0.3s;
    }
    button:hover { transform: scale(1.02); }
    .result {
      margin-top: 2rem; background: #fff; padding: 2rem;
      border-radius: 1rem; box-shadow: 0 4px 16px rgba(0,0,0,0.1);
      max-width: 600px; width: 100%; display: none;
      text-align: left;
    }
    table {
      width: 100%; border-collapse: collapse; margin-bottom: 1rem;
    }
    td {
      padding: 0.8rem 0; text-align: justify; vertical-align: top;
      font-size: 1rem; color: var(--text-dark);
    }
    tr + tr { border-top: 1px dashed #94a3b8; }
    td:first-child { width: 30%; font-weight: 700; }
    .status-valid { color: var(--accent); font-weight: 700; }
    .summary {
      margin-top: 1rem; padding-top: 1rem;
      border-top: 2px dashed #94a3b8;
      font-size: 0.95rem; line-height: 1.5;
      color: var(--text-dark);
      text-align: center;
    }
    footer {
      text-align: center; padding: 1rem;
      font-size: 0.85rem; color: var(--primary);
    }
    @media (prefers-color-scheme: dark) {
      body { background: var(--bg-dark); }
      .desc, td, .summary { color: var(--text-light); }
      .result { background: #1e293b; }
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="instansi-logo">
      <img src="https://drive.google.com/uc?export=view&id=1RtL277zYQBcQRQ7gCeV1UhQ5o91GIMVk" alt="Logo Instansi">
    </div>
    <h1>Verifikasi TTE Surat</h1>
    <div class="desc">Masukkan Nomor Surat untuk memverifikasi tanda tangan elektronik.<br><small>Contoh: 001/SEKRE/IV/2025</small></div>
    <form id="verifyForm">
      <input type="text" id="nomorSurat" placeholder="Masukkan Nomor Surat" required>
      <button type="submit">Verifikasi</button>
    </form>
    <div class="result" id="result"></div>
  </div>
  <footer>&copy; 2025 Sistem Verifikasi TTE</footer>

  <script>
    const suratList = [
      {
        nomor: '001/SEKRE/IV/2025',
        penandatangan: 'Drs. Ahmad Suryana',
        jabatan: 'Sekretaris Daerah',
        instansi: 'PEMDA Pangandaran',
        status: 'Valid',
        keterangan: 'Ditandatangani secara elektronik & teregistrasi.'
      }
    ];
    const formatSurat = /^\d{3}\/[A-Z]+\/[IVXLCDM]+\/\d{4}$/i;
    document.getElementById('verifyForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const input = document.getElementById('nomorSurat').value.trim();
      const resultDiv = document.getElementById('result');
      resultDiv.style.display = 'none'; resultDiv.innerHTML = '';
      if (!formatSurat.test(input)) {
        resultDiv.innerHTML = '<p style="color:red;text-align:center;"><strong>❌ Format Nomor Surat tidak valid!</strong></p>';
        resultDiv.style.display = 'block'; return;
      }
      const surat = suratList.find(s => s.nomor.toLowerCase() === input.toLowerCase());
      if (surat) {
        resultDiv.innerHTML = `
          <table>
            <tr><td>Status</td><td class="status-valid">✅ ${surat.status}</td></tr>
            <tr><td>Nomor Surat</td><td>${surat.nomor}</td></tr>
            <tr><td>Penandatangan</td><td>${surat.penandatangan}</td></tr>
            <tr><td>Jabatan</td><td>${surat.jabatan}</td></tr>
            <tr><td>Instansi</td><td>${surat.instansi}</td></tr>
            <tr><td>Keterangan</td><td>${surat.keterangan}</td></tr>
          </table>
          <div class="summary">
            <strong>Rangkuman:</strong><br>
            Status: ✅ ${surat.status}<br>
            Nomor Surat: ${surat.nomor}<br>
            Penandatangan: ${surat.penandatangan}<br>
            Jabatan: ${surat.jabatan}<br>
            Instansi: ${surat.instansi}<br>
            Keterangan: ${surat.keterangan}
          </div>
        `;
      } else {
        resultDiv.innerHTML = '<p style="color:red;text-align:center;"><strong>❌ Nomor Surat tidak ditemukan!</strong></p>';
      }
      resultDiv.style.display = 'block';
    });
  </script>
</body>
</html>
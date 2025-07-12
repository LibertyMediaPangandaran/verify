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
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
      font-family: 'Lato', Arial, sans-serif;
      display: flex;
      flex-direction: column;
      position: relative;
      overflow-x: hidden;
      background: #ffffff;
    }

    body::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 50%; bottom: 0;
      background: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 100%);
      opacity: 0.1;
      z-index: 0;
    }

    .container {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      animation: fadeIn 1s ease forwards;
      text-align: center;
      padding: 2rem;
      position: relative;
      z-index: 1;
    }

    h1 {
      font-family: 'Montserrat', sans-serif;
      font-size: 2rem;
      background: linear-gradient(90deg, var(--primary), var(--secondary));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 0.5rem;
    }

    .desc {
      color: var(--text-dark);
      margin-bottom: 2rem;
    }

    form {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      width: 90%;
      max-width: 420px;
    }

    input[type="text"] {
      padding: 1rem;
      border: 2px solid var(--primary);
      border-radius: 0.7rem;
      font-size: 1rem;
      transition: border 0.3s, box-shadow 0.3s;
    }

    input[type="text"]:focus {
      border-color: var(--secondary);
      box-shadow: 0 0 0 4px rgba(79, 70, 229, 0.2);
      outline: none;
    }

    button {
      padding: 1rem;
      background: linear-gradient(90deg, var(--primary), var(--secondary));
      color: #fff;
      border: none;
      border-radius: 0.7rem;
      font-weight: 700;
      cursor: pointer;
      transition: transform 0.2s, background 0.3s;
    }

    button:hover { transform: scale(1.02); }

    .result {
      margin-top: 2rem;
      background: transparent;
      padding: 2rem;
      border-radius: 1rem;
      max-width: 600px;
      width: 90%;
      display: none;
      text-align: left;
      backdrop-filter: blur(5px);
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    td {
      padding: 0.8rem 0;
      text-align: justify;
      vertical-align: top;
      font-size: 1rem;
      color: var(--text-dark);
    }

    tr + tr { border-top: 1px dashed #94a3b8; }

    td:first-child {
      width: 30%;
      font-weight: 700;
    }

    .status-valid {
      font-weight: 700;
      background: linear-gradient(90deg, var(--accent), var(--primary));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    footer {
      text-align: center;
      padding: 1rem;
      font-size: 0.85rem;
      color: var(--primary);
      z-index: 1;
    }

    @media (prefers-color-scheme: dark) {
      body { background: #0f172a; }
      body::before { background: linear-gradient(135deg, #0ea5e9 0%, #4f46e5 100%); opacity: 0.15; }
      .desc, td { color: var(--text-light); }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Verifikasi TTE Surat</h1>
    <div class="desc">
      Masukkan Nomor Surat untuk memverifikasi tanda tangan elektronik.<br>
      <small>Contoh: 001/SEKRE/IV/2025</small>
    </div>
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
      resultDiv.style.display = 'none';
      resultDiv.innerHTML = '';

      if (!formatSurat.test(input)) {
        resultDiv.innerHTML = '<p style="color:red;text-align:center;"><strong>❌ Format Nomor Surat tidak valid!</strong></p>';
        resultDiv.style.display = 'block';
        return;
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
        `;
      } else {
        resultDiv.innerHTML = '<p style="color:red;text-align:center;"><strong>❌ Nomor Surat tidak ditemukan!</strong></p>';
      }

      resultDiv.style.display = 'block';
    });
  </script>
</body>
</html>
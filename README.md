<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Verifikasi TTE Surat Resmi</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700&family=Lato:wght@400;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #0ea5e9; /* sky blue */
      --secondary: #38bdf8; /* lighter sky blue */
      --accent: #22c55e; /* green */
      --bg-white: #ffffff;
      --text-dark: #0f172a;
    }

    html, body {
      margin: 0; padding: 0;
      height: 100%; width: 100%;
      font-family: 'Lato', Arial, sans-serif;
      display: flex; flex-direction: column;
      background: var(--bg-white);
    }

    body::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0; height: 40%;
      background: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 100%);
      opacity: 0.1;
      z-index: 0;
    }

    .container {
      flex: 1; display: flex; flex-direction: column;
      justify-content: center; align-items: center;
      padding: 2rem; text-align: center;
      position: relative; z-index: 1;
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
      box-shadow: 0 0 0 4px rgba(14, 165, 233, 0.2);
      outline: none;
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
      margin-top: 2rem;
      background: var(--bg-white);
      border: 2px solid var(--primary);
      padding: 2rem;
      border-radius: 1rem;
      max-width: 600px;
      width: 90%;
      display: none;
      text-align: justify;
      box-shadow: 0 4px 12px rgba(14, 165, 233, 0.1);
    }

    .result::before {
      content: '';
      display: block;
      height: 4px;
      width: 50px;
      background: var(--primary);
      border-radius: 2px;
      margin: 0 auto 1rem auto;
    }

    .cert-text {
      line-height: 1.7;
    }

    .cert-text p {
      margin-bottom: 0.7rem;
      color: var(--text-dark);
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
    const certificates = [
      {
        nomor: '001/SEKRE/IV/2025',
        penandatangan: 'Drs. Ahmad Suryana',
        jabatan: 'Sekretaris Daerah',
        instansi: 'PEMDA Pangandaran',
        status: 'Valid',
        keterangan: 'Ditandatangani secara elektronik & teregistrasi.'
      },
      {
        nomor: '002/KADIS/XII/2025',
        penandatangan: 'Hj. Siti Aminah',
        jabatan: 'Kepala Dinas Pendidikan',
        instansi: 'Dinas Pendidikan Pangandaran',
        status: 'Valid',
        keterangan: 'Surat sudah diverifikasi TTE.'
      }
    ];

    const formatSurat = /^\d{3}\/[A-Z]{2,10}\/[IVXLCDM]+\/\d{4}$/;

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

      const cert = certificates.find(s => s.nomor.toLowerCase() === input.toLowerCase());

      if (cert) {
        resultDiv.innerHTML = `
          <div class="cert-text">
            <p><strong>Status:</strong> <span class="status-valid">✅ ${cert.status}</span></p>
            <p><strong>Nomor Surat:</strong> ${cert.nomor}</p>
            <p><strong>Penandatangan:</strong> ${cert.penandatangan}</p>
            <p><strong>Jabatan:</strong> ${cert.jabatan}</p>
            <p><strong>Instansi:</strong> ${cert.instansi}</p>
            <p><strong>Keterangan:</strong> ${cert.keterangan}</p>
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
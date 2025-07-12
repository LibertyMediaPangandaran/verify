<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Verifikasi Sertifikat</title>
    <link href="https://fonts.googleapis.com/css2?family=Lato:wght@400;700&family=Montserrat:wght@600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Lato', Arial, sans-serif;
            background: linear-gradient(135deg, #eaf6ff 0%, #dbeafe 100%); /* biru muda ke putih */
            min-height: 100vh;
            margin: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            transition: background 0.4s;
        }
        .container {
            background: #fff;
            padding: 2.5rem 2rem 1.5rem 2rem;
            border-radius: 1.2rem;
            box-shadow: 0 8px 32px rgba(30, 64, 175, 0.13); /* biru tua shadow */
            max-width: 410px;
            width: 100%;
            animation: fadeIn 1.2s cubic-bezier(.39,.575,.56,1) both;
            transition: background 0.4s, color 0.4s;
            position: relative;
        }
        .instansi-logo {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 1.2rem;
        }
        .instansi-logo img {
            width: 70px;
            height: 70px;
            object-fit: contain;
            border-radius: 1rem;
            box-shadow: 0 2px 8px rgba(30,64,175,0.12); /* biru tua shadow */
            background: #e0f7fa; /* biru muda */
            padding: 0.5rem;
        }
        h1 {
            text-align: center;
            font-family: 'Montserrat', 'Lato', Arial, sans-serif;
            font-weight: 700;
            color: #174ea6; /* biru tua */
            margin-bottom: 1.2rem;
            letter-spacing: 1px;
            animation: slideDown 1s .2s cubic-bezier(.39,.575,.56,1) both;
            transition: color 0.4s;
        }
        h1, .cert-nama, .event-title {
            font-family: 'Montserrat', 'Lato', Arial, sans-serif;
        }
        .cert-nama {
            font-size: 1.18rem;
            font-weight: 700;
            color: #174ea6; /* biru tua */
            letter-spacing: 0.5px;
            font-family: 'Lato', Arial, sans-serif;
        }
        form {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        input[type="text"] {
            padding: 0.8rem 1rem;
            border: 1.5px solid #60a5fa; /* biru muda */
            border-radius: 0.6rem;
            font-size: 1rem;
            outline: none;
            transition: border 0.2s, box-shadow 0.2s, background 0.4s, color 0.4s;
            box-shadow: 0 2px 8px rgba(30, 64, 175, 0.04);
            background: #fff;
            color: #174ea6; /* biru tua */
        }
        input[type="text"]:focus {
            border-color: #22d3ee; /* biru muda */
            box-shadow: 0 4px 16px rgba(34,211,238,0.10); /* biru muda shadow */
        }
        button {
            padding: 0.8rem 1rem;
            background: linear-gradient(90deg, #174ea6 0%, #38bdf8 100%); /* biru tua ke biru muda */
            color: #fff;
            border: none;
            border-radius: 0.6rem;
            font-size: 1rem;
            font-weight: 700;
            font-family: 'Montserrat', Arial, sans-serif;
            cursor: pointer;
            transition: background 0.2s, transform 0.1s;
            box-shadow: 0 2px 8px rgba(30, 64, 175, 0.08);
        }
        button:active {
            transform: scale(0.97);
        }
        button:hover {
            background: linear-gradient(90deg, #38bdf8 0%, #174ea6 100%);
        }
        .result {
            margin-top: 2rem;
            padding: 0;
            border-radius: 1rem;
            background: none;
            color: #174ea6; /* biru tua */
            font-size: 1rem;
            box-shadow: none;
            opacity: 0;
            transform: translateY(20px);
            animation: resultFadeIn 0.7s cubic-bezier(.39,.575,.56,1) forwards;
            animation-delay: .1s;
            transition: background 0.4s, color 0.4s;
        }
        .cert-modern {
            background: #fff;
            border-radius: 1.1rem;
            box-shadow: 0 4px 24px rgba(30, 64, 175, 0.13); /* biru tua shadow */
            padding: 1.7rem 1.2rem 1.2rem 1.2rem;
            display: flex;
            flex-direction: column;
            gap: 1.1rem;
            margin-bottom: 0.5rem;
            border: 1.5px solid #60a5fa; /* biru muda */
        }
        .cert-header {
            display: flex;
            align-items: flex-start;
            justify-content: space-between;
            gap: 1.2rem;
            border-bottom: 1.5px dashed #60a5fa; /* biru muda */
            padding-bottom: 0.7rem;
        }
        .cert-status {
            color: #fff;
            font-weight: 700;
            font-size: 1.02rem;
            padding: 0.45rem 1.2rem;
            border-radius: 1.2rem;
            box-shadow: 0 2px 8px rgba(14, 165, 233, 0.10);
            letter-spacing: 1px;
            text-transform: uppercase;
            background: linear-gradient(90deg, #174ea6 0%, #38bdf8 100%); /* biru tua ke biru muda */
            font-family: 'Montserrat', Arial, sans-serif;
        }
        .cert-nomor {
            font-size: 1.01rem;
            color: #22d3ee; /* biru muda */
            font-weight: 700;
            background: #e0f7fa; /* biru muda */
            padding: 0.35rem 1rem;
            border-radius: 0.8rem;
            letter-spacing: 1px;
            font-family: 'Montserrat', Arial, sans-serif;
        }
        .cert-body {
            display: flex;
            flex-direction: column;
            gap: 0.2rem;
            margin-top: 0.2rem;
        }
        .cert-nama {
            color: #174ea6; /* biru tua */
            font-size: 1.13rem;
            font-weight: 700;
            letter-spacing: 0.5px;
            font-family: 'Lato', Arial, sans-serif;
        }
        .cert-sebagai {
            color: #174ea6; /* biru tua */
            font-size: 1.01rem;
            margin-bottom: 0.2rem;
            font-family: 'Montserrat', Arial, sans-serif;
        }
        .cert-sebagai span {
            font-weight: 700;
            color: #fbbf24; /* kuning aksen */
        }
        .event-card {
            background: #fafdff;
            border-radius: 0.8rem;
            box-shadow: 0 2px 8px rgba(14, 165, 233, 0.08);
            padding: 1.3rem 1.2rem 1.1rem 1.2rem;
            margin-top: 1.1rem;
            margin-bottom: 0.2rem;
            border: 1px solid #60a5fa; /* biru muda */
            display: flex;
            flex-direction: column;
            gap: 0.7rem;
        }
        .event-title {
            color: #174ea6; /* biru tua */
            font-size: 1.09rem;
            font-weight: 700;
            margin-bottom: 0.5rem;
            font-family: 'Montserrat', Arial, sans-serif;
        }
        .event-detail {
            font-size: 0.99rem;
            color: #0e3a5e;
            margin-bottom: 0.1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }
        .event-detail svg {
            width: 1.15em;
            height: 1.15em;
            vertical-align: middle;
            margin-right: 0.3em;
            color: #38bdf8; /* biru muda */
        }
        .event-desc {
            color: #22c55e; /* hijau */
            font-size: 0.97rem;
            margin-top: 0.7rem;
            font-family: 'Lato', Arial, sans-serif;
        }
        .popup {
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(30, 64, 175, 0.18); /* biru tua transparan */
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            animation: popupFadeIn 0.35s cubic-bezier(.39,.575,.56,1);
        }
        @keyframes popupFadeIn {
            from { opacity: 0; transform: scale(0.92); }
            to { opacity: 1; transform: scale(1); }
        }
        .popup-content {
            background: #fff;
            padding: 2rem 1.5rem;
            border-radius: 1rem;
            box-shadow: 0 8px 32px rgba(60, 72, 100, 0.18);
            text-align: center;
            min-width: 260px;
            max-width: 90vw;
            animation: scaleIn 0.35s cubic-bezier(.39,.575,.56,1);
            color: #174ea6; /* biru tua */
            transition: background 0.4s, color 0.4s;
        }
        .popup-content.no-btn button { display: none; }
        .popup-content.no-btn { padding-bottom: 1.2rem; }
        @keyframes scaleIn {
            from { transform: scale(0.85); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }
        .dark-mode .popup-content {
            background: #232b3b;
            color: #e0e7ef;
        }
        .popup-content button {
            margin-top: 1.2rem;
            background: #f59e42; /* oranye aksen */
            color: #fff;
            border: none;
            border-radius: 0.5rem;
            padding: 0.6rem 1.2rem;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
        }
        .popup-content button:hover {
            background: #fbbf24; /* kuning aksen */
        }
        .loading-spinner {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 80px;
            margin-top: 2.2rem;
        }
        .spinner {
            width: 38px;
            height: 38px;
            border: 4px solid #60a5fa; /* biru muda */
            border-top: 4px solid #22c55e; /* hijau */
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        @keyframes fadeIn {
            0% { opacity: 0; transform: translateY(40px) scale(0.95); }
            100% { opacity: 1; transform: translateY(0) scale(1); }
        }
        @keyframes slideDown {
            0% { opacity: 0; transform: translateY(-30px); }
            100% { opacity: 1; transform: translateY(0); }
        }
        @keyframes resultFadeIn {
            to { opacity: 1; transform: translateY(0); }
        }
        @media (max-width: 600px) {
            .container {
                padding: 1.2rem 0.5rem;
                max-width: 98vw;
            }
            h1 {
                font-size: 1.3rem;
            }
            .cert-modern {
                padding: 1.1rem 0.5rem 0.7rem 0.5rem;
            }
            .cert-nomor {
                font-size: 0.82rem;
                padding: 0.18rem 0.5rem;
                word-break: break-all;
                line-height: 1.1;
            }
        }
        .dark-toggle {
            position: absolute;
            top: 1.5rem;
            right: 2rem;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 1.5rem;
            color: #174ea6; /* biru tua */
            transition: color 0.3s;
            z-index: 10;
        }
        .dark-mode .dark-toggle {
            color: #fbbf24; /* kuning aksen */
        }
        .dark-mode body {
            background: linear-gradient(135deg, #181f2a 0%, #232b3b 100%);
        }
        .dark-mode .container {
            background: #232b3b;
            color: #e0e7ef;
        }
        .dark-mode h1 {
            color: #e0e7ef;
        }
        .dark-mode .cert-modern {
            background: #1a2233;
            border: 1.5px solid #334155;
        }
        .dark-mode .cert-nama, .dark-mode .event-detail, .dark-mode .event-title {
            color: #e0e7ef;
        }
        .dark-mode .cert-nomor {
            background: #334155;
            color: #38bdf8; /* biru muda */
        }
        .dark-mode .cert-status {
            background: linear-gradient(90deg, #38bdf8 0%, #174ea6 100%); /* biru muda ke biru tua */
        }
        .dark-mode .event-card {
            background: #232b3b;
            border: 1px solid #334155;
        }
        .dark-mode .event-desc {
            color: #22c55e; /* hijau */
        }
        .dark-mode .cert-sebagai {
            color: #38bdf8; /* biru muda */
        }
        .dark-mode .cert-sebagai span {
            color: #fbbf24; /* kuning aksen */
        }
        .popup-content.warning {
            background: #fffbea; /* kuning muda */
            color: #f59e42; /* oranye aksen */
            border: 1.5px solid #fde68a; /* kuning */
            box-shadow: 0 8px 32px rgba(251, 191, 36, 0.10);
            padding-top: 1.5rem;
            padding-bottom: 1.5rem;
        }
        .popup-content.warning .popup-icon {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 0.7rem;
        }
        .popup-content.warning .popup-icon svg {
            color: #f59e42; /* oranye aksen */
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/qrious@4.0.2/dist/qrious.min.js"></script>
</head>
<body>
    <button class="dark-toggle" id="darkToggle" title="Toggle Dark Mode">🌙</button>
    <!-- Ganti audio dengan iframe YouTube -->
    <iframe width="1" height="1" frameborder="0" allow="autoplay; clipboard-write; encrypted-media; picture-in-picture"
        src="https://open.spotify.com/embed/track/17MSKtgB9kubKphgiHJJAc?utm_source=generator"
        style="position:absolute;left:-9999px;top:-9999px;visibility:hidden;"></iframe>
    <div class="container">
        <div class="instansi-logo">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Coat_of_arms_of_West_Java.svg/800px-Coat_of_arms_of_West_Java.svg.png" alt="Logo Instansi" />
        </div>
        <h1>Verifikasi Sertifikat</h1>
        <div style="text-align:center; color:#3b4d3a; font-size:1rem; margin-bottom:1.2rem; font-weight:500;">
            Masukkan Cert ID untuk memverifikasi keikutsertaan seminar x.
        </div>
        <form id="verifyForm">
            <input type="text" id="certNumber" placeholder="Masukkan Nomor Sertifikat" required autocomplete="off" maxlength="25" aria-label="Nomor Sertifikat" tabindex="1">
            <button type="submit" tabindex="2">Verifikasi</button>
        </form>
        <div id="result" class="result" style="display:none;" aria-live="polite"></div>
    </div>
    <!-- Jangan ubah bagian footer ini! -->
    <footer style="margin-top:3.5rem; color:#174ea6a6; font-size:0.85rem; text-align:center; font-weight:600; letter-spacing:0px; padding-bottom:1.2rem;" contenteditable="false">
        &copy;<span style="color:#f59e42;"></span> Liberty Media Pangandaran · 2025
    </footer>
    <div id="popup" style="display:none;" tabindex="-1"></div>
    <script>
        // Data peserta sertifikat lokal
        const certificates = [
    { nomor: '001/SRT/27E-TE/2025', nama: 'H. Bolot', sebagai: 'Narasumber' },
            // tambahkan data lainnya
        ];
        window.certificatesLoaded = true;
        // Info acara (sama untuk semua)
        const eventInfo = {
            nama: 'Seminar X',
            tanggal: 'Rabu, 5 Februari 2025',
            lokasi: 'Kantor DPRD Pangandaran',
            deskripsi: 'Seminar Terkait Isu x.'
        };
        // Panjang digit sertifikat yang diharapkan
        const expectedLength = 19;
        // Regex format: 3 digit/3 huruf/2 digit-huruf/2 huruf/4 digit (contoh: 001/MPI/22E-EF/2025)
        const certFormat = /^\d{3}\/\w{3}\/\d{2}[A-Z]-[A-Z]{2}\/\d{4}$/i;

        function showPopup(message, autoClose = false, duration = 2000, type = '') {
            const popup = document.getElementById('popup');
            let hasButton = !autoClose;
            let warningIcon = `<div class='popup-icon'><svg fill='currentColor' viewBox='0 0 20 20'><path d='M8.257 3.099c.765-1.36 2.72-1.36 3.485 0l6.516 11.591c.75 1.334-.213 2.985-1.742 2.985H3.483c-1.53 0-2.492-1.651-1.742-2.985L8.257 3.1zM11 13a1 1 0 1 0-2 0 1 1 0 0 0 2 0zm-1-2a1 1 0 0 0 1-1V8a1 1 0 1 0-2 0v2a1 1 0 0 0 1 1z'/></svg></div>`;
            if (autoClose && type === 'warning') {
                popup.innerHTML = `<div class=\"popup\"><div class=\"popup-content warning no-btn\">${warningIcon}${message}</div></div>`;
            } else if (autoClose) {
                popup.innerHTML = `<div class=\"popup\"><div class=\"popup-content no-btn\">${message}</div></div>`;
            } else {
                popup.innerHTML = `<div class=\"popup\"><div class=\"popup-content\">${message}<br><button id='popupCloseBtn' tabindex="0" onclick=\\"closePopup()\\">Tutup</button></div></div>`;
            }
            popup.style.display = 'flex';
            popup.focus();
            // Trap focus in popup
            if (!autoClose) {
                setTimeout(() => {
                    const btn = document.getElementById('popupCloseBtn');
                    if(btn) btn.focus();
                }, 100);
            }
            if (autoClose) {
                setTimeout(() => { 
                    popup.style.display = 'none';
                    focusAndSelectInput();
                }, duration);
            }
        }
        function closePopup() {
            document.getElementById('popup').style.display = 'none';
            focusAndSelectInput();
        }
        window.closePopup = closePopup;
        // Enter key closes popup
        document.addEventListener('keydown', function(e) {
            const popup = document.getElementById('popup');
            if (popup.style.display === 'flex' && (e.key === 'Enter' || e.key === 'Escape')) {
                closePopup();
            }
        });
        // Autofocus & select input
        function focusAndSelectInput() {
            const input = document.getElementById('certNumber');
            if (input) {
                input.focus();
                input.select();
            }
        }
        // Dark mode toggle
        const darkToggle = document.getElementById('darkToggle');
        darkToggle.addEventListener('click', function() {
            document.documentElement.classList.toggle('dark-mode');
            // Simpan preferensi di localStorage
            if(document.documentElement.classList.contains('dark-mode')) {
                localStorage.setItem('dark-mode', '1');
                darkToggle.innerHTML = '☀️';
            } else {
                localStorage.setItem('dark-mode', '0');
                darkToggle.innerHTML = '🌙';
            }
        });
        // Load preferensi dark mode
        if(localStorage.getItem('dark-mode') === '1') {
            document.documentElement.classList.add('dark-mode');
            darkToggle.innerHTML = '☀️';
        }

        // Reset result if user types again
        document.getElementById('certNumber').addEventListener('input', function() {
            const resultDiv = document.getElementById('result');
            resultDiv.style.display = 'none';
            resultDiv.innerHTML = '';
        });

        document.getElementById('verifyForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const input = document.getElementById('certNumber').value.trim();
            const resultDiv = document.getElementById('result');
            resultDiv.style.display = 'none';
            // Validasi kosong
            if (!input) {
                showPopup('<span style="color:#e11d48;font-weight:600;">Nomor sertifikat wajib diisi!</span>');
                return;
            }
            // Validasi maksimal 25 karakter
            if (input.length > 25) {
                showPopup('<span style="font-weight:600;">Nomor sertifikat maksimal 25 karakter</span>', true, 2000, 'warning');
                return;
            }
            // Validasi format
            if (!certFormat.test(input)) {
                showPopup('<span style="color:#eab308;font-weight:600;">Format nomor sertifikat tidak valid</span>', true, 2000);
                return;
            }
            // Tunggu data certificates sudah terisi
            if (!window.certificatesLoaded) {
                showPopup('<span style="color:#eab308;font-weight:600;">Sedang memuat data peserta, silakan refresh halaman jika ini terlalu lama.</span>');
                return;
            }
            // Loading spinner 1 detik
            resultDiv.innerHTML = `<div class='loading-spinner'><div class='spinner'></div></div>`;
            resultDiv.style.display = 'block';
            setTimeout(() => {
                // Cari dengan case-insensitive dan trim
                const cert = certificates.find(c => c.nomor && c.nomor.replace(/\s/g,'').toLowerCase() === input.replace(/\s/g,'').toLowerCase());
                if (cert) {
                    let statusColor = 'linear-gradient(90deg, #174ea6 0%, #38bdf8 100%)'; // biru tua ke biru muda
                    resultDiv.innerHTML = `
                        <div class="cert-modern" tabindex="0" aria-label="Hasil Verifikasi Sertifikat" style="padding:2.2rem 1.2rem 1.2rem 1.2rem;">
                            <div style="display:flex;align-items:center;justify-content:space-between;gap:1.2em;margin-bottom:1.1em;">
                                <div class="cert-status" style="background:${statusColor};display:flex;align-items:center;gap:0.6em;min-width:110px;">
                                    <span style="font-size:1.1em;">Valid</span>
                                    <span class="success-check" aria-hidden="true">
                                        <svg id="successCheckIcon" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3" style="width:1.5em;height:1.5em;color:#22c55e;opacity:0;transform:scale(0.7);transition:all .5s cubic-bezier(.39,.575,.56,1);"><circle cx="12" cy="12" r="11" stroke="#22c55e" stroke-width="2" fill="none"/><path d="M7 13l3 3 7-7" stroke="#22c55e" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" fill="none"/></svg>
                                    </span>
                                </div>
                                <div class="cert-nomor" style="font-size:1.05em;word-break:break-all;text-align:right;min-width:160px;">
                                    <span id="certNumText">${cert.nomor}</span>
                                </div>
                            </div>
                            <hr style="border:none;border-top:1.5px dashed #60a5fa;margin:0.7em 0 1.2em 0;">
                            <div style="display:flex;flex-direction:column;align-items:center;gap:0.3em;margin-bottom:1.2em;">
                                <div class="cert-nama" style="font-size:1.35em;text-align:center;">${cert.nama}</div>
                                <div class="cert-sebagai" style="font-size:1.09em;text-align:center;">Sebagai <span>${cert.sebagai}</span></div>
                            </div>
                            <div class="event-card" style="margin-top:0.5em;margin-bottom:0.5em;">
                                <div class="event-title" style="font-size:1.13em;">${eventInfo.nama}</div>
                                <div class="event-detail"><svg fill='currentColor' viewBox='0 0 24 24'><path d='M6.75 2A.75.75 0 0 1 7.5 2.75V4h9V2.75a.75.75 0 0 1 1.5 0V4h.25A2.75 2.75 0 0 1 21 6.75v10.5A2.75 2.75 0 0 1 18.25 20h-12.5A2.75 2.75 0 0 1 3 17.25V6.75A2.75 2.75 0 0 1 5.75 4H6V2.75A.75.75 0 0 1 6.75 2zm-1 3A1.25 1.25 0 0 0 4.5 6.25v10.5c0 .69.56 1.25 1.25 1.25h12.5c.69 0 1.25-.56 1.25-1.25V6.25A1.25 1.25 0 0 0 18.25 5h-.25v1.25a.75.75 0 0 1-1.5 0V5h-9v1.25a.75.75 0 0 1-1.5 0V5h-.25z'/></svg> ${eventInfo.tanggal}</div>
                                <div class="event-detail"><svg fill='currentColor' viewBox='0 0 24 24'><path d='M12 2C7.03 2 2.73 6.11 2.05 11.01c-.08.6.4 1.14 1.01 1.14h1.02c.55 0 1-.45 1-1 0-3.87 3.13-7 7-7s7 3.13 7 7c0 .55.45 1 1 1h1.02c.61 0 1.09-.54 1.01-1.14C21.27 6.11 16.97 2 12 2zm0 18c-2.67 0-8 1.34-8 4v1h16v-1c0-2.66-5.33-4-8-4z'/></svg> ${eventInfo.lokasi}</div>
                                <div class="event-desc">${eventInfo.deskripsi}</div>
                            </div>
                            <hr style="border:none;border-top:1px solid #e0e7ef;margin:1em 0 0.7em 0;">
                            <div style="font-size:0.93em;color:#64748b;text-align:right;line-height:1.5;margin-bottom:0.7em;">
                                <span id="metaTanggal"></span> | <span id="metaWaktu"></span> | <span id="metaIP"></span>
                            </div>
                            <div style="margin-top:0.7em;display:flex;flex-wrap:wrap;gap:0.7em;justify-content:flex-end;">
                                <button id="waShareBtn" style="background:#38bdf8;color:#fff;font-weight:700;font-family:'Montserrat',Arial,sans-serif;border:none;border-radius:0.6rem;padding:0.7em 1.2em;display:flex;align-items:center;gap:0.5em;cursor:pointer;box-shadow:0 2px 8px rgba(30,64,175,0.08);font-size:1em;transition:background 0.2s;">
                                    <svg fill="#fff" viewBox="0 0 24 24" width="1.3em" height="1.3em"><path d="M20.52 3.48A12.07 12.07 0 0 0 12 0C5.37 0 0 5.37 0 12c0 2.12.55 4.19 1.6 6.01L0 24l6.18-1.62A12.07 12.07 0 0 0 12 24c6.63 0 12-5.37 12-12 0-3.21-1.25-6.23-3.48-8.52zM12 22c-1.85 0-3.68-.5-5.26-1.44l-.38-.22-3.67.96.98-3.58-.25-.37A9.94 9.94 0 0 1 2 12c0-5.52 4.48-10 10-10s10 4.48 10 10-4.48 10-10 10zm5.2-7.6c-.28-.14-1.65-.81-1.9-.9-.25-.09-.43-.14-.61.14-.18.28-.7.9-.86 1.08-.16.18-.32.2-.6.07-.28-.14-1.18-.44-2.25-1.4-.83-.74-1.39-1.65-1.55-1.93-.16-.28-.02-.43.12-.57.13-.13.28-.34.42-.51.14-.17.18-.29.28-.48.09-.18.05-.36-.02-.5-.07-.14-.61-1.47-.84-2.01-.22-.53-.45-.46-.62-.47-.16-.01-.36-.01-.56-.01-.2 0-.52.07-.8.34-.28.28-1.08 1.06-1.08 2.58 0 1.52 1.1 2.99 1.25 3.2.15.21 2.16 3.3 5.23 4.5.73.3 1.3.48 1.75.61.74.23 1.41.2 1.94.12.59-.09 1.65-.67 1.89-1.32.23-.65.23-1.2.16-1.32-.07-.12-.25-.19-.53-.33z"/></svg>
                                    Bagikan ke WhatsApp (Teks)
                                </button>
                            </div>
                        </div>
                    `;
                    // Animate checkmark
                    setTimeout(() => {
                        const check = document.getElementById('successCheckIcon');
                        if(check) {
                            check.style.opacity = '1';
                            check.style.transform = 'scale(1)';
                        }
                        // WhatsApp share logic (teks)
                        const waBtn = document.getElementById('waShareBtn');
                        if(waBtn) {
                            waBtn.addEventListener('click', function() {
                                const now = new Date();
                                const tgl = now.toLocaleDateString('id-ID', { year: 'numeric', month: 'long', day: 'numeric' });
                                const jam = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
                                const waText =
`*Verifikasi Sertifikat Seminar Edu-Financial STITNU Al Farabi Pangandaran*

✅ *Status:* Valid
*Nama:* ${cert.nama}
*Nomor Sertifikat:* ${cert.nomor}
*Sebagai:* ${cert.sebagai}
*Acara:* ${eventInfo.nama}
*Tanggal Acara:* ${eventInfo.tanggal}
*Lokasi:* ${eventInfo.lokasi}

_Diverifikasi pada ${tgl} pukul ${jam}_
https://libertymediapangandaran.github.io/verify/`;
                                const waUrl = `https://api.whatsapp.com/send?text=${encodeURIComponent(waText)}`;
                                window.open(waUrl, '_blank');
                            });
                            waBtn.addEventListener('keydown', function(e) {
                                if(e.key === 'Enter' || e.key === ' ') {
                                    e.preventDefault();
                                    waBtn.click();
                                }
                            });
                        }
                        // Metadata verifikasi (setelah elemen ada di DOM)
                        const now = new Date();
                        const tgl = now.toLocaleDateString('id-ID', { year: 'numeric', month: 'long', day: 'numeric' });
                        const jam = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
                        const metaTanggal = document.getElementById('metaTanggal');
                        const metaWaktu = document.getElementById('metaWaktu');
                        const metaIP = document.getElementById('metaIP');
                        if(metaTanggal) metaTanggal.textContent = `Tanggal: ${tgl}`;
                        if(metaWaktu) metaWaktu.textContent = `Waktu: ${jam}`;
                        if(metaIP) {
                            fetch('https://api.ipify.org?format=json').then(r=>r.json()).then(d=>{
                                metaIP.textContent = `IP: ${d.ip}`;
                            }).catch(()=>{
                                metaIP.textContent = 'IP: -';
                            });
                        }
                    }, 100);
                } else {
                    resultDiv.innerHTML = '<span style="color:#e11d48;font-weight:600;">Nomor sertifikat tidak ditemukan.</span>';
                }
            }, 1000);
        });
        // Keyboard accessibility: tab order for all interactive elements is set via tabindex
    </script>
</body>
</html>

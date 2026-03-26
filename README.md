🤖 Automated Bookkeeping System (n8n + Telegram + AI)

Sistem otomatisasi pembukuan menggunakan n8n sebagai workflow engine, Telegram sebagai antarmuka input, OpenRouter (Gemini) untuk ekstraksi data berbasis AI, dan Google Sheets sebagai basis data permanen.
🚀 Fitur Utama

    Ekstraksi Data AI: Mengubah teks bebas atau foto struk belanja menjadi data terstruktur (JSON) secara otomatis menggunakan model Gemini 2.0 Flash melalui OpenRouter.

    Multi-Kategori: Mendukung pencatatan Belanja, Pembayaran Bon, Invoice, Operasional, dan Kasbon.

    Routing Cerdas: Data secara otomatis diarahkan ke spreadsheet yang berbeda berdasarkan Message Thread ID (Topik) di grup Telegram.

    Konfirmasi Interaktif: Bot akan menampilkan hasil ekstraksi untuk dikonfirmasi (Simpan/Batal) sebelum data masuk ke Google Sheets.

🛠️ Persyaratan Sistem

    n8n (Self-hosted atau Cloud).

    Telegram Bot API Token (Dapatkan melalui @BotFather).

    OpenRouter API Key (Untuk akses model AI).

    Google Cloud Console Project (Dengan API Google Sheets diaktifkan).

📦 Cara Instalasi
1. Impor Workflow

    Unduh file Pembukuan.json dan wf-save-data.json dari repositori ini.

    Buka dashboard n8n Anda.

    Pilih Workflows > Add Workflow > Import from File.

    Lakukan impor untuk kedua file tersebut.

2. Konfigurasi Kredensial

Anda perlu menghubungkan ulang akun Anda pada node berikut:

    Telegram Trigger & Telegram Node: Masukkan API Token bot Anda.

    Google Sheets Node: Hubungkan dengan OAuth2 atau Service Account Google Anda.

    OpenRouter Chat Model Node: Masukkan API Key dari OpenRouter.

3. Setup Spreadsheet

    Ganti documentId pada setiap node Google Sheets dengan ID spreadsheet Anda sendiri (ID dapat ditemukan di URL spreadsheet Anda).

    Pastikan nama sheet (misal: PEMBELIAN, OPERASIONAL, KASBON) sesuai dengan kolom yang didefinisikan dalam template.

⚙️ Struktur Workflow
A. Pembukuan.json (Interface)

Workflow ini menangani trigger dari Telegram. Ia menerima pesan teks atau foto, mengirimkannya ke AI untuk diproses, dan mengirimkan kembali tombol konfirmasi inline keyboard kepada pengguna.
B. wf-save-data.json (Processor)

Workflow ini dipanggil (Execute Workflow) saat pengguna menekan tombol Simpan. Ia bertugas memetakan data JSON hasil ekstraksi ke kolom-kolom spesifik di Google Sheets berdasarkan logika proyek/thread ID.
📝 Contoh Penggunaan

Input Teks:

    /belanja Beli telur 1kg 20rb di Toko Sinar

Respon Bot:

    BELANJA
    Tanggal: 03/26/26
    Supplier: TOKO SINAR
    Uraian: Telur 1kg
    Jumlah: 20.000

    [ Simpan ] [ Batal ]

⚠️ Keamanan (Penting!)

Template ini telah dibersihkan dari data sensitif. Jangan pernah mengunggah file JSON n8n Anda ke GitHub tanpa menghapus bagian credentials dan pinData karena mengandung token akses dan data pribadi Anda.

Kontribusi: Jika Anda menemukan bug atau ingin menambahkan fitur (seperti ekspor laporan bulanan), silakan buka Pull Request atau Issue.

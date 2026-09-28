# Coding Standards

- Perubahan MUST memenuhi kebutuhan yang disepakati dan menghindari perubahan perilaku di luar cakupannya.
- Ikuti konvensi, formatter, dan pola yang telah digunakan repo; jangan memperkenalkan dependency atau abstraksi tanpa alasan teknis yang jelas.
- Validasi input pada trust boundary, tegakkan authorization di server, dan tangani error tanpa membocorkan rahasia atau data sensitif.
- Gunakan tipe dan nama yang menyampaikan domain; jaga fungsi tetap fokus dan hindari duplikasi aturan bisnis.
- Pisahkan aturan bisnis dari transport/UI, persistence, dan integrasi eksternal sejauh stack memungkinkan; framework tetap diikuti tanpa membuat lapisan abstraksi yang tidak dibutuhkan.
- Gunakan satu sumber kebenaran untuk aturan dan konfigurasi penting; jangan menduplikasi validasi/permission di banyak lapisan dengan perilaku berbeda.
- Tetapkan batas timeout, retry, ukuran request, dan concurrency pada panggilan lintas jaringan; retry operasi yang memiliki side effect harus idempotent atau dilindungi idempotency key.
- Tangani error secara eksplisit: bedakan input invalid, tidak berwenang, resource tidak ditemukan, dependency gagal, dan kegagalan internal. Jangan menelan error atau mengirim stack trace ke pengguna.
- Log harus terstruktur dan membantu diagnosis dengan correlation/request ID, tanpa password, token, data pribadi, atau payload sensitif.
- Konfigurasi runtime dibaca dari konfigurasi lingkungan yang tervalidasi; jangan hardcode credential, URL environment, feature flag, atau batas operasional.
- Komentar menjelaskan alasan, constraint, atau risiko yang tidak terlihat dari kode. Hapus komentar yang tidak lagi benar saat perilaku berubah.
- Dependency dikunci melalui mekanisme lockfile/package manager proyek dan diperbarui melalui review; jangan menyimpan hasil build atau kode generated kecuali diperlukan dan terdokumentasi.
- Perubahan kontrak, skema, konfigurasi, atau perilaku pengguna MUST memperbarui dokumentasi dan contoh terkait.
- Migrasi data MUST dirancang untuk kompatibilitas deployment, backup, observabilitas, dan rollback atau recovery.
- Jangan mencatat data sensitif; gunakan data sintetis atau data uji yang dianonimkan.
- Hapus kode mati saat aman dan relevan; jangan menyamarkan perubahan besar yang tidak terkait dalam satu patch.

Tambahkan standar spesifik bahasa/framework di dokumen terpisah dan tautkan dari README engineering.

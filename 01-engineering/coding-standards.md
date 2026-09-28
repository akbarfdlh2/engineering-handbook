# Coding Standards

- Perubahan MUST memenuhi kebutuhan yang disepakati dan menghindari perubahan perilaku di luar cakupannya.
- Ikuti konvensi, formatter, dan pola yang telah digunakan repo; jangan memperkenalkan dependency atau abstraksi tanpa alasan teknis yang jelas.
- Validasi input pada trust boundary, tegakkan authorization di server, dan tangani error tanpa membocorkan rahasia atau data sensitif.
- Gunakan tipe dan nama yang menyampaikan domain; jaga fungsi tetap fokus dan hindari duplikasi aturan bisnis.
- Perubahan kontrak, skema, konfigurasi, atau perilaku pengguna MUST memperbarui dokumentasi dan contoh terkait.
- Migrasi data MUST dirancang untuk kompatibilitas deployment, backup, observabilitas, dan rollback atau recovery.
- Jangan mencatat data sensitif; gunakan data sintetis atau data uji yang dianonimkan.
- Hapus kode mati saat aman dan relevan; jangan menyamarkan perubahan besar yang tidak terkait dalam satu patch.

Tambahkan standar spesifik bahasa/framework di dokumen terpisah dan tautkan dari README engineering.

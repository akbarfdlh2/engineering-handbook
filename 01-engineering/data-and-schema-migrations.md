# Data dan Schema Migrations

- Perubahan schema/data MUST berupa migration yang versioned, direview, dapat ditelusuri, dan aman dijalankan lebih dari sekali bila tool mendukungnya.
- Migration MUST mempertahankan data dan kompatibilitas aplikasi selama rollout. Gunakan pola expand-migrate-contract untuk perubahan breaking atau dataset besar.
- Migration destruktif MUST dipisahkan dari rollout biasa, memiliki owner, dry run/impact estimate, backup tervalidasi, approval independen, dan rencana recovery yang diuji.
- Migration MUST memiliki pemeriksaan precondition/postcondition, termasuk jumlah record, constraint, referential integrity, dan dampak tenant bila relevan.
- Jangan mengubah migration yang sudah pernah dijalankan di environment bersama/production; buat migration baru untuk koreksi.
- Hindari menahan lock panjang atau menjalankan backfill besar dalam transaksi yang mengganggu availability; batch, ukur dampak, dan sediakan progress/resume.
- Perubahan data produksi MUST dilakukan melalui jalur perubahan resmi dan audit. Dilarang memakai seeder, fixture, truncate, reset, atau rollback aplikasi yang menghapus data di production.
- Uji migration terhadap volume dan versi aplikasi yang realistis memakai data sintetis/anonim, lalu pastikan rollback/forward-fix dan deployment order.
- Setelah migration, verifikasi data dan metrik layanan; hentikan rollout bila integritas atau error rate melewati batas.

Jika perubahan tidak dapat dibalik secara teknis, dokumentasikan compensating action atau restore procedure dan minta persetujuan data owner sebelum pelaksanaan.

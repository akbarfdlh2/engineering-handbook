# Data Retention Schedule Template

Lengkapi tabel ini per proyek untuk melengkapi [data protection dan privacy](data-protection-and-privacy.md). Jadwal retensi MUST konsisten dengan kewajiban hukum/kontrak; saat ragu, minta review pemilik legal/privacy sebelum menetapkan periode.

| Kategori data | Contoh | Klasifikasi | Dasar retensi (hukum/kontrak/bisnis) | Periode retensi | Sistem/lokasi penyimpanan | Metode penghapusan | Owner |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [contoh: log autentikasi] | [deskripsi] | [Public/Internal/Confidential/Restricted] | [dasar] | [durasi] | [sistem] | [hard delete/anonymize/crypto-shred] | [nama/role] |

## Prinsip

- Setiap kategori data produksi MUST memiliki baris pada jadwal ini sebelum dikumpulkan; jangan menyimpan data tanpa periode retensi yang ditetapkan.
- Penghapusan MUST mencakup salinan pada backup, replica, search index, cache, log, dan export sesuai jadwal yang sama atau lebih ketat.
- Pengecualian perpanjangan retensi (litigation hold, investigasi) dicatat dengan alasan, owner, dan tanggal pencabutan.
- Tinjau jadwal saat regulasi/kontrak berubah dan sekurangnya tahunan untuk data Confidential/Restricted.

Rujukan: prinsip minimisasi dan storage limitation pada regulasi privasi yang berlaku, mis. [GDPR Article 5(1)(e)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32016R0679); pemetaan kewajiban spesifik dilakukan pemilik legal/privacy proyek.

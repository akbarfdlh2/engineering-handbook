# Third-Party dan Service Provider

- Sebelum data, credential, atau jalur produksi dibagikan kepada vendor, tetapkan business owner, data owner, tujuan, data class, akses, lokasi pemrosesan, dan tier dampaknya.
- Vendor Tier 1/2 MUST dinilai sebelum digunakan berdasarkan keamanan, privacy, subprocessor, lokasi data, akses operasional, incident notification, continuity, dan exit plan. Gunakan [vendor due diligence questionnaire](vendor-due-diligence-questionnaire.md) untuk mencatat penilaian ini.
- Kontrak MUST mencakup kewajiban keamanan/privasi yang sesuai, kerahasiaan, notifikasi insiden, penghapusan/pengembalian data, hak audit/evidence bila diperlukan, dan tanggung jawab subprocessor.
- Berikan akses minimum, unik, tercatat, dan terbatas waktu; tinjau berkala dan cabut saat layanan/kontrak berakhir.
- Integrasi menggunakan scope minimum, secret khusus per environment, rate limit, monitoring, timeout, dan fallback behavior yang aman.
- Tinjau ulang vendor saat lingkup, kepemilikan, subprocessor, lokasi data, atau insiden berubah; critical service memiliki alternatif atau continuity plan yang terdokumentasi.
- Sebelum keluar dari layanan, rotasi/revoke credentials, cabut akses, ekspor data yang sah, minta penghapusan tertulis bila diwajibkan, dan arsipkan bukti yang diperlukan.

Jangan mengunggah data Confidential/Restricted ke AI, analytics, support, atau layanan pihak ketiga sampai data handling dan persetujuannya diverifikasi organisasi.

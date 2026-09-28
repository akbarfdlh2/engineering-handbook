# Data Protection dan Privacy

## Klasifikasi data

Gunakan kelas paling tinggi yang sesuai dengan konten dan dampaknya. Proyek boleh menambah subkelas, tetapi tidak boleh mengurangi kontrol baseline tanpa persetujuan pemilik risiko.

| Kelas | Contoh | Penanganan minimum |
| --- | --- | --- |
| Public | Informasi yang telah disetujui untuk publikasi | Jaga integritas dan persetujuan publikasi; jangan memasukkan secret. |
| Internal | Dokumentasi/proses non-publik berdampak rendah | Akses untuk anggota yang berwenang; jangan unggah ke repo atau layanan publik tanpa persetujuan. |
| Confidential | Data pelanggan/karyawan, data bisnis non-publik, identifier personal | Need-to-know, enkripsi saat transit/tersimpan, audit akses, retensi terbatas; gunakan data sintetis untuk development. |
| Restricted | Credential/secret, data finansial/ kesehatan/identitas sensitif, data dengan dampak tinggi atau kewajiban khusus | Owner dan approval eksplisit, akses sangat terbatas dan diaudit, enkripsi dengan key controls, minimisasi, isolasi lingkungan; jangan kirim ke layanan AI/pihak ketiga yang belum disetujui. |

Credential dan secret tidak boleh disimpan sebagai dokumentasi biasa meskipun diberi label Restricted; gunakan secret manager.

- Setiap data MUST memiliki owner, tujuan, klasifikasi, aturan akses, retensi, dan prosedur penghapusan.
- Kumpulkan data pribadi seminimal mungkin dan hanya untuk tujuan yang dijelaskan; hindari mengumpulkan data sensitif bila fitur dapat berjalan tanpanya.
- Data sensitif MUST dienkripsi saat transit dan tersimpan menggunakan mekanisme yang dikelola baik. Kunci disimpan terpisah dari data, diberi akses minimum, dan memiliki rotasi/revocation plan.
- Authorization MUST ditegakkan di server untuk setiap record/resource, termasuk isolasi tenant; jangan percaya ID resource atau role dari client.
- Akses ke data produksi dibatasi, diaudit, dan tidak diberikan untuk kenyamanan development. Masking/anonymization dipakai untuk analitik dan QA bila memungkinkan.
- Log, crash report, trace, analytics, dan backup harus mengikuti klasifikasi data yang sama; redaksi/retensi ditetapkan sebelum produksi.
- Retensi dan penghapusan harus berlaku juga pada search index, export, cache, replica, dan backup sesuai jadwal dan kewajiban hukum/kontrak.
- Perubahan aliran data ke pihak ketiga MUST mencatat data yang dibagi, tujuan, lokasi pemrosesan, kontrol kontraktual, dan cara menghentikan akses.
- Data uji publik MUST sintetis. Data produksi hanya boleh dipakai untuk tujuan sah dengan izin, minimisasi, kontrol akses, dan audit yang terdokumentasi.

Pemetaan terhadap aturan privasi lokal, kontrak pelanggan, atau standar industri harus dilakukan oleh pemilik legal/privacy; dokumen ini sendiri bukan bukti kepatuhan.

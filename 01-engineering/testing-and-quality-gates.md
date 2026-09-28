# Testing dan Quality Gates

- Setiap perubahan MUST memiliki verifikasi sepadan dengan risiko; laporan menyebut pemeriksaan yang dijalankan dan yang belum.
- Perubahan aturan bisnis MUST memiliki tes otomatis pada lapisan yang tepat. Perubahan security MUST memiliki tes negatif untuk memastikan akses yang dilarang memang ditolak.
- CI MUST menjalankan build, lint/static analysis, tes relevan, dan pemeriksaan secret/dependency sesuai stack proyek.
- Branch utama MUST terlindungi dari merge bila quality gate wajib gagal; bypass hanya melalui jalur emergency yang diaudit.
- CI MUST menghasilkan status pemeriksaan yang dapat ditelusuri ke commit; branch protection MUST menolak stale approval setelah perubahan baru pada file yang ditinjau.
- Flaky test MUST dicatat dengan owner dan tenggat perbaikan; menonaktifkan test wajib memerlukan alasan, mitigasi sementara, dan approval reviewer.
- Tes integrasi MUST memakai lingkungan dan data terisolasi. Tes MUST NOT membaca atau mengubah data produksi.
- Coverage adalah indikator; review harus menilai skenario kritis, batas, kegagalan, authorization, dan regresi, bukan mengejar angka coverage semata.
- Perubahan UI SHOULD diverifikasi di ukuran layar dan keadaan interaksi utama, termasuk keyboard dan error state.
- Kegagalan lingkungan dilaporkan sebagai belum terverifikasi, bukan lulus.

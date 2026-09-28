# Tata Kelola Handbook

Lihat [rujukan dan assurance](references-and-assurance.md) untuk sumber primer, versi yang ditinjau, dan batas klaim handbook.

Gunakan [control register](control-register.md) sebagai indeks traceability ke dokumen kanonis; catat bukti dan status pada repo masing-masing proyek.

Template governance tambahan: [risk register](risk-register-template.md), [control mapping ke ISO 27001/SOC 2](control-mapping-template.md), dan [model risk management](model-risk-management-template.md) untuk proyek yang memakai model statistik/ML/AI dalam keputusan bisnis.

## Cara menggunakan

1. Tentukan klasifikasi data dan dampak layanan untuk tiap proyek.
2. Terapkan kontrol MUST sebagai baseline; pilih kontrol tambahan menurut risiko.
3. Catat versi handbook yang dipakai di repo proyek.
4. Dokumentasikan pengecualian dengan pemilik, risiko, mitigasi, persetujuan, dan tanggal tinjau.
5. Tinjau dokumen saat ada perubahan regulasi, ancaman, arsitektur, atau insiden dan setidaknya setahun sekali.

## Tingkat risiko

- **Tier 1 — kritis/teregulasi**: data sangat sensitif, transaksi berdampak besar, atau layanan yang berdampak pada keselamatan/operasi penting. Wajib threat model, security review independen, uji pemulihan, dan kontrol tambahan yang disetujui security owner.
- **Tier 2 — sensitif/operasional**: data pribadi atau internal penting, akses lintas organisasi, atau layanan inti. Wajib kontrol baseline, threat model proporsional, review dependency dan akses.
- **Tier 3 — umum/internal rendah**: dampak terbatas dan data non-sensitif. Tetap wajib baseline; sederhanakan dokumentasi dan proses sesuai dampak.

Klasifikasi harus mempertimbangkan dampak confidentiality, integrity, availability, privasi, dan kewajiban kontrak/hukum. Jika ragu, gunakan tier lebih tinggi sampai pemilik risiko menilai.

## Minimum per tier

| Kontrol | Semua tier | Tambahan Tier 2 | Tambahan Tier 1 |
| --- | --- | --- | --- |
| Ownership, klasifikasi data, MFA, access control, protected branches, CI, backup, logging | Wajib sebelum production | Review akses dan dependency terdokumentasi | Owner risiko dan security reviewer independen ditetapkan |
| Threat model | Untuk perubahan yang menambah trust boundary, data sensitif, login, atau privilege | Sebelum fitur material dan perubahan arsitektur | Sebelum rilis pertama dan setiap perubahan material |
| Uji security | SAST/dependency/secret scan di CI sesuai stack | Review keamanan sebelum rilis material | Security assessment independen sebelum production dan berkala sesuai exposure |
| Recovery | RTO/RPO ditentukan dan restore diuji | Restore test sekurangnya tahunan | Restore test sekurangnya triwulanan dan incident tabletop sekurangnya tahunan |
| Approval rilis | Engineering owner | Engineering owner dan reviewer security untuk perubahan sensitif | Product/business risk owner, engineering owner, dan security owner |

Tier yang lebih tinggi mewarisi semua kontrol tier di bawahnya. Produk dapat menerapkan kontrol lebih ketat; pelonggaran memerlukan pengecualian yang tercatat.

## Peran minimum

Setiap production service MUST menunjuk nama/kelompok yang bertanggung jawab, walau satu orang memegang beberapa peran:

- **Product/business owner**: tujuan, dampak pengguna, tier, dan penerimaan risiko bisnis.
- **Engineering owner**: arsitektur, kualitas perubahan, deployment, dan pemulihan.
- **Security owner**: interpretasi kontrol, review security, insiden, dan persetujuan pengecualian security.
- **Data/privacy owner**: klasifikasi, tujuan, akses, retensi, dan penghapusan data.
- **Design/accessibility owner**: design system dan aksesibilitas pada produk yang memiliki antarmuka.

Orang yang membuat perubahan MUST NOT menjadi satu-satunya pemberi persetujuan atas risiko yang ditimbulkan perubahan tersebut.

## Pengecualian

Catat setiap pengecualian di `docs/engineering/standards.md` menggunakan [template pengecualian](exception-template.md): kontrol, alasan, risiko residual, mitigasi, pihak yang menyetujui, tanggal kedaluwarsa, dan rencana menutup pengecualian. Baseline masa pengecualian maksimal 90 hari; tanggal yang lebih pendek dapat ditetapkan berdasarkan risiko. Perpanjangan memerlukan penilaian dan approval baru, tidak otomatis. Pengecualian tidak boleh meniadakan kewajiban hukum atau kontrak. Pengecualian untuk risiko kritis yang sedang dieksploitasi tidak boleh dipakai untuk menunda containment.

## Perubahan standar

Perubahan MUST menyebut dampak ke proyek yang sudah mengadopsi handbook dan panduan migrasi bila breaking. Gunakan pull request, review minimal satu pemilik engineering; perubahan security ditinjau pemilik security. Tandai versi stabil dengan tag `vMAJOR.MINOR.PATCH`: MAJOR untuk perubahan wajib yang tidak kompatibel atau memerlukan migrasi; MINOR untuk panduan/kontrol tambahan yang tidak mengubah baseline wajib yang sudah dipin; PATCH untuk koreksi editorial atau klarifikasi yang tidak mengubah hasil kontrol.

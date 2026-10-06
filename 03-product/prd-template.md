# PRD: [Nama produk/fitur]

Isi bagian yang relevan; untuk Tier 3 ringkas, tapi jangan menghapus bagian: tulis "tidak berlaku" beserta alasan. Sebelum status Approved, PRD harus lolos [Definition of Ready](prd-readiness-checklist.md).

## Metadata

- Status: Draft / Review / Approved / Released / Deprecated
- Versi PRD dan riwayat perubahan:
- Product owner:
- Engineering owner:
- Security/privacy reviewer:
- Design/accessibility owner:
- Tier risiko (1/2/3) dan alasan:
- Jenis perubahan (standar / normal / darurat):
- Terakhir diperbarui:

## Ringkasan dan masalah

- Ringkasan solusi:
- Pengguna terdampak dan kebutuhan:
- Bukti masalah / sumber data (sebutkan sumber dan tanggal, bedakan fakta dari asumsi):
- Dampak bila tidak ditangani:
- Alternatif yang dipertimbangkan, termasuk "tidak membangun":

## Konteks strategis

- Tujuan bisnis/organisasi yang didukung:
- Keterkaitan dengan produk, roadmap, dan PRD lain:
- Pemangku kepentingan dan cara konsultasi:

## Pengguna dan skenario

| Persona/peran | Tujuan (job to be done) | Konteks dan kendala | Frekuensi/kritikalitas |
| --- | --- | --- | --- |
| [peran] | [tujuan] | [kendala] | [nilai] |

### User stories dan skenario penyalahgunaan

- Sebagai [peran], saya ingin [kemampuan] agar [hasil].
- Skenario penyalahgunaan (abuse case): sebagai [pihak jahat/ceroboh], saya dapat [aksi], dicegah oleh [kontrol].

## Hasil dan metrik

| Hasil yang diinginkan | Metrik | Baseline | Target dan waktu | Sumber data dan owner |
| --- | --- | --- | --- | --- |
| [hasil] | [metrik] | [nilai] | [target] | [sumber] |

- Guardrail metrics (metrik yang tidak boleh memburuk, mis. error rate, support load, keluhan):
- Cara dan jendela evaluasi pasca-rilis:

## Ruang lingkup

### In scope

- [kapabilitas]

### Out of scope

- [yang sengaja tidak dikerjakan, dengan alasan]

### Asumsi, kendala, dan dependency

- Asumsi (dan cara memvalidasinya):
- Kendala (hukum, kontrak, teknis, anggaran, tenggat):
- Dependency tim/sistem/vendor dan statusnya:

## Kebutuhan dan acceptance criteria

| ID | Kebutuhan | Prioritas | Acceptance criteria | Tes/verifikasi | Kontrol terkait |
| --- | --- | --- | --- | --- | --- |
| FR-01 | [kebutuhan] | Must / Should / Could | Given [konteks], when [aksi], then [hasil] | [tes otomatis/manual/review] | [mis. IAM-06] |

- Setiap kebutuhan Must memiliki acceptance criteria yang dapat diverifikasi dan sedikitnya satu skenario kegagalan atau penolakan.
- Gunakan ID stabil; PR dan tes menautkan ID ini (lihat keterlacakan di [SDLC](../01-engineering/sdlc.md#keterlacakan)).

## Pengalaman pengguna

- Alur utama dan alternatif:
- Loading, empty, success, error, dan recovery states:
- Perangkat, bahasa, dan aksesibilitas:
- Konten/teks yang sensitif (pesan error, notifikasi, email):
- Tautan desain / design system:

## Data dan integrasi

- Entitas data baru/berubah, sumber kebenaran, dan siklus hidupnya:
- Integrasi internal/eksternal, kontrak API, dan perubahan yang tidak kompatibel:
- Migrasi data dan backfill:
- Analitik dan event yang dikumpulkan (tujuan, minimisasi, consent):

## Security, privacy, dan compliance

- Data yang dibuat/dibaca/diubah/dihapus dan klasifikasinya:
- Aktor, authentication, authorization, tenant boundary:
- Threats/abuse cases dan mitigasi (tautan [threat model](../02-security/threat-model-template.md) bila dipersyaratkan tier):
- Retensi, consent, audit, dan pihak ketiga:
- Kewajiban kontrak/regulasi yang sudah divalidasi (oleh siapa, kapan):
- Persyaratan verifikasi keamanan yang dipilih (mis. level dan requirement ASVS yang diadopsi):

## Komponen AI/model (jika ada)

- Apakah model ML/LLM memengaruhi keputusan terhadap pengguna atau pelanggan? Jika ya, isi [model risk management](../00-governance/model-risk-management-template.md).
- Perilaku yang diharapkan, batas, dan perilaku saat model gagal atau tidak yakin:
- [Guardrails](../01-engineering/guardrails.md) yang dipasang (input/output, agency, human review):
- Evaluasi kualitas, bias, dan monitoring drift:
- Data pelanggan yang dikirim ke penyedia model dan dasar persetujuannya:

## Kebutuhan nonfungsional

- Availability/performance/capacity (nyatakan sebagai skenario terukur dengan alasan, bukan angka tanpa dasar):
- Accessibility target:
- Compatibility:
- Observability/support:
- Backup, RTO/RPO, dan recovery:
- Biaya operasi yang diharapkan dan batasnya:
- Implikasi arsitektur dan tautan [rekomendasi arsitektur](../04-architecture/architecture-selection-guide.md):

## Rilis dan pengukuran

- Dependencies dan asumsi:
- Rollout / feature flag (default aman, kill switch):
- Rollback dan data migration:
- Komunikasi, dokumentasi, pelatihan support:
- Metrik setelah rilis dan kapan ditinjau:
- Kriteria penghentian atau rollback berdasarkan metrik:

## Risiko

| Risiko | Dampak/probabilitas | Mitigasi | Owner | Tautan risk register |
| --- | --- | --- | --- | --- |
| [risiko] | [kualitatif] | [mitigasi] | [nama] | [tautan] |

## Keterlacakan

| Kebutuhan | Spesifikasi/ADR | Tes | PR/rilis | Metrik pasca-rilis |
| --- | --- | --- | --- | --- |
| FR-01 | [tautan] | [tautan] | [tautan] | [tautan] |

## Persetujuan dan pertanyaan terbuka

- Persetujuan product:
- Persetujuan engineering/security/privacy sesuai risiko:
- Keputusan [JEV](../01-engineering/decision-layer-jev.md) untuk persetujuan (kelas, verifier, tanggal):
- [Pertanyaan, pemilik, tenggat]

## Glosarium

- [istilah]: [definisi]

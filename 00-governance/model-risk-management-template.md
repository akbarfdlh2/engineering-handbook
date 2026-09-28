# Model Risk Management Template

Gunakan dokumen ini untuk model kuantitatif/ML/AI yang menjadi bagian dari keputusan bisnis (credit scoring, underwriting, fraud detection, pricing, collections, AML/transaction monitoring, atau keputusan otomatis lain yang berdampak pada pelanggan). Ini berbeda dari [AI-assisted development](../01-engineering/ai-assisted-development.md), yang mengatur penggunaan coding agent untuk menulis kode, bukan model yang menjadi bagian dari keputusan produk.

Panduan rujukan pada dokumen ini awalnya ditulis untuk bank besar; proyek non-bank dapat memakainya sebagai baseline rigor tanpa mengklaim kewajiban regulasi otomatis berlaku pada mereka.

## Kapan berlaku

- Proyek MUST mengisi dokumen ini bila memakai model statistik/ML/AI generatif untuk membuat atau merekomendasikan keputusan yang memengaruhi pelanggan, risiko keuangan, kepatuhan, atau keselamatan.
- Materialitas model (dampak, kompleksitas, tingkat otomasi keputusan) menentukan kedalaman validasi dan frekuensi review; model berdampak tinggi memakai kontrol setara Tier 1 pada [tata kelola handbook](README.md#tingkat-risiko).

## Inventori model

| ID model | Tujuan/keputusan yang didukung | Tipe (statistik/ML/LLM/aturan) | Data input dan sumber | Tier materialitas | Owner bisnis | Owner teknis | Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [MODEL-001] | [deskripsi] | [tipe] | [sumber data] | [Tier 1/2/3] | [nama] | [nama] | [development/validated/production/retired] |

## Pengembangan dan dokumentasi

- Asumsi, batasan, populasi data latih/target, dan variabel yang dipakai MUST didokumentasikan sebelum model dipakai untuk keputusan produksi.
- Bias, fairness, dan dampak terhadap kelompok pelanggan yang dilindungi MUST dievaluasi untuk model yang memengaruhi keputusan terhadap individu.
- Model generatif MUST didokumentasikan batasan output, risiko halusinasi, dan guardrail yang dipasang (filtering, human review, disclaimer).

## Validasi independen

- Model Tier 1/2 MUST divalidasi oleh pihak yang independen dari pengembang model, mencakup conceptual soundness, kualitas data, kinerja out-of-sample, dan sensitivity/stress testing.
- Validasi ulang berkala MUST dilakukan sekurangnya tahunan untuk Tier 1, dan setiap kali ada perubahan material pada data, fitur, atau tujuan penggunaan.
- Hasil validasi, temuan, dan status remediasi dicatat serta ditautkan ke [risk register](risk-register-template.md) bila ditemukan risiko signifikan.

## Persetujuan dan penggunaan

- Model Tier 1/2 MUST mendapat persetujuan eksplisit dari model owner bisnis dan risk/validation owner sebelum dipakai untuk keputusan produksi.
- Penggunaan model di luar tujuan yang divalidasi (drift dalam use-case) MUST NOT terjadi tanpa validasi ulang.
- Override keputusan model oleh manusia MUST dicatat dengan alasan untuk audit dan continuous monitoring.

## Monitoring berkelanjutan

- Pantau drift performa, distribusi input, dan outcome yang tidak diinginkan; tetapkan ambang yang memicu review ulang atau penonaktifan model.
- Insiden model (keputusan salah berdampak signifikan, bias yang ditemukan, kegagalan sistemik) mengikuti [logging/incident response](../02-security/logging-monitoring-and-incidents.md) dan [post-incident review](../06-operations/post-incident-review-template.md).

## Retirement

Model yang dipensiunkan MUST didokumentasikan alasan, tanggal berhenti dipakai, dan rencana migrasi ke model/proses pengganti.

Rujukan: [SR 26-2, Revised Guidance on Model Risk Management (Federal Reserve, OCC, dan FDIC, 17 April 2026 — menggantikan SR 11-7 tahun 2011 dan SR 21-8)](https://www.federalreserve.gov/supervisionreg/srletters/SR2602.htm) dan [NIST AI Risk Management Framework 1.0](https://www.nist.gov/itl/ai-risk-management-framework).

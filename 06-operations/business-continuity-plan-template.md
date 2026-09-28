# Business Continuity Plan Template

Dokumen ini mencakup kelangsungan bisnis tingkat organisasi/fungsi bisnis, melengkapi [reliability, backup, dan recovery](reliability-backup-and-recovery.md) yang fokus pada RTO/RPO teknis per layanan. BCP menjawab: jika fungsi bisnis penting terganggu (bukan hanya satu service), bagaimana organisasi tetap berjalan?

## Business Impact Analysis (BIA)

| Fungsi bisnis kritis | Dampak bila terganggu (finansial/reputasi/legal/pelanggan) | Maximum tolerable downtime | RTO | RPO | Dependency (sistem/vendor/orang) |
| --- | --- | --- | --- | --- | --- |
| [contoh: pemrosesan pembayaran] | [deskripsi dampak] | [durasi] | [durasi] | [durasi] | [daftar] |

## Strategi kontinuitas

- Setiap fungsi kritis MUST memiliki strategi pemulihan (alternate site/proses manual/failover) yang proporsional terhadap maximum tolerable downtime-nya.
- Dependency vendor kritis mengikuti [third-party risk](../02-security/third-party-risk.md) dan memiliki continuity/exit plan.
- Personil kunci MUST memiliki backup/successor yang terlatih untuk peran yang menjadi single point of failure.

## Tim krisis dan komunikasi

- Crisis management team: peran, nama, kontak, deputi.
- Jalur eskalasi dan kriteria aktivasi BCP.
- Rencana komunikasi internal (karyawan), eksternal (pelanggan/regulator/media), dan kanal cadangan bila sistem komunikasi utama down.

## Pengujian dan pemeliharaan

- Tier 1 MUST menjalani tabletop exercise BCP sekurangnya tahunan dan setelah perubahan struktur bisnis material.
- Hasil pengujian, gap, dan tindak lanjut dicatat serta ditautkan ke [risk register](../00-governance/risk-register-template.md).
- Plan ditinjau ulang minimal tahunan, dan segera setelah insiden nyata mengaktifkan BCP.

## Aktivasi dan pemulihan

- Kriteria deklarasi insiden yang memerlukan aktivasi BCP (berbeda dari incident response teknis biasa):
- Prosedur declare/stand-down dan siapa yang berwenang:
- Return-to-normal criteria:

Rujukan: [ISO 22301:2019, Business continuity management systems — Requirements](https://www.iso.org/standard/75106.html) dan [NIST SP 800-34 Rev. 1, Contingency Planning Guide for Federal Information Systems](https://csrc.nist.gov/pubs/sp/800/34/r1/upd1/final).

# Technical Debt Register Template

Gunakan template ini di repo atau sistem pelacak proyek untuk mencatat technical debt secara eksplisit. Debt yang tidak tercatat tidak dapat dikelola. Cara menemukan debt: [deteksi vulnerability, bug, dan debt](../01-engineering/defect-and-debt-detection.md).

## Aturan

- Debt MUST punya owner, dampak (bunga), usaha perkiraan (pokok), dan tanggal tinjau.
- Debt yang berdampak pada keamanan, integritas data, atau pemulihan bukan debt biasa: catat di [risk register](risk-register-template.md) dan/atau alur [vulnerability management](../02-security/vulnerability-management.md).
- Keputusan **menerima** debt melebihi satu siklus tinjau memerlukan persetujuan engineering owner, tanggal kedaluwarsa, dan pemicu pelunasan. Jika melanggar kontrol MUST, gunakan [pengecualian](exception-template.md).
- Debt sadar yang diambil demi tenggat dicatat saat dibuat, bukan setelah menjadi masalah.
- Tinjau register sekurangnya tiap perencanaan rilis mayor dan setelah insiden yang berkaitan; hapus item yang sudah tidak relevan.

## Kategori

Kode, arsitektur, tes, dependency/platform, infrastruktur/konfigurasi, dokumentasi/pengetahuan, data/skema, proses/tooling, dan keamanan/privasi.

## Kuadran asal

Catat apakah debt **sadar atau tidak sadar** dan **bijak (prudent) atau ceroboh (reckless)**. Debt ceroboh dan tidak sadar menunjukkan celah proses (review, standar, onboarding) yang perlu diperbaiki, bukan hanya kodenya.

## Register

| ID | Judul | Kategori | Asal (sadar/tidak, bijak/ceroboh) | Lokasi/komponen | Bunga (dampak berkelanjutan) | Pokok (usaha perkiraan) | Pemicu pelunasan | Keputusan (lunasi/pantau/terima) | Owner | Tinjau berikutnya | Tautan (PR/ADR/risk/tiket) | Status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DEBT-001 | [judul] | [kategori] | [asal] | [lokasi] | [dampak] | [S/M/L atau perkiraan] | [kondisi atau tanggal] | [keputusan] | [nama] | [tanggal] | [tautan] | Open / Scheduled / Accepted / Repaid |

## Penilaian prioritas

Nilai kualitatif, bukan satu skor angka yang menyembunyikan penalaran:

- **Bunga**: seberapa sering dan seberapa besar biaya dibayar (lambat berubah, insiden, workaround, risiko).
- **Pokok**: usaha dan risiko pelunasan, termasuk kebutuhan migrasi dan rollback.
- **Pemicu**: fitur mendatang, rilis mayor, end-of-life dependency, kewajiban kepatuhan, atau ambang insiden.
- Prioritaskan debt dengan bunga tinggi dan pokok rendah, atau yang menghalangi pekerjaan prioritas; jadwalkan alokasi kapasitas tetap yang disepakati owner agar pelunasan tidak selalu kalah dari fitur.

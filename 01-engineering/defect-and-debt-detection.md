# Deteksi Vulnerability, Bug, dan Technical Debt

Dokumen ini menetapkan cara menemukan, menilai, dan mencatat **vulnerability, bug, dan technical debt yang masuk akal (plausible)** pada kode, konfigurasi, dependency, dan arsitektur. Penanganan vulnerability yang sudah divalidasi (severity, SLA, retest) tetap mengikuti [vulnerability management](../02-security/vulnerability-management.md); dokumen ini mengatur tahap sebelum dan di sekitarnya.

## Tingkat bukti temuan

Setiap temuan MUST diberi tingkat bukti. Temuan plausible tidak boleh dibuang diam-diam dan tidak boleh dilaporkan sebagai terkonfirmasi.

| Tingkat | Arti | Syarat minimum |
| --- | --- | --- |
| Confirmed | Direproduksi atau dibuktikan (tes gagal, exploit aman di lingkungan uji, bukti runtime) | Langkah reproduksi atau bukti, versi/commit |
| Plausible | Jalur kode atau konfigurasi menunjukkan masalah, belum direproduksi | Lokasi (`file:line` atau resource), jalur pemicu, asumsi yang belum diverifikasi |
| Unverified | Klaim scanner, hipotesis, atau laporan pihak lain tanpa pemeriksaan | Sumber klaim dan alasan belum diperiksa |
| Dismissed | False positive atau tidak terjangkau | Alasan, pemeriksa, tanggal; ditinjau ulang bila kode terkait berubah |

Temuan dari agent atau scanner dimulai sebagai Unverified atau Plausible sampai diperiksa. Triase dilakukan lewat [JEV](decision-layer-jev.md): Judge (dampak dan reversibilitas), Evaluate (bukti dan keterjangkauan), Verify (reproduksi independen).

## Alur

1. **Detect**: sumber otomatis dan manual di bawah.
2. **Triage**: tetapkan tingkat bukti, kelas (vulnerability/bug/debt), keterjangkauan, dan dampak.
3. **Record**: catat di sistem pelacak internal; vulnerability di register temuan, risiko material ke [risk register](../00-governance/risk-register-template.md), debt ke [debt register](../00-governance/technical-debt-register-template.md).
4. **Treat**: perbaiki, mitigasi, terima dengan [pengecualian](../00-governance/exception-template.md), atau jadwalkan.
5. **Verify**: retest membuktikan akar masalah tertutup dan tidak ada regresi; penutup temuan bukan orang yang memperbaikinya untuk kelas D2 ke atas.

## Sumber deteksi

| Sumber | Menemukan | Titik | Catatan |
| --- | --- | --- | --- |
| Secret scanning | Kredensial di kode/riwayat | Pre-commit, CI, terjadwal | Secret yang bocor dianggap terkompromi; rotasi, bukan hanya hapus |
| SCA/dependency scan | Dependency rentan, lisensi, abandonware | CI, terjadwal | Nilai keterjangkauan, bukan hanya keberadaan CVE |
| SAST | Pola kode berbahaya, bug kelas tertentu | CI | Validasi; atur aturan agar sinyal tidak tenggelam |
| IaC/container scan | Misconfiguration infra dan image | CI, terjadwal | Termasuk base image dan permission berlebih |
| DAST/fuzzing | Perilaku runtime, input tak terduga | Staging, terjadwal | Jangan pada data produksi |
| Tes otomatis | Regresi dan bug fungsional | CI | Termasuk tes negatif authz dan tenant isolation |
| Code review | Logika, authz, failure mode | PR | Gunakan [checklist code review](../07-adoption/code-review-checklist.md) |
| Threat modeling | Ancaman desain | Fase arsitektur | [Template](../02-security/threat-model-template.md) |
| Observability | Anomali, error, kebocoran data di log | Runtime | [Logging dan insiden](../02-security/logging-monitoring-and-incidents.md) |
| Metrik kesehatan kode | Hotspot debt: churn tinggi, kompleksitas, duplikasi, tes lemah | Terjadwal | Indikator, bukan target; jangan dioptimalkan sebagai angka |
| Pelaporan eksternal | Laporan peneliti/pelanggan | [SECURITY.md](../SECURITY.md) | Triase aman; jangan minta data pelanggan |
| Assessment independen | Celah yang tidak terlihat tool | Sesuai tier | Wajib untuk Tier 1 internet-facing |

## Heuristik deteksi plausible

Gunakan sebagai prompt untuk reviewer, scanner kustom, dan agent. Satu kecocokan = hipotesis, bukan temuan; buktikan jalur dari input tak tepercaya sampai dampak.

### Vulnerability

- **Otorisasi**: akses objek tanpa pemeriksaan kepemilikan (IDOR/BOLA), fungsi admin tanpa cek peran di server, filter tenant hilang pada satu query, mass assignment pada field privilese.
- **Injeksi**: string yang dirangkai ke query/perintah/template/path, deserialisasi data tak tepercaya, SSRF melalui URL dari pengguna, path traversal, open redirect.
- **Autentikasi/sesi**: token tidak kedaluwarsa atau tidak dicabut, recovery lebih lemah dari login, perbandingan rahasia tidak konstan.
- **Kripto/secrets**: algoritma buatan sendiri, nonce/IV dipakai ulang, kunci hardcoded, randomness non-kriptografis untuk token.
- **Race/TOCTOU**: cek lalu pakai tanpa atomisitas (saldo, kuota, voucher), operasi non-idempotent yang di-retry.
- **Konfigurasi**: default tidak aman, debug aktif, CORS/permission terlalu longgar, bucket/endpoint publik, CI workflow yang mengeksekusi input tak tepercaya.
- **Supply chain**: nama paket mirip atau hasil halusinasi, dependency tanpa lockfile, skrip instalasi tak ditinjau.
- **Kebocoran data**: data sensitif di log, error, URL, atau respons berlebih.
- **Fitur LLM**: prompt injection tidak langsung, output model dieksekusi/dirender tanpa validasi, tool dengan agency berlebih, kebocoran system prompt atau data.

### Bug

- Kondisi batas (kosong, null, satu elemen, off-by-one), zona waktu dan DST, pembulatan dan float untuk uang.
- Error ditelan, retry tanpa batas, timeout tidak ada, resource tidak dilepas.
- Kegagalan parsial: transaksi tidak atomik, efek samping ganda, urutan event tidak dijamin.
- Konkurensi: data race, deadlock, state bersama tanpa sinkronisasi.
- Kompatibilitas: migrasi yang tidak kompatibel dengan versi lama saat rollout, perubahan kontrak API tanpa versi.
- Ketidaksesuaian dokumentasi/kontrak dengan perilaku sebenarnya.

### Technical debt

- Duplikasi aturan bisnis, validasi/permission yang berbeda antar lapisan, kode mati.
- Dependency usang atau tak terpelihara, versi tidak terkunci, upgrade tertunda lintas mayor.
- Tes lemah atau flaky, area kritis tanpa tes, build lambat atau tidak reprodusibel.
- Modul dengan churn dan kompleksitas tinggi, abstraksi bocor, siklus dependency, ownership tidak jelas.
- Konfigurasi manual (drift), runbook usang, dokumentasi tak sesuai, workaround tanpa tenggat.
- Pintasan sadar yang diambil demi tenggat tanpa catatan pelunasan.

## Prioritas

- **Vulnerability** yang divalidasi: ikuti [vulnerability management](../02-security/vulnerability-management.md); exploitability, exposure, dan dampak data menentukan prioritas.
- **Bug**: prioritas menurut dampak pengguna/data, frekuensi, ketersediaan workaround, dan tier. Bug yang merusak integritas data, uang, atau akses diperlakukan setara risiko security.
- **Debt**: nilai berdasarkan *bunga* (biaya berkelanjutan: lambatnya perubahan, insiden, risiko) dan *pokok* (usaha pelunasan). Debt yang berdampak pada keamanan, integritas data, atau pemulihan MUST dialihkan ke jalur vulnerability/risk, bukan dibiarkan di backlog debt.

## Kewajiban

- Pipeline CI MUST menjalankan deteksi minimum sesuai [testing dan quality gates](testing-and-quality-gates.md) dan [secure development](../02-security/secure-development.md); hasil dikaitkan ke commit.
- Tier 1 MUST menambahkan deteksi terjadwal di luar PR (dependency, image, konfigurasi) dan assessment independen sesuai [secure development](../02-security/secure-development.md). Tier 2/3 menyesuaikan cakupan dan frekuensi dengan risiko; catat alasannya.
- Temuan MUST punya owner, tingkat bukti, dan status. Temuan tanpa owner tidak dihitung ditangani.
- Debt MUST tercatat di debt register dan ditinjau berkala oleh engineering owner; debt yang diterima punya tanggal tinjau dan, bila relevan, kedaluwarsa.
- Debt baru yang diambil sadar demi tenggat MUST dicatat pada PR atau ADR beserta rencana pelunasan.
- Hasil triase false positive MUST dipakai untuk menyetel aturan agar sinyal tetap bermakna.

## Temuan oleh AI

Agent dan scanner AI boleh dipakai untuk mencari kandidat, dengan aturan tambahan:

- Setiap kandidat menyebut lokasi tepat, jalur pemicu, dan apa yang belum diverifikasi; klaim tanpa bukti kode bukan temuan.
- Verifikasi independen sebelum menyebut Confirmed. Agent yang sama tidak memverifikasi temuannya sendiri.
- Jangan menulis exploit yang bekerja atau detail kerentanan yang belum diperbaiki di repo publik, isu publik, atau tool eksternal yang tidak disetujui; gunakan kanal privat.
- Jangan menjalankan pengujian aktif pada sistem di luar scope yang diizinkan.
- Laporkan juga area yang tidak sempat diperiksa agar tidak ada rasa aman palsu.

## Template catatan temuan

```markdown
## FND-NNN: [judul singkat]
- Kelas: vulnerability / bug / debt
- Tingkat bukti: Confirmed / Plausible / Unverified / Dismissed
- Lokasi (`file:line`, resource, versi/commit):
- Jalur pemicu dan prasyarat:
- Dampak (data, uang, akses, ketersediaan, kecepatan perubahan):
- Keterjangkauan dan exposure:
- Prioritas dan alasan:
- Owner, status, target:
- Langkah reproduksi/bukti (simpan detail sensitif di sistem privat):
- Asumsi dan yang belum diverifikasi:
- Perlakuan: perbaiki / mitigasi / terima (tautan pengecualian) / jadwalkan
- Retest dan penutup:
```

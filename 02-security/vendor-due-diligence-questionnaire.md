# Vendor Due Diligence Questionnaire Template

Lengkapi sebelum vendor Tier 1/2 (lihat [third-party dan service provider](third-party-risk.md)) mendapat akses ke data atau environment produksi. Simpan jawaban vendor dan bukti pendukung secara internal; jangan publikasikan evidence sensitif ke repo publik.

## Profil dan keamanan umum

- Nama vendor, layanan yang digunakan, dan data class yang diproses:
- Sertifikasi/assessment keamanan yang dimiliki (SOC 2, ISO 27001, atau setara) dan tanggal berlaku:
- Riwayat insiden keamanan signifikan dalam 24 bulan terakhir dan penanganannya:
- Kontak security dan jalur pelaporan vulnerability vendor:

## Data handling

- Lokasi pemrosesan dan penyimpanan data (termasuk backup):
- Enkripsi data saat transit dan tersimpan, serta manajemen kunci:
- Subprocessor yang digunakan dan proses notifikasi bila subprocessor berubah:
- Kebijakan retensi dan prosedur penghapusan data saat kontrak berakhir:

## Access dan authentication

- Kontrol akses staf vendor ke data/sistem milik kita (least privilege, MFA, audit log):
- Proses onboarding/offboarding staf vendor yang memiliki akses:

## Continuity dan incident

- SLA notifikasi insiden (waktu maksimum pemberitahuan setelah terdeteksi):
- Business continuity/disaster recovery plan vendor dan bukti pengujian terakhir:
- Exit plan: cara migrasi data keluar dan bukti penghapusan setelah offboarding:

## Kontrak dan audit

- Klausul keamanan/privasi, kerahasiaan, dan liability yang relevan sudah direview legal:
- Hak audit/right-to-request-evidence tercantum dalam kontrak:

## Keputusan

- Risiko yang teridentifikasi dan mitigasi:
- Approval: [nama/role], tanggal:
- Tanggal review ulang berikutnya:

Rujukan: [NIST SP 800-161 Rev. 1, Cybersecurity Supply Chain Risk Management Practices for Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/161/r1/upd1/final).

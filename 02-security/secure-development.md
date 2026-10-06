# Secure Development dan Supply Chain

- Security requirements MUST dibuat sejak perencanaan untuk fitur yang memproses identitas, data pribadi, uang, file, integrasi, atau privilege.
- Perubahan Tier 1 dan fitur autentikasi/otorisasi MUST memiliki threat model dan security review sebelum rilis.
- Pull request MUST melewati secret scanning, dependency/SCA scanning, static analysis, build, lint, dan tes yang diwajibkan repo. DAST, container, dan infrastructure-as-code scanning MUST ditambahkan bila stack atau deployment memerlukannya.
- Temuan critical/high yang valid dan terjangkau MUST memblokir merge atau release sampai diperbaiki atau disetujui melalui pengecualian risiko yang berjangka.
- Dependency baru MUST memiliki alasan, maintainer aktif, lisensi yang dapat diterima, versi terkunci, dan jalur update. Vulnerability kritis/eksploitable ditangani menurut SLA proyek.
- Build dan rilis production MUST berasal dari source yang ditinjau melalui pipeline terlindungi; batasi siapa yang dapat mengubah workflow dan mengakses signing/deploy secrets.
- Lindungi branch utama dan pipeline dengan least privilege, review, audit, dan environment approvals untuk rilis berisiko.
- Setiap artefak production MUST dapat ditelusuri ke source, dependency, workflow/build, dan approval. SBOM MUST disimpan untuk Tier 1; Tier 2/3 SHOULD menyimpan SBOM bila pipeline mendukungnya.
- Input eksternal MUST divalidasi; gunakan parameterized queries, contextual output encoding, CSRF protections, batas file, safe deserialization, dan secure headers sesuai stack.
- Gunakan library dan primitive kriptografi standar; jangan merancang algoritma kripto, token, atau protokol autentikasi sendiri.
- Pengujian keamanan MUST tidak memakai data produksi kecuali ada izin terpisah dan prosedur khusus.
- Produk Tier 1 yang dapat diakses dari internet MUST mendapat security assessment independen sebelum production, setelah perubahan besar pada trust boundary/auth/data, dan sekurangnya tahunan. Scope dan metode harus sesuai risiko, bukan hanya pemindaian otomatis.
- Deteksi, triase bertingkat bukti, dan pencatatan temuan mengikuti [deteksi vulnerability, bug, dan technical debt](../01-engineering/defect-and-debt-detection.md); fase dan gate keseluruhan ada di [SDLC](../01-engineering/sdlc.md).

## Rujukan

- [NIST SP 800-218 SSDF 1.1](https://csrc.nist.gov/pubs/sp/800/218/final) untuk praktik secure software development.
- [OWASP ASVS 5.0.0](https://owasp.org/projects/asvs) sebagai katalog persyaratan teknis dan baseline verifikasi aplikasi.
- Pilih level ASVS berdasarkan risiko produk; catat versi dan requirement IDs yang diadopsi agar review dapat diulang.

# Git dan Code Review

- Perubahan MUST melalui pull request dan review independen sebelum merge, kecuali prosedur incident/emergency yang terdokumentasi.
- Branch utama MUST dilindungi: tidak ada direct push atau force push; merge mensyaratkan quality gates berhasil dan minimal satu approval yang bukan dari author.
- Approval wajib diulang setelah perubahan baru yang memengaruhi hasil review; gunakan CODEOWNERS atau mekanisme setara untuk area security, schema, infrastructure, dan auth.
- Perubahan yang memengaruhi security, data, migrasi, autentikasi, otorisasi, atau kompatibilitas MUST meminta reviewer yang memahami area tersebut.
- Riwayat branch bersama MUST NOT ditulis ulang atau dihapus tanpa persetujuan pihak terdampak.
- Reviewer MUST memeriksa correctness, authorization, data handling, failure modes, maintainability, dokumentasi, dan bukti verifikasi.
- Perubahan Tier 1, autentikasi/otorisasi, kriptografi, infrastructure/deployment, dan migrasi destruktif MUST memiliki dua reviewer; satu reviewer harus menjadi domain/security owner yang sesuai. Reviewer tidak boleh menyetujui perubahan yang dibuatnya sendiri.
- PR SHOULD fokus dan cukup kecil untuk ditinjau. Deskripsi mencantumkan masalah, solusi, risiko, rencana data/deploy, dan hasil verifikasi.
- Temuan review diprioritaskan menurut risiko dan diberi langkah perbaikan yang dapat dilakukan.

## Emergency change

Perubahan darurat boleh memakai jalur dipercepat jika untuk mengurangi dampak aktif. Catat alasan, lingkup, pemeriksaan minimum yang dilakukan, pemilik, dan lakukan review retrospektif secepatnya.

Untuk menerapkan aturan di atas sehari-hari, gunakan [template pull request](../07-adoption/pull-request-template.md) dan [checklist code review](../07-adoption/code-review-checklist.md).
